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