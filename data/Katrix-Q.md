## L-5: Missing checks for `address(0)` when assigning values to address state variables  
  
Impact:  
-------
`address(0)` checks are missing in address variable initializations/changes in many places. As `address(0)` is used as an indicator, there is a greater risk of using it accidentally.  
Allowing zero-addresses will lead to contract reverts and force redeployments if there are no setters for such address variables. Check for `address(0)` when assigning values to address state variables.  
  
Proof of concept:  
--------
>1. Vault.kerosine.bounded.sol#L29
>https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L29  
  
>2. Vault.kerosine.unbounded.sol#L47
>https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L47  
  
>3. VaultManagerV2.sol#L63
>https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L63  
  
>4. KerosineDenominator.sol#L14
>https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L14