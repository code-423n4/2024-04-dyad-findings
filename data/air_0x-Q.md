The current implementation of the `withdraw()` function in VaultManagerV2 lacks a precondition check to verify whether any vaults are associated with the given NFT ID. This oversight allows users to initiate withdrawal calls without any linked vaults, potentially leading to transaction failures.

Impact

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134


When users call the `withdraw()` function without associated vaults:

Failed Transactions: The function may fail, leading to unnecessary gas expenditures for users. These failed transactions contribute to a poor user experience and could reduce trust in the system's reliability.


Recommendation

Implement a check at the start of the withdraw() function to verify that the NFT ID has at least one associated vault. If no vaults are found, the function 