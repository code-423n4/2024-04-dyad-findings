# QA findings report for 2024-04-dyad | Code4rena audit

## Summary

### Medium
| Id|Issue|Instances|
|-|:-|:-:|
| [M-1] | The owner is a single point of failure and a centralization risk | 4 |

### Low
| Id|Issue|Instances|
|-|:-|:-:|
| [L-1] | Functions calling contracts&#x2F;addresses with transfer hooks are missing reentrancy guards | 1 |
| [L-2] | Contracts are vulnerable to fee-on-transfer token related accounting issues | 1 |
| [L-3] | External calls in an un-bounded for-loop may result in a DOS | 1 |
| [L-4] | Division by zero not prevented | 1 |

### Non-critical
| Id|Issue|Instances|
|-|:-|:-:|
| [NC-1] | Public functions not called by the contract should be declared external instead | 3 |
| [NC-2] | File is missing NatSpec | 2 |
| [NC-3] | NatSpec @param is missing | 28 |
| [NC-4] | Overridden function has no body | 9 |
| [NC-5] | Mixed usage of int&#x2F;uint with int256&#x2F;uint256 | 15 |
| [NC-6] | NatSpec @return argument is missing | 7 |
| [NC-7] | Function ordering does not follow the Solidity style guide | 4 |
| [NC-8] | Typos in the code | 13 |
| [NC-9] | Imports could be organized more systematically | 3 |
| [NC-10] | constants should be defined rather than using magic numbers | 3 |
| [NC-11] | Events may be emitted out of order due to reentrancy | 3 |
| [NC-12] | Named mappings is recommended for understandability | 1 |
| [NC-13] | Consider using named mappings | 1 |
| [NC-14] | Events are missing sender information | 3 |
| [NC-15] | Events that mark critical parameter changes should contain both the old and the new value | 3 |
| [NC-16] | Variables need not be initialized to zero | 1 |
| [NC-17] | Custom error has no error details | 3 |
| [NC-18] | Non-external&#x2F;public variable and function names should begin with an underscore | 1 |

### Gas Optimizations


| Id|Issue|Instances|Total Gas Saved|
|-|:-|:-:|:-:|
| [G-1] | Constructors can be marked payable | 4 |  - |
| [G-2] | Functions guaranteed to revert when called by normal users can be marked payable | 4 |  - |
| [G-3] | Optimize method and variable names to save gas | 5 |  - |
| [G-4] | Zero initialization is redundant | 1 |  - |
| [G-5] | Save gas by using private instead of public for constants | 1 |  - |



## Details

### Medium
### [M-1]: The owner is a single point of failure and a centralization risk

Having a single EOA as the only owner of contracts is a large centralization risk and a single point of failure. A single private key may be taken in a hack, or the sole holder of the key may become unable to retrieve the key when necessary. Consider changing to a multi-signature setup, or having a role-based authorization model
 
There are 4 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 23 */
	   function setUnboundedKerosineVault(
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L23)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 43 */
	   function setDenominator(KerosineDenominator _kerosineDenominator) 
```
[Line 43](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L43)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 18 */
	   function add(address vault) external onlyOwner {
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L18)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 23 */
	   function remove(address vault) external onlyOwner {
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L23)




---
### Low

### [L-1]: Functions calling contracts&#x2F;addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to read-only reentrancies. Check: https:&#x2F;&#x2F;chainsecurity.com&#x2F;curve-lp-oracle-manipulation-post-mortem&#x2F;
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 39 */
	     asset.safeTransfer(to, amount); 
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L39)


### [L-2]: Contracts are vulnerable to fee-on-transfer token related accounting issues

Without measuring the balance before and after the transfer, there&#39;s no way to ensure that the exact amount was transferred. This is not safe when the token has a fee-on-transfer mechanism
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 39 */
	     asset.safeTransfer(to, amount); 
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L39)


### [L-3]: External calls in an un-bounded for-loop may result in a DOS

Consider limiting the number of iterations in for-loops that make external calls
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 58 */
	       for (uint i = 0; i < numberOfVaults; i++) {
```
[Line 58](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L58)


### [L-4]: Division by zero not prevented

The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 67 */
	       return numerator * 1e8 / denominator;
```
[Line 67](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L67)



---
### Non-critical

### [NC-1]: Public functions not called by the contract should be declared external instead

Contracts are allowed to override their parents&#39; functions and change the visibility from external to public
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 37 */
	   function assetPrice() public view override returns (uint) {
```
[Line 37](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L37)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 54 */
	   function assetPrice() public view virtual returns (uint);
