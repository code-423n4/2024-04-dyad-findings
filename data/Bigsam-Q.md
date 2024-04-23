## L-01 Report on Unused Modifier Declaration in VaultManagerV2 Contract

## Introduction

The `VaultManagerV2` contract from the code-423n4/2024-04-dyad repository contains an issue related to redundant code. Specifically, an unused modifier is declared within the contract, but instead of utilizing this modifier, the contract contains nested checks that render the modifier redundant.

## Issue Identification

### Unused Modifier Declaration

In the `VaultManagerV2` contract, an unused modifier is declared as shown below:

```solidity
 modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47

### Redundant Code Instance

Instead of using the  modifier, the contract contains nested checks within the `add` function:

```solidity
function add(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L75 

## Recommendation

### Mitigation Strategy

To avoid code duplication and enhance code readability, one of the redundant checks should be cleared, and the other should be utilized consistently throughout the contract.






## L-02 Report on Redundant Calculations in VaultManagerV2 Contract

## Introduction

The `VaultManagerV2` contract an upgrade from `VaultManagerV` from the code-423n4/2024-04-dyad repository contains redundant calculations in both the `withdrawal` and `redeem` functions. This redundancy can lead to inefficiencies and potential inconsistencies in the contract's behavior.

## Issue Identification

### Redundant Calculations in Redeem Function

In the `redeem` function, calculations are performed to determine the asset value based on the amount, asset price, and decimals of the oracle and asset:

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L194-L199

```solidity
Vault _vault = Vault(vault);
uint asset = amount 
            * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
            / _vault.assetPrice() 
            / 1e18;
```

### Redundant Calculations in Withdrawal Function

Similarly, in the `withdrawal` function, the same calculations are recalculated to determine the Amount value(note this Amount is the input in the redeem function, we are taking the asset value calculated from the redeem function as input to recalculate the same Amount again):

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L153

```solidity
Vault _vault = Vault(vault);
uint value = amount * _vault.assetPrice() 
             * 1e18 
             / 10**_vault.oracle().decimals() 
             / 10**_vault.asset().decimals();
```

## Recommendation

### Mitigation Strategy

To streamline the code and eliminate redundancy, the critical checks and calculations needed in the `withdrawal` function should be introduced also to the `redeem` function. By implementing the full logic within the `redeem` function and avoiding external calls to `withdrawal`, the contract's integrity can be maintained without duplicating calculations.
By consolidating the necessary calculations and checks within the `redeem` function, the contract's code can be simplified, and potential inconsistencies can be avoided.
```solidity
 if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
    uint dyadMinted = dyad.mintedDyad(address(this), id);
 if (getNonKeroseneValue(id) - amount < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
```

## Conclusion

The redundant calculations in the `withdrawal` and `redeem` functions of the `VaultManagerV2` contract introduce unnecessary complexity and potential risks. By reorganizing the code and implementing the full logic within the `redeem` function, the contract can be improved in terms of efficiency, readability, and maintainability.

