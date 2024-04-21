
### Prevent re-setting a state variable with the same value
Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.

```solidity
Path: ./src/core/VaultManagerV2.sol

63:      keroseneManager = _keroseneManager;	// @audit-issue
```
[63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63-L63), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

29:    unboundedKerosineVault = _unboundedKerosineVault;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29-L29), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

47:    kerosineDenominator = _kerosineDenominator;	// @audit-issue
```
[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47-L47), 


#### Recommendation

Implement checks in your Solidity contracts to avoid re-setting state variables to their existing values. Prior to updating a state variable, compare the new value with the current value and proceed with the assignment only if they differ. Additionally, ensure that events related to state variable updates are emitted only when actual changes occur. This approach not only saves gas but also prevents confusion and unnecessary triggers in event listeners. Regularly reviewing and optimizing your contract for such redundancies can significantly enhance efficiency and clarity in contract operations.

### State Variable Access Within a Loop
State variable reads and writes are more expensive than local variable reads and writes. Therefore, it is recommended to replace state variable reads and writes within loops with a local variable. Gas savings should be multiplied by the average loop length.

```solidity
Path: ./src/core/VaultManagerV2.sol

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue: `vaults` used in loop.

259:        Vault vault = Vault(vaults[id].at(i));	// @audit-issue: `vaults` used in loop.

278:        Vault vault = Vault(vaultsKerosene[id].at(i));	// @audit-issue: `vaultsKerosene` used in loop.

280:        if (keroseneManager.isLicensed(address(vault))) {	// @audit-issue: `keroseneManager` used in loop.
```
[223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), [259](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L259-L259), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278-L278), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280-L280), 


#### Recommendation

Optimize gas usage in Solidity by replacing state variable reads and writes within loops with local variable operations. This reduces gas costs significantly, especially when multiplied by the average loop length.

### Another Constant With Same Value Is Already Defined
Defining multiple constants with the same value in a Solidity contract introduces unnecessary redundancy and can lead to confusion and potential errors in contract maintenance. Constants are used to define values that remain unchanged throughout the contract's lifecycle, enhancing readability and efficiency. However, when multiple constants representing the same value are defined, it not only clutters the code but also complicates the process of updating values and understanding the contract's logic. Consolidating these constants into a single definition improves code clarity and maintainability.

```solidity
Path: ./src/core/VaultManagerV2.sol

23:  uint public constant MAX_VAULTS_KEROSENE = 5;	// @audit-issue: Same value `5` is already defined on line `22` as variable: `MAX_VAULTS`
```
[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23-L23), 


#### Recommendation

Identify and consolidate duplicate constants in your Solidity contracts. Examine your contract's constants to find any with identical values and refactor your code to use a single constant definition for each unique value. This may involve choosing the most descriptive and appropriate name for the consolidated constant and updating all references accordingly. Such consolidation not only makes your contract more concise and easier to read but also simplifies future updates to constant values. Document the purpose and usage of each constant clearly, ensuring that the chosen names accurately reflect their role within the contract.

### Unnecessary casting as variable is already of the same type
In Solidity, explicitly casting a variable to a type that it already represents is redundant and can lead to confusion and clutter in the code. This unnecessary casting doesn't typically consume additional gas since Solidity's optimizer often removes such redundant conversions during compilation. However, it does affect code readability and may obscure the actual intent of the code, making it harder for developers to understand and maintain. Ensuring that casting is used only when necessary helps maintain clean, clear, and efficient code.

```solidity
Path: ./src/core/VaultManagerV2.sol

129:    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);	// @audit-issue: Variable `vault` is converted to `address` from type `address`.
```
[129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129-L129), 


#### Recommendation

Review your Solidity code for instances of unnecessary casting where variables are cast to their own type. Remove these redundant casts to enhance code clarity and maintainability. When writing new code, ensure that casting is only applied when changing a variable's type is genuinely needed. This practice helps in keeping the codebase straightforward and understandable, reducing potential confusion and errors associated with misinterpreting the variable types.

### Unused Modifier
Modifier is declared in the project, but never used.

```solidity
Path: ./src/core/VaultManagerV2.sol

