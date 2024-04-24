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

## [L-3] If amount in `VaultManagerV2:redeemDyad` is more than the dyad minted, function is going to revert

```diff
function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
    returns (uint) {
+     if(dyad.mintedDyad(address(this), id) < amount) {
+     amount = dyad.mintedDyad(address(this), id);
+     }
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