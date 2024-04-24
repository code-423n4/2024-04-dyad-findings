# 1 Low. Only borrowers can redeem DYAD
Strange and not popular design of stable coin in which only those who borrowed stable coin against collateral can redeem it back for collateral. If user received DYAD from third party and not from VaultManager, he can't exchange it for collateral.

It is because DYAD is burned on redeem and user's position is decreased:
```solidity
  function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
    returns (uint) { 
      dyad.burn(id, msg.sender, amount);
      ...
  }

  function burn(
      uint    id, 
      address from,
      uint    amount
  ) external 
      licensedVaultManager 
    {
      _burn(from, amount);
@>    mintedDyad[msg.sender][id] -= amount;
  }
```
That is not how usually CDP protocols work for the sake of interoperobility with third party. However significant design update must be applied to resolve it.