```
[Line 54](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L54)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 50 */
	   function assetPrice() 
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L50)


### [NC-2]: File is missing NatSpec

Solidity contracts can use a special form of comments to provide rich documentation for functions, return variables and more. This special form is named the Ethereum Natural Language Specification Format (NatSpec).
 
There are 2 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 12 */
	 contract BoundedKerosineVault is KerosineVault {
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L12)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 15 */
	 contract UnboundedKerosineVault is KerosineVault {
```
[Line 15](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L15)


### [NC-3]: NatSpec @param is missing


 
There are 28 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 18 */
	     IVaultManager _vaultManager,
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L18)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 19 */
	     ERC20 _asset,
```
[Line 19](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L19)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 20 */
	     KerosineManager _kerosineManager
```
[Line 20](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L20)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 24 */
	     UnboundedKerosineVault _unboundedKerosineVault
```
[Line 24](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L24)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 30 */
	     uint id,
```
[Line 30](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L30)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 31 */
	     address to,
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L31)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 32 */
	     uint amount
```
[Line 32](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L32)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 30 */
	     IVaultManager _vaultManager,
```
[Line 30](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L30)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 31 */
	     ERC20 _asset,
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L31)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 32 */
	     KerosineManager _kerosineManager
```
[Line 32](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L32)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 39 */
	   function deposit(uint id, uint amount) public onlyVaultManager {
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L39)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 39 */
	   function deposit(uint id, uint amount) public onlyVaultManager {
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L39)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 44 */
	   function move(uint from, uint to, uint amount) external onlyVaultManager {
```
[Line 44](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L44)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 44 */
	   function move(uint from, uint to, uint amount) external onlyVaultManager {
```
[Line 44](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L44)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 44 */
	   function move(uint from, uint to, uint amount) external onlyVaultManager {
```
[Line 44](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L44)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 50 */
	   function getUsdValue(uint id) public view returns (uint) {
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L50)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 22 */
	       IVaultManager   _vaultManager,
```
[Line 22](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L22)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 23 */
	       ERC20           _asset, 
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L23)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 24 */
	       Dyad            _dyad, 
```
[Line 24](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L24)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 25 */
	       KerosineManager _kerosineManager
```
[Line 25](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L25)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 31 */
	     uint    id,
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L31)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 32 */
	     address to,
```
[Line 32](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L32)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 33 */
	     uint    amount
```
[Line 33](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L33)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 43 */
	   function setDenominator(KerosineDenominator _kerosineDenominator) 
```
[Line 43](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L43)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 18 */
	   function add(address vault) external onlyOwner {
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L18)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 23 */
	   function remove(address vault) external onlyOwner {
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L23)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 31 */
	   function isLicensed(address vault) external view returns (bool) {
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L31)


```solidity
	
	/* File: KerosineDenominator.sol
	   Line: 12 */
	     Kerosine _kerosine
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L12)


### [NC-4]: Overridden function has no body

Consider adding a NatSpec comment describing why the function doesn&#39;t need a body and or the purpose it serves
 
There are 9 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 23 */
	   function setUnboundedKerosineVault(
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L23)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 29 */
	   function withdraw(
```
[Line 29](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L29)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 39 */
	   function deposit(uint id, uint amount) public onlyVaultManager {
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L39)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 44 */
	   function move(uint from, uint to, uint amount) external onlyVaultManager {
```
[Line 44](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L44)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 30 */
	   function withdraw(
```
[Line 30](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L30)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 43 */
	   function setDenominator(KerosineDenominator _kerosineDenominator) 
```
[Line 43](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L43)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 50 */
	   function assetPrice() 
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L50)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 18 */
	   function add(address vault) external onlyOwner {
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L18)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 23 */
	   function remove(address vault) external onlyOwner {
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L23)


### [NC-5]: Mixed usage of int&#x2F;uint with int256&#x2F;uint256

int256&#x2F;uint256 are the preferred type names (they&#39;re what are used for function signatures), so they should be used consistently
 
There are 15 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 13 */
	   error NotWithdrawable(uint id, address to, uint amount);
```
[Line 13](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L13)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 30 */
	     uint id,
```
[Line 30](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L30)


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 32 */
	     uint amount
```
[Line 32](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L32)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 22 */
	   mapping(uint => uint) public id2asset;
```
[Line 22](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L22)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 39 */
	   function deposit(uint id, uint amount) public onlyVaultManager {
```
[Line 39](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L39)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 44 */
	   function move(uint from, uint to, uint amount) external onlyVaultManager {
```
[Line 44](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L44)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 50 */
	   function getUsdValue(uint id) public view returns (uint) {
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L50)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 31 */
	     uint    id,
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L31)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 33 */
	     uint    amount
```
[Line 33](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L33)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 55 */
	       uint tvl;
```
[Line 55](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L55)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 57 */
	       uint numberOfVaults = vaults.length;
```
[Line 57](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L57)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 58 */
	       for (uint i = 0; i < numberOfVaults; i++) {
```
[Line 58](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L58)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 65 */
	       uint numerator   = tvl - dyad.totalSupply();
```
[Line 65](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L65)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 66 */
	       uint denominator = kerosineDenominator.denominator();
```
[Line 66](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L66)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 14 */
	   uint public constant MAX_VAULTS = 10;
```
[Line 14](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L14)


### [NC-6]: NatSpec @return argument is missing


 
There are 7 instances of this issue:


```solidity
	@audit function assetPrice missing NatSpec @return uint
	/* File: Vault.kerosine.bounded.sol
	   Line: 37 */
	   function assetPrice() public view override returns (uint) {
```
[Line 37](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L37)


```solidity
	@audit function getUsdValue missing NatSpec @return uint
	/* File: Vault.kerosine.sol
	   Line: 50 */
	   function getUsdValue(uint id) public view returns (uint) {
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L50)


```solidity
	@audit function assetPrice missing NatSpec @return uint
	/* File: Vault.kerosine.sol
	   Line: 54 */
	   function assetPrice() public view virtual returns (uint);
```
[Line 54](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L54)


```solidity
	@audit function assetPrice missing NatSpec @return uint
	/* File: Vault.kerosine.unbounded.sol
	   Line: 54 */
	     returns (uint) {
```
[Line 54](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L54)


```solidity
	@audit function getVaults missing NatSpec @return undefined
	/* File: KerosineManager.sol
	   Line: 27 */
	   function getVaults() external view returns (address[] memory) {
```
[Line 27](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L27)


```solidity
	@audit function isLicensed missing NatSpec @return bool
	/* File: KerosineManager.sol
	   Line: 31 */
	   function isLicensed(address vault) external view returns (bool) {
```
[Line 31](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L31)


```solidity
	@audit function denominator missing NatSpec @return uint
	/* File: KerosineDenominator.sol
	   Line: 17 */
	   function denominator() external view returns (uint) {
```
[Line 17](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L17)


### [NC-7]: Function ordering does not follow the Solidity style guide

According to the [Solidity style guide](https:&#x2F;&#x2F;docs.soliditylang.org&#x2F;en&#x2F;v0.8.9&#x2F;style-guide.html#order-of-functions), functions should be laid out in the following order :constructor(), receive(), fallback(), external, public, internal, private, but the cases below do not follow this pattern
 
There are 4 instances of this issue:


```solidity
	@audit Functions not orderd correctly in this contract
	/* File: Vault.kerosine.bounded.sol
	   Line: 12 */
	 contract BoundedKerosineVault is KerosineVault {
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L12)


```solidity
	@audit Functions not orderd correctly in this contract
	/* File: Vault.kerosine.sol
	   Line: 12 */
	 abstract contract KerosineVault is
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L12)


```solidity
	@audit Functions not orderd correctly in this contract
	/* File: Vault.kerosine.unbounded.sol
	   Line: 15 */
	 contract UnboundedKerosineVault is KerosineVault {
```
[Line 15](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L15)


```solidity
	@audit Functions not orderd correctly in this contract
	/* File: KerosineDenominator.sol
	   Line: 7 */
	 contract KerosineDenominator is Parameters {
```
[Line 7](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L7)


### [NC-8]: Typos in the code


 
There are 13 instances of this issue:


```solidity
	@audit Kerosine
	/* File: Vault.kerosine.bounded.sol
	   Line: 15 */
	   UnboundedKerosineVault public unboundedKerosineVault;
```
[Line 15](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L15)


```solidity
	@audit kerosine
	/* File: Vault.kerosine.bounded.sol
	   Line: 20 */
	     KerosineManager _kerosineManager
```
[Line 20](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L20)


```solidity
	@audit Kerosine
	/* File: Vault.kerosine.bounded.sol
	   Line: 23 */
	   function setUnboundedKerosineVault(
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L23)


```solidity
	@audit Kerosine
	/* File: Vault.kerosine.bounded.sol
	   Line: 24 */
	     UnboundedKerosineVault _unboundedKerosineVault
```
[Line 24](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L24)


```solidity
	@audit kerosine
	/* File: Vault.kerosine.sol
	   Line: 32 */
	     KerosineManager _kerosineManager
```
[Line 32](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L32)


```solidity
	@audit Usd
	/* File: Vault.kerosine.sol
	   Line: 50 */
	   function getUsdValue(uint id) public view returns (uint) {
```
[Line 50](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L50)


```solidity
	@audit kerosine
	/* File: Vault.kerosine.unbounded.sol
	   Line: 19 */
	   KerosineDenominator  public kerosineDenominator;
```
[Line 19](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L19)


```solidity
	@audit kerosine
	/* File: Vault.kerosine.unbounded.sol
	   Line: 25 */
	       KerosineManager _kerosineManager
```
[Line 25](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L25)


```solidity
	@audit kerosine
	/* File: Vault.kerosine.unbounded.sol
	   Line: 43 */
	   function setDenominator(KerosineDenominator _kerosineDenominator) 
```
[Line 43](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L43)


```solidity
	@audit tvl
	/* File: Vault.kerosine.unbounded.sol
	   Line: 55 */
	       uint tvl;
```
[Line 55](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L55)


```solidity
	@audit sig
	/* File: KerosineDenominator.sol
	   Line: 18 */
	     // @dev: We subtract all the Kerosene in the multi-sig.
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L18)


```solidity
	@audit kerosine
	/* File: KerosineDenominator.sol
	   Line: 9 */
	   Kerosine public kerosine;
```
[Line 9](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L9)


```solidity
	@audit kerosine
	/* File: KerosineDenominator.sol
	   Line: 12 */
	     Kerosine _kerosine
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L12)


### [NC-9]: Imports could be organized more systematically

The contract&#39;s interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 4 */
	 import { KerosineVault } from "./Vault.kerosine.sol";
```
[Line 4](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L4)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 4 */
	 import { IVaultManager } from "../interfaces/IVaultManager.sol";
```
[Line 4](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L4)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 4 */
	 import {KerosineVault}        from "./Vault.kerosine.sol";
```
[Line 4](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L4)


### [NC-10]: constants should be defined rather than using magic numbers

assembly can benefit from using readable constants instead of hex&#x2F;numeric literals
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 51 */
	     return (id2asset[id] * assetPrice()) / 1e8;
```
[Line 51](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L51)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 61 */
	                 * vault.assetPrice() * 1e18
```
[Line 61](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L61)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 67 */
	       return numerator * 1e8 / denominator;
```
[Line 67](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L67)


### [NC-11]: Events may be emitted out of order due to reentrancy

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 41 */
	     emit Deposit(id, amount);
```
[Line 41](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L41)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 47 */
	     emit Move(from, to, amount);
```
[Line 47](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L47)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 40 */
	     emit Withdraw(id, to, amount);
```
[Line 40](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L40)


### [NC-12]: Named mappings is recommended for understandability

Consider moving to solidity version 0.8.18 or later, and use named mappings to make it easier to understand the purpose of each mapping
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 22 */
	   mapping(uint => uint) public id2asset;
```
[Line 22](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L22)


### [NC-13]: Consider using named mappings

Consider moving to solidity version 0.8.18 or later, and using  [named mappings](https:&#x2F;&#x2F;ethereum.stackexchange.com&#x2F;questions&#x2F;51629&#x2F;how-to-name-the-arguments-in-mapping&#x2F;145555#145555) to make it easier to understand the purpose of each mapping
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 22 */
	   mapping(uint => uint) public id2asset;
```
[Line 22](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L22)


### [NC-14]: Events are missing sender information

When an action is triggered based on a user&#39;s action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the msg.sender the events of these types of action will make events much more useful to end users, especially when msg.sender is not tx.origin.
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 41 */
	     emit Deposit(id, amount);
```
[Line 41](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L41)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 47 */
	     emit Move(from, to, amount);
```
[Line 47](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L47)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 40 */
	     emit Withdraw(id, to, amount);
```
[Line 40](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L40)


### [NC-15]: Events that mark critical parameter changes should contain both the old and the new value

This should especially be done if the new value is not required to be different from the old value
 
There are 3 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 41 */
	     emit Deposit(id, amount);
```
[Line 41](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L41)


```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 47 */
	     emit Move(from, to, amount);
```
[Line 47](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L47)


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 40 */
	     emit Withdraw(id, to, amount);
```
[Line 40](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L40)


### [NC-16]: Variables need not be initialized to zero

The default value for variables is zero, so initializing them to zero is superfluous.
 
There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 58 */
	       for (uint i = 0; i < numberOfVaults; i++) {
```
[Line 58](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L58)


### [NC-17]: Custom error has no error details

Consider adding parameters to the error to indicate which user or values caused the failure
 
There are 3 instances of this issue:


```solidity
	
	/* File: KerosineManager.sol
	   Line: 8 */
	   error TooManyVaults();
```
[Line 8](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L8)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 9 */
	   error VaultAlreadyAdded();
```
[Line 9](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L9)


```solidity
	
	/* File: KerosineManager.sol
	   Line: 10 */
	   error VaultNotFound();
```
[Line 10](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L10)


### [NC-18]: Non-external&#x2F;public variable and function names should begin with an underscore

Non-external&#x2F;public variable and function names should begin with an [underscore](https:&#x2F;&#x2F;docs.soliditylang.org&#x2F;en&#x2F;latest&#x2F;style-guide.html#underscore-prefix-for-non-external-functions-and-variables)
 
There are 1 instances of this issue:


```solidity
	
	/* File: KerosineManager.sol
	   Line: 16 */
	   EnumerableSet.AddressSet private vaults;
```
[Line 16](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L16)



---
### Gas Optimizations

### [G-1]: Constructors can be marked payable

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn&#39;t provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds

There are 4 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 17 */
	   constructor(
```
[Line 17](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L17)

```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 29 */
	   constructor(
```
[Line 29](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L29)

```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 21 */
	   constructor(
```
[Line 21](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L21)

```solidity
	
	/* File: KerosineDenominator.sol
	   Line: 11 */
	   constructor(
```
[Line 11](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L11)

### [G-2]: Functions guaranteed to revert when called by normal users can be marked payable

If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are CALLVALUE(2),DUP1(3),ISZERO(3),PUSH2(3),JUMPI(10),PUSH1(3),DUP1(3),REVERT(0),JUMPDEST(1),POP(2), which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost

There are 4 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 23 */
	   function setUnboundedKerosineVault(
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L23)

```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 43 */
	   function setDenominator(KerosineDenominator _kerosineDenominator) 
```
[Line 43](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L43)

```solidity
	
	/* File: KerosineManager.sol
	   Line: 18 */
	   function add(address vault) external onlyOwner {
```
[Line 18](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L18)

```solidity
	
	/* File: KerosineManager.sol
	   Line: 23 */
	   function remove(address vault) external onlyOwner {
```
[Line 23](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L23)

### [G-3]: Optimize method and variable names to save gas

public&#x2F;external function names and public state variable names can be optimized to save gas. Have a look at this [link](https:&#x2F;&#x2F;medium.com&#x2F;joyso&#x2F;solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92) for an idea of how it works. Below are the interfaces&#x2F;contracts that can be optimized. This could save 128 gas for each method during deployment and 22 gas per call

There are 5 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.bounded.sol
	   Line: 12 */
	 contract BoundedKerosineVault is KerosineVault {
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.bounded.sol#L12)

```solidity
	
	/* File: Vault.kerosine.sol
	   Line: 12 */
	 abstract contract KerosineVault is
```
[Line 12](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.sol#L12)

```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 15 */
	 contract UnboundedKerosineVault is KerosineVault {
```
[Line 15](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L15)

```solidity
	
	/* File: KerosineManager.sol
	   Line: 7 */
	 contract KerosineManager is Owned(msg.sender) {
```
[Line 7](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L7)

```solidity
	
	/* File: KerosineDenominator.sol
	   Line: 7 */
	 contract KerosineDenominator is Parameters {
```
[Line 7](https://github.com/code-423n4/2024-04-dyad/src/staking/KerosineDenominator.sol#L7)

### [G-4]: Zero initialization is redundant

In Solidity uint variables are initialized to zero. Setting a uint variable to zero is redundant and can waste gas.

There are 1 instances of this issue:


```solidity
	
	/* File: Vault.kerosine.unbounded.sol
	   Line: 58 */
	       for (uint i = 0; i < numberOfVaults; i++) {
```
[Line 58](https://github.com/code-423n4/2024-04-dyad/src/core/Vault.kerosine.unbounded.sol#L58)

### [G-5]: Save gas by using private instead of public for constants

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that returns a tuple of the values of all currently-public constants. Saves 3406-3606 gas in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it&#39;s used, and not adding another entry to the method ID table

There are 1 instances of this issue:


```solidity
	
	/* File: KerosineManager.sol
	   Line: 14 */
	   uint public constant MAX_VAULTS = 10;
```
[Line 14](https://github.com/code-423n4/2024-04-dyad/src/core/KerosineManager.sol#L14)


