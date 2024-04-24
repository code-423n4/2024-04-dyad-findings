## [GAS-1] State variable `KerosineDenominator::kerosine` should be immutable as it is a state variable only set in the constructor  
  
# Description:  
-----
State variable `kerosine` declared in the `KerosineDenominator` contract should be immutable as it is only set in the constructor.  
  
# Impact:  
-----  
Setting `kerosine` as immutable will optimize gas.  
  
# PoC:  
-----  
>KerosineDenominator.sol L#9
>https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L9