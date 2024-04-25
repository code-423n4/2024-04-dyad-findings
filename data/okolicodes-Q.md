## An attacker can set themselves as kerosene manager  

## Impact
The call to `setkeroseneManager` lacks access control as it can be called by anyone. This function has an initializer to it and this means the kerosene manager can only be set once. Calls to this function can be frontrunned by an attacker and thus prevent the appropriate kerosene manager to be set. 
The attacker could keep on executing this attack on multiple users across the protocol and thus leads to undesired/unintended behaviour.
```solidity
 function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager;
  }
```
## Proof of Concept

## Recommended Mitigation Steps
Implement an access control mechanism to allow this function be called by the owner etc in other to guard against this sort of attacks