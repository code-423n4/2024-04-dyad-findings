# QA Report for `DYAD`


## QA 1: Unhandled Return Value in Transfer Functions

### Proof of Concept:
In the `deposit` function of the `KerosineVault` contract and the `withdraw` function of the `UnboundedKerosineVault` contract, the return value of the `safeTransferFrom` and `safeTransfer` functions is not handled properly. This can lead to silent failures and inconsistencies in the contract's state.

**Look at the code:** 
`deposit`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L45
`withdraw`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L41
```solidity
function deposit(uint id, uint amount) public onlyVaultManager {
  id2asset[id] += amount;
  emit Deposit(id, amount);
}

function withdraw(uint id, address to, uint amount) external onlyVaultManager {
  id2asset[id] -= amount;
  asset.safeTransfer(to, amount); 
  emit Withdraw(id, to, amount);
}
```

### Impact:
Failing to handle the return value of the transfer functions can result in silent failures, where the transfer may fail without any indication or error. This can lead to inconsistencies between the actual token balances and the recorded balances in the contract's state, potentially causing loss of funds or incorrect accounting.

### Recommended Mitigation Steps:
To mitigate this issue, it is essential to properly handle the return value of the transfer functions and revert the transaction if the transfer fails. This ensures that the contract's state remains consistent and prevents any discrepancies.

Modify the [`deposit`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L45) and [`withdraw`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L41) functions as follows:

```diff
function deposit(uint id, uint amount) public onlyVaultManager {
+  require(asset.safeTransferFrom(msg.sender, address(this), amount), "Transfer failed");
  id2asset[id] += amount;
  emit Deposit(id, amount);
}

function withdraw(uint id, address to, uint amount) external onlyVaultManager {
  id2asset[id] -= amount;
-  asset.safeTransfer(to, amount); 
+  require(asset.safeTransfer(to, amount), "Transfer failed");
  emit Withdraw(id, to, amount);
}
```

By adding a `require` statement to check the return value of the transfer functions, the transaction will revert if the transfer fails, ensuring that the contract's state remains consistent and preventing any silent failures or discrepancies.

## QA 2: Lack of Input Validation

### Proof of Concept:
The `deposit`, `withdraw`, and `move` functions in the contracts lack proper input validation for the `amount` parameter. This allows users to pass invalid or unintended values, such as zero or extremely large amounts, which can lead to unintended behavior and potential vulnerabilities.

**Look at the code:**
`deposit`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L45
`withdraw`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L41
`move`: https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L58

```solidity
function deposit(uint id, uint amount) public onlyVaultManager {
  // ...
}

function withdraw(uint id, address to, uint amount) external onlyVaultManager {
  // ...
}

function move(uint from, uint to, uint amount) external onlyVaultManager {
  // ...
}
```

### Impact:
The absence of input validation for the `amount` parameter can result in several issues:
- Allowing zero-value transfers, which can lead to unnecessary transactions and state changes.
- Permitting extremely large amounts, potentially exceeding the available token balance and causing unexpected behavior or reverts.
- Enabling users to manipulate the contract's state by passing unintended or malicious values.

These issues can compromise the integrity and security of the contract by the Vault manager, leading to potential vulnerabilities and unexpected behavior.

### Recommended Mitigation Steps:
To mitigate this issue, it is crucial to implement proper input validation for the `amount` parameter in the relevant functions. This ensures that only valid and reasonable values are accepted, preventing any unintended behavior or potential exploits.

Modify the functions as follows:

```diff
function deposit(uint id, uint amount) public onlyVaultManager {
+  require(amount > 0, "Deposit amount must be greater than zero");
  // ...
}

function withdraw(uint id, address to, uint amount) external onlyVaultManager {
+  require(amount > 0, "Withdrawal amount must be greater than zero");
+  require(amount <= id2asset[id], "Insufficient balance");
  // ...
}

function move(uint from, uint to, uint amount) external onlyVaultManager {
+  require(amount > 0, "Move amount must be greater than zero");
  // ...
}
```

By adding these validation checks, the contract ensures that only valid and reasonable amounts are accepted, mitigating the risks associated with zero-value transfers, extremely large amounts, and potential manipulation of the contract's state.

## QA 3: Missing Event Emissions for Critical State Changes

### Proof of Concept:
Several critical functions in the contracts modify important state variables without emitting corresponding events. This lack of event emissions hinders the transparency and observability of the contract's behavior, making it difficult for external entities to track and respond to important changes.

