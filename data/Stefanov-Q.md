[L-1] `IsLicensed` modifier missing  in `VaultManagerV2:deposit` 

`VaultManagerV2` is using only licensed vaults. Depositing in vaults that are not licensed is in no use.

```diff
function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
+     isLicensed(vault)
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```