## [L-1] Missing event for setDenominator function in Vault.kerosine.unbounded.sol

## [L-2] Missing event for setUnboundedKerosineVault function in Vault.kerosine.bounded.sol

## [I-1] Inappropriate variable name as the Vault should contains weth
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L49
In Deploy.V2.s.sol is created vault named ```ethVault```  which actually holds weth so it is going to be more consistent if the variable name is ```wethVault```.

