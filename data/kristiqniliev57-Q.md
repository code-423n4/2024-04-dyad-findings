```VaultManagerV2.deposit(uint id, address vault, uint amount)```:

 variable 'vault' is of type address, reduntant cast to address
function body:
```
idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, ***address(vault)***, amount);
    _vault.deposit(id, amount);
```

The case can be ommited