45:  modifier isLicensed(address vault) {	// @audit-issue
```
[45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45-L45), 


#### Recommendation

Remove redundant code..

### Optimization of Loop Control for Early Termination
The identified issue is a common inefficiency in programming related to loop control during search operations. In the current implementation, loops are designed to traverse through the entire dataset (like arrays or lists) even after the required condition has been met or the target element has been found. This lack of early termination results in unnecessary processing and can lead to increased execution times, particularly in large datasets. The issue is not about the correctness of the function but its efficiency, as continuing the loop after meeting the required condition is redundant and wastes computational resources.

```solidity
Path: ./src/core/VaultManagerV2.sol

258:      for (uint i = 0; i < numberOfVaults; i++) {
259:        Vault vault = Vault(vaults[id].at(i));
260:        uint usdValue;
261:        if (vaultLicenser.isLicensed(address(vault))) {
262:          usdValue = vault.getUsdValue(id);        	// @audit-issue

277:      for (uint i = 0; i < numberOfVaults; i++) {
278:        Vault vault = Vault(vaultsKerosene[id].at(i));
279:        uint usdValue;
280:        if (keroseneManager.isLicensed(address(vault))) {
281:          usdValue = vault.getUsdValue(id);        	// @audit-issue
```
[262](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258-L262), [281](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277-L281), 


#### Recommendation

To optimize such functions, it is recommended to incorporate an early exit mechanism within the loop. This can be achieved by introducing a `break` statement (or an equivalent control structure) immediately after the condition is satisfied or the target element is located. This approach ensures that the loop terminates as soon as its objective is achieved, preventing further unnecessary iterations. Implementing this optimization will enhance the performance, especially in scenarios involving large data sets or resource-intensive operations, by minimizing the time and resources expended on redundant processing. This optimization strategy is applicable and beneficial across various programming languages and scenarios where loop-based search or check operations are utilized.

### Multiple accesses of a mapping/array should use a local variable cache
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's keccak256 hash (Gkeccak256 - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

```solidity
Path: ./src/core/VaultManagerV2.sol

76:    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();	// @audit-issue: Same index access of variable `vaults` is used also on line(s): ['74'].

87:    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();	// @audit-issue: Same index access of variable `vaultsKerosene` is used also on line(s): ['89'].

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue: Same index access of variable `vaults` is used also on line(s): ['221'].

257:      uint numberOfVaults = vaults[id].length(); 	// @audit-issue: Same index access of variable `vaults` is used also on line(s): ['259'].

278:        Vault vault = Vault(vaultsKerosene[id].at(i));	// @audit-issue: Same index access of variable `vaultsKerosene` is used also on line(s): ['276'].
```
[76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87-L87), [223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), [257](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L257-L257), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278-L278), 


#### Recommendation

When a mapping or array value is accessed multiple times within a function, cache it in a local `storage` or `calldata` variable. This approach minimizes the gas cost by reducing the number of hash computations for mappings and offset calculations for arrays. Carefully review your functions to identify opportunities for such optimizations, especially in functions with frequent or repeated accesses to the same mapping or array element, to enhance gas efficiency in your contracts.

### State Variables That Are Used Multiple Times In a Function Should Be Cached In Stack Variables
When performing multiple operations on a state variable in a function, it is recommended to cache it first. Either multiple reads or multiple writes to a state variable can save gas by caching it on the stack. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses. Saves 100 gas per instance.


```solidity
Path: ./src/core/VaultManagerV2.sol

76:    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();	// @audit-issue: State variable `vaults` is used also on line(s): ['74'].

87:    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();	// @audit-issue: State variable `vaultsKerosene` is used also on line(s): ['89'].

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue: State variable `vaults` is used also on line(s): ['221'].

257:      uint numberOfVaults = vaults[id].length(); 	// @audit-issue: State variable `vaults` is used also on line(s): ['259'].

278:        Vault vault = Vault(vaultsKerosene[id].at(i));	// @audit-issue: State variable `vaultsKerosene` is used also on line(s): ['276'].
```
[76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87-L87), [223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), [257](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L257-L257), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278-L278), 


#### Recommendation

Cache state variables in stack or local memory variables within functions when they are used multiple times. This approach replaces costlier Gwarmaccess operations with cheaper stack reads, saving approximately 100 gas per instance and optimizing overall contract performance.

### Divisions can be unchecked to save gas
The expression type(int).min/(-1) is the only case where division causes an overflow. Therefore, uncheck can be used to save gas in scenarios where it is certain that such an overflow will not occur.

```solidity
Path: ./src/core/VaultManagerV2.sol

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue

195:      uint asset = amount 	// @audit-issue
```
[146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L146), [195](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L195-L195), 


```solidity
Path: ./src/core/Vault.kerosine.sol

66:      return id2asset[id] * assetPrice() / 1e8;	// @audit-issue
```
[66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L66-L66), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue

67:      return numerator * 1e8 / denominator;	// @audit-issue
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L60), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67-L67), 


#### Recommendation

Utilize 'unchecked' blocks in Solidity for divisions where overflow is impossible, such as when 'type(int).min/(-1)' is not a concern. This can save gas by bypassing overflow checks in these specific cases.

### Stack variable is only used once
If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend

```solidity
Path: ./src/core/VaultManagerV2.sol

144:    uint dyadMinted = dyad.mintedDyad(address(this), id);	// @audit-issue: dyadMinted used only on line: 150

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue: value used only on line: 150
147:                  * 1e18 
148:                  / 10**_vault.oracle().decimals() 
149:                  / 10**_vault.asset().decimals();

164:    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;	// @audit-issue: newDyadMinted used only on line: 165

218:      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);	// @audit-issue: liquidationEquityShare used only on line: 219
```
[144](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L144-L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L149), [164](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L164-L164), [218](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L218-L218), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

65:      uint numerator   = tvl - dyad.totalSupply();	// @audit-issue: numerator used only on line: 67

66:      uint denominator = kerosineDenominator.denominator();	// @audit-issue: denominator used only on line: 67
```
[65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L66-L66), 


#### Recommendation

Eliminate single-use stack variables in Solidity to optimize gas consumption. Directly use the assigned value in the place of the variable. This approach saves the 3 gas typically used for the extra stack assignment, streamlining the function's execution and enhancing overall gas efficiency.

### Consider pre-calculating the address of `address(this)` to save gas
Use `foundry`'s [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady`'s [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

```solidity
Path: ./src/core/VaultManagerV2.sol

144:    uint dyadMinted = dyad.mintedDyad(address(this), id);	// @audit-issue

164:    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;	// @audit-issue

215:      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));	// @audit-issue

236:      uint _dyad = dyad.mintedDyad(address(this), id);	// @audit-issue
```
[144](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L144-L144), [164](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L164-L164), [215](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L215-L215), [236](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L236-L236), 


#### Recommendation

To enhance gas efficiency, cache the contract's address by storing `address(this)` in a state variable at the point of contract deployment or initialization. Use this cached address throughout the contract instead of repeatedly calling `address(this)`. This practice reduces the gas cost associated with multiple computations of the contract's address, leading to more efficient contract execution, especially in scenarios with frequent usage of the contract's address.

### Counting down in for statements is more gas efficient
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

```solidity
Path: ./src/core/VaultManagerV2.sol

222:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

258:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

277:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222-L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258-L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277-L277), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

58:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58-L58), 


#### Recommendation

Where feasible, refactor `for` loops in your Solidity contracts to count downwards. Adjust the loop initialization, condition, and iteration statements to decrement the loop variable and terminate the loop when it reaches zero. This approach can lead to gas savings, making your contract more efficient in terms of execution costs. Ensure that this refactoring aligns with the logic and requirements of your contract, and thoroughly test to confirm that the revised loop behavior matches the intended functionality.

### Consider using solady's 'FixedPointMathLib'
Using Solady's "FixedPointMathLib" for multiplication or division operations in Solidity can lead to significant gas savings. This library is designed to optimize fixed-point arithmetic operations, which are common in financial calculations involving tokens or currencies. By implementing more efficient algorithms and assembly optimizations, "FixedPointMathLib" minimizes the computational resources required for these operations. For contracts that frequently perform such calculations, integrating this library can reduce transaction costs, thereby enhancing overall performance and cost-effectiveness. However, developers must ensure compatibility with their existing codebase and thoroughly test for accuracy and expected behavior to avoid any unintended consequences.

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

49:      return unboundedKerosineVault.assetPrice() * 2;	// @audit-issue
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L49-L49), 


```solidity
Path: ./src/core/Vault.kerosine.sol

66:      return id2asset[id] * assetPrice() / 1e8;	// @audit-issue
```
[66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L66-L66), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue

67:      return numerator * 1e8 / denominator;	// @audit-issue
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L60), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67-L67), 


#### Recommendation

Consider integrating Solady's 'FixedPointMathLib' into your Solidity contracts for optimized fixed-point arithmetic operations. This library can provide substantial gas savings and enhance the performance of your contract. Before integration, evaluate how 'FixedPointMathLib' aligns with your contract’s requirements. Ensure thorough testing for accuracy and compatibility with your existing contract logic. Carefully document any changes and keep track of how these optimizations affect your contract's operations to maintain transparency and reliability in your application. Adopting 'FixedPointMathLib' should be a considered decision, balancing the benefits of gas efficiency with the need for maintaining code clarity and functionality.

### Reduce Gas Usage by Moving to Solidity 0.8.19 or Later
This issue highlights the opportunity to reduce gas consumption in a smart contract by upgrading the Solidity compiler version to 0.8.19 or a later release. Gas usage is a critical consideration in Ethereum smart contracts, as it directly affects transaction costs and contract execution efficiency. Newer compiler versions often come with optimizations and improvements that can lead to reduced gas costs for certain operations and contract structures.


```solidity
Path: ./src/staking/KerosineDenominator.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2-L2), 


```solidity
Path: ./src/core/VaultManagerV2.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2-L2), 


```solidity
Path: ./src/core/KerosineManager.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2-L2), 


#### Recommendation

Consider upgrading to Solidity version 0.8.19 or later to leverage compiler optimizations for reduced gas consumption. Newer versions often include improvements that enhance transaction cost-efficiency and overall contract execution.

### Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead
When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.
https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html Each operation involving a `uint8` costs an extra [22-28](https://gist.github.com/IllIllI000/9388d20c70f9a4632eb3ca7836f54977) gas (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving `uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the `uint8`, as well as the associated stack operations of doing so. Use a larger size then downcast where needed


```solidity
Path: ./src/core/VaultManagerV2.sol

22:  uint public constant MAX_VAULTS          = 5;	// @audit-issue

23:  uint public constant MAX_VAULTS_KEROSENE = 5;	// @audit-issue

25:  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%	// @audit-issue

26:  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%	// @audit-issue

34:  mapping (uint => EnumerableSet.AddressSet) internal vaults; 	// @audit-issue

35:  mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 	// @audit-issue

37:  mapping (uint => uint) public idToBlockOfLastDeposit;	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26-L26), [34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L35-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L37-L37), 


```solidity
Path: ./src/core/KerosineManager.sol

14:  uint public constant MAX_VAULTS = 10;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14-L14), 


```solidity
Path: ./src/core/Vault.kerosine.sol

19:  mapping(uint => uint) public id2asset;	// @audit-issue
```
[19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L19-L19), 


#### Recommendation

Minimize gas overhead by using 'uint256' or 'int256' instead of smaller integer types in Solidity contracts. The EVM operates more efficiently with 32-byte sizes. Downcast to smaller types only when necessary, as operations with smaller types like 'uint8' incur extra gas due to additional EVM operations for size adjustment.

### Refactor modifiers to call a local function
Modifiers code is copied in all instances where it's used, increasing bytecode size. If deployment gas costs are a concern for this contract, refactoring modifiers into functions can reduce bytecode size significantly at the cost of one JUMP.

```solidity
Path: ./src/core/VaultManagerV2.sol

39:  modifier isDNftOwner(uint id) {	// @audit-issue

42:  modifier isValidDNft(uint id) {	// @audit-issue

45:  modifier isLicensed(address vault) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42-L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45-L45), 


```solidity
Path: ./src/core/Vault.kerosine.sol

21:  modifier onlyVaultManager() {	// @audit-issue
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21-L21), 


#### Recommendation

Evaluate your contract's use of modifiers, particularly those applied across multiple functions, to identify candidates for refactoring into functions. Convert these modifiers into external or public functions that perform the same checks or actions. Then, replace the modifier usage in function declarations with calls to these functions at the start of your functions

### Avoid Unnecessary Public Variables
Public state variables in Solidity automatically generate getter functions, increasing contract size and potentially leading to higher deployment and interaction costs. To optimize gas usage and contract efficiency, minimize the use of public variables unless external access is necessary. Instead, use internal or private visibility combined with explicit getter functions when required. This practice not only reduces contract size but also provides better control over data access and manipulation, enhancing security and readability. Prioritize lean, efficient contracts to ensure cost-effectiveness and better performance on the blockchain.

```solidity
Path: ./src/staking/KerosineDenominator.sol

9:  Kerosine public kerosine;	// @audit-issue
```
[9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L9-L9), 


```solidity
Path: ./src/core/VaultManagerV2.sol

22:  uint public constant MAX_VAULTS          = 5;	// @audit-issue

23:  uint public constant MAX_VAULTS_KEROSENE = 5;	// @audit-issue

25:  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%	// @audit-issue

26:  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%	// @audit-issue

28:  DNft     public immutable dNft;	// @audit-issue

29:  Dyad     public immutable dyad;	// @audit-issue

30:  Licenser public immutable vaultLicenser;	// @audit-issue

32:  KerosineManager public keroseneManager;	// @audit-issue

37:  mapping (uint => uint) public idToBlockOfLastDeposit;	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26-L26), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L28-L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L29-L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L30-L30), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L32-L32), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L37-L37), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

15:  UnboundedKerosineVault public unboundedKerosineVault;	// @audit-issue

16:	// @audit-issue

17:  constructor(	// @audit-issue

19:    ERC20           _asset, 	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17-L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L19-L19), 


```solidity
Path: ./src/core/KerosineManager.sol

14:  uint public constant MAX_VAULTS = 10;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14-L14), 


```solidity
Path: ./src/core/Vault.kerosine.sol

15:  IVaultManager   public immutable vaultManager;	// @audit-issue

16:  ERC20           public immutable asset;	// @audit-issue

17:  KerosineManager public immutable kerosineManager;	// @audit-issue

19:  mapping(uint => uint) public id2asset;	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L17-L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L19-L19), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue

16:  using SafeTransferLib for ERC20;	// @audit-issue

17:	// @audit-issue

19:  KerosineDenominator  public kerosineDenominator;	// @audit-issue

18:  Dyad                 public immutable dyad;	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L17-L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L19-L19), [18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L18-L18), 


#### Recommendation

Avoid creating explicit getter functions for 'public' state variables in Solidity. The compiler automatically generates getters for such variables, making additional functions redundant. This practice helps reduce contract size, lowers deployment costs, and simplifies maintenance and understanding of the contract.

### Use `do while` loops intead of for loops
A `do while` loop will cost less gas since the condition is not being checked for the first iteration.
```solidity
uint256 i = 1;
do {                   
    param2 += i;
    i++;
}
while (i < 50);
``` 
is better than
```solidity
for(uint256 i = 1; i< 50; i++){
    param1 += i;
}
```


```solidity
Path: ./src/core/VaultManagerV2.sol

222:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

258:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

277:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222-L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258-L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277-L277), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

58:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58-L58), 