**Look at the code:**
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L25
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L64
```solidity
function setKeroseneManager(KerosineManager _keroseneManager) external initializer {
  keroseneManager = _keroseneManager;
}

function  setUnboundedKerosineVault(UnboundedKerosineVault _unboundedKerosineVault) external onlyOwner {
  unboundedKerosineVault = _unboundedKerosineVault; 
}
```

### Impact:
The absence of event emissions for critical state changes can lead to several problems:
- Reduced transparency and auditability of the contract's behavior.
- Difficulty in monitoring and tracking important actions and state transitions.
- Hindered integration with external tools and systems that rely on events for real-time updates and notifications.

This lack of transparency can undermine trust in the contract and make it challenging for users and stakeholders to stay informed about the contract's state and any significant changes.

### Recommended Mitigation Steps:
To address this issue, it is highly recommended to emit events for critical state changes and important actions within the contract. This enhances transparency, improves monitoring capabilities, and facilitates integration with external systems.

Modify the relevant functions to include event emissions:

```diff
+ event KeroseneManagerSet(address indexed keroseneManager);
+
function setKeroseneManager(KerosineManager _keroseneManager) external initializer {
  keroseneManager = _keroseneManager;
+  emit KeroseneManagerSet(address(_keroseneManager));
}

+ event UnboundedKerosineVaultSet(address indexed unboundedKerosineVault);
+
function  setUnboundedKerosineVault(UnboundedKerosineVault _unboundedKerosineVault) external onlyOwner {
  unboundedKerosineVault = _unboundedKerosineVault; 
+  emit UnboundedKerosineVaultSet(address(_unboundedKerosineVault));
}
```

By adding event emissions for critical state changes, such as setting the kerosene manager or initializing the vault, external entities can easily track and respond to these changes in real-time. This improves the overall transparency and auditability of the contract, building trust among users and stakeholders.


## QA 4: Potential Division by Zero

### Proof of Concept:
The `collatRatio` function in the `VaultManagerV2` contract and the `assetPrice` function in the `UnboundedKerosineVault` contract perform division operations without checking for potential division by zero scenarios. If the divisor is zero, it will cause a runtime exception and revert the transaction.

**Look at the code:**
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L239
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L68

```solidity
function collatRatio(uint id) public view returns (uint) {
  uint _dyad = dyad.mintedDyad(address(this), id);
  if (_dyad == 0) return type(uint).max;
  return getTotalUsdValue(id).divWadDown(_dyad);
}

function assetPrice() public view override returns (uint) {
  // ...
  uint denominator = kerosineDenominator.denominator();
  return numerator * 1e8 / denominator;
}
```

### Impact:
Division by zero can lead to unexpected behavior and cause the transaction to revert. If the `_dyad` value in the `collatRatio` function or the `denominator` value in the `assetPrice` function is zero, the division operation will fail, and the function will revert. This can result in the following issues:
- Inability to calculate the collateral ratio or asset price when the divisor is zero.
- Transactions relying on these functions will fail, potentially causing disruption to the contract's functionality and user experience.
- Potential denial of service if the divisor can be manipulated to be zero by an attacker.

### Recommended Mitigation Steps:
To mitigate the risk of division by zero, it is essential to add checks to ensure that the divisor is not zero before performing the division operation. If the divisor is zero, the contract should handle the situation gracefully by returning a default value, reverting with a meaningful error message, or taking an alternative action based on the contract's requirements.

Modify the [`collatRatio`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L239) and [`assetPrice`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L68) functions as follows:

```diff
function collatRatio(uint id) public view returns (uint) {
  uint _dyad = dyad.mintedDyad(address(this), id);
-  if (_dyad == 0) return type(uint).max;
+  require(_dyad != 0, "No minted Dyad for the given ID");
  return getTotalUsdValue(id).divWadDown(_dyad);
}

function assetPrice() public view override returns (uint) {
  // ...
  uint denominator = kerosineDenominator.denominator();
+  require(denominator != 0, "Denominator cannot be zero");
  return numerator * 1e8 / denominator;
}
```

By adding these checks, the contract ensures that division by zero scenarios are explicitly handled. If the divisor is zero, the transaction will revert with a descriptive error message, preventing unexpected behavior and potential exploits.

## QA 5: Inefficient Looping and Storage Access

### Proof of Concept:
The `getTotalUsdValue` function in the `VaultManagerV2` contract and the `assetPrice` function in the `UnboundedKerosineVault` contract contain inefficient looping mechanisms and storage access patterns. These inefficiencies can lead to high gas consumption and potential out-of-gas errors, especially when dealing with a large number of vaults.

