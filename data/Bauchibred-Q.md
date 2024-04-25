# QA Report for DYAD

## Table of Contents

| Issue ID                                                                                                                                       | Description                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| [QA-01](<#qa-01-cr-could-be-over/undervalued-due-to-its-unsafe-dependance-on-vault.getusdvalue()>)                                             | `cr` could be over/undervalued due to its unsafe dependance on `vault.getUsdValue()`                                           |
| [QA-02](#qa-02-protocol-does-not-enforce-cr-buffer-in-regards-to-users-protection)                                                             | Protocol does not enforce CR buffer in regards to user's protection                                                            |
| [QA-03](<#qa-03-vault.getusdvalue()-should-be-wrappped-in-a-try-catch>)                                                                        | `vault.getUsdValue()` should be wrappped in a try catch                                                                        |
| [QA-04](#qa-04-protocol-might-overvalue-the-asset-transferred-in-by-a-user-and-unintentionally-flaw-their-accounting-logic)                    | Protocol might overvalue the asset transferred in by a user and unintentionally flaw their accounting logic                    |
| [QA-05](#qa-05-the-kerosene-price-can-be-manipulated-via-donation-attacks)                           | The kerosene price can be manipulated via donation attacks                      |
| [QA-06](#qa-06-dnft-owners-can-liquidate-themselves)                                                                                           | `dNFT` owners can liquidate themselves                                                                                         |
| [QA-07](#qa-07-protocols-reward-vesting-logic-could-unfairly-make-users-liquidatable)                                                          | Protocol's reward vesting logic could unfairly make users liquidatable                                                         |
| [QA-08](#qa-08-update-stale-modifiers-from-vaultmanagerv1-used-in-vaultmanagerv2)                                                              | Update stale modifiers from `VaultManagerV1` used in `VaultManagerV2`                                                          |
| [QA-09](#qa-09-owner-transfer-actions-done-in-a-single-step-manner-are-dangerous)                                                              | Owner transfer actions done in a single-step manner are dangerous                                                              |
| [QA-10](<#qa-10-protocol-might-be-incompatible-with-some-to-be-integrated-tokens-due-to-dependency-on-.decimals()-during-withdrawal-attempts>) | Protocol might be incompatible with some to-be integrated tokens due to dependency on `.decimals()` during withdrawal attempts |
| [QA-11](#qa-11-fix-documentation)                                                                                                              | Fix documentation                                                                                                              |
| [QA-05](#qa-05-protocol-intends-to-have-a-duration-between-deposits-and-wothdrawals-but-instead-hardcodes-this-to-0)                           | Protocol intends to have a duration between deposits and wothdrawals but instead hardcodes this to `0`                         |

## QA-01 `cr` could be over/undervalued due to its unsafe dependance on `vault.getUsdValue()`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L50-L68

```solidity
  function assetPrice()
    public
    view
    override
    returns (uint) {
      uint tvl;
      //@audit
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

This function is used to get the price of an asset, and it gets that by querying the specific vault of that asset for it's balance and price.

Keep in mind that this function is also used whenever getting price from the bounded vault as show here https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L44-L50

```solidity

  function assetPrice()
    public
    view
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
        }
```

Going back to the VaultManagerV2.sol, we can see that the line `usdValue = vault.getUsdValue(id);  ` is queried whenever there is a need to get the collateral ratio for asset as confirmed by this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+usdValue+%3D+vault.getUsdValue%28id%29%3B+++NOT+language%3AMarkdown&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+usdValue+%3D+vault.getUsdValue%28id%29%3B+++NOT+language%3AMarkdown&type=code) and queries the two aforementioned functions as shown below https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L79-L104

```solidity
  function getUsdValue(
    uint id
  )
    external
    view
    returns (uint) {
      return id2asset[id] * assetPrice()
              * 1e18
              / 10**oracle.decimals()
              / 10**asset.decimals();
  }



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
      return answer.toUint256();
  }

```

That is to say that the pricing logic requires us to query chainlink at the end of the calls, but evidently, we can see that this call lacks any check on the in-aggregator built min/max circuits, which would make protocol either overvalue or undervalue the collateral depending on which boundary is crossed.

A little bit more on the min/max circuits is that, Chainlink price feeds have in-built minimum & maximum prices they will return; if during a flash crash, bridge compromise, or depegging event, an asset’s value falls below the price feed’s minimum price, the oracle price feed will continue to report the (now incorrect) minimum price, so an An attacker could:

- Have their asset in protocol
- Real price of value dropped very low
- Attacker buys these assets in bulk from an exchange
- Brings it back to mint undercolaterized DYAD, since protocol would assume a way higher price than really is for the asset

### Impact

Borderline medium/low, as this essentially breaks core functionalities like documented collaterization level of DYAD to always be > 150%, and in sever cases this could even cause the DYAD to depeg

### Recommended Mitigation Steps

Store the asset's min/max checks, reimplement the way `vault.getUsdValue()` is being queried and have direct access to the price data being returned and check if its at these boundaries and revert or alternatively integrate a fallback oracle and then use the price from this instead.

## QA-02 Protocol does not enforce CR buffer in regards to user's protection

### Proof of Concept

Protocol includes a liquidation logic as can be seen here https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L214-L239

```solidity
  function liquidate(
    uint id,
    uint to
  )
    external
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

      uint numberOfVaults = vaults[id].length();
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
      emit Liquidate(id, msg.sender, to);
  }

```

However, when getting into a position, protocol allows users to have their positions to be `== collateralRatio` which only then subtly breaks protocol's logic as users are now immediately liquidatable in the next block.

### Impact

Users could be immediately liquidatable in the next block.

### Recommended Mitigation Steps

Consider introducing a buffer logic not to allow users be immediately liquidatable, alternatively have a strict enforcal that there is always a reasonable gap between user's position and the CR when they are opening a position.

## QA-03 `vault.getUsdValue()` should be wrapped in a try catch

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L50-L68

```solidity
  function assetPrice()
    public
    view
    override
    returns (uint) {
      uint tvl;
      //@audit
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

This function is used to get the price of an asset, and it gets that by querying the specific vault of that asset for it's balance and price.

Keep in mind that this function is also used whenever getting price from the bounded vault as show here https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L44-L50

```solidity

  function assetPrice()
    public
    view
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
        }
```

Going back to the VaultManager, we can see that the line `usdValue = vault.getUsdValue(id);  ` is queried whenever there is a need to get the prices as confirmed by this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+usdValue+%3D+vault.getUsdValue%28id%29%3B+++NOT+language%3AMarkdown&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+usdValue+%3D+vault.getUsdValue%28id%29%3B+++NOT+language%3AMarkdown&type=code) and queries the two aforementioned functions as shown below https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L79-L104

```solidity
  function getUsdValue(
    uint id
  )
    external
    view
    returns (uint) {
      return id2asset[id] * assetPrice()
              * 1e18
              / 10**oracle.decimals()
              / 10**asset.decimals();
  }



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
      return answer.toUint256();
  }

```

That is to say that the pricing logic requires us to query chainlink at the end of the calls, but evidently, we can see that this call lacks error handling for the potential failure of `vault.getUsdValue` which could fail due to the call to `oracle.latestRoundData()` via `assetPrice()`, note that Chainlink pricefeeds could revert due to whatever reason, i.e say maintenance or maybe the Chainlink team decide to change the underlying address. Now this omission of not considering this call failing would lead to systemic issues, since calls to this would now revert halting any action that requires this call to succeed.

### Impact

Borderline medium/low, as this essentially breaks core functionalities like liquidating and whatever requires for the usd value of an asset to be queried since there would be a complete revert

### Recommended Mitigation Steps

Wrap the ``vault.getUsdValue()` call in a try-catch block, then handle the error (e.g., revert with a specific message or use an alternative pricing method, the latter is a better fix as it ensures the protocol still functions as expected on the fallback oracle.

## QA-04 Protocol might overvalue the asset transferred in by a user and unintentionally flaw their accounting logic

### Proof of Concept

First would be key to note that protocol is to support different types of ERC20, which include tokens that apply fee whenever being transferred, this can be seen from the _### ERC20 token behaviours in scope_ section of the contest's readMe.

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/README.md#L155

```markdown
| [Fee on transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer) | ✅ |
```

Now take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L122-L134

```solidity
  function deposit(
    uint    id,
    address vault,
    uint    amount
  )
    external
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```

This function allows a `dNFT` owner to deposit collateral into a vault, it first transfers the amount from the caller and then deposits it to the vault with the function https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L42-L52

```solidity
  function deposit(
    uint id,
    uint amount
  )
    external
      onlyVaultManager
  {
    id2asset[id] += amount;
    emit Deposit(id, amount);
  }

```

Issue with this implementation is that it could get very faulty for some assets, that's to say for tokens that remove fees whenever they are being transferred, then protocol is going to have an accounting flaw as it assumes the amount of assets sent with this line: `    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);` is what's being received, would be key to note that the impact of this varies on the logic of the `asset` in some cases this could be just fees that might amount to little value which would still be considered as a leak of value.

However in some cases, for some tokens such as the [cUSDCv3](https://etherscan.io/address/0xbfc4feec175996c08c8f3a0469793a7979526065#code), it contain a special case for when the amount to be `deposited == type(uint256).max` in their transfer functions that result in only the user's balance being transferred. This can easily be used to exploit or rug pull the vault depending on the context, as in the vault during deposits, this execution `id2asset[id] += amount` would assume `amount` to be ` type(uint256).max` and depositor can then withdraw as much tokens as they like in [consequent withdrawals](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L53-L64), breaking the intended rate of redemption `1 DYAD` to always be `$1`, as they are no collaterals to back this.

Also protocol has stated that among tokens to consider as collaterals, we should consider LSTs and LRTs, however even these set of tokens are vulnerable to this, from LSTs that support positive/negative rebases to LSTs that [have 1-2 wei corner cases when querying their transfers](https://docs.lido.fi/guides/lido-tokens-integration-guide/).

### Impact

As explained in the last section of _[Proof of Concept](#proof-of-concept)_, this could lead to multiple bug cases depending on the specific `fee/transfer` logic applied to the asset, but in both cases this leads to a heavy accounting flaw and one might easily game the system by coupling this with the minting/withdrawal logic.

Keep in mind that protocol already integrates Lido's `WSTETH` on the mainnet, but since Chainlink does not have a specific feed for `WSTETH/USD` on the mainnet, protocol uses the Chainlink mainnet's `STETH/USD` feed instead as seen [here](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/script/deploy/Deploy.V2.s.sol#L55-L61), since this is not for the asset used as collateral, protocol would decide to change and decide to integrate into protocol `STETH` directly instead which still opens them up to this issue, specifically the ` 1-2 wei corner case`, otherwise this bug case is still applicable to other.

> Additional Note to Judge: This finding was first submitted as a H/M finding and then withdrawn after the scope of tokens to consider were refactored, however going through the docs and information passed by sponsors we can see that protocol plans on integrating LSTs and LRTs and in that case the `1-2` wei corner case is applicable to LSTs which still makes protocol vulnerable to bug case, so consider upgrading.

### Recommended Mitigation Steps

Do not support these tokens, alternatively a pseudo fix would be to only account for the difference in balance when receiving tokens, but this might not suffice for all tokens considering the future integration of LSTs/LRTs that have rebasing logic attached to them.

### Additional Note

This bug case is applicable to attempts of `safeTransfer/safeTransferFrom` in scope, and can be pinpointed using these search commands

- [https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+safeTransfer%28&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+safeTransfer%28&type=code)

- [https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+safeTransferFrom%28&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-04-dyad+safeTransferFrom%28&type=code)

> Main focus should be in the instances where these tokens are being deposited to protocol.

## QA-05 The kerosene price can be manipulated via donation attacks 

### Proof Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L50-L68

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

Would be key to note that this function is also used in the bounded vault to get the asset price via https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L43-L49

```solidity
  function assetPrice()
    public
    view
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }
```

The issue with this stems from how the Kerosine token price is calculated, the TVL is determined by fetching the balance of each vault's asset using the `balanceOf()` function and then multiplying it by the vault's asset price:

```solidity
        tvl += vault.asset().balanceOf(address(vault))
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals())
                / (10**vault.oracle().decimals());
```

However, this method relies on the `balanceOf()` function to retrieve the asset balance of each vault, rather than using a storage variable that internally tracks deposits. This opens up a vulnerability where an attacker could donate an arbitrary amount of assets to any vault, thereby artificially increasing the Kerosine token price.

### Recommended Mitigation Steps

Devise a solution that ensures the accurate calculation of the Kerosine token price without being susceptible to manipulation via unauthorized asset donations, this can be done by having a storage variable tracking the deposits internally

## QA-06 `dNFT` owners can liquidate themselves

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L214-L240

```solidity
  function liquidate(
    uint id,
    uint to
  )
    external
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

      uint numberOfVaults = vaults[id].length();
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
      emit Liquidate(id, msg.sender, to);
  }

```

This function is used to liquidate a dNFT that's currently underwater, i.e whose collateral ratio is less than `MIN_COLLATERIZATION_RATIO` which is `150%` however this attempt does not check to ensure that the `to` address is not the current owner of the `dNFT` that's to be liquidated, this then allows any user whose position goes underwater to instead of bringing back their positions afloat just liquidate themselves.

### Impact

Some `dNFT` owners can attempt gaming the system by liquidating themselves instead of getting their positions back afloat when it's profitable to do so.

### Recommended Mitigation Steps

Consider checking that the position to be liquidated is not owned by the liquidator who's liquidating it.

## QA-07 Protocol's reward vesting logic could unfairly make users liquidatable

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/KerosineDenominator.sol#L17-L23

```solidity
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  }
}
```

We can see that the final price that's gotten for kerosene is dependent on this, however the multi sig's balance is not always going to be constant, that;s to say in a case where there is a need to reward users for staking the multi sig must send out tokens for this.

Undergoing this action however can directly cause some positions that were narrowly afloat to become immediately liquidatable, this is cause the higher this denominator is, the lower the price returned from https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L65-L67

```solidity
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
```

### Impact

Borderline medium low, submitted as low as there is a little bit of dependecy on the admin having to transfer out tokens.

### Recommended Mitigation Steps

Consider making the denominator independent of the multi sig.

## QA-08 Update stale modifiers from `VaultManagerV1` used in `VaultManagerV2`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L49-L51

```solidity
  modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```

This modifier is used to know if a vault is licensed or not, however the implementation is stale and is only correctly applicable to the V1 vault manager, i.e with the V2 there is the introduction of the kerosene vaults logic but these vaults do not have a modifier to confirm if they are licensed or not.

### Impact

No modifier to know if a kerosene vault is licensed or not

### Recommended Mitigation Steps

Implement similar functionalities for sister integrations, i.e introduce a modifier to cover kerosene vaults too

## QA-09 Owner transfer actions done in a single-step manner are dangerous

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/script/deploy/Deploy.V2.s.sol#L69-L70

```solidity
    kerosineManager.transferOwnership(MAINNET_OWNER);

```

However, protocol uses Solmates Owned.sol and inheriting from solmate's Owned contract means you are using a single-step ownership transfer pattern. If an admin provides an incorrect address for the new owner this will result in none of the onlyOwner marked methods being callable again. The better way to do this is to use a two-step ownership transfer approach, where the new owner should first claim its new rights before they are transferred.

Here is the implementation of Solmate's Owned.sol https://github.com/transmissions11/solmate/blob/main/src/auth/Owned.sol#L39

```solidity
    function transferOwnership(address newOwner) public virtual onlyOwner {
        owner = newOwner;

        emit OwnershipTransferred(msg.sender, newOwner);
    }
```

### Impact

Admin role could be permanently lost

### Recommended Mitigation Steps

Use OpenZeppelin's Ownable2Step instead of Ownable.

## QA-10 Protocol might be incompatible with some to-be integrated tokens due to dependency on `.decimals()` during withdrawal attempts

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L137-L158

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
    //@audit
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

We can see that whenever there is a need to withdraw, protocol queries the `asset.decimals()` for the underlying asset, however some very popular ERC20 that might be used as assets, do not support the `.decimals()`format and as such this attempt at withdrawal would always revert for these tokens

### Impact

Specific assets would not work with protocol as it directly attempts to call `asset().decimals()` which would revert since the functionality is non-existent for that token, leading to deposits to be completely locked in the vaults since withdrawals can't be processed and during deposits no query to `.decimals()` are being made.

### Recommended Mitigation Steps

Consider try/catching the logic or outrightly not supporting these tokens.

## QA-11 Fix documentation

### Proof of Concept

Take a look at the docs here https://dyadstable.notion.site/DYAD-design-outline-v6-3fa96f99425e458abbe574f67b795145, most instances of explanation of `dNFTs` are being prefixed by the name NOTE which is wrong.

### Impact

Bad documentation make sit harder to understand code.

### Recommended Mitigation Steps

Change instances of NOTEs to dNFTs.

## QA-12 Protocol intends to have a duration between deposits and wothdrawals but instead hardcodes this to `0`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L138-L163

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
      //@audit
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

Evidently as hinted by the @audit tag we can see that protocol intends to apply a duration logic, after discussions with the sponsor this check is placed so as not to allow the kerosene price to be manipulated, however this check is not really sufficient as it doesn't have any waiting duration, which means that a user can just deposit and withdraw in the next block allowing them to still game the sytem with a 12 seconds wait time

### Impact

Check can easily be sidestepped in 12 seconds (block mining duration).

### Recommended Mitigation Steps

Consider having a waiting period whenever attemoting to withdraw, i.e apply this pseudo fix to https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L138-L163

```diff

  function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    public
      isDNftOwner(id)
  {
      //@audit
-    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
+    if (idToBlockTimestampOfLastDeposit[id] + WAITING_DURATION < block.timestamp) revert DepositedForTooShortDuration();
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
