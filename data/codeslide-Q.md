2024-04-dyad QA Report
___
## Table of Contents
1. [Summary](#summary)

    1. [Low Risk Issues](#summary-low-risk-issues)

    1. [Non-Critical Issues](#summary-non-critical-issues)

1. [Details](#details)

    1. [Low Risk Issues](#details-low-risk-issues)

    1. [Non-Critical Issues](#details-non-critical-issues)
___
## <a id="summary"></a> Summary

### <a id="summary-low-risk-issues"></a> Low Risk Issues
There are 34 instances over 6 issues.
|      ID       | Description                                                                                                          | Count |
| :-----------: | :------------------------------------------------------------------------------------------------------------------- | ----: |
| [L-01](#l-01) | Critical functions should be a two step procedure                                                                    |     2 |
| [L-02](#l-02) | `for` and `while` loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS |     4 |
| [L-03](#l-03) | Large transfers may not work with some `ERC20` tokens                                                                |     2 |
| [L-04](#l-04) | Missing zero address check in constructor/initializer                                                                |     5 |
| [L-05](#l-05) | Missing zero address check in functions with address parameters                                                      |    15 |
| [L-06](#l-06) | Vulnerable versions of packages are being used                                                                       |     6 |

### <a id="summary-non-critical-issues"></a> Non-Critical Issues
There are 238 instances over 37 issues.
|      ID       | Description                                                                        | Count |
| :-----------: | :--------------------------------------------------------------------------------- | ----: |
| [N-01](#n-01) | Complex arithmetic                                                                 |     3 |
| [N-02](#n-02) | Consider adding formal verification proofs                                         |     1 |
| [N-03](#n-03) | Consider adding validation of user inputs                                          |    11 |
| [N-04](#n-04) | Consider defining system-wide `constant`s in a single file                         |     5 |
| [N-05](#n-05) | Consider emitting an event at the end of the constructor                           |     5 |
| [N-06](#n-06) | Consider making contracts `Upgradeable`                                            |     6 |
| [N-07](#n-07) | Consider using named function arguments                                            |     4 |
| [N-08](#n-08) | Consider using named mappings                                                      |     1 |
| [N-09](#n-09) | Constants in comparisons should appear on the left side                            |    10 |
| [N-10](#n-10) | Contract should expose an `interface`                                              |    29 |
| [N-11](#n-11) | Empty function body                                                                |     1 |
| [N-12](#n-12) | Enable IR-based code generation                                                    |     1 |
| [N-13](#n-13) | Events are missing sender information                                              |     6 |
| [N-14](#n-14) | Events may be emitted out of order due to reentrancy                               |     8 |
| [N-15](#n-15) | Import declarations should import specific identifiers, rather than the whole file |     1 |
| [N-16](#n-16) | Local variable shadows state variable                                              |     1 |
| [N-17](#n-17) | Missing checks for state variable assignments                                      |     4 |
| [N-18](#n-18) | Missing event emission in initializer                                              |     1 |
| [N-19](#n-19) | Missing event for critical parameter change                                        |     3 |
| [N-20](#n-20) | Named imports of parent contracts are missing                                      |     1 |
| [N-21](#n-21) | NatSpec: Contract declarations should have `@author` tags                          |     7 |
| [N-22](#n-22) | NatSpec: Contract declarations should have `@dev` tags                             |     7 |
| [N-23](#n-23) | NatSpec: Contract declarations should have `@notice` tag                           |     6 |
| [N-24](#n-24) | NatSpec: Contract declarations should have `@title` tag                            |     7 |
| [N-25](#n-25) | NatSpec: Contract declarations should have descriptions                            |     5 |
| [N-26](#n-26) | NatSpec: Error declarations should have descriptions                               |     4 |
| [N-27](#n-27) | NatSpec: Function declarations should have `@notice` tag                           |    29 |
| [N-28](#n-28) | NatSpec: Function declarations should have descriptions                            |    29 |
| [N-29](#n-29) | NatSpec: Invalid NatSpec comment style                                             |     1 |
| [N-30](#n-30) | NatSpec: Modifier declarations should have NatSpec descriptions                    |     4 |
| [N-31](#n-31) | NatSpec: State variable declarations should have descriptions                      |    21 |
| [N-32](#n-32) | Setters should prevent re-setting of the same value                                |     5 |
| [N-33](#n-33) | Style guide: Horizontal whitespace in mapping definitions                          |     3 |
| [N-34](#n-34) | Typos                                                                              |     1 |
| [N-35](#n-35) | Unnecessary cast                                                                   |     1 |
| [N-36](#n-36) | Unused import                                                                      |     3 |
| [N-37](#n-37) | Use more recent OpenZeppelin version for bug fixes and performance improvements    |     3 |

### <a id="summary-gas-optimizations"></a> Gas Optimizations
There are 161 instances over 29 issues.
|      ID       | Description                                                                         | Count | Gas Per Instance | Gas Savings |
| :-----------: | :---------------------------------------------------------------------------------- | ----: | ---------------: | ----------: |
| [G-01](#g-01) | `address(this)` should be cached                                                    |     4 |              100 |         400 |
| [G-02](#g-02) | Assembly: Check `msg.sender` using `xor` and the scratch space                      |     2 |                3 |           6 |
| [G-03](#g-03) | Assembly: Optimize `address` storage value management with assembly                 |    11 |               66 |         726 |
| [G-04](#g-04) | Assembly: Simple checks for `uint` zero can be done using assembly to save gas      |     1 |                6 |           6 |
| [G-05](#g-05) | Assembly: Use scratch space for building calldata                                   |    25 |              220 |       5,500 |
| [G-06](#g-06) | Assembly: Use scratch space when building emitted events with two data arguments    |     5 |               38 |         190 |
| [G-07](#g-07) | Avoid transferring amounts of zero in order to save gas                             |     2 |              100 |         200 |
| [G-08](#g-08) | Avoid updating storage when the value hasn't changed to save gas                    |     5 |              800 |       4,000 |
| [G-09](#g-09) | Consider using Solady's `FixedPointMathLib` for multiplication followed by division |    10 |                - |           - |
| [G-10](#g-10) | Constructors can be marked `payable`                                                |     5 |               21 |         105 |
| [G-11](#g-11) | `do`-`while` is cheaper than `for`-loops when the initial check can be skipped      |     4 |                - |           - |
| [G-12](#g-12) | Initializers can be marked `payable`                                                |     1 |               21 |          21 |
| [G-13](#g-13) | Multiple accesses of a `mapping`/`array` should use a local variable cache          |     2 |               42 |          84 |
| [G-14](#g-14) | Only emit event in setter function if the state variable was changed                |     3 |                - |           - |
| [G-15](#g-15) | Optimize names to save gas                                                          |     4 |               22 |          88 |
| [G-16](#g-16) | `public` functions not called by the contract should be declared `external` instead |     1 |               41 |          41 |
| [G-17](#g-17) | Reduce deployment costs by tweaking contracts' metadata                             |     6 |                - |           - |
| [G-18](#g-18) | Reduce gas usage by moving to Solidity 0.8.19 or later                              |     7 |                - |           - |
| [G-19](#g-19) | Refactor `modifier`s to call a local `function`                                     |     4 |                - |           - |
| [G-20](#g-20) | Replace OpenZeppelin components with Solady equivalents to save gas                 |     1 |                - |           - |
| [G-21](#g-21) | Same cast is done multiple times                                                    |     2 |                5 |          10 |
| [G-22](#g-22) | State variable read in a loop                                                       |     4 |              100 |         400 |
| [G-23](#g-23) | Strict inequality operators are more expensive than non-strict ones                 |    10 |                3 |          30 |
| [G-24](#g-24) | The result of function calls should be cached rather than re-calling the function   |     1 |               20 |          20 |
| [G-25](#g-25) | Use more recent OpenZeppelin version for gas boost                                  |     3 |                - |           - |
| [G-26](#g-26) | Use named `return` values                                                           |    15 |               44 |         660 |
| [G-27](#g-27) | Use predefined address instead of `address(this)`                                   |     4 |               50 |         200 |
| [G-28](#g-28) | Using `private` rather than `public` for constants, saves gas                       |    12 |            3,406 |      40,872 |
| [G-29](#g-29) | Variables should be declared outside of loops                                       |     7 |                - |           - |
|               | Total Gas Savings                                                                   |       |                  |      53,559 |

Gas totals use lower bounds of ranges and count two iterations of each `for` loop. Gas savings values are runtime values except for cases where only deployment values are applicable, like for constant declarations.
## <a id="details"></a> Details

### <a id="details-low-risk-issues"></a> Low Risk Issues
#### <a id="l-01"></a> \[L-01\] Critical functions should be a two step procedure
##### Description:
Critical functions in Solidity contracts should follow a two-step procedure to enhance security, minimize human error, and ensure proper access control. By dividing sensitive operations into two distinct phases, such as initiation and confirmation, developers can introduce a safeguard against unintended actions or unauthorized access.

##### Instances:
There are 2 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
#### <a id="l-02"></a> \[L-02\] `for` and `while` loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS
##### Description:
In Solidity, `for` and `while` loops can potentially cause denial of service (DOS) attacks if not handled carefully. DOS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where `for` or `while` loops can lead to DOS attacks: Nested `for` and `while` loops can become exceptionally gas expensive and should be used sparingly.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit public function assetPrice()
58:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit external function liquidate()
222:       for (uint i = 0; i < numberOfVaults; i++) {

/// @audit public function getNonKeroseneValue()
258:       for (uint i = 0; i < numberOfVaults; i++) {

/// @audit public function getKeroseneValue()
277:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                         |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              3 | [222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222),[258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258),[277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277) |
___
#### <a id="l-03"></a> \[L-03\] Large transfers may not work with some `ERC20` tokens
##### Description:
Some `IERC20` implementations (e.g., `UNI`, `COMP`) may fail if the valued transferred is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20/blob/main/src/Uint96.sol).

##### Recommendation:
Check the actual balance before and after vs. the expected balance.

##### Instances:
There are 2 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit uint256 amount
39:     asset.safeTransfer(to, amount);
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L39) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit uint256 amount
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

| File Link                                                                                              | Instance Count | Instance Link                                                                                |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129) |
___
#### <a id="l-04"></a> \[L-04\] Missing zero address check in constructor/initializer
##### Description:
Constructors and initializer functions often take address parameters to initialize important components of a contract, such as the owner or linked contracts. However, without validation, there is a risk that an address parameter could be mistakenly set to the zero address (0x0) due to an error or an oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address. Any funds sent to it will be irretrievable. It is therefore crucial to include a zero address check in constructors to prevent such problems. If a zero address is detected, the constructor should revert the transaction.

##### Recommendation:
Consider adding explicit zero-address validation prior to use of `address` parameters in constructors.

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

/// @audit Not checked against address zero: _vaultManager, _asset, _kerosineManager
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset,
29:     KerosineManager _kerosineManager
30:   ) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit Not checked against address zero: _vaultManager, _asset, _dyad, _kerosineManager
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset,
24:       Dyad            _dyad,
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit Not checked against address zero: _dNft, _dyad, _licenser
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

/// @audit Not checked against address zero: _keroseneManager
59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49),[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59) |
___
```solidity
File: src/staking/KerosineDenominator.sol

/// @audit Not checked against address zero: _kerosine
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11) |
___
#### <a id="l-05"></a> \[L-05\] Missing zero address check in functions with address parameters
##### Description:
A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address. Any funds sent to it will be irretrievable. Even for protected functions, an explicit zero address check can prevent user errors due to typos, copy/paste errors, and similar.

##### Recommendation:
Consider adding explicit zero-address validation prior to use of `address` parameters in functions.

##### Instances:
There are 15 instances of this issue.
<details><summary>View 15 Instances</summary>

```solidity
File: src/core/KerosineManager.sol

/// @audit Not checked against address zero: vault
18:   function add(
19:     address vault
20:   )
21:     external
22:       onlyOwner
23:   {

/// @audit Not checked against address zero: vault
28:   function remove(
29:     address vault
30:   )
31:     external
32:       onlyOwner
33:   {

/// @audit Not checked against address zero: vault
44:   function isLicensed(
45:     address vault
46:   )
47:     external
48:     view
49:     returns (bool) {
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                                                                                                                      |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              3 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit Not checked against address zero: _unboundedKerosineVault
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

/// @audit Not checked against address zero: to
32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   )
37:     external
38:     view
39:       onlyVaultManager
40:   {
```

| File Link                                                                                                              | Instance Count | Instance Links                                                                                                                                                                                        |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              2 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit Not checked against address zero: to
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

/// @audit Not checked against address zero: _kerosineDenominator
43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit Not checked against address zero: vault
67:   function add(
68:       uint    id,
69:       address vault
70:   )
71:     external
72:       isDNftOwner(id)
73:   {

/// @audit Not checked against address zero: vault
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   )
84:     external
85:       isDNftOwner(id)
86:   {

/// @audit Not checked against address zero: vault
 94:   function remove(
 95:       uint    id,
 96:       address vault
 97:   )
 98:     external
 99:       isDNftOwner(id)
100:   {

/// @audit Not checked against address zero: vault
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   )
110:     external
111:       isDNftOwner(id)
112:   {

/// @audit Not checked against address zero: vault, to
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   )
140:     public
141:       isDNftOwner(id)
142:   {

/// @audit Not checked against address zero: to
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external
162:       isDNftOwner(id)
163:   {

/// @audit Not checked against address zero: vault, to
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external
191:       isDNftOwner(id)
192:     returns (uint) {

/// @audit Not checked against address zero: vault
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   )
303:     external
304:     view
305:     returns (bool) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              8 | [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67),[80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80),[94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94),[106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106),[134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134),[156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156),[184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184),[299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299) |
___
</details>

#### <a id="l-06"></a> \[L-06\] Vulnerable versions of packages are being used
##### Description:
This project's dependencies are vulnerable to the Common Vulnerabilities and Exposures (CVEs) listed below.

##### Recommendation:
Although the CVEs may involve code not in use by this project, consider switching to more recent versions of these packages that do not have these vulnerabilities, to avoid trying to determine whether there is vulnerable code from these packages in use.

##### Instances:
There are 6 instances of this issue.
<details><summary>View 6 Instances</summary>

1. [CVE-2023-26488](https://nvd.nist.gov/vuln/detail/CVE-2023-26488) - Severity: <span style="color:yellow">**Medium**</span> - OpenZeppelin Contracts is a library for secure smart contract development. The ERC721Consecutive contract designed for minting NFTs in batches does not update balances when a batch has size 1 and consists of a single token. Subsequent transfers from the receiver of that token may overflow the balance as reported by `balanceOf`. The issue exclusively presents with batches of size 1. The issue has been patched in 4.8.2.
1. [CVE-2023-30541](https://nvd.nist.gov/vuln/detail/CVE-2023-30541) - Severity: <span style="color:yellow">**Medium**</span> - OpenZeppelin Contracts is a library for secure smart contract development. A function in the implementation contract may be inaccessible if its selector clashes with one of the proxy's own selectors. Specifically, if the clashing function has a different signature with incompatible ABI encoding, the proxy could revert while attempting to decode the arguments from calldata. The probability of an accidental clash is negligible, but one could be caused deliberately and could cause a reduction in availability. The issue has been fixed in version 4.8.3. As a workaround if a function appears to be inaccessible for this reason, it may be possible to craft the calldata such that ABI decoding does not fail at the proxy and the function is properly proxied through.

1. [CVE-2023-30542](https://nvd.nist.gov/vuln/detail/CVE-2023-30542) - Severity: <span style="color:red">**High**</span> - OpenZeppelin Contracts is a library for secure smart contract development. The proposal creation entrypoint (`propose`) in `GovernorCompatibilityBravo` allows the creation of proposals with a `signatures` array shorter than the `calldatas` array. This causes the additional elements of the latter to be ignored, and if the proposal succeeds the corresponding actions would eventually execute without any calldata. The `ProposalCreated` event correctly represents what will eventually execute, but the proposal parameters as queried through `getActions` appear to respect the original intended calldata. This issue has been patched in 4.8.3. As a workaround, ensure that all proposals that pass through governance have equal length `signatures` and `calldatas` parameters.

1. [CVE-2023-34234](https://nvd.nist.gov/vuln/detail/CVE-2023-34234) - Severity: <span style="color:yellow">**Medium**</span> - OpenZeppelin Contracts is a library for smart contract development. By frontrunning the creation of a proposal, an attacker can become the proposer and gain the ability to cancel it. The attacker can do this repeatedly to try to prevent a proposal from being proposed at all. This impacts the `Governor` contract in v4.9.0 only, and the `GovernorCompatibilityBravo` contract since v4.3.0. This problem has been patched in 4.9.1 by introducing opt-in frontrunning protection. Users are advised to upgrade. Users unable to upgrade may submit the proposal creation transaction to an endpoint with frontrunning protection as a workaround.

1. [CVE-2023-34459](https://nvd.nist.gov/vuln/detail/CVE-2023-34459) - Severity: <span style="color:yellow">**Medium**</span> - OpenZeppelin Contracts is a library for smart contract development. Starting in version 4.7.0 and prior to version 4.9.2, when the `verifyMultiProof`, `verifyMultiProofCalldata`, `procesprocessMultiProof`, or `processMultiProofCalldat` functions are in use, it is possible to construct merkle trees that allow forging a valid multiproof for an arbitrary set of leaves. A contract may be vulnerable if it uses multiproofs for verification and the merkle tree that is processed includes a node with value 0 at depth 1 (just under the root). This could happen inadvertedly for balanced trees with 3 leaves or less, if the leaves are not hashed. This could happen deliberately if a malicious tree builder includes such a node in the tree. A contract is not vulnerable if it uses single-leaf proving (`verify`, `verifyCalldata`, `processProof`, or `processProofCalldata`), or if it uses multiproofs with a known tree that has hashed leaves. Standard merkle trees produced or validated with the @openzeppelin/merkle-tree library are safe. The problem has been patched in version 4.9.2. Some workarounds are available. For those using multiproofs: When constructing merkle trees hash the leaves and do not insert empty nodes in your trees. Using the @openzeppelin/merkle-tree package eliminates this issue. Do not accept user-provided merkle roots without reconstructing at least the first level of the tree. Verify the merkle tree structure by reconstructing it from the leaves.

1. [CVE-2023-40014](https://nvd.nist.gov/vuln/detail/CVE-2023-40014) - Severity: <span style="color:yellow">**Medium**</span> - OpenZeppelin Contracts is a library for secure smart contract development. Starting in version 4.0.0 and prior to version 4.9.3, contracts using `ERC2771Context` along with a custom trusted forwarder may see `_msgSender` return `address(0)` in calls that originate from the forwarder with calldata shorter than 20 bytes. This combination of circumstances does not appear to be common, in particular it is not the case for `MinimalForwarder` from OpenZeppelin Contracts, or any deployed forwarder the team is aware of, given that the signer address is appended to all calls that originate from these forwarders. The problem has been patched in v4.9.3.


</details>


### <a id="details-non-critical-issues"></a> Non-Critical Issues
#### <a id="n-01"></a> \[N-01\] Complex arithmetic
##### Description:
The longer a string of operations is, the harder it is to understand it. To increase readability and maintainability, particularly in Solidity which often involves complex mathematical operations, it is recommended to limit the number of arithmetic operations to two to three per statement. Too many arithmetic operations in a single statement can make the code difficult to comprehend, increase the likelihood of mistakes, and complicate the process of debugging and reviewing the code.

##### Recommendation:
Consider splitting complex arithmetic operations into more steps, with more descriptive temporary variable names, and add extensive comments.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit arithmetic operator count: 4
60:         tvl += vault.asset().balanceOf(address(vault))
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals())
63:                 / (10**vault.oracle().decimals());
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit arithmetic operator count: 4
146:     uint value = amount * _vault.assetPrice()
147:                   * 1e18
148:                   / 10**_vault.oracle().decimals()
149:                   / 10**_vault.asset().decimals();

/// @audit arithmetic operator count: 4
195:       uint asset = amount
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals()))
197:                     / _vault.assetPrice()
198:                     / 1e18;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146),[195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195) |
___
#### <a id="n-02"></a> \[N-02\] Consider adding formal verification proofs
##### Description:
Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The Solidity compiler has this functionality built in. See [SMTChecker and Formal Verification](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification) for more information. Use of the SMTChecker module was not detected based on the project configuration.

##### Instances:
There is 1 instance of this issue.

#### <a id="n-03"></a> \[N-03\] Consider adding validation of user inputs
##### Description:
There are no validations done on the arguments below. Input validation helps to ensure that the function receives valid and expected inputs. Without proper validation, malicious users or even accidental errors could pass invalid data, leading to unexpected behavior or vulnerabilities in the contract.

##### Recommendation:
Add validation to prevent use of an invalid/undesirable value.

##### Instances:
There are 11 instances of this issue.
<details><summary>View 11 Instances</summary>

```solidity
File: src/core/KerosineManager.sol

/// @audit not validated: vault
18:   function add(
19:     address vault
20:   )
21:     external
22:       onlyOwner
23:   {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                               |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit not validated: id, vault
67:   function add(
68:       uint    id,
69:       address vault
70:   )
71:     external
72:       isDNftOwner(id)
73:   {

/// @audit not validated: id, vault
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   )
84:     external
85:       isDNftOwner(id)
86:   {

/// @audit not validated: vault
 94:   function remove(
 95:       uint    id,
 96:       address vault
 97:   )
 98:     external
 99:       isDNftOwner(id)
100:   {

/// @audit not validated: vault
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   )
110:     external
111:       isDNftOwner(id)
112:   {

/// @audit not validated: id, vault, amount, to
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   )
140:     public
141:       isDNftOwner(id)
142:   {

/// @audit not validated: amount, to
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external
162:       isDNftOwner(id)
163:   {

/// @audit not validated: id, to
205:   function liquidate(
206:     uint id,
207:     uint to
208:   )
209:     external
210:       isValidDNft(id)
211:       isValidDNft(to)
212:     {

/// @audit not validated: id
230:   function collatRatio(
231:     uint id
232:   )
233:     public
234:     view
235:     returns (uint) {

/// @audit not validated: id
250:   function getNonKeroseneValue(
251:     uint id
252:   )
253:     public
254:     view
255:     returns (uint) {

/// @audit not validated: id
269:   function getKeroseneValue(
270:     uint id
271:   )
272:     public
273:     view
274:     returns (uint) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             10 | [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67),[80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80),[94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94),[106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106),[134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134),[156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156),[205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205),[230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230),[250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250),[269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269) |
___
</details>

#### <a id="n-04"></a> \[N-04\] Consider defining system-wide `constant`s in a single file
##### Description:
```solidity
// Before:
ContractA.X = 0;
ContractB.Y = 1;
ContractC.Z = 2;

// After:
Constants.X = 0;
Constants.Y = 1;
Constants.Z = 2;

ContractA.X = X;
ContractB.Y = Y;
ContractC.Z = Z;
```

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;
```

| File Link                                                                                                | Instance Count | Instance Link                                                                               |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14) |
___
```solidity
File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              4 | [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22),[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23),[25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25),[26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26) |
___
#### <a id="n-05"></a> \[N-05\] Consider emitting an event at the end of the constructor
##### Description:
Consider emitting an event when the contract is constructed to make it easier for off-chain tools to track when and by whom the contract was constructed.

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset,
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17) |
___
```solidity
File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset,
29:     KerosineManager _kerosineManager
30:   ) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset,
24:       Dyad            _dyad,
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21) |
___
```solidity
File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49) |
___
```solidity
File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11) |
___
#### <a id="n-06"></a> \[N-06\] Consider making contracts `Upgradeable`
##### Description:
Making a contract `Upgradeable` allows for bugs to be fixed in production, at the expense of significantly increasing centralization.

##### Instances:
There are 6 instances of this issue.
<details><summary>View 6 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="n-07"></a> \[N-07\] Consider using named function arguments
##### Description:
Function call arguments can be given by name, in any order, if they are enclosed in `{` and `}`. The argument list has to coincide by name with the list of parameters from the function declaration, but can be in arbitrary order. Using named function parameters can improve code readability and maintainability by explicitly mapping arguments to their respective parameter names, reducing potential errors due to out of order arguments. The following findings are for function calls with 4 or more parameters.

##### Instances:
There are 4 instances of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

71:     UnboundedKerosineVault unboundedKerosineVault = new UnboundedKerosineVault(
72:       vaultManager,
73:       Kerosine(MAINNET_KEROSENE),
74:       Dyad    (MAINNET_DYAD),
75:       kerosineManager
76:     );

102:     return Contracts(
103:       Kerosine(MAINNET_KEROSENE),
104:       vaultLicenser,
105:       vaultManager,
106:       ethVault,
107:       wstEth,
108:       kerosineManager,
109:       unboundedKerosineVault,
110:       boundedKerosineVault,
111:       kerosineDenominator
112:     );
```

| File Link                                                                                             | Instance Count | Instance Links                                                                                                                                                                              |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              2 | [71](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L71),[102](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L102) |
___
```solidity
File: src/core/VaultManagerV2.sol

199:       withdraw(id, vault, asset, to);

200:       emit RedeemDyad(id, vault, amount, to);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [199](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L199),[200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200) |
___
#### <a id="n-08"></a> \[N-08\] Consider using named mappings
##### Description:
To help clarify the purpose of a `mapping` and make maintenance easier, consider using named mappings. Named mappings were [introduced in Solidity 0.8.18](https://blog.soliditylang.org/2023/02/01/solidity-0.8.18-release-announcement/).

Example:
```solidity
// Before:
mapping(address => uint256) private mappingName;

// After:
mapping(address contractAddress => uint256 functionCount) private mappingName;
```

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19) |
___
#### <a id="n-09"></a> \[N-09\] Constants in comparisons should appear on the left side
##### Description:
Constants or literal values in comparisons should appear on the left side of the comparison operator in order to prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html). If an operator character is missing, an unintentional variable assignment can occur. For example:
```solidity
// Intent - compare value to ten
if (voteCount == 10) {
    // do something
}

// Typo - forgot one equal sign causing variable assignment
if (voteCount = 10) {
    // now voteCount equals ten
}

// Preventative style - a missing equal sign will not compile
if (10 == voteCount) {
   // do something
}
```

##### Recommendation:
Place constants and literal values on the left side of the comparison operator.

##### Instances:
There are 10 instances of this issue.
<details><summary>View 10 Instances</summary>

```solidity
File: src/core/KerosineManager.sol

/// @audit constant: MAX_VAULTS
24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
```

| File Link                                                                                                | Instance Count | Instance Link                                                                               |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [24](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L24) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit constant: MAX_VAULTS
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

/// @audit constant: MAX_VAULTS_KEROSENE
87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

/// @audit literal: 0
101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

/// @audit literal: 0
113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

/// @audit constant: MIN_COLLATERIZATION_RATIO
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow();

/// @audit constant: MIN_COLLATERIZATION_RATIO
167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();

/// @audit constant: MIN_COLLATERIZATION_RATIO
214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

/// @audit literal: 1e18
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

/// @audit literal: 0
237:       if (_dyad == 0) return type(uint).max;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              9 | [74](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L74),[87](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L87),[101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101),[113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113),[152](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L152),[167](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L167),[214](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L214),[217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217),[237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237) |
___
</details>

#### <a id="n-10"></a> \[N-10\] Contract should expose an `interface`
##### Description:
All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.

##### Instances:
There are 29 instances of this issue.
<details><summary>View 29 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36) |
___
```solidity
File: src/core/KerosineManager.sol

18:   function add(
19:     address vault
20:   )
21:     external
22:       onlyOwner
23:   {

28:   function remove(
29:     address vault
30:   )
31:     external
32:       onlyOwner
33:   {

37:   function getVaults()
38:     external
39:     view
40:     returns (address[] memory) {

44:   function isLicensed(
45:     address vault
46:   )
47:     external
48:     view
49:     returns (bool) {
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                  |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              4 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28),[37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   )
37:     external
38:     view
39:       onlyVaultManager
40:   {
```

| File Link                                                                                                              | Instance Count | Instance Links                                                                                                                                                                                        |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              2 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32) |
___
```solidity
File: src/core/Vault.kerosine.sol

36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public
41:       onlyVaultManager
42:   {

47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view
65:     returns (uint) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              3 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47),[60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
```solidity
File: src/core/VaultManagerV2.sol

67:   function add(
68:       uint    id,
69:       address vault
70:   )
71:     external
72:       isDNftOwner(id)
73:   {

80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   )
84:     external
85:       isDNftOwner(id)
86:   {

 94:   function remove(
 95:       uint    id,
 96:       address vault
 97:   )
 98:     external
 99:       isDNftOwner(id)
100:   {

106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   )
110:     external
111:       isDNftOwner(id)
112:   {

119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   )
124:     external
125:       isValidDNft(id)
126:   {

134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   )
140:     public
141:       isDNftOwner(id)
142:   {

156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external
162:       isDNftOwner(id)
163:   {

172:   function burnDyad(
173:     uint id,
174:     uint amount
175:   )
176:     external
177:       isValidDNft(id)
178:   {

184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external
191:       isDNftOwner(id)
192:     returns (uint) {

205:   function liquidate(
206:     uint id,
207:     uint to
208:   )
209:     external
210:       isValidDNft(id)
211:       isValidDNft(to)
212:     {

230:   function collatRatio(
231:     uint id
232:   )
233:     public
234:     view
235:     returns (uint) {

241:   function getTotalUsdValue(
242:     uint id
243:   )
244:     public
245:     view
246:     returns (uint) {

250:   function getNonKeroseneValue(
251:     uint id
252:   )
253:     public
254:     view
255:     returns (uint) {

269:   function getKeroseneValue(
270:     uint id
271:   )
272:     public
273:     view
274:     returns (uint) {

290:   function getVaults(
291:     uint id
292:   )
293:     external
294:     view
295:     returns (address[] memory) {

299:   function hasVault(
300:     uint    id,
301:     address vault
302:   )
303:     external
304:     view
305:     returns (bool) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             16 | [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67),[80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80),[94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94),[106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106),[119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119),[134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134),[156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156),[172](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L172),[184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184),[205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205),[230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230),[241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241),[250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250),[269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269),[290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290),[299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299) |
___
```solidity
File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17) |
___
</details>

#### <a id="n-11"></a> \[N-11\] Empty function body
##### Description:
Consider emitting an event or adding a comment about why the function body is empty.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset,
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17) |
___
#### <a id="n-12"></a> \[N-12\] Enable IR-based code generation
##### Description:
Solidity can generate EVM bytecode in two different ways: Either directly from Solidity to EVM opcodes (“old codegen”) or through an intermediate representation (“IR”) in Yul (“new codegen” or “IR-based codegen”). The IR-based code generator was introduced with an aim to not only allow code generation to be more transparent and auditable but also to enable more powerful optimization passes that span across functions.

##### Recommendation:
Use `--via-ir` (command line) or `{"viaIR": true}` (in [standard-json](https://docs.soliditylang.org/en/latest/using-the-compiler.html#compiler-input-and-output-json-description)) to take advantage of [the benefits of IR-based codegen](https://docs.soliditylang.org/en/latest/ir-breaking-changes.html#solidity-ir-based-codegen-changes) including extra gas savings. When using Foundry, set the [via_ir](https://book.getfoundry.sh/reference/config/solidity-compiler#via_ir) property to `true`.

##### Instances:
There is 1 instance of this issue.

#### <a id="n-13"></a> \[N-13\] Events are missing sender information
##### Description:
When an event is emitted based on a user's action, not being able to filter based on the address that triggered the event makes event processing more difficult, particularly when `msg.sender` is not `tx.origin`.

##### Recommendation:
Include `msg.sender` in user-triggered event emissions.

##### Instances:
There are 6 instances of this issue.
<details><summary>View 6 Instances</summary>

```solidity
File: src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

200:       emit RedeemDyad(id, vault, amount, to);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              6 | [77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77),[90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90),[103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103),[115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115),[168](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L168),[200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200) |
___
</details>

#### <a id="n-14"></a> \[N-14\] Events may be emitted out of order due to reentrancy
##### Description:
Ensure that events follow the [check-effects-interactions pattern](https://docs.soliditylang.org/en/latest/security-considerations.html#use-the-checks-effects-interactions-pattern), and are emitted *before* external calls.

##### Recommendation:
Place the event emitter ahead of the external call ensures the log is updated and correct. Should the transfer fail for some reason, it will cause a revert and there will be no event emitted.

##### Instances:
There are 8 instances of this issue.
<details><summary>View 8 Instances</summary>

```solidity
File: src/core/VaultManagerV2.sol

/// @audit external call prior to this emission: isLicensed():75
77:     emit Added(id, vault);

/// @audit external call prior to this emission: isLicensed():88
90:     emit Added(id, vault);

/// @audit external call prior to this emission: id2asset():101
103:     emit Removed(id, vault);

/// @audit external call prior to this emission: id2asset():113
115:     emit Removed(id, vault);

/// @audit external calls prior to this emission: mintedDyad():164, mint():166
168:     emit MintDyad(id, amount, to);

/// @audit external calls prior to this emission: burn():179
180:     emit BurnDyad(id, amount, msg.sender);

/// @audit external calls prior to this emission: burn():193
200:       emit RedeemDyad(id, vault, amount, to);

/// @audit external calls prior to this emission: burn():215, id2asset():224, move():225
227:       emit Liquidate(id, msg.sender, to);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              8 | [77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77),[90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90),[103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103),[115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115),[168](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L168),[180](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L180),[200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200),[227](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L227) |
___
</details>

#### <a id="n-15"></a> \[N-15\] Import declarations should import specific identifiers, rather than the whole file
##### Description:
Using import declarations of the form `import {Bar} from "foo/Bar.sol"` avoids polluting the symbol namespace (making flattened files smaller), and speeds up compilation. (Using this form of import does not save any gas over importing the whole file.)

##### Recommendation:
Use specific identifiers when specifying an import directive.

##### Instances:
There is 1 instance of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

4: import "forge-std/Script.sol";
```

| File Link                                                                                             | Instance Count | Instance Link                                                                              |
| :---------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [4](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L4) |
___
#### <a id="n-16"></a> \[N-16\] Local variable shadows state variable
##### Description:
Note that this is not the same as shadowing, which is reported with a different compiler warning.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

66:       uint denominator = kerosineDenominator.denominator();
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L66) |
___
#### <a id="n-17"></a> \[N-17\] Missing checks for state variable assignments
##### Description:
Consider whether reasonable bounds checks for variables would be useful.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

43:     id2asset[id] += amount;

55:     id2asset[from] -= amount;

56:     id2asset[to]   += amount;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              3 | [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L43),[55](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L55),[56](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L56) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

38:     id2asset[id] -= amount;
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [38](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L38) |
___
#### <a id="n-18"></a> \[N-18\] Missing event emission in initializer
##### Description:
Consider emitting an event when the contract is initialized to make it easier for to off-chain tools to track the exact point in time when the contract was initialized.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59) |
___
#### <a id="n-19"></a> \[N-19\] Missing event for critical parameter change
##### Description:
Events help off-chain tools to track changes.

##### Recommendation:
Emit an event for critical parameter changes, including the old and new values.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit state variable changed: unboundedKerosineVault
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit state variable changed: kerosineDenominator
43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit state variable changed: keroseneManager
59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59) |
___
#### <a id="n-20"></a> \[N-20\] Named imports of parent contracts are missing
##### Description:
For clarity and to make the contracts being used explicit, the parent contracts should be explicitly imported.

##### Instances:
There is 1 instance of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit Script
35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
#### <a id="n-21"></a> \[N-21\] NatSpec: Contract declarations should have `@author` tags
##### Description:
The `@author` tag provides the name of the author of the contract/interface. If there is a comment with the `@author` tag, verify that the comment block starts with the NatSpec comment indicator, either `///` or `/**`.

##### Instances:
There are 7 instances of this issue.
<details><summary>View 7 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="n-22"></a> \[N-22\] NatSpec: Contract declarations should have `@dev` tags
##### Description:
`@dev` tags are used to explain to a developer any extra details. If there is a comment with the `@dev` tag, verify that the comment block starts with the NatSpec comment indicator, either `///` or `/**`.

##### Instances:
There are 7 instances of this issue.
<details><summary>View 7 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="n-23"></a> \[N-23\] NatSpec: Contract declarations should have `@notice` tag
##### Description:
`@notice` tags are used to explain to end users what the contract does. If there is a comment with the `@notice` tag, verify that the comment block starts with the NatSpec comment indicator, either `///` or `/**`.

##### Instances:
There are 6 instances of this issue.
<details><summary>View 6 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="n-24"></a> \[N-24\] NatSpec: Contract declarations should have `@title` tag
##### Description:
The `@title` tag provides a title that describes the contract/interface. If there is a comment with the `@title` tag, verify that the comment block starts with the NatSpec comment indicator, either `///` or `/**`.

##### Instances:
There are 7 instances of this issue.
<details><summary>View 7 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="n-25"></a> \[N-25\] NatSpec: Contract declarations should have descriptions
##### Description:
The [Solidity documentation recommends](https://docs.soliditylang.org/en/latest/natspec-format.html) "that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI)." NatSpec documentation should be used for improved readability, a better user experience, enhanced auditability, enablement of automated testing and verification, and to promote standardization and interoperability.

##### Recommendation:
Add NatSpec documentation to all public contracts. It must appear above the contract definition braces in order to be identified by the compiler as NatSpec

##### Instances:
There are 5 instances of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
#### <a id="n-26"></a> \[N-26\] NatSpec: Error declarations should have descriptions
##### Description:
[NatSpec documentation](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) should be used for improved readability, a better user experience, enhanced auditability, enablement of automated testing and verification, and to promote standardization and interoperability.

##### Recommendation:
Add NatSpec documentation to all error declarations.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                                                                                                                  |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              3 | [8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L8),[9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L9),[10](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L10) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13) |
___
#### <a id="n-27"></a> \[N-27\] NatSpec: Function declarations should have `@notice` tag
##### Description:
`@notice` tags are used to explain to end users what the function does. If there is a comment with the `@notice` tag, verify that the comment block starts with the NatSpec comment indicator, either `///` or `/**`.

##### Instances:
There are 29 instances of this issue.
<details><summary>View 29 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36) |
___
```solidity
File: src/core/KerosineManager.sol

18:   function add(
19:     address vault
20:   )
21:     external
22:       onlyOwner
23:   {

28:   function remove(
29:     address vault
30:   )
31:     external
32:       onlyOwner
33:   {

37:   function getVaults()
38:     external
39:     view
40:     returns (address[] memory) {

44:   function isLicensed(
45:     address vault
46:   )
47:     external
48:     view
49:     returns (bool) {
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                  |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              4 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28),[37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset,
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   )
37:     external
38:     view
39:       onlyVaultManager
40:   {

44:   function assetPrice()
45:     public
46:     view
47:     override
48:     returns (uint) {
```

| File Link                                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                              |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              4 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17),[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.sol

36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public
41:       onlyVaultManager
42:   {

47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view
65:     returns (uint) {

69:   function assetPrice()
70:     public
71:     view
72:     virtual
73:     returns (uint);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              4 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47),[60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60),[69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset,
24:       Dyad            _dyad,
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {

50:   function assetPrice()
51:     public
52:     view
53:     override
54:     returns (uint) {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              4 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21),[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43),[50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50) |
___
```solidity
File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {

80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   )
84:     external
85:       isDNftOwner(id)
86:   {

106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   )
110:     external
111:       isDNftOwner(id)
112:   {

230:   function collatRatio(
231:     uint id
232:   )
233:     public
234:     view
235:     returns (uint) {

241:   function getTotalUsdValue(
242:     uint id
243:   )
244:     public
245:     view
246:     returns (uint) {

250:   function getNonKeroseneValue(
251:     uint id
252:   )
253:     public
254:     view
255:     returns (uint) {

269:   function getKeroseneValue(
270:     uint id
271:   )
272:     public
273:     view
274:     returns (uint) {

290:   function getVaults(
291:     uint id
292:   )
293:     external
294:     view
295:     returns (address[] memory) {

299:   function hasVault(
300:     uint    id,
301:     address vault
302:   )
303:     external
304:     view
305:     returns (bool) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             10 | [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49),[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59),[80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80),[106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106),[230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230),[241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241),[250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250),[269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269),[290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290),[299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299) |
___
```solidity
File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {

17:   function denominator() external view returns (uint) {
```

| File Link                                                                                                           | Instance Count | Instance Links                                                                                                                                                                                        |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              2 | [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11),[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17) |
___
</details>

#### <a id="n-28"></a> \[N-28\] NatSpec: Function declarations should have descriptions
##### Description:
The [Solidity documentation recommends](https://docs.soliditylang.org/en/latest/natspec-format.html) "that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI)." NatSpec documentation should be used for improved readability, a better user experience, enhanced auditability, enablement of automated testing and verification, and to promote standardization and interoperability.

##### Recommendation:
Add NatSpec documentation to all public functions.

##### Instances:
There are 29 instances of this issue.
<details><summary>View 29 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36) |
___
```solidity
File: src/core/KerosineManager.sol

18:   function add(
19:     address vault
20:   )
21:     external
22:       onlyOwner
23:   {

28:   function remove(
29:     address vault
30:   )
31:     external
32:       onlyOwner
33:   {

37:   function getVaults()
38:     external
39:     view
40:     returns (address[] memory) {

44:   function isLicensed(
45:     address vault
46:   )
47:     external
48:     view
49:     returns (bool) {
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                  |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              4 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28),[37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset,
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   )
37:     external
38:     view
39:       onlyVaultManager
40:   {

44:   function assetPrice()
45:     public
46:     view
47:     override
48:     returns (uint) {
```

| File Link                                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                              |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              4 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17),[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.sol

36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public
41:       onlyVaultManager
42:   {

47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view
65:     returns (uint) {

69:   function assetPrice()
70:     public
71:     view
72:     virtual
73:     returns (uint);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              4 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47),[60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60),[69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset,
24:       Dyad            _dyad,
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {

50:   function assetPrice()
51:     public
52:     view
53:     override
54:     returns (uint) {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              4 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21),[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43),[50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50) |
___
```solidity
File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {

80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   )
84:     external
85:       isDNftOwner(id)
86:   {

106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   )
110:     external
111:       isDNftOwner(id)
112:   {

230:   function collatRatio(
231:     uint id
232:   )
233:     public
234:     view
235:     returns (uint) {

241:   function getTotalUsdValue(
242:     uint id
243:   )
244:     public
245:     view
246:     returns (uint) {

250:   function getNonKeroseneValue(
251:     uint id
252:   )
253:     public
254:     view
255:     returns (uint) {

269:   function getKeroseneValue(
270:     uint id
271:   )
272:     public
273:     view
274:     returns (uint) {

290:   function getVaults(
291:     uint id
292:   )
293:     external
294:     view
295:     returns (address[] memory) {

299:   function hasVault(
300:     uint    id,
301:     address vault
302:   )
303:     external
304:     view
305:     returns (bool) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             10 | [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49),[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59),[80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80),[106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106),[230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230),[241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241),[250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250),[269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269),[290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290),[299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299) |
___
```solidity
File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {

17:   function denominator() external view returns (uint) {
```

| File Link                                                                                                           | Instance Count | Instance Links                                                                                                                                                                                        |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              2 | [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11),[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17) |
___
</details>

#### <a id="n-29"></a> \[N-29\] NatSpec: Invalid NatSpec comment style
##### Description:
NatSpec must begin with `///`, or use `/** ... */` syntax.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/staking/KerosineDenominator.sol

18:     // @dev: We subtract all the Kerosene in the multi-sig.
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L18) |
___
#### <a id="n-30"></a> \[N-30\] NatSpec: Modifier declarations should have NatSpec descriptions
##### Description:
[NatSpec documentation](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) should be used for improved readability, a better user experience, enhanced auditability, enablement of automated testing and verification, and to promote standardization and interoperability.

##### Recommendation:
Add NatSpec documentation to all modifiers.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

21:   modifier onlyVaultManager() {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21) |
___
```solidity
File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              3 | [39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39),[42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42),[45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45) |
___
#### <a id="n-31"></a> \[N-31\] NatSpec: State variable declarations should have descriptions
##### Description:
[NatSpec documentation](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) should be used for improved readability, a better user experience, enhanced auditability, enablement of automated testing and verification, and to promote standardization and interoperability.

##### Recommendation:
Use `@notice` for public state variables, and `@dev` for non-public ones.

##### Instances:
There are 21 instances of this issue.
<details><summary>View 21 Instances</summary>

```solidity
File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

16:   EnumerableSet.AddressSet private vaults;
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                          |
| :------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              2 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14),[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

15:   UnboundedKerosineVault public unboundedKerosineVault;
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L15) |
___
```solidity
File: src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

19:   mapping(uint => uint) public id2asset;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              4 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15),[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L16),[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L17),[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

19:   KerosineDenominator  public kerosineDenominator;
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18),[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L19) |
___
```solidity
File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;

32:   KerosineManager public keroseneManager;

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults;

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;

37:   mapping (uint => uint) public idToBlockOfLastDeposit;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :----------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             11 | [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22),[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23),[25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25),[26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28),[29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L29),[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L30),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L32),[34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34),[35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35),[37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37) |
___
```solidity
File: src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9) |
___
</details>

#### <a id="n-32"></a> \[N-32\] Setters should prevent re-setting of the same value
##### Description:
When setting the value of a state variable, validation should be added to prevent resetting it to its current value. This is particularly important if the setter also emits the new (same) value, which may be confusing to off-chain tools that parse events.

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit state variable: unboundedKerosineVault
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23) |
___
```solidity
File: src/core/Vault.kerosine.sol

/// @audit state variable: id2asset
36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public
41:       onlyVaultManager
42:   {

/// @audit state variable: id2asset
47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              2 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit state variable: id2asset
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

/// @audit state variable: kerosineDenominator
43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
#### <a id="n-33"></a> \[N-33\] Style guide: Horizontal whitespace in mapping definitions
##### Description:
Per the [Solidity style guide](https://docs.soliditylang.org/en/latest/style-guide.html#mappings), in variable declarations, do not separate the keyword `mapping` from its type by a space. Do not separate any nested `mapping` keyword from its type by whitespace.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults;

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;

37:   mapping (uint => uint) public idToBlockOfLastDeposit;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              3 | [34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34),[35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35),[37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37) |
___
#### <a id="n-34"></a> \[N-34\] Typos
##### Description:
Typos in comments reflect poorly on the protocol, can indicate a lack of attention to detail by the developers, and can decrease confidence in the project.

##### Recommendation:
Correct the typos and use an IDE extension/plugin to assist with spelling.

##### Instances:
There is 1 instance of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit wsteth
55:     // wsteth vault
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [55](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L55) |
___
#### <a id="n-35"></a> \[N-35\] Unnecessary cast
##### Description:
The variable is being cast to its own type.

##### Recommendation:
Remove unnecessary casting to increase code clarity and readability.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/VaultManagerV2.sol

/// @audit address()
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

| File Link                                                                                              | Instance Count | Instance Link                                                                                |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129) |
___
#### <a id="n-36"></a> \[N-36\] Unused import
##### Description:
The identifier is imported but never used within the file.

##### Instances:
There are 3 instances of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit IWETH
13: import {IWETH}                  from "../../src/interfaces/IWETH.sol";
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [13](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L13) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit Dyad
6: import {Dyad}                   from "./Dyad.sol";
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                    |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L6) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit BoundedKerosineVault
9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L9) |
___
#### <a id="n-37"></a> \[N-37\] Use more recent OpenZeppelin version for bug fixes and performance improvements
##### Description:
OpenZeppelin version 5.0.0+ provides bug fixes and performance improvements. See [the release notes](https://github.com/OpenZeppelin/openzeppelin-contracts/releases/tag/v5.0.0) for more info.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/KerosineManager.sol

/// @audit version in use: 4.8.0
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [4](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L4) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit version in use: 4.8.0
14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

/// @audit version in use: 4.8.0
15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L14),[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L15) |
___

### <a id="details-gas-optimizations"></a> Gas Optimizations
#### <a id="g-01"></a> \[G-01\] `address(this)` should be cached
##### Description:
The instances below point to the second+ access of `address(this)` within a function. Caching saves gas when compared to repeating the calculation at each point it is used in the contract.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/VaultManagerV2.sol

144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

236:       uint _dyad = dyad.mintedDyad(address(this), id);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                      |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              4 | [144](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L144),[164](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L164),[215](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L215),[236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236) |
___
#### <a id="g-02"></a> \[G-02\] Assembly: Check `msg.sender` using `xor` and the scratch space
##### Description:
Assembly can be used to efficiently validate `msg.sender` with the least amount of opcodes necessary. Additionally, `xor()` can be used, saving 3 gas. Potentially more gas can be saved by using scratch space to store the error selector, potentially avoiding memory expansion costs. An example is available for reference in [this prior finding](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender).

##### Instances:
There are 2 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

/// @audit comparing against address(vaultManager)
22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L22) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit comparing against dNft.ownerOf(id)
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [40](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L40) |
___
#### <a id="g-03"></a> \[G-03\] Assembly: Optimize `address` storage value management with assembly
##### Description:
Save gas by using assembly to manage `address` storage values. Example:
```solidity
// Before:
owner = newOwner;

// After:
assembly {
    sstore(owner.slot, newOwner)
}
```

##### Instances:
There are 11 instances of this issue.
<details><summary>View 11 Instances</summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

29:     unboundedKerosineVault = _unboundedKerosineVault;
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L29) |
___
```solidity
File: src/core/Vault.kerosine.sol

31:     vaultManager    = _vaultManager;

32:     asset           = _asset;

33:     kerosineManager = _kerosineManager;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              3 | [31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L31),[32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L32),[33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L33) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

27:       dyad = _dyad;

47:     kerosineDenominator = _kerosineDenominator;
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [27](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L27),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L47) |
___
```solidity
File: src/core/VaultManagerV2.sol

54:     dNft          = _dNft;

55:     dyad          = _dyad;

56:     vaultLicenser = _licenser;

63:       keroseneManager = _keroseneManager;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              4 | [54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L54),[55](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L55),[56](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L56),[63](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63) |
___
```solidity
File: src/staking/KerosineDenominator.sol

14:     kerosine = _kerosine;
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L14) |
___
</details>

#### <a id="g-04"></a> \[G-04\] Assembly: Simple checks for `uint` zero can be done using assembly to save gas
##### Description:
It is more gas efficient to use assembly to check for a `uint` being zero.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/VaultManagerV2.sol

237:       if (_dyad == 0) return type(uint).max;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                                |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237) |
___
#### <a id="g-05"></a> \[G-05\] Assembly: Use scratch space for building calldata
##### Description:
If an external call's calldata can fit into two or fewer words (64 bytes), use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

##### Instances:
There are 25 instances of this issue.
<details><summary>View 25 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

64:     kerosineManager.add(address(ethVault));

65:     kerosineManager.add(address(wstEth));

69:     kerosineManager.transferOwnership(MAINNET_OWNER);

90:     unboundedKerosineVault.transferOwnership(MAINNET_OWNER);

91:     boundedKerosineVault.  transferOwnership(MAINNET_OWNER);

93:     vaultLicenser.add(address(ethVault));

94:     vaultLicenser.add(address(wstEth));

95:     vaultLicenser.add(address(unboundedKerosineVault));

98:     vaultLicenser.transferOwnership(MAINNET_OWNER);
```

| File Link                                                                                             | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              9 | [64](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L64),[65](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L65),[69](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L69),[90](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L90),[91](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L91),[93](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L93),[94](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L94),[95](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L95),[98](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L98) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

60:         tvl += vault.asset().balanceOf(address(vault))
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60) |
___
```solidity
File: src/core/VaultManagerV2.sol

75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();

88:     if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

130:     _vault.deposit(id, amount);

144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

236:       uint _dyad = dyad.mintedDyad(address(this), id);

261:         if (vaultLicenser.isLicensed(address(vault))) {

262:           usdValue = vault.getUsdValue(id);

280:         if (keroseneManager.isLicensed(address(vault))) {

281:           usdValue = vault.getUsdValue(id);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |             14 | [75](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L75),[88](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L88),[101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101),[113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113),[130](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L130),[144](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L144),[164](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L164),[215](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L215),[224](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L224),[236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236),[261](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L261),[262](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L262),[280](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L280),[281](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L281) |
___
```solidity
File: src/staking/KerosineDenominator.sol

21:     return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L21) |
___
</details>

#### <a id="g-06"></a> \[G-06\] Assembly: Use scratch space when building emitted events with two data arguments
##### Description:
Using the [scratch space](https://github.com/Vectorized/solady/blob/30558f5402f02351b96eeb6eaf32bcea29773841/src/tokens/ERC1155.sol#L501-L504) for event arguments (two words or fewer) will save gas over needing Solidity's full abi memory expansion used for emitting normally. Note: In order to do this optimization safely, the free memory pointer must be first cached and subsequently restored.

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L44) |
___
```solidity
File: src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                  |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              4 | [77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77),[90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90),[103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103),[115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115) |
___
#### <a id="g-07"></a> \[G-07\] Avoid transferring amounts of zero in order to save gas
##### Description:
Skipping the external call when nothing will be transferred will save at least 100 gas.

##### Instances:
There are 2 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

39:     asset.safeTransfer(to, amount);
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L39) |
___
```solidity
File: src/core/VaultManagerV2.sol

129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

| File Link                                                                                              | Instance Count | Instance Link                                                                                |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129) |
___
#### <a id="g-08"></a> \[G-08\] Avoid updating storage when the value hasn't changed to save gas
##### Description:
If the old value is equal to the new value, not re-storing the value will avoid a `Gsreset` (2900 gas), potentially at the expense of a `Gcoldsload` (2100 gas) or a `Gwarmaccess` (100 gas)

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit state variable: unboundedKerosineVault
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23) |
___
```solidity
File: src/core/Vault.kerosine.sol

/// @audit state variable: id2asset
36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public
41:       onlyVaultManager
42:   {

/// @audit state variable: id2asset
47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              2 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36),[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit state variable: id2asset
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   )
35:     external
36:       onlyVaultManager
37:   {

/// @audit state variable: kerosineDenominator
43:   function setDenominator(KerosineDenominator _kerosineDenominator)
44:     external
45:       onlyOwner
46:   {
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30),[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43) |
___
#### <a id="g-09"></a> \[G-09\] Consider using Solady's `FixedPointMathLib` for multiplication followed by division
##### Description:
Using Solady's [`FixedPointMathLib.fullMulDiv()`](https://github.com/Vectorized/solady/blob/6cce088e69d6e46671f2f622318102bd5db77a65/src/utils/FixedPointMathLib.sol#L267) for multiplication followed by division saves gas and works to avoid unnecessary overflows.

##### Instances:
There are 10 instances of this issue.
<details><summary>View 10 Instances</summary>

```solidity
File: src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L66) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

60:         tvl += vault.asset().balanceOf(address(vault))
61:                 * vault.assetPrice() * 1e18

62:                 / (10**vault.asset().decimals())

63:                 / (10**vault.oracle().decimals());

67:       return numerator * 1e8 / denominator;
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              4 | [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60),[62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L62),[63](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L63),[67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67) |
___
```solidity
File: src/core/VaultManagerV2.sol

146:     uint value = amount * _vault.assetPrice()
147:                   * 1e18

148:                   / 10**_vault.oracle().decimals()

149:                   / 10**_vault.asset().decimals();

195:       uint asset = amount
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals()))

196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals()))
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              5 | [146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146),[148](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L148),[149](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L149),[195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195),[196](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L196) |
___
</details>

#### <a id="g-10"></a> \[G-10\] Constructors can be marked `payable`
##### Description:
`payable` functions cost less gas to execute since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A `constructor` can safely be marked as `payable` since only the deployer can pass funds.

##### Instances:
There are 5 instances of this issue.
```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset,
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17) |
___
```solidity
File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset,
29:     KerosineManager _kerosineManager
30:   ) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset,
24:       Dyad            _dyad,
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21) |
___
```solidity
File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49) |
___
```solidity
File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11) |
___
#### <a id="g-11"></a> \[G-11\] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped
##### Description:
A `do`-`while` loop will cost less gas since the condition is not being checked for the first iteration. Example:
```solidity
// Before:
for (uint256 i; i < len; ++i) {
    ...;
}

// After:
do {
    ...;
    ++i;
} while (i < len);
```

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58) |
___
```solidity
File: src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                         |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              3 | [222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222),[258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258),[277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277) |
___
#### <a id="g-12"></a> \[G-12\] Initializers can be marked `payable`
##### Description:
`payable` functions cost less gas to execute since the compiler does not have to add extra checks to ensure that a payment wasn't provided. An initializer can safely be marked as `payable` since only the deployer can pass funds.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager)
60:     external
61:       initializer
62:     {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59) |
___
#### <a id="g-13"></a> \[G-13\] Multiple accesses of a `mapping`/`array` should use a local variable cache
##### Description:
The instances below point to the second+ access of a value inside a `mapping`/`array` within a function. Caching the value in a local `storage` or `calldata` variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key's `keccak256` hash (`Gkeccak256` - 30 gas) and that calculation's associated stack operations. Caching an `array`'s struct avoids recalculating the array offsets into `memory`/`calldata`.

##### Instances:
There are 2 instances of this issue.
```solidity
File: src/core/VaultManagerV2.sol

/// @audit vaults[] read 2 times in function add()
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

/// @audit vaultsKerosene[] read 2 times in function addKerosene()
87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [74](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L74),[87](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L87) |
___
#### <a id="g-14"></a> \[G-14\] Only emit event in setter function if the state variable was changed
##### Description:
Gas can be saved in a setter function by skipping the event emission if the value of the state variable was not changed.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

/// @audit potentially unnecessary emit
44:     emit Deposit(id, amount);

/// @audit potentially unnecessary emit
57:     emit Move(from, to, amount);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              2 | [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L44),[57](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L57) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit potentially unnecessary emit
40:     emit Withdraw(id, to, amount);
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [40](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40) |
___
#### <a id="g-15"></a> \[G-15\] Optimize names to save gas
##### Description:
`public` and `external` function names and `public` member variable names can be optimized to save gas. The contracts listed below can be optimized so that the most frequently called functions use the least amount of gas possible during the Method ID lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment. Renaming functions to have lower Method IDs will save 22 gas per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92).

##### Recommendation:
Use a tool like [Solidity Optimize Name](https://emn178.github.io/solidity-optimize-name/) to find names that will generate Method IDs that will prioritize the most used functions.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/KerosineManager.sol

/// @audit add(), remove(), getVaults(), isLicensed()
7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit setUnboundedKerosineVault(), withdraw()
12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit withdraw(), setDenominator()
15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit setKeroseneManager(), add(), addKerosene(), remove(), removeKerosene(), deposit(), withdraw(), mintDyad(), burnDyad(), redeemDyad(), liquidate(), collatRatio(), getTotalUsdValue(), getNonKeroseneValue(), getKeroseneValue(), getVaults(), hasVault()
17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
#### <a id="g-16"></a> \[G-16\] `public` functions not called by the contract should be declared `external` instead
##### Description:
Public functions that are not used internally should be made `external` to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for `public` functions. Per Solidity's [Function Overriding](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding), an "overriding function may only change the visibility of the overridden function from `external` to `public`." The visibility of an overridden `public` function cannot be changed to `external`, so this guidance does not apply to overridden `public` functions that are not called internally.

##### Recommendation:
Reduce function visibility from `public` to `external` when unused from within the contract and not required to be `public` by a parent contract.

##### Instances:
There is 1 instance of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36) |
___
#### <a id="g-17"></a> \[G-17\] Reduce deployment costs by tweaking contracts' metadata
##### Description:
As explained in [Understanding smart contract metadata](https://www.rareskills.io/post/solidity-metadata):
> ...reduce the gas cost by mining for IPFS hashes that have a lot of zero bytes in them. When the contract is deployed, the zero bytes will reduce the cost of the calldata.

##### Instances:
There are 6 instances of this issue.
<details><summary>View 6 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [35](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35) |
___
```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15) |
___
```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17) |
___
```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7) |
___
</details>

#### <a id="g-18"></a> \[G-18\] Reduce gas usage by moving to Solidity 0.8.19 or later
##### Description:
See [Preventing Dead Code in Runtime Bytecode](https://blog.soliditylang.org/2023/02/22/solidity-0.8.19-release-announcement/#preventing-dead-code-in-runtime-bytecode) for the full details. Additionally, every new release has new optimizations which will save gas.

##### Instances:
There are 7 instances of this issue.
<details><summary>View 7 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                             | Instance Count | Instance Link                                                                              |
| :---------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L2) |
___
```solidity
File: src/core/KerosineManager.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L2) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                    |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2) |
___
```solidity
File: src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2) |
___
```solidity
File: src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                              | Instance Count | Instance Link                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2) |
___
```solidity
File: src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                    |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :----------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L2) |
___
</details>

#### <a id="g-19"></a> \[G-19\] Refactor `modifier`s to call a local `function`
##### Description:
A `modifier`s code is copied to all instances where it is used, increasing bytecode size. By refactoring a `modifier` to an `internal` `function`, bytecode size can be significantly reduced at the cost of one `JUMP`.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.sol

21:   modifier onlyVaultManager() {
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              1 | [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21) |
___
```solidity
File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              3 | [39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39),[42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42),[45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45) |
___
#### <a id="g-20"></a> \[G-20\] Replace OpenZeppelin components with Solady equivalents to save gas
##### Description:
The following OpenZeppelin imports have a [Solady](https://github.com/Vectorized/solady/tree/main) equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.

##### Recommendation:
Switch to use Solady's, "[Gas optimized Solidity snippets.](https://github.com/Vectorized/solady/blob/main/README.md)"

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/VaultManagerV2.sol

/// @audit Initializable
15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

| File Link                                                                                              | Instance Count | Instance Link                                                                              |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              1 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L15) |
___
#### <a id="g-21"></a> \[G-21\] Same cast is done multiple times
##### Description:
It is cheaper to do the cast once and store the result to a variable.

##### Instances:
There are 2 instances of this issue.
```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit address(ethVault) on line 64
93:     vaultLicenser.add(address(ethVault));

/// @audit address(wstEth) on line 65
94:     vaultLicenser.add(address(wstEth));
```

| File Link                                                                                             | Instance Count | Instance Links                                                                                                                                                                            |
| :---------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              2 | [93](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L93),[94](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L94) |
___
#### <a id="g-22"></a> \[G-22\] State variable read in a loop
##### Description:
State variables should be cached in a local variable rather than reading them every iteration of the `for`-loop, which will replace each `Gwarmaccess` (100 gas) with a much cheaper stack read.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit asset
60:         tvl += vault.asset().balanceOf(address(vault))
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals())
63:                 / (10**vault.oracle().decimals());

/// @audit asset
60:         tvl += vault.asset().balanceOf(address(vault))
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals())
```

| File Link                                                                                                                  | Instance Count | Instance Links                                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              2 | [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60),[60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit vaultLicenser
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit keroseneManager
280:         if (keroseneManager.isLicensed(address(vault))) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [261](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L261),[280](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L280) |
___
#### <a id="g-23"></a> \[G-23\] Strict inequality operators are more expensive than non-strict ones
##### Description:
The strict inequality operators `<` and `>` cost three more gas than the non-strict operators `<=` and `>=`. A simple example demonstrating this is available [here](https://gist.github.com/ezcodeslide/173dc7eb726bd469883d1461e9bfb04f).

##### Recommendation:
Adjust comparisons to use the non-strict inequality operators `<=` and `>=` instead of the strict ones `<` and `>`.

##### Instances:
There are 10 instances of this issue.
<details><summary>View 10 Instances</summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58) |
___
```solidity
File: src/core/VaultManagerV2.sol

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow();

165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              9 | [101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101),[113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113),[150](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L150),[152](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L152),[165](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L165),[167](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L167),[222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222),[258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258),[277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277) |
___
</details>

#### <a id="g-24"></a> \[G-24\] The result of function calls should be cached rather than re-calling the function
##### Description:
The instances below point to the second+ call of the function within a single function.

##### Instances:
There is 1 instance of this issue.
```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit vault.asset() on line 60
62:                 / (10**vault.asset().decimals())
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L62) |
___
#### <a id="g-25"></a> \[G-25\] Use more recent OpenZeppelin version for gas boost
##### Description:
OpenZeppelin version 5.0.0+ provides many small gas optimizations. See [the release notes](https://github.com/OpenZeppelin/openzeppelin-contracts/releases/tag/v5.0.0) for more info.

##### Instances:
There are 3 instances of this issue.
```solidity
File: src/core/KerosineManager.sol

/// @audit version in use: 4.8.0
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
```

| File Link                                                                                                | Instance Count | Instance Link                                                                             |
| :------------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [4](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L4) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit version in use: 4.8.0
14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

/// @audit version in use: 4.8.0
15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              2 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L14),[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L15) |
___
#### <a id="g-26"></a> \[G-26\] Use named `return` values
##### Description:
Naming `function` `return` values reduces gas consumption, as it eliminates the need to initialize and explicitly return variables.

##### Instances:
There are 15 instances of this issue.
<details><summary>View 15 Instances</summary>

```solidity
File: script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
```

| File Link                                                                                             | Instance Count | Instance Link                                                                                |
| :---------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------- |
| [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol) |              1 | [36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36) |
___
```solidity
File: src/core/KerosineManager.sol

37:   function getVaults()
38:     external
39:     view
40:     returns (address[] memory) {

44:   function isLicensed(
45:     address vault
46:   )
47:     external
48:     view
49:     returns (bool) {
```

| File Link                                                                                                | Instance Count | Instance Links                                                                                                                                                                          |
| :------------------------------------------------------------------------------------------------------- | -------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              2 | [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37),[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice()
45:     public
46:     view
47:     override
48:     returns (uint) {
```

| File Link                                                                                                              | Instance Count | Instance Link                                                                                      |
| :--------------------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.bounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol) |              1 | [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44) |
___
```solidity
File: src/core/Vault.kerosine.sol

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view
65:     returns (uint) {

69:   function assetPrice()
70:     public
71:     view
72:     virtual
73:     returns (uint);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                        |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              2 | [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60),[69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice()
51:     public
52:     view
53:     override
54:     returns (uint) {
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50) |
___
```solidity
File: src/core/VaultManagerV2.sol

184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external
191:       isDNftOwner(id)
192:     returns (uint) {

230:   function collatRatio(
231:     uint id
232:   )
233:     public
234:     view
235:     returns (uint) {

241:   function getTotalUsdValue(
242:     uint id
243:   )
244:     public
245:     view
246:     returns (uint) {

250:   function getNonKeroseneValue(
251:     uint id
252:   )
253:     public
254:     view
255:     returns (uint) {

269:   function getKeroseneValue(
270:     uint id
271:   )
272:     public
273:     view
274:     returns (uint) {

290:   function getVaults(
291:     uint id
292:   )
293:     external
294:     view
295:     returns (address[] memory) {

299:   function hasVault(
300:     uint    id,
301:     address vault
302:   )
303:     external
304:     view
305:     returns (bool) {
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              7 | [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184),[230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230),[241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241),[250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250),[269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269),[290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290),[299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299) |
___
```solidity
File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {
```

| File Link                                                                                                           | Instance Count | Instance Link                                                                                      |
| :------------------------------------------------------------------------------------------------------------------ | -------------: | :------------------------------------------------------------------------------------------------- |
| [KerosineDenominator.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol) |              1 | [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17) |
___
</details>

#### <a id="g-27"></a> \[G-27\] Use predefined address instead of `address(this)`
##### Description:
Instead of using `address(this)`, it is more gas-efficient to pre-calculate and use the predefined address. Foundry's `script.sol` and Solmate's `LibRlp.sol` contracts can help pre-determine the address (see [computeCreateAddress](https://book.getfoundry.sh/reference/forge-std/compute-create-address)). The address can be passed in via a constructor argument and assigned to an immutable variable (rather than using a hardcoded constant) so that the code can remain the same across deployments on different networks.

##### Instances:
There are 4 instances of this issue.
```solidity
File: src/core/VaultManagerV2.sol

144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

236:       uint _dyad = dyad.mintedDyad(address(this), id);
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                      |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              4 | [144](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L144),[164](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L164),[215](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L215),[236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236) |
___
#### <a id="g-28"></a> \[G-28\] Using `private` rather than `public` for constants, saves gas
##### Description:
If needed, the constant values can be read from the verified contract source code. If there are multiple values, an alternative approach is to have a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of all the constant values. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table.

##### Instances:
There are 12 instances of this issue.
<details><summary>View 12 Instances</summary>

```solidity
File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;
```

| File Link                                                                                                | Instance Count | Instance Link                                                                               |
| :------------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------ |
| [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol) |              1 | [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14) |
___
```solidity
File: src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                   |
| :----------------------------------------------------------------------------------------------------- | -------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol) |              3 | [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15),[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L16),[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L17) |
___
```solidity
File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18) |
___
```solidity
File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :----------------------------------------------------------------------------------------------------- | -------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              7 | [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22),[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23),[25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25),[26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26),[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28),[29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L29),[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L30) |
___
</details>

#### <a id="g-29"></a> \[G-29\] Variables should be declared outside of loops
##### Description:
Declaring variables inside a loop consumes more gas compared to declaring them outside the loop and just reassigning values to them inside the loop.

##### Instances:
There are 7 instances of this issue.
<details><summary>View 7 Instances</summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit loop starts on line 58
59:         Vault vault = Vault(vaults[i]);
```

| File Link                                                                                                                  | Instance Count | Instance Link                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------- | -------------: | :--------------------------------------------------------------------------------------------------- |
| [Vault.kerosine.unbounded.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol) |              1 | [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L59) |
___
```solidity
File: src/core/VaultManagerV2.sol

/// @audit loop starts on line 222
223:           Vault vault      = Vault(vaults[id].at(i));

/// @audit loop starts on line 222
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

/// @audit loop starts on line 258
259:         Vault vault = Vault(vaults[id].at(i));

/// @audit loop starts on line 258
260:         uint usdValue;

/// @audit loop starts on line 277
278:         Vault vault = Vault(vaultsKerosene[id].at(i));

/// @audit loop starts on line 277
279:         uint usdValue;
```

| File Link                                                                                              | Instance Count | Instance Links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :----------------------------------------------------------------------------------------------------- | -------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol) |              6 | [223](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L223),[224](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L224),[259](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L259),[260](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L260),[278](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L278),[279](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L279) |
___
</details>