**Look at the code:**
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L248
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L68

```solidity
function getTotalUsdValue(uint id) public view returns (uint) {
  return getNonKeroseneValue(id) + getKeroseneValue(id);
}

function assetPrice() public view override returns (uint) {
  uint tvl;
  address[] memory vaults = kerosineManager.getVaults();
  uint numberOfVaults = vaults.length;
  for (uint i = 0; i < numberOfVaults; i++) {
    // ...
  }
  // ...
}
```

### Impact:
Inefficient looping and storage access can have significant consequences:
- High gas consumption: Looping through large arrays and making multiple storage reads can consume a significant amount of gas, leading to expensive transactions and potential out-of-gas errors.
- Scalability issues: As the number of vaults grows, the gas cost of these functions increases linearly, making the contract less scalable and more expensive to use.
- Performance degradation: Inefficient storage access patterns can impact the contract's overall performance, leading to slower execution times and reduced throughput.

These issues can negatively affect the usability and adoption of the contract, as users may face high transaction costs and potential failures when interacting with the contract.

### Recommended Mitigation Steps:
To mitigate the inefficiencies in looping and storage access, consider the following optimizations:

1. Optimize the `getTotalUsdValue` function:
   - Combine the loops for non-kerosene and kerosene values into a single function to reduce the number of iterations.
   - Cache frequently accessed storage variables to minimize repeated storage reads.

   ```diff
   function getTotalUsdValue(uint id) public view returns (uint) {
   -  return getNonKeroseneValue(id) + getKeroseneValue(id);
   +  uint totalValue;
   +  uint numVaults = vaults[id].length();
   +  for (uint i = 0; i < numVaults; i++) {
   +    Vault vault = Vault(vaults[id].at(i));
   +    totalValue += vault.getUsdValue(id);
   +  }
   +  uint numKeroseneVaults = vaultsKerosene[id].length();
   +  for (uint i = 0; i < numKeroseneVaults; i++) {
   +    Vault vault = Vault(vaultsKerosene[id].at(i));
   +    totalValue += vault.getUsdValue(id);
   +  }
   +  return totalValue;
   }
   ```

2. Optimize the `assetPrice` function:
   - Consider caching the TVL value to avoid recalculating it for each function call.
   - Explore alternative approaches to calculate the TVL without looping through all the vaults, such as maintaining a running total or using a separate contract to store and update the TVL value.

   ```diff
   function assetPrice() public view override returns (uint) {
     // ...
   -  uint tvl;
   -  address[] memory vaults = kerosineManager.getVaults();
   -  uint numberOfVaults = vaults.length;
   -  for (uint i = 0; i < numberOfVaults; i++) {
   -    // ...
   -  }
   +  // Consider caching the TVL or using an alternative approach to avoid looping through all vaults
     // ...
   }
   ```

By implementing these optimizations, the contract can reduce gas consumption, improve performance, and enhance scalability. However, it's important to carefully analyze the contract's requirements and consider the trade-offs between gas efficiency and functionality when applying these optimizations.





## QA 6: Lack of Comprehensive Documentation


### Proof of Concept:
The contracts lack detailed NatSpec documentation, which can make it difficult for developers, auditors, and users to understand the purpose, behavior, and potential risks associated with each function and the contract as a whole.

Example:
```solidity
function getTotalUsdValue(uint id) public view returns (uint) {
  return getNonKeroseneValue(id) + getKeroseneValue(id);
}

Dyad public immutable dyad;
KerosineDenominator public kerosineDenominator;
```

### Impact:
The absence of comprehensive documentation can have several consequences:
- Difficulty in understanding the contract: Without clear and detailed documentation, developers, auditors, and users may struggle to grasp the intended behavior and functionality of the contract. This can lead to misinterpretations, incorrect usage, and potential vulnerabilities.
- Increased audit and review time: Lack of documentation makes the audit and security review process more challenging and time-consuming. Auditors need to spend additional effort to understand the contract's logic and potential risks, which can delay the audit process and increase costs.
- Hindered maintainability and upgradability: As the contract evolves and new developers join the project, the lack of documentation can make it difficult for them to understand the existing codebase and make necessary changes or upgrades. This can lead to increased development time, bugs, and potential security issues.
- Reduced user adoption and trust: Comprehensive documentation helps users understand how to interact with the contract, what to expect, and any potential risks involved. Without clear documentation, users may hesitate to use or trust the contract, hindering its adoption and overall success.

