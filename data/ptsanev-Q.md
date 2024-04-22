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

[L-02] - inside ``liquidate()`` we cap the minimum CR we work with which is 100%, meaning no matter how low of a CR a vault has, it always gets capped at 100%, which leads to 2 things:
1. People can potentially abuse this by intentionally minting Dyad to get as low of a CR as possible, since they always get liquidated for a minimum a 100% ratio
2. Using 100% as the cap (1e18), would lead to getting zeroes when calculating equity shares and asset shares, leading to the liquidator getting no reward for liquidating <= 100% vaults. This incentivization can hurt the liquidation mechanism.
If the intention is for there to be a cap on the minimum CR, then consider increasing it to atleast 110% to retain the reward and incentive. Otherwise, consider refactoring reward calculation to properly reward liquidations of CR<100%.