## [L-1] Anyaone can burn users DYAD
Due to lack of access control anyone can call of the other user `burn()` function (mistakenly or not) and decrease the value of user's id minted dyad at one's own expense. User's balance will not suffer, but now his real `collatRatio` will be differen, thus in some cases liquidatable user cannot be liquidated or extra tokens can be minted. Recommended to add the `isDNftOwner` modifier:
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
## [L-2] User can deposit to unlicensed vaul
When depositing, there is no check if vaults[id] contains vault address. Assets deposited to unlicensed vault can be lost forever. Recommended to add this check:
```solidity
if (!hasVault(id, vault)) revert;
```