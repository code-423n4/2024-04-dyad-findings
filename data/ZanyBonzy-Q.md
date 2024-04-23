
# 1. Querying of mainnet owner's balance makes it vulnerable to a donation attact

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/KerosineDenominator.sol#L21

### Impact

Anyone with kerosene can potentially maniulate denominator, hence asset prices by donating tokens to mainnet address due to querying of balance of mainnet owner's address.

```solidity
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```


***


# 2. Kerosene's address can be marked as immutable since it cannot be changed

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/KerosineDenominator.sol#L9

### Impact
Kerosene address is not set in the KerosineDenominator contract, only in the constructor. Since it cannot be changed, the parameter can be marked immutable.

```solidity
  Kerosine public immutable kerosine;
```

***

# 3. Add checks for same parameter updates

Lines of code* 
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L29
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L47

***


# 4. `assetPrice` can easily be manipulated through donations to the vault

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L60

### Impact

The use of balanceOf of the vault opens the assetPrice manipulation by donating tokens to vault's address.

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
***


# 5. `setKeroseneManager` can be frontrun

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L59

### Impact

Anyone who frontruns call to the `setKeroseneManager` can essentially take over an important part of the protocol which can be significantly misuesed. Important to note that once the address is set, it cannot be changed, hence it's imperative that the function be protected from frontrunners to prevent need for redeployment.
```solidity
  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager;
  }
```

### Recommended Mitigation Steps
Consider calling the function in the constructor instead.

***

# 6. KeroseneManager's address can be marked as immutable since it cannot be changed

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L32

### Impact
The `setKeroseneManager` function is protected by the initializer modifier, meaning, once set, cannot be changed.

```solidity
  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager;
  }
```

Consider then marking its declaration as immutable.

```solidity
KerosineManager public immutable keroseneManager;
```

# 7. Bounded kerosene vaults cannot be removed

Lines of code *

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L101
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L41

## Impact
Users who have had bounded kerosene vaults added to their list of vaults cannot have it removed, due to a check in the remove function that ensures that vaults must not have any assets deposited in them. 
```solidity
  function remove(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
    if (!vaults[id].remove(vault))     revert VaultNotAdded();
    emit Removed(id, vault);
  }

```
This causes that the owner cannot remove bounded kerosene vaults due to inability to withdraw from it. Since anyone can deposit into a vault, a malicious user can deposit as low as 1 wei into the vault and permanently DOS vault removal.

```solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
    view
      onlyVaultManager
  {
    revert NotWithdrawable(id, to, amount);
  }
```
 Considering that there's a limit on the amount vaults that can be added, and that for a host of reasons including if vaults get compromised, a user might want to switch vaults, having a functionality to do that is quite handy.

***

# 8. Potential DOS of kerosine vaults due to division by zero when calculating asset prices

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/KerosineDenominator.sol#L21
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L66

### Impact

The denominator is calculated as totalSupply - mainnetowner's balance. 

```solidity
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```
And upon, kerosene minting in the constructor, the total supply (and max supply) of 1 billion, and the entire supply is minted to the deployer of the kerosene contract which can potentially be the mainnet owner, denominator during this time period will always 0, 
```solidity
  constructor() {
      _mint(msg.sender, 1_000_000_000 * 10**18); // 1 billion
  }
```

which will DOS involving getting assetprices as a division by zero error will occur. Any user using the bounded or unbounded kerosene vaults will be affected by this.
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
Important to also note that if transferred by the mainnet owner, the tokens can always be donated back to the address to trigger this bug.


# 9. Chainlink asset price validation allows for zero prices

Lines of code*

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.wsteth.sol#L103
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.sol#L102
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L146
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L197
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L238

### Impact

The asset prices is gotten from the vault contracts, which queries chainlink feed for token prices. The issue is that the `answer` validation is not sufficient enough as it only accounts for negative prices and not 0.

