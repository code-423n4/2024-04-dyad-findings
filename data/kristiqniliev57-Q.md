* Redunant cast
VaultManagerV2.sol:  
```deposit(uint id, address vault, uint amount)```:

variable 'vault' is of type address, reduntant cast to address
function body:
```
idToBlockOfLastDeposit[id] = block.number;
   Vault _vault = Vault(vault);
   _vault.asset().safeTransferFrom(msg.sender, ***address(vault)***, amount);
   _vault.deposit(id, amount);
```

The address cast can be ommited

* Inconsistency with variable naming :{Kerosene, Kerosine} might lead to confusions.
e.g.
VaultManagerV2.sol:
```function removeKerosene()```

Vault.kerosine.bounded.sol:
```function setUnboundedKerosineVault()```

* Future considerations
VaultManagerV2:
```deposit()```
safeTransferFrom can lead to misscalculation with future integrations of arbitrary ERC-20 token vaults