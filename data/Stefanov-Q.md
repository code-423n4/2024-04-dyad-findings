## [L-1] If amount in `VaultManagerV2:redeemDyad` is more than the dyad minted, function is going to revert

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

## [L-2] `IsLicensed` modifier missing  in `VaultManagerV2:deposit` 

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

## [L-3] `IsLicensed` modifier missing  in `VaultManagerV2:withdraw` 

`VaultManagerV2` is using only licensed vaults. Depositing in vaults that are not licensed is in no use.

```diff
 function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
+     isLicensed(vault)
      isDNftOwner(id)
  {
    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }

```

## [L-4] Only the owner of DNft should be able to burn their dyad


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