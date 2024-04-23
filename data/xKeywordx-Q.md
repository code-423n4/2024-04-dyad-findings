### [L-1] A user can deposit users on behalf of a DNft that they don't own

**Github Code:** https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119

**Description:** The `VaultManagerV2::deposit` function only checks if the ID of the Nft on behalf of which the deposit is made is valid or not, but it doesn't validate that the depositor is the actual owner of that NFT.

**Impact:** A user can mistakenly or purposefully deposit assets on behalf of an NFT ID that they don't owner.

**Proof of Concept and recommended mitigation:** Add the `isDNftOwner` modifier on the `VaultManagerV2::deposit` function.

```diff
-   function deposit(uint id, address vault, uint amount) external isValidDNft(id) {
+   function deposit(uint id, address vault, uint amount) external isValidDNft(id) isDNftOwner(id) {
        idToBlockOfLastDeposit[id] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }
```