#### Recommendation

Where appropriate, consider using a `do while` loop instead of a `for` loop in your Solidity contracts. This is especially beneficial when the first iteration of the loop does not require a condition check. Refactor your loop logic to fit the `do while` structure for more gas-efficient execution. However, ensure that the loop's logic and termination conditions are correctly implemented to avoid infinite loops or other logical errors. Always balance gas efficiency with code readability and the specific requirements of your contract's logic.

### Using XOR (^) and AND (&) bitwise equivalents for gas optimizations
Given 4 variables a, b, c and d represented as such:
```
0 0 0 0 0 1 1 0 <- a
0 1 1 0 0 1 1 0 <- b
0 0 0 0 0 0 0 0 <- c
1 1 1 1 1 1 1 1 <- d
```
To have a == b means that every 0 and 1 match on both variables. Meaning that a XOR (operator ^) would evaluate to 0 ((a ^ b) == 0), as it excludes by definition any equalities.Now, if a != b, this means that there’s at least somewhere a 1 and a 0 not matching between a and b, making (a ^ b) != 0.Both formulas are logically equivalent and using the XOR bitwise operator costs actually the same amount of gas.However, it is much cheaper to use the bitwise OR operator (|) than comparing the truthy or falsy values.These are logically equivalent too, as the OR bitwise operator (|) would result in a 1 somewhere if any value is not 0 between the XOR (^) statements, meaning if any XOR (^) statement verifies that its arguments are different.


