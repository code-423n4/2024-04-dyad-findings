# QA

- [QA](#qa)
  - [Low](#low)
    - [1. `KerosineManager.sol` vaults license is not synchronize with `VaultManagerV2` Licenser contract](#1-kerosinemanagersol-vaults-license-is-not-synchronize-with-vaultmanagerv2-licenser-contract)
    - [2. DOS `remove()` vault. Anyone can deposit dust token to prevent remove vault from active list](#2-dos-remove-vault-anyone-can-deposit-dust-token-to-prevent-remove-vault-from-active-list)
    - [3. Allow mint 0 DYAD and small loan not worth liquidation](#3-allow-mint-0-dyad-and-small-loan-not-worth-liquidation)
    - [4. If Admin remove license from active vault. Liquidation still take tokens from deprecated vaults when it is not used as collateral](#4-if-admin-remove-license-from-active-vault-liquidation-still-take-tokens-from-deprecated-vaults-when-it-is-not-used-as-collateral)
    - [5. If Admin remove license from active vault. Chance user cannot withdraw asset out of deprecated vault when collateral value drop along](#5-if-admin-remove-license-from-active-vault-chance-user-cannot-withdraw-asset-out-of-deprecated-vault-when-collateral-value-drop-along)
    - [6. It is possible for user mint loan with x3 leverage](#6-it-is-possible-for-user-mint-loan-with-x3-leverage)


## Low

### 1. `KerosineManager.sol` vaults license is not synchronize with `VaultManagerV2` Licenser contract

`KerosineManager.sol` use its own license vaults list to calculate TVL value for Unbounded Kerosine.
These vaults are WETH and wstETH vault.

`VaultManagerV2` also use WETH and wstETH vault to calculate TVL for collateral. But it include license check.
<https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L261-L263>

So if WETH or wstETH vault removed from license list. Admin must also update `KerosineManager` license vault to reflect this too.
Otherwise Kerosene `AssetPrice()` not return correct value as it only return value of all vaults including deprecated one.

This is a bit messy. It make more sense to make Enumerable Licenser for both non-Kerosene vault and Kerosene vault.

### 2. DOS `remove()` vault. Anyone can deposit dust token to prevent remove vault from active list

`VaultManagerV2` allow 5 max normal vaults and 5 max Kerosene vault.
To remove vault from active vault list. User must have no deposit inside these vault.
<https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L101>

This can be prevented by other user.
Other user can deposit into any DNFT id.
<https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L125>

By frontrun depositing 1 wei token, `remove()` vault transaction will fail.

### 3. Allow mint 0 DYAD and small loan not worth liquidation

Mint DYAD accept zero as value.
<https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L156-L169>

DNFT cost minimum 0.1 ETH to mint.
So it is not worth anyone time to spread small loan minting to prevent liquidation gas cost.
It is still reasonable to have minimum loan amount.

### 4. If Admin remove license from active vault. Liquidation still take tokens from deprecated vaults when it is not used as collateral

Summarize underlying issue with 2 lines:

1. [Getting Total Collateral USD value exclude vault missing license.](https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L241-L286)
2. [liquidation does not check vault is licensed before transfer assets from user to liquidator.](https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L221-L226)

This resulted in Unfair liquidation taking away assets not belong to collateral anymore when admin remove vault license.

### 5. If Admin remove license from active vault. Chance user cannot withdraw asset out of deprecated vault when collateral value drop along

When a vault is deprecated and removed from license list, it is still possible to [deposit into deprecated vault.](https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L118-L131)
Withdrawal is not possible without passing collateral check.
Because [deprecated vault not included as collateral](https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L250-L286), user holding all tokens inside deprecated vault [cannot withdraw until collateral Ratio rise 150% again by deposit different tokens which they might not have](https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L133-L153).

### 6. It is possible for user mint loan with x3 leverage

By converting stable coin DYAD back to WETH and keep deposit to vault and mint more DYAD.
Repeat this process sequence and 150% minimum collateral give x3 leverage after loop this 9 times.

Because liquidation and mint have no fee. This give user abilities to use this project as trading long/short call with 3x leverage.

