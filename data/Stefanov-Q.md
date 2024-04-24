## [L-1] `IsLicensed` modifier missing  in `VaultManagerV2:deposit` 

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

## [L-2] Only the owner of DNft should be able to burn their dyad


```diff
function burnDyad(
    uint id,
    uint amount
  ) 
    external 
+     isDNftOwner(id)
      isValidDNft(id)
  {
    dyad.burn(id, msg.sender, amount);
    emit BurnDyad(id, amount, msg.sender);
  }

```