```solidity
Path: ./src/core/VaultManagerV2.sol

43:    if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;	// @audit-issue

143:    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();	// @audit-issue

237:      if (_dyad == 0) return type(uint).max;	// @audit-issue
```
[43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43-L43), [143](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L143-L143), [237](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L237-L237), 


#### Recommendation

Review your Solidity contracts to identify any computations that are performed multiple times with the same inputs. Cache the results of these computations in local variables and reuse them within the function or across function calls if the state remains unchanged.

### The result of a function call should be cached rather than re-calling the function
The function calls in solidity are expensive. If the same result of the same function calls are to be used several times, the result should be cached to reduce the gas consumption of repeated calls.        

```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue: Function call `asset` is called multiple times at lines [62].
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L60), 


#### Recommendation

Cache the result of function calls in Solidity instead of making repeated calls to the same function. This practice significantly reduces gas consumption by minimizing costly function call operations.

### Avoid updating storage when the value hasn't changed
Manipulating storage in solidity is gas-intensive. It can be optimized by avoiding unnecessary storage updates when the new value equals the existing value. If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (2900 gas), potentially at the expense of a Gcoldsload (2100 gas) or a Gwarmaccess (100 gas).

```solidity
Path: ./src/core/VaultManagerV2.sol

63:      keroseneManager = _keroseneManager;	// @audit-issue
```
[63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63-L63), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

29:    unboundedKerosineVault = _unboundedKerosineVault;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29-L29), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

47:    kerosineDenominator = _kerosineDenominator;	// @audit-issue
```
[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47-L47), 


