# Quality Assurance Report

## [L-01] Function deposit() does not check if vault is licensed and added by user

[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119)

Function deposit() does not check if the vault parameter supplied by the caller is added by the owner of the DNft id or not. This should be added as a sanity check to prevent users from landing in unexpected situations and prevent possible misuse.
```solidity
File: VaultManagerV2.sol
123:   function deposit(
124:     uint    id,
125:     address vault,
126:     uint    amount
127:   ) 
128:     external 
129:       isValidDNft(id)
130:   {
131:     idToBlockOfLastDeposit[id] = block.number;
132:     Vault _vault = Vault(vault);
133:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
134:     _vault.deposit(id, amount);
135:   }
```


## [L-02] Protocol works incorrectly with fee-on-transfer tokens

[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119)

Although FOT tokens were removed from the README mid-contest, it would be good if the sponsors were aware of how they could break accounting. When depositing, line 133 will transfer the fee reduced amount while line 134 will deposit the parameter amount that was originally supplied. This means that id2asset in the vault would account for more than what the user deposited. This breaks accounting of the system and could allow users to tap into other user's funds when withdrawing.
```solidity
File: VaultManagerV2.sol
123:   function deposit(
124:     uint    id,
125:     address vault,
126:     uint    amount
127:   ) 
128:     external 
129:       isValidDNft(id)
130:   {
131:     idToBlockOfLastDeposit[id] = block.number;
132:     Vault _vault = Vault(vault);
133:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
134:     _vault.deposit(id, amount);
135:   }
```

## [L-03] withdraw() function does not consider kerosene value

Kerosene value is not considered here in the check above the withdraw() call on the vault contract. This is problematic for kerosene vaults because getNonKeroseneValue() for users only using kerosene vaults would lead to revert due to 0 - non-zero amount occurring. 
```solidity
  function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
      isDNftOwner(id)
  {
    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();

    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }
```

## [L-04] Attacker can grief users from redeeming collateral

The burnDyad() function allows anyone to burn DYAD on behalf of any id. This allows an attacker to burn DYAD and thus prevent users from possible redeeming their collateral back due to mintedDyad underflowing during redeem.
```solidity
  function burnDyad(
    uint id,
    uint amount
  ) 
    external 
      isValidDNft(id)
  {
    dyad.burn(id, msg.sender, amount);
    emit BurnDyad(id, amount, msg.sender);
  }
```

## [L-05] Function liquidate() does not check if id and to are the same

Function liquidate() checks if id and to parameters are valid DNFTs but does not check if they are the same. This allows users to frontrun liquidation calls and retain the collateral that was supposed to be the original liquidator's. 
```solidity
File: VaultManagerV2.sol
210:   function liquidate(
211:     uint id,
212:     uint to
213:   ) 
214:     external 
215:       isValidDNft(id)
216:       isValidDNft(to)
217:     {
218:       uint cr = collatRatio(id);
219:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
220:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
221: 
222:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;
223:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
224:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
225: 
226:       uint numberOfVaults = vaults[id].length();
227:       for (uint i = 0; i < numberOfVaults; i++) {
228:           Vault vault      = Vault(vaults[id].at(i));
229:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare); 
230:           vault.move(id, to, collateral);
231:       }
232:       emit Liquidate(id, msg.sender, to);
233:   }
```

## [L-06] Protocol could become insolvent if the price of collateral fell before liquidations could occur

If the price of collateral in USD goes from $150 to 60$ and the user has minted 100 DYAD, the protocol would become insolvent since liquidators would have no incentive to liquidate such positions. This is possible since Chainlink reports prices within max 3600s and if the price stays stale as it is, it would return a min answer value due to its circuit-breaker model. 
```solidity
File: VaultManagerV2.sol
206:   function liquidate(
207:     uint id,
208:     uint to
209:   ) 
210:     external 
211:       isValidDNft(id)
212:       isValidDNft(to)
213:     {
214:       uint cr = collatRatio(id);
215:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
216:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
217: 
218:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;
219:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
220:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
221: 
222:       uint numberOfVaults = vaults[id].length();
223:       for (uint i = 0; i < numberOfVaults; i++) {
224:           Vault vault      = Vault(vaults[id].at(i));
225:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare); 
226:           vault.move(id, to, collateral);
227:       }
228:       emit Liquidate(id, msg.sender, to);
229:   }
```

## [L-07] Price of kerosene can be increased by sending tokens to multisig directly

Price of kerosene can be increased by sending dyad to multisig directly. Since multisig balance would be greater in totalSupply - multisig balance operation in KeroseneDenominator contract, the denominator would be smaller, thus making the assetPrice returned larger. This could be misused by whales by sending dyad (obtained from a market) to multisig and then withdrawing collateral all in one batch transaction from the VaultManager contract at an increased price. This allows the attacker to tap into other user's funds. 
```solidity
  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
     
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
     
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
  
      return numerator * 1e8 / denominator;
  }
```

## [L-08] Issue in kerosene manager vaults approval

When calculating tvl in the for loop, we retrieve the asset price from the vaults added in the kerosene manager contract. These are the wsteth and weth vaults as per the deploy script. The issue is that, the assetPrice() function (not one in for loop) but the one embodying it, is called by the bounded and unbounded vaults, which are called by the VaultManager contract. The issue is that if wsteth and weth vaults are approved in kerosene manager, how are the bounded and unbounded ones approved as well. This causes an issue in the vaults being used by the manager and potential misuse.
```solidity
  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
     
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
     
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
  
      return numerator * 1e8 / denominator;
  }
```
```

## [R-01] Use one constant max vaults variable since both share the same value

[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22)

Both constants below share the same value. Thus, removing one of them and keeping only MAX_VAULTS should be a better rafactoring of the code.
```solidity
File: VaultManagerV2.sol
22:   uint public constant MAX_VAULTS          = 5;
23:   uint public constant MAX_VAULTS_KEROSENE = 5; 
```