## A. KerosineDenominator contract Relies on `MAINNET_OWNER` balance, which is a single point of failure
[KerosineDenominator.sol#L1-L23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L1-L23)
The denominator function calculates a value based on the total supply of the Kerosine token minus the balance held by `MAINNET_OWNER`. Here's the relevant code snippet:
```solidity
function denominator() external view returns (uint) {
  return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
}
```
This function's output is heavily dependent on the balance of a single address, `MAINNET_OWNER`. If this address is compromised or behaves maliciously, it can manipulate the denominator value, which could be critical if it's used for calculating ratios, rewards, or governance decisions.
### Impact:
 A compromised or malicious `MAINNET_OWNER` can skew important system metrics or functionalities that depend on the denominator value, potentially destabilizing the entire contract ecosystem.

### Mitigation: 
Implement a decentralized mechanism for calculating the denominator. This could involve using a smart contract-controlled address with multisig requirements or a DAO structure to distribute control over the `MAINNET_OWNER` balance impact, thus reducing the risk of single-point failure or manipulation.
## B. Risk of Hardcoded Address Dependency
[KerosineDenominator.sol#L1-L23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L1-L23)
The denominator function within the `KerosineDenominator` contract references an address identified as `MAINNET_OWNER`:
```solidity
function denominator() external view returns (uint) {
  return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
}
```
This code suggests that `MAINNET_OWNER` is a critical component in the calculation of the denominator. If `MAINNET_OWNER` is a hardcoded address within the contract or configuration, it presents a risk as the contract's behavior is tied to the state of this specific address, which may not be transparent or adaptable to changes such as ownership transfer or upgradeability.
### Impact: 
The reliance on a potentially hardcoded address could lead to a lack of flexibility and increased risk if the address needs to be updated due to security concerns or operational changes, and the contract does not support such updates.

### Mitigation: 
Replace the hardcoded address with a modifiable state variable that can be updated through a secure governance process. This could involve role-based access control or a multisignature mechanism that allows for address updates without requiring contract migration or redeployment.