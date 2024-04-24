| Number | Title                                                           |
|--------|-----------------------------------------------------------------|
| [01]   | Flash loan attack may be possible to be used to liquidate users |
| [02]   | Underflow causes unclear revert reason                           |
| [03]   | Trailing whitespace in code                                      |
| [04]   | No input validation for vault addresses in `deposit()` and `withdraw()` |
| [05]   | Price of kerosine can be manipulated via donation attacks       |
| [06]   | Inconsistent spelling of 'kerosine' / 'kerosene'                |
| [07]   | Lack of 'fallback' for price oracles                             |


# [01] Flash loan attack may be possible to be used to liquidate users

The price of kerosine is directly linked with the degree of overcollateralization.

It increases when:
- Collateral is deposited in vaults
- DYAD is burned
- dNFT positions are liquidated

And decreases when:
- Collateral is withdrawn / DYAD is redeemed
- DYAD is minted

Lets assume the protocol is running at an average collateral ratio (CR) of 170%. Bob deposits into his vault at a ratio of 160%, a bit above the minimum ratio of 150%. His collateral consists of 60% kerosine and 100% exogenous collateral.

Alice wishes to liquidate Bob. She takes out a flash loan of kerosine and a exogenous collateral, for example, wstETH. She deposits wstETH and kerosine into vaults, with 100% wstETH and 50% kerosine. She then mints as much DYAD as she can, which is equal to 100% of her collateral (all of her wstETH).

As she minted DYAD at a CR of 150%, which is below the average CR of 170%, this decreases the average CR, to lets say, 165%. As the price of kerosine is directly linked to how much overcollateralization there is, the price of kerosine decreases. Bob's 60% kerosine as collateral drops to <50%, allowing him to be liquidated. Alice liquidates bob, transferring his collateral over into her own dNFT position. She uses this to again, mint DYAD using Bob's collateral, and repays the kerosine debt by swapping the minted DYAD to kerosine.

This situation is very specific in terms of constraints required, therefore is unlikely to occur, but I think it is still a scenario to consider.

Recommended mitigations would be to disallow liquidations in the same block (or same transaction) as a deposit.

# [02] Underflow causes unclear revert reason

There are instances where a subtraction is done between `uint`s and checked, however if the result is negative it will revert due to underflow instead of emitting the actual revert reason. This may cause the revert reason to become unclear to users.

For example:
```solidity
if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L150

Can be rewritten as:
```solidity
if (getNonKeroseneValue(id) < dyadMinted + value) revert NotEnoughExoCollat();
```

# [03] Trailing whitespace in code

There are trailing spaces in some lines of the source code. Consider removing them.

```solidity
          usdValue = vault.getUsdValue(id);        
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L262
```solidity
          usdValue = vault.getUsdValue(id);        
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L281

# [04] No input validation for vault addresses in `deposit()` and `withdraw()`

Vault addresses aren't checked in the VaultManagerV2 `deposit()` and `withdraw()` functions, which makes it easy for user errors such as depositing to a vault that is unlicensed or has an invalid address, causing them to lose funds.

There is also no check in `redeemDyad()` which emits the event `RedeemDyad(id, vault, amount, to)`, so incorrect events can be emitted.

Consider adding a check if the vault address and provided dNFT id exists in the set `mapping (uint => EnumerableSet.AddressSet) internal vaults;`, and if the vault is licensed.

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

  /// @inheritdoc IVaultManager
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
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L153

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
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L202

# [05] Price of kerosine can be manipulated via donation attacks

In the KerosineDenominator contract, `denominator()` returns the total kerosine currently in circulation. To do this, it subtracts the total kerosine supply from the kerosine locked in the multi sig `MAINNET_OWNER`.

```solidity
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L21

However, as it directly checks the balance of the multi sig using `balanceOf()`, the price of kerosine can be inflated via donating kerosine directly to the multi sig. Comments in the code point out that the currently denominator is not a great solution, rightfully so, thus this change should be considered. Perhaps add an internal tracking for kerosine in circulation instead, to avoid direct price manipulation.

# [06] Inconsistent spelling of 'kerosine' / 'kerosene'

Throughout the codebase, there have been many instances where the spelling of kerosine/kerosene varies.

For example, the `KerosineManager` uses the 'i' spelling, as with the kerosine bounded and unbounded vaults.

The `Kerosine` token contract itself is named with the 'i' spelling, but the token name uses the 'e' spelling:
`contract Kerosine is ERC20("Kerosene", "KEROSENE", 18) {`

The rest of the codebase also uses the 'e' spelling primarily, such as in VaultManagerV2 `setKeroseneManager()`, `keroseneManager()`, `getNonKeroseneValue()`, etc.

It is unclear whether this is an intentional design plan for contract names to be spelt with an 'i', and other things to be spelt with an 'e'.

Either way, this should be clarified or changed to be consistent throughout the codebase, to avoid typos and confusion.

# [07] Lack of 'fallback' for price oracles

Currently, vaults use a chainlink oracle to determine the price of their underlying assets, and have a threshold (`90 minutes`) for when data is considered to be 'stale' and unsafe for use.

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
      return answer.toUint256()                        // 1e8
             * IWstETH(address(asset)).stEthPerToken() // 1e18
             / 1e18;
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.wsteth.sol#L92-L106

However, there is not another secondary oracle to fall back to if chainlink stops working, which halts the entire protocol as `assetPrice()` will keep reverting due to stale data. This means whenever chainlink stops working for 90 minutes, the entire protocol will become unusuable, which includes withdrawals, minting and redeeming DYAD and liquidating.

Consider adding a secondary oracle to fall back to incase chainlink fails.


