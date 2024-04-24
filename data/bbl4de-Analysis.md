
### [L-1] Possibly incorrect exogenous collateral check may pass for a boundary condition `getNonKeroseneValue(id) == newDyadMinted`

In `VaultManagerV2::mintDyad()` the mint collateral check is performed. The docs are not consistent with defining whether $1 of non-Kerosene collateral per DYAD should be allowed or not, as the text states it should:

`"These equations ensure that Notes can only ... mint more DYAD if there will be at least $1 of non-Kerosene collateral per DYAD minted in their Note upon the successful execution of the mint..."`

,but the pseudocode suggests that it should be greater than $1 collateral per DYAD:

`"If (C_non-K > D_debt + D_mint) Then: Approve the mint transaction; Else:  Reject the mint transaction;"`

If the pseudocode is right, user with collateral value being exactly equal to new dyad minted will be unrightfully allowed to mint DYAD. To make sure this is not the case make the following change:

```diff
-if (getNonKeroseneValue(id) < newDyadMinted)
+if (getNonKeroseneValue(id) <= newDyadMinted)
            revert NotEnoughExoCollat();
```

### [L-2] Lack of getter function for `vaultsKerosene` in `VaultManagerV2` forces `KerosineManager` to exist

As explained in my high severity vulnerability with the title: "Attempt to withdraw from unbounded kerosene vault will always fail due to wrong implementation" there is an issue with licensing causing unusability of the kerosene vaults. This issue could be also solved by filling a gap as suggested in this finding, which is creating a getter function to view the internal `vaultsKerosene` mapping. This together with mitigation of the high could potentially make the `KerosineManager` completely redundant as both licensing and id => vault tracking for kerosene vaults is done either way in `VaultManagerV2`. This finding however is submitted seperately from the high, because the underlying bug may be solved without adding additional getter or removing `KerosineManager`.

### [I-1] `Kerosine` used instead of `Kerosene`

In the entire codebase "Kerosine" is used extensively even though it should always be "Kerosene".
I does not present any vulnerabilities, it's just an incorrect naming convention.

### [I-2] Add a view function `hasVaultKerosene` in `VaultManagerV2`

In `VaultManagerV2` there is a view function `hasVault` to check whether `vaults[id]` contains the `vault` passed as a parameter. There is no such function for `vaultsKerosene[id]`, which might be added:

```diff
function hasVaultKerosene(uint id, address vault) external view returns (bool) {
        return vaultsKerosene[id].contains(vault);
    }
```


### Time spent:
12 hours