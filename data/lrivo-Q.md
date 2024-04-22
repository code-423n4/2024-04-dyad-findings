# [QA-1] VaultManagerV2 allows users to deposit to arbitrary vault addresses, potentially resulting in phishing attacks

The deposit() function allows users to specify an arbitrary vault address they want to deposit into.
However, no checks are in place to prevent an unlicensed Vault address from being passed.

```js
function deposit(
        uint id, 
        address vault, // <@ arbitrary address - can be unlicensed
        uint amount
) {
   idToBlockOfLastDeposit[id] = block.number;
   Vault _vault = Vault(vault);
   _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
   _vault.deposit(id, amount); 
}
```

A malicious user can craft a malicious contract that looks like a Vault but, inside his deposit function, transfers every token to the attacker.

## Recommended Mitigation
Add a check in `VaultManagerV2:deposit()` that the vault address is licensed before transferring funds

# [QA-2] `VaultManagerV2:deposit()` should use `isDNftOwner(id)` instead of `isValidDNft(id)`

This modification will prevent users from accidentally passing in an NFT id they do not possess.
In this case, they cannot withdraw the funds because `VaultManagerV2:withdraw()` uses `isDNftOwner(id)`.
The NFT owner however can withdraw the accidentally deposited funds.

## Recommended Mitigation
Use `isDNftOwner(id)` instead of `isValidDNft(id)`
