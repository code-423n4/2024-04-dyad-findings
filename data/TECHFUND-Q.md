### KerosineVault::move()
As a good practice, it is better to validate that "to" and "from" address are not same and non zero. Also, the amount is greater than 0.
```
  function move(
    uint from,
    uint to,
    uint amount
  )
    external
      onlyVaultManager
  {
    id2asset[from] -= amount;
    id2asset[to]   += amount;
    emit Move(from, to, amount);
  }
```