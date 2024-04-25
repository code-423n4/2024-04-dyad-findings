# [L-1] Griefing is possible on vault removal
In [VaultManagerV2.sol line 101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101)
Since anyone can deposit into a vault, someone can deny removal of a vault if will be able to frontrun removal transaction with a 1 wei deposit. However, this is rated as low at best, since this doesn’t look like efficient and impactful attack vector. 

### Remediation: 
Either allow owner to pause deposits or implement minimum deposit to make attack more expensive. 

# [I-1] Redundant code
In [VaultManagerV2.sol line 17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17)
use of Initializer is not needed, use a simple logic instead of importing a whole contract, which is designed for use with upgradeable contracts. The initializer is not used elsewhere just in that one function, so it's unnecessary to use whole contract. 

### Remediation:
For example the function can look like this, which mimics what initializer does:

```solidity

  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
  
    {
      require(keroseneManager == 0, "Already set!");
      keroseneManager = _keroseneManager;
  }

```