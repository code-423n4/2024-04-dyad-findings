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
## C. Non-Compliance with Checks-Effects-Interactions Pattern in Withdraw Function
[VaultManagerV2.sol#L134-L153](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L153)
[VaultManagerV2.sol#L156-L169](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L169)
The withdraw function in the VaultManagerV2 contract does not fully adhere to the Checks-Effects-Interactions (CEI) pattern. The pattern is a best practice in smart contract development to prevent reentrancy attacks. The function signature and relevant code snippet are as follows:
```solidity
function withdraw(
  uint    id,
  address vault,
  uint    amount,
  address to
) 
  public
    isDNftOwner(id)
{
  if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
  // ... (other checks)
  Vault _vault = Vault(vault);
  _vault.withdraw(id, to, amount); // Interaction before final state change
  // ... (additional logic)
  if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
}
```
The function is intended to allow DNft owners to withdraw assets from their vault. It performs several checks, interacts with an external Vault contract to transfer assets, and then performs a final collateralization ratio check.
### Impact: 
The current ordering allows for a potential reentrancy attack, where an attacker could take advantage of the state changes that occur after the external call to the `_vault.withdraw` function.

### Mitigation: 
To mitigate this issue, the function should be refactored to ensure that all state changes, including the final collateralization ratio check, are completed before the external call to `_vault.withdraw`. 
## D. Lack of Two-Step Ownership Transfer in DeployV2 Contract
[Deploy.V2.s.sol#L69](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L69)
[Deploy.V2.s.sol#L90-L91](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L90-L91)
[Deploy.V2.s.sol#L98](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L98)
The `DeployV2` contract lacks a two-step ownership transfer mechanism when transferring ownership of certain contracts. Specifically, in the `run` function of the contract, ownership of the `unboundedKerosineVault`, `boundedKerosineVault`, and `vaultLicenser` contracts is transferred directly to the final owner (`MAINNET_OWNER`) without an intermediate step.
```SOLIDITY
// Transfer ownership to the final owner directly
unboundedKerosineVault.transferOwnership(MAINNET_OWNER);
boundedKerosineVault.transferOwnership(MAINNET_OWNER);
vaultLicenser.transferOwnership(MAINNET_OWNER);
```
This direct transfer of ownership can pose a security risk as it leaves these contracts vulnerable to potential attacks during the ownership transfer process. Without an intermediate step, malicious actors could potentially interfere with the ownership transfer, leading to unintended consequences or loss of control over the contracts.
### Impact:
The lack of a two-step ownership transfer mechanism exposes the contracts to potential attacks during the ownership transfer process. Malicious actors could exploit this vulnerability to gain unauthorized access or control over the contracts, leading to potential loss of funds or disruption of the system's functionality.

### Mitigation:
Implement a two-step ownership transfer mechanism to enhance the security of the contract deployment process.

## E. Inconsistent Function Modifier in BoundedKerosineVault's withdraw Function
[Vault.kerosine.bounded.sol#L32-L42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L42)
The `withdraw` function in the `BoundedKerosineVault` contract is marked with the `view` modifier, indicating that it's a read-only function that won't modify the contract's state. However, within this function, a `revert` statement is used to revert the transaction with an error message, `NotWithdrawable(id, to, amount`). Reverting transactions is a state-changing operation, contradicting the `view` modifier and potentially leading to unexpected behavior or exploitation.
```solidity
function withdraw(
    uint    id,
    address to,
    uint    amount
) 
    external 
    view
    onlyVaultManager
{
    revert NotWithdrawable(id, to, amount);
}
```
### Impact:
The inconsistency in the function modifier could lead to confusion for developers and potentially enable attackers to exploit unexpected behavior, such as bypassing intended access controls or manipulating contract state.

### Mitigation:
Remove the view modifier from the withdraw function to accurately reflect its behavior and ensure consistency with its implementation. Here's the corrected version:

```solidity
function withdraw(
    uint    id,
    address to,
    uint    amount
) 
    external 
    onlyVaultManager
{
    revert NotWithdrawable(id, to, amount);
}
```