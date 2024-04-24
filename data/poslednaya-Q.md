# Unused modifier in `VaultManagerV2`:

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45C1-L47C4

```solidity
  modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```

Consider to delete. 


# Critical events not emitted. 

Main contract to interact user <> protocol is `VaultManagerV2`, but there no emits about deposit/withdraw. 

Change Denominator-contract is important to user's positions. But doesn't emitted. 

Change UnboundedVault is important to user's positions. But doesn't emitted. 

Consider to add emits:
- `VaultMangerV2`:
    ∆ https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119
    ∆ https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134 
- `UnboundedKerosineVault`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43
- `BoundedKerosineVault`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23
