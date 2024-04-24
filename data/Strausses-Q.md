#### L-1 Missing checks for `address(0)` when assigning values to address state variables

##### Code snippet:
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L29
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L48
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L64
https://github.com/code-423n4/2024-04-dyad/blob/main/src/periphery/Payments.sol#L47
https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L14


#### L-2 Can be rewritten to consume less gas
`getKeroseneValue` function to this
```solidity
  function getKeroseneValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
      uint totalUsdValue;
      uint numberOfVaults = vaultsKerosene[id].length(); 
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaultsKerosene[id].at(i));
        
        if (keroseneManager.isLicensed(address(vault))) {
          uint usdValue;
          usdValue = vault.getUsdValue(id); 
          totalUsdValue += usdValue;
        }
        
      }
      return totalUsdValue;
  }
```
##### Code snippet:
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L286

#### L-3 Add sanitary check

As a static call to `vault` before adding it to the list

##### Code snippet:
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L25