### Recommended Mitigation Steps:
To mitigate the issues associated with lack of documentation, it is strongly recommended to add comprehensive NatSpec documentation to the contracts. NatSpec (Ethereum Natural Language Specification) is a standard for documenting Ethereum smart contracts. It uses a specific format and tags to provide structured and readable documentation.

Here are some guidelines for adding NatSpec documentation:

1. Use the `@title` tag to provide a brief title for the contract, explaining its overall purpose.
2. Use the `@notice` tag to provide a concise description of each function, explaining its behavior and any important considerations.
3. Use the `@dev` tag to provide more detailed technical explanations, assumptions, or potential risks associated with each function.
4. Use the `@param` tag to describe the purpose and expected format of each function parameter.
5. Use the `@return` tag to describe the return value(s) of each function.

Example:
```diff
+/**
+ * @title UnboundedKerosineVault
+ * @notice This contract manages Kerosine Vaults with unbounded assets.
+ */
contract UnboundedKerosineVault is KerosineVault {
  // ...

+  /**
+   * @notice Retrieves the total USD value for a given ID.
+   * @dev Calculates the sum of non-kerosene and kerosene values for the specified ID.
+   * @param id The ID for which to retrieve the total USD value.
+   * @return The total USD value for the given ID.
+   */
  function getTotalUsdValue(uint id) public view returns (uint) {
    return getNonKeroseneValue(id) + getKeroseneValue(id);
  }

+  /**
+   * @notice The Dyad contract instance.
+   * @dev This variable is immutable and set during contract deployment.
+   */
  Dyad public immutable dyad;

+  /**
+   * @notice The KerosineDenominator contract instance.
+   * @dev This variable represents the contract responsible for providing the kerosine denominator value.
+   */
  KerosineDenominator public kerosineDenominator;

  // ...
}
```

By adding comprehensive NatSpec documentation, the contracts become more readable, understandable, and maintainable. It helps developers, auditors, and users quickly grasp the purpose and behavior of each function and the contract as a whole. This improves the overall quality of the codebase, facilitates audits and reviews, and enhances user adoption and trust.


## QA 7: Inefficient Contract Size and Redundant Code

### Proof of Concept:
The `VaultManagerV2` and `UnboundedKerosineVault` contracts contain inefficiencies in terms of contract size and redundant code.

**Look at the code:**
```solidity
function getVaults(uint id) external view returns (address[] memory) {
  return vaults[id].values();
}

function hasVault(uint id, address vault) external view returns (bool) {
  return vaults[id].contains(vault);
}
```

```solidity
Dyad public immutable dyad;
KerosineDenominator public kerosineDenominator;
```

### Impact:
Inefficient contract size and redundant code can have the following consequences:
- Increased gas costs: Larger contract sizes result in higher deployment and execution costs. Redundant code and unnecessary functions contribute to the overall contract size, leading to increased gas consumption for users interacting with the contract.
- Reduced readability and maintainability: Redundant code and inefficient contract structure can make the codebase harder to read, understand, and maintain. It increases the cognitive overhead for developers and auditors working with the contract.
- Potential performance issues: Inefficient code and unnecessary computations can impact the contract's performance, especially when dealing with large datasets or complex operations. This can lead to slower execution times and potential bottlenecks.

### Recommended Mitigation Steps:
To optimize contract size and eliminate redundant code, consider the following approaches:

1. Remove redundant getter functions:
   - Instead of defining separate getter functions for accessing public state variables, make the state variables public and directly accessible.
   - This eliminates the need for redundant getter functions and reduces the contract size.

   ```diff
   - function getVaults(uint id) external view returns (address[] memory) {
   -   return vaults[id].values();
   - }
   -
   - function hasVault(uint id, address vault) external view returns (bool) {
   -   return vaults[id].contains(vault);
   - }
   + 
   + mapping (uint => EnumerableSet.AddressSet) public vaults;
   ```

2. Optimize state variable visibility:
   - Review the visibility of state variables and adjust them according to their intended usage.
   - If a state variable is only accessed internally within the contract, consider making it `private` or `internal` to save gas and reduce the contract's attack surface.

   ```diff
   - Dyad public immutable dyad;
   - KerosineDenominator public kerosineDenominator;
   + Dyad internal immutable dyad;
   + KerosineDenominator private kerosineDenominator;
   ```




















