[L-01] - currently the licensers for kerosene and regular vaults are multi-sigs, but would be shifted to a voting mechanism in the future, which leads to the importance of checking the asset of the vault. Currently the function:
```solidity
function addKerosene(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
    emit Added(id, vault);
  }
```
does no validation if the vault's asset is actually a kerosene asset.
It currently is not needed, but shifting to voting would beg the need for checking asset correctness.

[L-02] - the ``redeemDyad`` function of the manager is tied closely to the asset's oracle price, based on the amount of burned Dyad. Having slippage protection, deadline or best-case both is crucial in times of price volatility, oracle fluctuations, etc to make sure the user withdraws funds in an acceptable time and amount range.