# Low Severity


## The protocol doesn't force any min brorrow (dyad) amount leading to the accumulation of dust positions in the Protocol
The protocol doesn't force any min mint amount on users, as long they have bought a Dnft and his position stays healthy after minting. This could the accumulation of dust positions in the protocol. This can be a big issue because there will be no incentive for liquidators to liquidate small unhealthy positions given the gas cost to do so would not make economic sense based on the incentive they would receive

## `remove()` and `removeKerosene()` could be Dossed by depositing 1 wei of collateral
The `VaultManagerV2` allows any one to deposit collateral assocciated with a DNft and doesn't force the sender to be theDNft owner
```solidity
  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```
`remove()` and `removeKerosene()` however checks that the removed Vaults from the `MarketManagerV2` must have 0 tokens posted as collateral. And in this case it is possible for an attacker to deposit 1 wei to the vault in the name of the dnft which will make vault removal revert
##  VaultManagerV2 only allows for querring non-kerosene vaults 

The `VaultManagerV2` only allows for querring non-kerosene vaults, but it does not allow for querying kerosene vaults. After Adding the Kerosene Vaults to the manager, it would make sense for the manager to allow other contracts to also querry the kerosene vaults of a dnft. This is at least a low severity bug, as the frontend wouldn't be able to querry the kerosene vaults of a dnft.
We recommend the following fix:
```diff
  function getVaults(
    uint id
  ) 
    external 
    view 
    returns (address[] memory) {
      return vaults[id].values();
  }
+function getKeroseneVaults(
+    uint id
+  ) 
+   external 
+    view 
+    returns (address[] memory) {
+      return vaultsKerosene[id].values();
+  } 

```
## VaultManagerV2 needs to update `hasVault()` to check for Kerosene Vaults
With the addition of kereosene Vaults in the `VaultManagerV2`, the `hasVault()` function needs to be updated to check for both non-kerosene and kerosene vaults.
A possible mitigation is as follows:
```diff
  function hasVault(
    uint    id,
    address vault
  ) 
    external 
    view 
    returns (bool) {
-      return vaults[id].contains(vault);
+      return vaults[id].contains(vault) || vaultsKerosene[id].contains(vault);
  }
```


# Non Criticals
## Kerosene Vaults unnecessarily use `safeTransfer()`
the `safeTransfer()` function is not needed for the kerosene vaults, as the token that will be used in those vaults is already known to the protocol. (Kerosine Token)
```diff
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
      onlyVaultManager
  {
    id2asset[id] -= amount;
-    asset.safeTransfer(to, amount); 
+    asset.transfer(to, amount); 
    emit Withdraw(id, to, amount);
  }
```


## The protocol sometimes uses Kerosene and other times Kerosine

We advise the protocol to use the same naming for Kerosene and replace the use of the term Kerosine with Kerosene. 
e.g: 
Replace`Vault.kerosine.unbounded` with `Vault.kerosene.unbounded`
Replace `Vault.kerosine` with `Vault.kerosene`
Replace `Vault.kerosine.bounded` with `Vault.kerosene.bounded`
Replace `KerosineManager` with `KeroseneManager`

## Unnecessary double casting of address in VaultManagerV2
vault is already an address no need to cast it to an address again
```diff
  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
-    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
+    _vault.asset().safeTransferFrom(msg.sender, vault, amount);
    _vault.deposit(id, amount);
  }
```

## keroseneManager could be set as constant
The state variable `keroseneManager` is only set during intialisation with the method `setKeroseneManager()` and therefore could be set as a constant

```diff
-  KerosineManager public keroseneManager;
+  KerosineManager public constant keroseneManager;
```