#### Recommendation

Optimize gas usage by avoiding storage updates in Solidity when the new value is the same as the existing one. This prevents unnecessary gas expenditure from storage resets, balancing the cost against cold or warm storage access as needed.

### Functions guaranteed to `revert` when called by normal users can be marked `payable`
If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

23:  function setUnboundedKerosineVault(	// @audit-issue

32:  function withdraw(	// @audit-issue
```
[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23-L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L32), 


```solidity
Path: ./src/core/KerosineManager.sol

18:  function add(	// @audit-issue

28:  function remove(	// @audit-issue
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18-L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28-L28), 


```solidity
Path: ./src/core/Vault.kerosine.sol

36:  function deposit(	// @audit-issue

47:  function move(	// @audit-issue
```
[36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47-L47), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

30:  function withdraw(	// @audit-issue

43:  function setDenominator(KerosineDenominator _kerosineDenominator) 	// @audit-issue
```
[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43-L43), 


#### Recommendation

Mark functions with access restrictions like 'onlyOwner' as 'payable' in Solidity. This reduces gas costs for legitimate callers by removing the compiler's checks for incoming payments, as the function will revert for unauthorized users anyway.

### Multiple mappings can be replaced with a single struct mapping
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

```solidity
Path: ./src/core/VaultManagerV2.sol

35:  mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 	// @audit-issue: Can be combined with: 
	 vaults in VaultManagerV2 at line: 34
```
[35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L35-L35), 


#### Recommendation

Refactor your Solidity contracts to replace multiple related mappings with a single mapping that uses a struct. This struct should contain all the fields that were previously in separate mappings. This consolidation optimizes storage usage by reducing the number of storage slots and hash computations required, leading to significant gas savings. Ensure that the fields within the struct are logically related and frequently accessed or modified together. This strategy is most effective when the size of struct fields allows them to fit within a single storage slot, maximizing the benefits of the EVM's storage packing capabilities.

### Operator `>=`/`<=` costs less gas than operator `>`/`<`
The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behaviour applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`.


```solidity
Path: ./src/core/VaultManagerV2.sol

217:      uint cappedCr               = cr < 1e18 ? 1e18 : cr;	// @audit-issue
```
[217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217-L217), 


#### Recommendation

Opt for '>=', '<=' operators over '>' and '<' in Solidity where logically appropriate, as they consume less gas. This is because '>=' and '<=' require only one opcode ('LT' or 'GT'), compared to the two opcodes ('GT'/'LT' and 'ISZERO') needed for '>' and '<'.

### Constructor Can Be Marked As Payable
`payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A `constructor` can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds.



```solidity
Path: ./src/staking/KerosineDenominator.sol

11:  constructor(	// @audit-issue
```
[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11-L11), 


```solidity
Path: ./src/core/VaultManagerV2.sol

49:  constructor(	// @audit-issue
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49-L49), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

17:  constructor(	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.sol

26:  constructor(	// @audit-issue
```
[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26-L26), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

21:  constructor(	// @audit-issue
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21-L21), 


#### Recommendation

Mark constructors as 'payable' in Solidity contracts to reduce gas costs, as this eliminates the need for the compiler to add checks against incoming payments. This is safe because only the deployer can send funds during contract creation, and typically no funds are sent at this stage.

### Optimize names to save gas
`public`/`external` function names and `public` member variable names can be optimized to save gas. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92).


```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Optimize gas usage by renaming 'public'/'external' functions and 'public' member variables in Solidity. Aim for shorter and more efficient names, especially for frequently called functions. This can save gas during deployment and reduce gas costs per call due to lower method ID sorting positions.

### Consider activating `via-ir` for deploying
The IR-based code generator was developed to make code generation more performant by enabling optimization passes that can be applied across functions.

It is possible to activate the IR-based code generator through the command line by using the flag `--via-ir`or by including the option `{"viaIR": true}`.

Keep in mind that compiling with this option may take longer. However, you can simply test it before deploying your code. If you find that it provides better performance, you can add the `--via-ir` flag to your deploy command.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Consider activating `via-ir`.

### Optimize Deployment Size by Fine-tuning IPFS Hash
The Solidity compiler appends 53 bytes of metadata to the smart contract code, incurring an extra cost of 10,600 gas. This additional expense arises from 200 gas per bytecode, plus calldata cost, which amounts to 16 gas for non-zero bytes and 4 gas for zero bytes. This results in a maximum of 848 extra gas in calldata cost.

Reducing this cost is crucial for the following reasons:

The metadata's 53-byte addition leads to a deployment cost increase of 10,600 gas. It can also result in an additional calldata cost of up to 848 gas. Ways to Minimize Gas Consumption:

Employ the `--no-cbor-metadata` compiler option to exclude metadata. Be cautious as this might impact contract verification. Search for code comments that yield an IPFS hash with more zeros, thereby reducing calldata costs.

```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

To optimize deployment size and reduce associated costs, consider the following strategies:
1. **Exclude Metadata with Compiler Option**: Use the `solc` compiler’s `--metadata-hash none` or `--no-cbor-metadata` option to prevent the inclusion of metadata in the compiled bytecode. This action reduces the bytecode size, thus lowering deployment gas costs. However, exercise caution with this approach, as it might affect the ability to verify the contract on platforms like Etherscan.

2. **Optimize IPFS Hash for More Zeros**: If excluding metadata is not desirable, another approach involves optimizing code comments or elements that influence the metadata hash generation to achieve an IPFS hash with a higher proportion of zeros. Since calldata costs are lower for zero bytes, a metadata hash with more zeros can reduce the calldata costs associated with contract interactions.

Example for excluding metadata:
```bash
solc --metadata-hash none YourContract.sol
```


### Assembly: Use scratch space for building calldata
If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

```solidity
Path: ./src/staking/KerosineDenominator.sol

21:    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);	// @audit-issue
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L21-L21), 


```solidity
Path: ./src/core/VaultManagerV2.sol

40:    if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;	// @audit-issue

43:    if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;	// @audit-issue

46:    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;	// @audit-issue

74:    if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();	// @audit-issue

75:    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();	// @audit-issue

76:    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();	// @audit-issue

87:    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();	// @audit-issue

88:    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();	// @audit-issue

89:    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();	// @audit-issue

101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();	// @audit-issue

102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();	// @audit-issue

113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();	// @audit-issue

114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();	// @audit-issue

129:    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);	// @audit-issue

130:    _vault.deposit(id, amount);	// @audit-issue

144:    uint dyadMinted = dyad.mintedDyad(address(this), id);	// @audit-issue

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue

148:                  / 10**_vault.oracle().decimals() 	// @audit-issue

149:                  / 10**_vault.asset().decimals();	// @audit-issue

164:    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;	// @audit-issue

196:                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 	// @audit-issue

197:                    / _vault.assetPrice() 	// @audit-issue

215:      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));	// @audit-issue

218:      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);	// @audit-issue

219:      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);	// @audit-issue

221:      uint numberOfVaults = vaults[id].length();	// @audit-issue

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue

224:          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);	// @audit-issue

236:      uint _dyad = dyad.mintedDyad(address(this), id);	// @audit-issue

238:      return getTotalUsdValue(id).divWadDown(_dyad);	// @audit-issue

257:      uint numberOfVaults = vaults[id].length(); 	// @audit-issue

259:        Vault vault = Vault(vaults[id].at(i));	// @audit-issue

261:        if (vaultLicenser.isLicensed(address(vault))) {	// @audit-issue

262:          usdValue = vault.getUsdValue(id);        	// @audit-issue

276:      uint numberOfVaults = vaultsKerosene[id].length(); 	// @audit-issue

278:        Vault vault = Vault(vaultsKerosene[id].at(i));	// @audit-issue

280:        if (keroseneManager.isLicensed(address(vault))) {	// @audit-issue

281:          usdValue = vault.getUsdValue(id);        	// @audit-issue

296:      return vaults[id].values();	// @audit-issue

306:      return vaults[id].contains(vault);	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L46-L46), [74](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L114-L114), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129-L129), [130](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L130-L130), [144](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L144-L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L146), [148](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L148-L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L149-L149), [164](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L164-L164), [196](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L196-L196), [197](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L197-L197), [215](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L215-L215), [218](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L218-L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L219-L219), [221](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L221-L221), [223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), [224](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L224-L224), [236](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L236-L236), [238](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L238-L238), [257](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L257-L257), [259](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L259-L259), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261-L261), [262](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L262-L262), [276](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L276-L276), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278-L278), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280-L280), [281](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L281-L281), [296](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L296-L296), [306](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L306-L306), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

49:      return unboundedKerosineVault.assetPrice() * 2;	// @audit-issue
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L49-L49), 


```solidity
Path: ./src/core/KerosineManager.sol

24:    if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();	// @audit-issue

25:    if (!vaults.add(vault))            revert VaultAlreadyAdded();	// @audit-issue

34:    if (!vaults.remove(vault)) revert VaultNotFound();	// @audit-issue

41:      return vaults.values();	// @audit-issue

50:      return vaults.contains(vault);	// @audit-issue
```
[24](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L25-L25), [34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L34-L34), [41](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L41-L41), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L50-L50), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

39:    asset.safeTransfer(to, amount); 	// @audit-issue

56:      address[] memory vaults = kerosineManager.getVaults();	// @audit-issue

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue

61:                * vault.assetPrice() * 1e18	// @audit-issue

62:                / (10**vault.asset().decimals()) 	// @audit-issue

63:                / (10**vault.oracle().decimals());	// @audit-issue

65:      uint numerator   = tvl - dyad.totalSupply();	// @audit-issue

66:      uint denominator = kerosineDenominator.denominator();	// @audit-issue
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L39-L39), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L56-L56), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L60), [61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L61-L61), [62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62-L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63-L63), [65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L66-L66), 


#### Recommendation

Review your smart contracts to identify and remove `block.number` and `block.timestamp` from the parameters of emitted events. Instead of manually adding these fields, rely on the Ethereum blockchain's inherent inclusion of this information within the block context. Simplify your event definitions to include only the essential data specific to the event's purpose, excluding universally available block metadata.

### Use assembly to check for `0`
Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

```solidity
Path: ./src/core/VaultManagerV2.sol

101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();	// @audit-issue

113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();	// @audit-issue

237:      if (_dyad == 0) return type(uint).max;	// @audit-issue
```
[101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101-L101), [113](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L113-L113), [237](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L237-L237), 


#### Recommendation

To optimize gas usage in your Solidity code, consider using inline assembly for checking `0`. This approach can significantly reduce gas costs, especially in high-frequency or gas-sensitive operations, leading to more efficient contract execution.

### Use assembly to write `address` storage values
Using assembly `{ sstore(state.slot, addr)}` instead of `state = addr` can save gas.


```solidity
Path: ./src/staking/KerosineDenominator.sol

14:    kerosine = _kerosine;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14-L14), 


```solidity
Path: ./src/core/VaultManagerV2.sol

54:    dNft          = _dNft;	// @audit-issue

55:    dyad          = _dyad;	// @audit-issue

56:    vaultLicenser = _licenser;	// @audit-issue

63:      keroseneManager = _keroseneManager;	// @audit-issue
```
[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54-L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55-L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56-L56), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63-L63), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

29:    unboundedKerosineVault = _unboundedKerosineVault;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29-L29), 


```solidity
Path: ./src/core/Vault.kerosine.sol

31:    vaultManager    = _vaultManager;	// @audit-issue

33:    kerosineManager = _kerosineManager;	// @audit-issue
```
[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31-L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33-L33), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

27:      dyad = _dyad;	// @audit-issue

47:    kerosineDenominator = _kerosineDenominator;	// @audit-issue
```
[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27-L27), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47-L47), 


#### Recommendation

To reduce gas costs in your Solidity code, consider using assembly with `{ sstore(state.slot, addr) }` for writing `address` storage values instead of `state = addr`. This approach can result in significant gas savings.

### Use assembly to emit an `event`
To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.


```solidity
Path: ./src/core/VaultManagerV2.sol

77:    emit Added(id, vault);	// @audit-issue

90:    emit Added(id, vault);	// @audit-issue

103:    emit Removed(id, vault);	// @audit-issue

115:    emit Removed(id, vault);	// @audit-issue

168:    emit MintDyad(id, amount, to);	// @audit-issue

180:    emit BurnDyad(id, amount, msg.sender);	// @audit-issue

200:      emit RedeemDyad(id, vault, amount, to);	// @audit-issue

227:      emit Liquidate(id, msg.sender, to);	// @audit-issue
```
[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77-L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90-L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L103-L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L115-L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168-L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L180-L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200-L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L227-L227), 


```solidity
Path: ./src/core/Vault.kerosine.sol

44:    emit Deposit(id, amount);	// @audit-issue

57:    emit Move(from, to, amount);	// @audit-issue
```
[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L44-L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L57-L57), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

40:    emit Withdraw(id, to, amount);	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40-L40), 


#### Recommendation

To optimize event emission in your Solidity code, consider using assembly with scratch space and the free memory pointer. This approach can help reduce gas costs by avoiding memory expansion expenses. However, it's crucial to ensure safe optimization by caching and restoring the free memory pointer, as demonstrated in examples like Solady's codebase.

### Use assembly to validate `msg.sender`
We can use assembly to efficiently validate `msg.sender` with the least amount of opcodes necessary. For more details check the following report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender)


```solidity
Path: ./src/core/VaultManagerV2.sol

40:    if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40-L40), 


```solidity
Path: ./src/core/Vault.kerosine.sol

22:    if (msg.sender != address(vaultManager)) revert NotVaultManager();	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L22-L22), 


#### Recommendation

To optimize the validation of `msg.sender` in your Solidity code, consider using assembly to achieve this with the minimum number of opcodes required. You can refer to the detailed report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender) for more insights and examples on efficient implementation.
