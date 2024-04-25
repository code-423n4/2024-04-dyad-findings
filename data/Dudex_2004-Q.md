The `burnDyad` function burns the dyad token from user account. However, the function missing the modifier `isDNftOwner(id)` and allow anyone to call this function .

```diff
function burnDyad(
    uint id,
    uint amount
  ) 
    external 
+     isDNftOwner(id)      
-     isValidDNft(id)
  {
    dyad.burn(id, msg.sender, amount);
    emit BurnDyad(id, amount, msg.sender);
  }
```