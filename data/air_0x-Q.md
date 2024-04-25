The absence of a precondition check for the existence of vaults in the `withdraw()` function  allows users to call the function without any associated vaults, potentially leading to failed transactions . This could result in unnecessary gas expenditure since transaction.



https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134

Recommendation
Implement a check to ensure that the caller of the withdraw function has added a vault

