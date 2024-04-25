# [L-01] No check on `vault` passed to `VaultManagerV2::redeemDyad` can lead to the contract emitting erroneous events

[1 Instance](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184)

The function `redeemDyad` allows users to pass any address as `vault` with no checks that it is licensed. If the fake vault address doesn't revert when called it can lead to the `RedeemDyad` event being emitted. A user could make a fake vault contract and cause the `VaultMangerV2` contract to emit multiple false `RedeemDyad` events, causing issues for any indexers of these values such as the projects frontend website.

# [I-01] `VaultManagerV2` has getter functions for exogenous collateral vaults but no similar ones for Kerosene Vaults

The `VaultManagerV2` contract has the functions `getVaults` and `hasVault` to query a DNft's internal `vaults` mapping. However there are no matching `getVaultsKerosene` and `hasVaultKerosene` functions. These should be added to improve user experience and provide more transparency.

# [I-02] `VaultManagerV2::isLicensed` modifier is unused

The modifier `isLicensed` is declared in the contract but unused. The function `add` should use the modifier and remove the following line:
```solidity    
  if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
```
# [NC-01] Inconsistent Kerosene spelling across the project

The project mixes the spelling "Kerosene" & "Kerosine" throughout, this should be standardised before launch.

# [NC-02] Typo in `VaultManagerV2::MIN_COLLATERIZATION_RATIO` variable

This should be changed to the correct spelling `MIN_COLLATERALIZATION_RATIO`.