```solidity
  function assetPrice() 
    public 
    view 
    returns (uint) {
      (
        ,
        int256 answer,
        , 
        uint256 updatedAt, 
      ) = oracle.latestRoundData();
      if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
      return answer.toUint256(); //@note
  }
```
The function uses `toUint256` function to convert the asset price, which however only reverts on negative prices but not zero.
```solidity
    
        function toUint256(int256 value) internal pure returns (uint256) {
        require(value >= 0, "SafeCast: value must be positive");
        return uint256(value);
    }
```
This means that when chainlink prices return zero for one reason or the other, the protocol uses the value. This can lead to a host of unexpected issues in the protocol including unfair liquidations, unprofitable or blocked redemptions/withdrawals and so on. A user for instance with only the vault will instantly have his switch from healthy to zero in an instant, opening him up to be unfairly liquidated by malicious liquidators.

### Recommended Mitigation Steps

Include a check to ensure prive is > 0 instead.

***

# 10. Protocol will be frozen if undelying pricefeed is disabled.

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.wsteth.sol#L103
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.sol#L102

# Impact

Chainlink oracles can be taken offline or token prices can fall to below zero, especially during times of high volatility. In these cases, liquidations and other protocol operations will be frozen (all calls will revert) for any debt holders holding this token, even though they may be some of the most important times to allow liquidations to retain the solvency of the protocol. This is because there is no fallback logic to be executed when the access to the Chainlink data feed is denied by Chainlink's multisigs. The multisigs can immediately block access to price feeds at will.

https://blog.openzeppelin.com/secure-smart-contract-guidelines-the-dangers-of-price-oracles/

```solidity
        uint256 updatedAt, 
      ) = oracle.latestRoundData();
      if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
      return answer.toUint256(); //
  }
```
This can cause a full time lockdown of the protocol's operations.
## Recommended Mitigation Steps

A fallback oracle should be provided that will be used in place of chainklink to handle this scenario. The whole set up should be placed in a try-catch block.

***

# 11. Rounding errors in `redeem` function can turn a one step burn and withdraw process into two.

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L195-L198C

### Impact

The `redeemDyad` function allows for burning and withdrawing in one atomic transaction. It however calculates the asset to withdraw without accounting for solidity's rounding down feature, which defeats the purpose of the function.

```solidity
  function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
    returns (uint) { 
      dyad.burn(id, msg.sender, amount);
      Vault _vault = Vault(vault);
      uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;
      withdraw(id, vault, asset, to);
      emit RedeemDyad(id, vault, amount, to);
      return asset;
  }
```
The `asset` calculation formula can be simplified to this: amt * 10**(OD + VD) / (P * 10**OD) / 1e18
Considering `_vault.asset().decimals())` is 18, the formula when broken down equals amt / P;

And due to solidity's rounding down feature, whenever amount of dyad to redeem is less than price, the function simply burns the tokens and withdraws zero assets. This can pose issues in cases of integrations with other protcols and defeats the purpose of having the function. 

### Recommended Mitigation Steps
Consider introducing a normalizer parameter which should be accounted for in the `withdraw` function.


# 12. dNFTs are transferrable, which can be used to honeypot unsuspecting users

Lines of code* 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L230-L239
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/DNft.sol#L4
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/extensions/ERC721Enumerable.sol#L6
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L150-L170

### Impact

Depending on valuable the price of dyad becomes, a user can use a `dNFT` to mint dyad worth lots of usd value, while racking up a poor collateral ratio. Considering that collateral ratio is calculated by comparing usd value of the vaults held by the nft against the amount of dyad minted not its usd value. It can become more profitable for a user to , rather than burn dyad to retrieve his collateral, sell it on the market place to an unsuspecting victim. The victim pays possibly a substantial amount for the nft and receives an nft with a poor collateral ratio opening him up to liquidations, or having to pay extra to put the vault in a stable state.

```solidity
  function collatRatio(
    uint id
  )
    public 
    view
    returns (uint) {
      uint _dyad = dyad.mintedDyad(address(this), id);
      if (_dyad == 0) return type(uint).max;
      return getTotalUsdValue(id).divWadDown(_dyad);
  }
```

### Recommended Mitigation Steps
Disable transfer of NFTs when its undercollateralized.