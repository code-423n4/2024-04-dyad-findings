
## Low Issues


*Total <b>65</b> instances over <b>10</b> issues:*

|ID|Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | Missing zero address check in functions with address parameters | 8 |
| [L-2](#L-2) | Consider implementing two-step procedure for updating protocol addresses | 3 |
| [L-3](#L-3) | Constructor / initialization function lacks parameter validation | 5 |
| [L-4](#L-4) | External function calls within loops | 10 |
| [L-5](#L-5) | Missing checks for state variable assignments | 11 |
| [L-6](#L-6) | Missing zero address check in constructor | 5 |
| [L-7](#L-7) | Consider some checks for `address(0)` when setting address state variables | 11 |
| [L-8](#L-8) | Vulnerable version of OZ contarcts is used (`4.8.0`) | 1 |
| [L-9](#L-9) | Centralization Risk for trusted owners | 8 |
| [L-10](#L-10) | External calls in modifiers should be avoided | 3 |

## Non Critical Issues


*Total <b>423</b> instances over <b>49</b> issues:*

|ID|Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | Consider adding a block/deny-list | 6 |
| [NC-2](#NC-2) | Consider adding emergency-stop functionality | 5 |
| [NC-3](#NC-3) | Consider adding formal verification proofs | 1 |
| [NC-4](#NC-4) | Constant redefined elsewhere | 1 |
| [NC-5](#NC-5) | Constants should be put on the left side of comparisons | 2 |
| [NC-6](#NC-6) | `Constructor` should emit an event | 5 |
| [NC-7](#NC-7) | Contract does not follow the Solidity Style Guide's suggested layout ordering | 3 |
| [NC-8](#NC-8) | Contract should expose an `interface` | 32 |
| [NC-9](#NC-9) | Contracts should have full test coverage | 1 |
| [NC-10](#NC-10) | Events that mark critical parameter changes should contain both the old and the new value | 11 |
| [NC-11](#NC-11) | Custom errors has no error details | 3 |
| [NC-12](#NC-12) | `mapping` definitions do not comply with best practices | 3 |
| [NC-13](#NC-13) | Enable IR-based code generation | 1 |
| [NC-14](#NC-14) | Events are emitted without the sender information | 9 |
| [NC-15](#NC-15) | Events may be emitted out of order due to reentrancy | 7 |
| [NC-16](#NC-16) |  Function ordering does not follow the Solidity Style Guide | 7 |
| [NC-17](#NC-17) | Variable names for `immutable`s should use CONSTANT_CASE | 7 |
| [NC-18](#NC-18) | Incorrect withdraw declaration | 3 |
| [NC-19](#NC-19) | Invalid NatSpec comment style | 1 |
| [NC-20](#NC-20) | It is best practice to use linear inheritance | 2 |
| [NC-21](#NC-21) | Large or complicated code bases should implement invariant tests | 1 |
| [NC-22](#NC-22) | Magic numbers should be replaced with constants | 15 |
| [NC-23](#NC-23) | Named mappings are recommended | 1 |
| [NC-24](#NC-24) | Missing NatSpec from contract/error/event/function/modifier declarations | 43 |
| [NC-25](#NC-25) | Missing NatSpec `@author` from contract declaration | 6 |
| [NC-26](#NC-26) | Missing NatSpec `@dev` from contract/event/function/modifier declarations | 47 |
| [NC-27](#NC-27) | Public variable declarations should have NatSpec descriptions | 18 |
| [NC-28](#NC-28) | Missing NatSpec `@notice` from contract/event/function/modifier declarations | 47 |
| [NC-29](#NC-29) | Missing NatSpec `@param` from event/function/modifier declarations | 35 |
| [NC-30](#NC-30) | Missing NatSpec `@return` from function declaration | 14 |
| [NC-31](#NC-31) | Missing NatSpec `@title` from contract declaration | 6 |
| [NC-32](#NC-32) | There is no need to initialize variables with 0 | 4 |
| [NC-33](#NC-33) | Put all system-wide constants in one file | 5 |
| [NC-34](#NC-34) | Setters should prevent re-setting the same value | 3 |
| [NC-35](#NC-35) | State variables should include comments | 4 |
| [NC-36](#NC-36) | Unnecessary cast | 27 |
| [NC-37](#NC-37) | Unused import | 2 |
| [NC-38](#NC-38) | Unused contract variables | 1 |
| [NC-39](#NC-39) | Expressions for constant values should use `immutable` rather than `constant` | 5 |
| [NC-40](#NC-40) | Upgrade `openzeppelin` to the latest version (`5.0.2`) | 1 |
| [NC-41](#NC-41) | Use the latest solidity version for deployment (`0.8.25`) | 6 |
| [NC-42](#NC-42) | Use the Modern Upgradeable Contract Paradigm | 6 |
| [NC-43](#NC-43) | Consider using modifiers for address control | 2 |
| [NC-44](#NC-44) | Use of `override` is unnecessary | 2 |
| [NC-45](#NC-45) | Empty body - Consider commenting why | 1 |
| [NC-46](#NC-46) | Names of `private`/`internal` state variables should be prefixed with an underscore | 3 |
| [NC-47](#NC-47) | Functions not used internally could be marked `external` | 4 |
| [NC-48](#NC-48) | Don't only depend on Solidity's arithmetic ordering | 1 |
| [NC-49](#NC-49) | Incorrect comparison against a max value | 3 |

## Gas Optimizations


*Total <b>166</b> instances over <b>26</b> issues:*

|ID|Issue|Instances|Gas|
|-|:-|:-:|:-:|
| [GAS-1](#GAS-1) | Optimize gas by using do-while loops | 4 | 1020 |
| [GAS-2](#GAS-2) | Consider activating via-ir for deploying | 1 | - |
| [GAS-3](#GAS-3) | Counting down in for statements is more gas efficient | 4 | - |
| [GAS-4](#GAS-4) | Divisions can be `unchecked` to save gas | 8 | 160 |
| [GAS-5](#GAS-5) | Increments can be `unchecked` to save gas | 4 | 240 |
| [GAS-6](#GAS-6) | Multiple accesses of the same mapping/array key/index should be cached | 5 | 210 |
| [GAS-7](#GAS-7) | Operator `>=`/`<=` costs less gas than operator `>`/`<` | 6 | 18 |
| [GAS-8](#GAS-8) | Optimize names to save gas | 5 | 110 |
| [GAS-9](#GAS-9) | Reduce gas usage by moving to Solidity 0.8.19 or later | 6 | 6000 |
| [GAS-10](#GAS-10) | Remove or replace unused state variables | 1 | - |
| [GAS-11](#GAS-11) | State variables access within a loop | 2 | 530 |
| [GAS-12](#GAS-12) | State variables only set in the constructor should be declared immutable | 1 | 20000 |
| [GAS-13](#GAS-13) | Optimize external calls with assembly for memory efficiency | 18 | 3960 |
| [GAS-14](#GAS-14) | Use assembly to emit events | 11 | 418 |
| [GAS-15](#GAS-15) | Use assembly to validate `msg.sender` | 2 | - |
| [GAS-16](#GAS-16) | Use assembly to write address/contract type storage values | 11 | 550 |
| [GAS-17](#GAS-17) | Use a more recent version of solidity | 6 | - |
| [GAS-18](#GAS-18) | Use != 0 instead of > 0 | 2 | 6 |
| [GAS-19](#GAS-19) | Consider Using Solady's Gas Optimized Lib for Math | 5 | - |
| [GAS-20](#GAS-20) | Don't initialize variables with default value | 4 | - |
| [GAS-21](#GAS-21) | `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too) | 4 | 20 |
| [GAS-22](#GAS-22) | Using `private` rather than `public` for constants, saves gas | 5 | - |
| [GAS-23](#GAS-23) | Use assembly to check for `address(0)` | 1 | 6 |
| [GAS-24](#GAS-24) | Avoid updating storage when the value hasn't changed | 16 | - |
| [GAS-25](#GAS-25) | Unnecessary casting as variable is already of the same type | 27 | - |
| [GAS-26](#GAS-26) | Variable declared within iteration | 7 | - |

## Low Issues

<a name="L-1"></a> 
### [L-1] Missing zero address check in functions with address parameters
Adding a zero address check for each address type parameter can prevent errors.

*There are <b>8</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit missing zero check for `_unboundedKerosineVault`
23:   function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
      )
        external
        onlyOwner
      {

/// @audit missing zero check for `to`
32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
        view
          onlyVaultManager
      {

```
*Github:* [[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit missing zero check for `to`
30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
          onlyVaultManager
      {

/// @audit missing zero check for `_kerosineDenominator`
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
        external 
          onlyOwner
      {

```
*Github:* [[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit missing zero check for `_keroseneManager`
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
        external
          initializer 
        {

/// @audit missing zero check for `to`
134:   function withdraw(
         uint    id,
         address vault,
         uint    amount,
         address to
       ) 
         public
           isDNftOwner(id)
       {

/// @audit missing zero check for `to`
156:   function mintDyad(
         uint    id,
         uint    amount,
         address to
       )
         external 
           isDNftOwner(id)
       {

/// @audit missing zero check for `to`
184:   function redeemDyad(
         uint    id,
         address vault,
         uint    amount,
         address to
       )
         external 
           isDNftOwner(id)
         returns (uint) { 

```
*Github:* [[59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184)]



<a name="L-2"></a> 
### [L-2] Consider implementing two-step procedure for updating protocol addresses
A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must "accept" the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the "set" functions ensure that the recipient is of the right interface type.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `unboundedKerosineVault`
23:   function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
      )
        external
        onlyOwner
      {

```
*Github:* [[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `kerosineDenominator`
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
        external 
          onlyOwner
      {

```
*Github:* [[43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `keroseneManager`
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
        external
          initializer 
        {

```
*Github:* [[59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59)]



<a name="L-3"></a> 
### [L-3] Constructor / initialization function lacks parameter validation
Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `_vaultManager` not validated
/// @audit `_asset` not validated
/// @audit `_kerosineManager` not validated
17:   constructor(

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17)]


```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit `_vaultManager` not validated
/// @audit `_asset` not validated
/// @audit `_kerosineManager` not validated
26:   constructor(

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `_vaultManager` not validated
/// @audit `_asset` not validated
/// @audit `_dyad` not validated
/// @audit `_kerosineManager` not validated
21:   constructor(

```
*Github:* [[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `_dNft` not validated
/// @audit `_dyad` not validated
/// @audit `_licenser` not validated
49:   constructor(

```
*Github:* [[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit `_kerosine` not validated
11:   constructor(

```
*Github:* [[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11)]



<a name="L-4"></a> 
### [L-4] External function calls within loops
Calling external functions within loops can easily result in insufficient gas. This greatly increases the likelihood of transaction failures, DOS attacks, and other unexpected actions. It is recommended to limit the number of loops within loops that call external functions, and to limit the gas line for each external call.

*There are <b>10</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `.asset(...)`
60:         tvl += vault.asset().balanceOf(address(vault)) 

/// @audit `.assetPrice(...)`
61:                 * vault.assetPrice() * 1e18

/// @audit `.asset(...)`
62:                 / (10**vault.asset().decimals()) 

/// @audit `.oracle(...)`
63:                 / (10**vault.oracle().decimals());

```
*Github:* [[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60), [61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L61), [62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `.id2asset(...)`
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

/// @audit `.move(...)`
225:           vault.move(id, to, collateral);

/// @audit `.isLicensed(...)`
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit `.getUsdValue(...)`
262:           usdValue = vault.getUsdValue(id);        

/// @audit `.isLicensed(...)`
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit `.getUsdValue(...)`
281:           usdValue = vault.getUsdValue(id);        

```
*Github:* [[224](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L224), [225](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L225), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [262](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L262), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [281](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L281)]



<a name="L-5"></a> 
### [L-5] Missing checks for state variable assignments
There are some missing checks in these functions, and this could lead to unexpected scenarios. Consider always adding a sanity check for state variables.

<details>
<summary>
There are <b>11</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `_unboundedKerosineVault`
29:     unboundedKerosineVault = _unboundedKerosineVault;

```
*Github:* [[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29)]


```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit `_vaultManager`
31:     vaultManager    = _vaultManager;

/// @audit `_asset`
32:     asset           = _asset;

/// @audit `_kerosineManager`
33:     kerosineManager = _kerosineManager;

```
*Github:* [[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `_dyad`
27:       dyad = _dyad;

/// @audit `_kerosineDenominator`
47:     kerosineDenominator = _kerosineDenominator;

```
*Github:* [[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `_dNft`
54:     dNft          = _dNft;

/// @audit `_dyad`
55:     dyad          = _dyad;

/// @audit `_licenser`
56:     vaultLicenser = _licenser;

/// @audit `_keroseneManager`
63:       keroseneManager = _keroseneManager;

```
*Github:* [[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit `_kerosine`
14:     kerosine = _kerosine;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14)]


</details>


<a name="L-6"></a> 
### [L-6] Missing zero address check in constructor
Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address (0x0). This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit missing zero check for `_vaultManager`
/// @audit missing zero check for `_asset`
/// @audit missing zero check for `_kerosineManager`
17:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17)]


```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit missing zero check for `_vaultManager`
/// @audit missing zero check for `_asset`
/// @audit missing zero check for `_kerosineManager`
26:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager 
      ) {

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit missing zero check for `_vaultManager`
/// @audit missing zero check for `_asset`
/// @audit missing zero check for `_dyad`
/// @audit missing zero check for `_kerosineManager`
21:   constructor(
          IVaultManager   _vaultManager,
          ERC20           _asset, 
          Dyad            _dyad, 
          KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```
*Github:* [[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit missing zero check for `_dNft`
/// @audit missing zero check for `_dyad`
/// @audit missing zero check for `_licenser`
49:   constructor(
        DNft          _dNft,
        Dyad          _dyad,
        Licenser      _licenser
      ) {

```
*Github:* [[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit missing zero check for `_kerosine`
11:   constructor(
        Kerosine _kerosine
      ) {

```
*Github:* [[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11)]



<a name="L-7"></a> 
### [L-7] Consider some checks for `address(0)` when setting address state variables
Check for zero-address to avoid the risk of setting `address(0)` for state variables after an update.

<details>
<summary>
There are <b>11</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `_unboundedKerosineVault`
29:     unboundedKerosineVault = _unboundedKerosineVault;

```
*Github:* [[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29)]


```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit `_vaultManager`
31:     vaultManager    = _vaultManager;

/// @audit `_asset`
32:     asset           = _asset;

/// @audit `_kerosineManager`
33:     kerosineManager = _kerosineManager;

```
*Github:* [[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `_dyad`
27:       dyad = _dyad;

/// @audit `_kerosineDenominator`
47:     kerosineDenominator = _kerosineDenominator;

```
*Github:* [[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `_dNft`
54:     dNft          = _dNft;

/// @audit `_dyad`
55:     dyad          = _dyad;

/// @audit `_licenser`
56:     vaultLicenser = _licenser;

/// @audit `_keroseneManager`
63:       keroseneManager = _keroseneManager;

```
*Github:* [[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit `_kerosine`
14:     kerosine = _kerosine;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14)]


</details>


<a name="L-8"></a> 
### [L-8] Vulnerable version of OZ contarcts is used (`4.8.0`)
The project is using a vulnerable version.
See the list of OZ vulnerabilities [here](https://security.snyk.io/package/npm/@openzeppelin%2Fcontracts).

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="L-9"></a> 
### [L-9] Centralization Risk for trusted owners
Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*There are <b>8</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

18:   function add(
        address vault
      ) 
        external 
          onlyOwner

28:   function remove(
        address vault
      ) 
        external 
          onlyOwner

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
      )
        external
        onlyOwner

32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
        view
          onlyVaultManager

```
*Github:* [[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32)]


```solidity
File: ./src/core/Vault.kerosine.sol

36:   function deposit(
        uint id,
        uint amount
      )
        public 
          onlyVaultManager

47:   function move(
        uint from,
        uint to,
        uint amount
      )
        external
          onlyVaultManager

```
*Github:* [[36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
          onlyVaultManager

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
        external 
          onlyOwner

```
*Github:* [[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43)]



<a name="L-10"></a> 
### [L-10] External calls in modifiers should be avoided
External calls within modifiers can introduce unintended reentrancy risks and obscure the flow of a contract's logic. Modifiers are designed to perform checks before executing function logic, and using external calls can make the flow unpredictable due to the potential for state changes or reentrancy by the called contract. Such ambiguity makes code harder to audit and understand. To ensure clarity and security, avoid external calls in modifiers. Instead, place them in the function body, where their execution order and effects are more explicit. This practice enhances contract readability, aids auditors, and minimizes unexpected behaviors.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `.ownerOf(...)`
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

/// @audit `.ownerOf(...)`
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

/// @audit `.isLicensed(...)`
46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L46)]




## Non Critical Issues

<a name="NC-1"></a> 
### [NC-1] Consider adding a block/deny-list
Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="NC-2"></a> 
### [NC-2] Consider adding emergency-stop functionality
Consider adding `Pausable` to the following contracts so it's possible to stop them in case of an emergency.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="NC-3"></a> 
### [NC-3] Consider adding formal verification proofs
Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="NC-4"></a> 
### [NC-4] Constant redefined elsewhere
Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

*There is one instance of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit also seen in ./src/core/KerosineManager.sol
22:   uint public constant MAX_VAULTS          = 5;

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22)]



<a name="NC-5"></a> 
### [NC-5] Constants should be put on the left side of comparisons
Putting constants on the left side of comparison statements is a best practice known as [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions). Although solidity's static typing system prevents accidental assignments within conditionals, adopting this practice can improve code readability and consistency, especially when working across multiple languages.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

237:       if (_dyad == 0) return type(uint).max;

```
*Github:* [[43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43), [237](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L237)]



<a name="NC-6"></a> 
### [NC-6] `Constructor` should emit an event
Use events to signal significant changes to off-chain monitoring tools.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

17:   constructor(

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17)]


```solidity
File: ./src/core/Vault.kerosine.sol

26:   constructor(

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

21:   constructor(

```
*Github:* [[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21)]


```solidity
File: ./src/core/VaultManagerV2.sol

49:   constructor(

```
*Github:* [[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49)]


```solidity
File: ./src/staking/KerosineDenominator.sol

11:   constructor(

```
*Github:* [[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11)]



<a name="NC-7"></a> 
### [NC-7] Contract does not follow the Solidity Style Guide's suggested layout ordering
The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be `1) Type declarations`, `2) State variables`, `3) Events`, `4) Modifiers`, and `5) Functions`, but the contract(s) below do not follow this ordering

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

/// @audit event/error `TooManyVaults` came earlier
/// @audit event/error `VaultAlreadyAdded` came earlier
/// @audit event/error `VaultNotFound` came earlier
14:   uint public constant MAX_VAULTS = 10;

/// @audit event/error `TooManyVaults` came earlier
/// @audit event/error `VaultAlreadyAdded` came earlier
/// @audit event/error `VaultNotFound` came earlier
16:   EnumerableSet.AddressSet private vaults;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L16)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit event/error `NotWithdrawable` came earlier
15:   UnboundedKerosineVault public unboundedKerosineVault;

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L15)]



<a name="NC-8"></a> 
### [NC-8] Contract should expose an `interface`
All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.

*Note:* It is possible that the interface is out-of-scope and has not been seen by the bot.

<details>
<summary>
There are <b>32</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice() 

```
*Github:* [[23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

36:   function deposit(

47:   function move(

60:   function getUsdValue(

69:   function assetPrice() 

```
*Github:* [[36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

50:   function assetPrice() 

```
*Github:* [[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]


```solidity
File: ./src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

67:   function add(

80:   function addKerosene(

94:   function remove(

106:   function removeKerosene(

119:   function deposit(

134:   function withdraw(

156:   function mintDyad(

172:   function burnDyad(

184:   function redeemDyad(

205:   function liquidate(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(

```
*Github:* [[59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17)]


</details>


<a name="NC-9"></a> 
### [NC-9] Contracts should have full test coverage
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="NC-10"></a> 
### [NC-10] Events that mark critical parameter changes should contain both the old and the new value
This should especially be done if the new value is not required to be different from the old value.

<details>
<summary>
There are <b>11</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);

```
*Github:* [[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L57)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40)]


```solidity
File: ./src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

180:     emit BurnDyad(id, amount, msg.sender);

200:       emit RedeemDyad(id, vault, amount, to);

227:       emit Liquidate(id, msg.sender, to);

```
*Github:* [[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L227)]


</details>


<a name="NC-11"></a> 
### [NC-11] Custom errors has no error details
Consider adding parameters to the error to indicate which user or values caused the failure.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

```
*Github:* [[8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L10)]



<a name="NC-12"></a> 
### [NC-12] `mapping` definitions do not comply with best practices
This is a [best practice](https://docs.soliditylang.org/en/latest/style-guide.html#mappings) that should be followed. In variable declarations, do not separate the keyword mapping from its type by a space. Do not separate any nested mapping keyword from its type by whitespace.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```
*Github:* [[34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L37)]



<a name="NC-13"></a> 
### [NC-13] Enable IR-based code generation
The IR-based code generator was introduced with an aim to not only allow code generation to be more transparent and auditable but also to enable more powerful optimization passes that span across functions. You can enable it on the command line using `--via-ir` or with the option `{"viaIR": true}`. This will take longer to compile, but you can just simple test it before deploying and if you got a better benchmark then you can add --via-ir to your deploy command More on: https://docs.soliditylang.org/en/v0.8.17/ir-breaking-changes.html

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="NC-14"></a> 
### [NC-14] Events are emitted without the sender information
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

*There are <b>9</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);

```
*Github:* [[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L57)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40)]


```solidity
File: ./src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

200:       emit RedeemDyad(id, vault, amount, to);

```
*Github:* [[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200)]



<a name="NC-15"></a> 
### [NC-15] Events may be emitted out of order due to reentrancy
Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls.

*There are <b>7</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `.safeTransfer(...)` is called on line 39
40:     emit Withdraw(id, to, amount);

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `.isLicensed(...)` is called on line 75
77:     emit Added(id, vault);

/// @audit `.isLicensed(...)` is called on line 88
90:     emit Added(id, vault);

/// @audit `.mintedDyad(...)` is called on line 164
/// @audit `.mint(...)` is called on line 166
168:     emit MintDyad(id, amount, to);

/// @audit `.burn(...)` is called on line 179
180:     emit BurnDyad(id, amount, msg.sender);

/// @audit `.burn(...)` is called on line 193
/// @audit `.oracle(...)` is called on line 196
/// @audit `.asset(...)` is called on line 196
/// @audit `.assetPrice(...)` is called on line 197
200:       emit RedeemDyad(id, vault, amount, to);

/// @audit `.mintedDyad(...)` is called on line 215
/// @audit `.burn(...)` is called on line 215
/// @audit `.id2asset(...)` is called on line 224
/// @audit `.move(...)` is called on line 225
227:       emit Liquidate(id, msg.sender, to);

```
*Github:* [[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L227)]



<a name="NC-16"></a> 
### [NC-16]  Function ordering does not follow the Solidity Style Guide
According to the [solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order: `constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*There are <b>7</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit public function `deposit` came earlier from this external function
47:   function move(

```
*Github:* [[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit public function `withdraw` came earlier from this external function
156:   function mintDyad(

/// @audit public function `withdraw` came earlier from this external function
172:   function burnDyad(

/// @audit public function `withdraw` came earlier from this external function
184:   function redeemDyad(

/// @audit public function `withdraw` came earlier from this external function
205:   function liquidate(

/// @audit public function `withdraw` came earlier from this external function
/// @audit public function `collatRatio` came earlier from this external function
/// @audit public function `getTotalUsdValue` came earlier from this external function
/// @audit public function `getNonKeroseneValue` came earlier from this external function
/// @audit public function `getKeroseneValue` came earlier from this external function
290:   function getVaults(

/// @audit public function `withdraw` came earlier from this external function
/// @audit public function `collatRatio` came earlier from this external function
/// @audit public function `getTotalUsdValue` came earlier from this external function
/// @audit public function `getNonKeroseneValue` came earlier from this external function
/// @audit public function `getKeroseneValue` came earlier from this external function
299:   function hasVault(

```
*Github:* [[156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]



<a name="NC-17"></a> 
### [NC-17] Variable names for `immutable`s should use CONSTANT_CASE
For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)

*There are <b>7</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L17)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L18)]


```solidity
File: ./src/core/VaultManagerV2.sol

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;

```
*Github:* [[28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L30)]



<a name="NC-18"></a> 
### [NC-18] Incorrect withdraw declaration
In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for withdraw should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
        view
          onlyVaultManager
      {

```
*Github:* [[32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
          onlyVaultManager
      {

```
*Github:* [[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30)]


```solidity
File: ./src/core/VaultManagerV2.sol

134:   function withdraw(
         uint    id,
         address vault,
         uint    amount,
         address to
       ) 
         public
           isDNftOwner(id)
       {

```
*Github:* [[134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134)]



<a name="NC-19"></a> 
### [NC-19] Invalid NatSpec comment style
NatSpec must begin with `///` or use `/* ... */` syntax

*There is one instance of this issue:*
```solidity
File: ./src/staking/KerosineDenominator.sol

18:     // @dev: We subtract all the Kerosene in the multi-sig.

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L18)]



<a name="NC-20"></a> 
### [NC-20] It is best practice to use linear inheritance
In Solidity, complex inheritance structures can obfuscate code understanding, introducing potential security risks. Multiple inheritance, especially with overlapping function names or state variables, can cause unintentional overrides or ambiguous behavior. 

Resolution: Strive for linear and simple inheritance chains. Avoid diamond or circular inheritance patterns. Clearly document the purpose and relationships of base contracts, ensuring that overrides are intentional. Tools like Remix or Hardhat can visualize inheritance chains, assisting in verification. Keeping inheritance streamlined aids in better code readability, reduces potential errors, and ensures smoother audits and upgrades.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]



<a name="NC-21"></a> 
### [NC-21] Large or complicated code bases should implement invariant tests
This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts. Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="NC-22"></a> 
### [NC-22] Magic numbers should be replaced with constants
Magic numbers are hard-coded values in code that can make it difficult for developers and maintainers to understand the code, and can also cause confusion or errors. To improve the readability and maintainability of code, it is recommended to replace magic numbers with constants that have good readability.

<details>
<summary>
There are <b>15</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.bounded.sol

// @audit `2`
49:       return unboundedKerosineVault.assetPrice() * 2;

```
*Github:* [[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L49)]


```solidity
File: ./src/core/Vault.kerosine.sol

// @audit `1e8`
66:       return id2asset[id] * assetPrice() / 1e8;

```
*Github:* [[66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L66)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

// @audit `1e18`
61:                 * vault.assetPrice() * 1e18

// @audit `10`
62:                 / (10**vault.asset().decimals()) 

// @audit `10`
63:                 / (10**vault.oracle().decimals());

// @audit `1e8`
67:       return numerator * 1e8 / denominator;

```
*Github:* [[61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L61), [62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67)]


```solidity
File: ./src/core/VaultManagerV2.sol

// @audit `1e18`
147:                   * 1e18 

// @audit `10`
148:                   / 10**_vault.oracle().decimals() 

// @audit `10`
149:                   / 10**_vault.asset().decimals();

// @audit `10`
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 

// @audit `1e18`
198:                     / 1e18;

// @audit `1e18`
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

// @audit `1e18`
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

// @audit `1e18`
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

// @audit `1e18`
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

```
*Github:* [[147](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L147), [148](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L149), [196](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L196), [198](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L198), [217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217), [217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L219)]


</details>


<a name="NC-23"></a> 
### [NC-23] Named mappings are recommended
[Named mappings](https://docs.soliditylang.org/en/v0.8.18/types.html#mapping-types) (with syntax `mapping(KeyType KeyName? => ValueType ValueName?)`) are recommended.It can make the mapping variables clearer, more readable and easier to maintain.

*There is one instance of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;

```
*Github:* [[19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L19)]



<a name="NC-24"></a> 
### [NC-24] Missing NatSpec from contract/error/event/function/modifier declarations
e.g. `@dev` or `@notice`, and it must appear above the contract definition braces in order to be identified by the compiler as NatSpec.

<details>
<summary>
There are <b>43</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

18:   function add(
        address vault
      ) 
        external 
          onlyOwner
      {

28:   function remove(
        address vault
      ) 
        external 
          onlyOwner
      {

37:   function getVaults() 
        external 
        view 
        returns (address[] memory) {

44:   function isLicensed(
        address vault
      ) 
        external 
        view 
        returns (bool) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7), [8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L10), [18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

13:   error NotWithdrawable(uint id, address to, uint amount);

17:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

23:   function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
      )
        external
        onlyOwner
      {

32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
        view
          onlyVaultManager
      {

44:   function assetPrice() 
        public 
        view 
        override
        returns (uint) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L13), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

21:   modifier onlyVaultManager() {

26:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager 
      ) {

36:   function deposit(
        uint id,
        uint amount
      )
        public 
          onlyVaultManager
      {

47:   function move(
        uint from,
        uint to,
        uint amount
      )
        external
          onlyVaultManager
      {

60:   function getUsdValue(
        uint id
      )
        public
        view 
        returns (uint) {

69:   function assetPrice() 

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

21:   constructor(
          IVaultManager   _vaultManager,
          ERC20           _asset, 
          Dyad            _dyad, 
          KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
          onlyVaultManager
      {

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
        external 
          onlyOwner
      {

50:   function assetPrice() 
        public 
        view 
        override
        returns (uint) {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(
        DNft          _dNft,
        Dyad          _dyad,
        Licenser      _licenser
      ) {

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
        external
          initializer 
        {

80:   function addKerosene(
          uint    id,
          address vault
      ) 
        external
          isDNftOwner(id)
      {

106:   function removeKerosene(
           uint    id,
           address vault
       ) 
         external
           isDNftOwner(id)
       {

230:   function collatRatio(
         uint id
       )
         public 
         view
         returns (uint) {

241:   function getTotalUsdValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

250:   function getNonKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

269:   function getKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

290:   function getVaults(
         uint id
       ) 
         external 
         view 
         returns (address[] memory) {

299:   function hasVault(
         uint    id,
         address vault
       ) 
         external 
         view 
         returns (bool) {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17), [39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

11:   constructor(
        Kerosine _kerosine
      ) {

17:   function denominator() external view returns (uint) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7), [11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17)]


</details>


<a name="NC-25"></a> 
### [NC-25] Missing NatSpec `@author` from contract declaration
Some contract definitions have an incomplete NatSpec: add a `@author` notation to improve the code documentation.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="NC-26"></a> 
### [NC-26] Missing NatSpec `@dev` from contract/event/function/modifier declarations
Some contract definitions have an incomplete NatSpec: add a `@dev` notation to improve the code documentation.

<details>
<summary>
There are <b>47</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7), [18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

17:   constructor(

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice() 

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

21:   modifier onlyVaultManager() {

26:   constructor(

36:   function deposit(

47:   function move(

60:   function getUsdValue(

69:   function assetPrice() 

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

21:   constructor(

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

50:   function assetPrice() 

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

67:   function add(

80:   function addKerosene(

94:   function remove(

106:   function removeKerosene(

119:   function deposit(

134:   function withdraw(

156:   function mintDyad(

172:   function burnDyad(

184:   function redeemDyad(

205:   function liquidate(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17), [39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

11:   constructor(

17:   function denominator() external view returns (uint) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7), [11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17)]


</details>


<a name="NC-27"></a> 
### [NC-27] Public variable declarations should have NatSpec descriptions

<details>
<summary>
There are <b>18</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

15:   UnboundedKerosineVault public unboundedKerosineVault;

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L15)]


```solidity
File: ./src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

19:   mapping(uint => uint) public id2asset;

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L19)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

19:   KerosineDenominator  public kerosineDenominator;

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L18), [19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L19)]


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;

32:   KerosineManager public keroseneManager;

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L30), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L32), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L37)]


```solidity
File: ./src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;

```
*Github:* [[9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L9)]


</details>


<a name="NC-28"></a> 
### [NC-28] Missing NatSpec `@notice` from contract/event/function/modifier declarations
Some contract definitions have an incomplete NatSpec: add a `@notice` notation to improve the code documentation.

<details>
<summary>
There are <b>47</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7), [18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

17:   constructor(

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice() 

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

21:   modifier onlyVaultManager() {

26:   constructor(

36:   function deposit(

47:   function move(

60:   function getUsdValue(

69:   function assetPrice() 

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

21:   constructor(

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

50:   function assetPrice() 

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15), [21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

67:   function add(

80:   function addKerosene(

94:   function remove(

106:   function removeKerosene(

119:   function deposit(

134:   function withdraw(

156:   function mintDyad(

172:   function burnDyad(

184:   function redeemDyad(

205:   function liquidate(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17), [39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

11:   constructor(

17:   function denominator() external view returns (uint) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7), [11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17)]


</details>


<a name="NC-29"></a> 
### [NC-29] Missing NatSpec `@param` from event/function/modifier declarations
Some event definitions have an incomplete NatSpec: add a `@param` notation to improve the code documentation.

<details>
<summary>
There are <b>35</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

/// @audit missing @param for `vault`
18:   function add(
        address vault
      ) 
        external 
          onlyOwner
      {

/// @audit missing @param for `vault`
28:   function remove(
        address vault
      ) 
        external 
          onlyOwner
      {

/// @audit missing @param for `vault`
44:   function isLicensed(
        address vault
      ) 
        external 
        view 
        returns (bool) {

```
*Github:* [[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit missing @param for `_vaultManager`
/// @audit missing @param for `_asset`
/// @audit missing @param for `_kerosineManager`
17:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

/// @audit missing @param for `_unboundedKerosineVault`
23:   function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
      )
        external
        onlyOwner
      {

/// @audit missing @param for `id`
/// @audit missing @param for `to`
/// @audit missing @param for `amount`
32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
        view
          onlyVaultManager
      {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32)]


```solidity
File: ./src/core/Vault.kerosine.sol

/// @audit missing @param for `_vaultManager`
/// @audit missing @param for `_asset`
/// @audit missing @param for `_kerosineManager`
26:   constructor(
        IVaultManager   _vaultManager,
        ERC20           _asset, 
        KerosineManager _kerosineManager 
      ) {

/// @audit missing @param for `id`
/// @audit missing @param for `amount`
36:   function deposit(
        uint id,
        uint amount
      )
        public 
          onlyVaultManager
      {

/// @audit missing @param for `from`
/// @audit missing @param for `to`
/// @audit missing @param for `amount`
47:   function move(
        uint from,
        uint to,
        uint amount
      )
        external
          onlyVaultManager
      {

/// @audit missing @param for `id`
60:   function getUsdValue(
        uint id
      )
        public
        view 
        returns (uint) {

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit missing @param for `_vaultManager`
/// @audit missing @param for `_asset`
/// @audit missing @param for `_dyad`
/// @audit missing @param for `_kerosineManager`
21:   constructor(
          IVaultManager   _vaultManager,
          ERC20           _asset, 
          Dyad            _dyad, 
          KerosineManager _kerosineManager
      ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

/// @audit missing @param for `id`
/// @audit missing @param for `to`
/// @audit missing @param for `amount`
30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 
        external 
          onlyVaultManager
      {

/// @audit missing @param for `_kerosineDenominator`
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
        external 
          onlyOwner
      {

```
*Github:* [[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43)]


```solidity
File: ./src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

/// @audit missing @param for `_dNft`
/// @audit missing @param for `_dyad`
/// @audit missing @param for `_licenser`
49:   constructor(
        DNft          _dNft,
        Dyad          _dyad,
        Licenser      _licenser
      ) {

/// @audit missing @param for `_keroseneManager`
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
        external
          initializer 
        {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
67:   function add(
          uint    id,
          address vault
      ) 
        external
          isDNftOwner(id)
      {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
80:   function addKerosene(
          uint    id,
          address vault
      ) 
        external
          isDNftOwner(id)
      {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
94:   function remove(
          uint    id,
          address vault
      ) 
        external
          isDNftOwner(id)
      {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
106:   function removeKerosene(
           uint    id,
           address vault
       ) 
         external
           isDNftOwner(id)
       {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
/// @audit missing @param for `amount`
119:   function deposit(
         uint    id,
         address vault,
         uint    amount
       ) 
         external 
           isValidDNft(id)
       {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
/// @audit missing @param for `amount`
/// @audit missing @param for `to`
134:   function withdraw(
         uint    id,
         address vault,
         uint    amount,
         address to
       ) 
         public
           isDNftOwner(id)
       {

/// @audit missing @param for `id`
/// @audit missing @param for `amount`
/// @audit missing @param for `to`
156:   function mintDyad(
         uint    id,
         uint    amount,
         address to
       )
         external 
           isDNftOwner(id)
       {

/// @audit missing @param for `id`
/// @audit missing @param for `amount`
172:   function burnDyad(
         uint id,
         uint amount
       ) 
         external 
           isValidDNft(id)
       {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
/// @audit missing @param for `amount`
/// @audit missing @param for `to`
184:   function redeemDyad(
         uint    id,
         address vault,
         uint    amount,
         address to
       )
         external 
           isDNftOwner(id)
         returns (uint) { 

/// @audit missing @param for `id`
/// @audit missing @param for `to`
205:   function liquidate(
         uint id,
         uint to
       ) 
         external 
           isValidDNft(id)
           isValidDNft(to)
         {

/// @audit missing @param for `id`
230:   function collatRatio(
         uint id
       )
         public 
         view
         returns (uint) {

/// @audit missing @param for `id`
241:   function getTotalUsdValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

/// @audit missing @param for `id`
250:   function getNonKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

/// @audit missing @param for `id`
269:   function getKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

/// @audit missing @param for `id`
290:   function getVaults(
         uint id
       ) 
         external 
         view 
         returns (address[] memory) {

/// @audit missing @param for `id`
/// @audit missing @param for `vault`
299:   function hasVault(
         uint    id,
         address vault
       ) 
         external 
         view 
         returns (bool) {

```
*Github:* [[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit missing @param for `_kerosine`
11:   constructor(
        Kerosine _kerosine
      ) {

```
*Github:* [[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11)]


</details>


<a name="NC-30"></a> 
### [NC-30] Missing NatSpec `@return` from function declaration
Some function definitions have an incomplete NatSpec: add a `@return` notation to improve the code documentation.

<details>
<summary>
There are <b>14</b> instances (click to show):
</summary>

```solidity
File: ./src/core/KerosineManager.sol

37:   function getVaults() 
        external 
        view 
        returns (address[] memory) {

44:   function isLicensed(
        address vault
      ) 
        external 
        view 
        returns (bool) {

```
*Github:* [[37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
        public 
        view 
        override
        returns (uint) {

```
*Github:* [[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

60:   function getUsdValue(
        uint id
      )
        public
        view 
        returns (uint) {

69:   function assetPrice() 

```
*Github:* [[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
        public 
        view 
        override
        returns (uint) {

```
*Github:* [[50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]


```solidity
File: ./src/core/VaultManagerV2.sol

184:   function redeemDyad(
         uint    id,
         address vault,
         uint    amount,
         address to
       )
         external 
           isDNftOwner(id)
         returns (uint) { 

230:   function collatRatio(
         uint id
       )
         public 
         view
         returns (uint) {

241:   function getTotalUsdValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

250:   function getNonKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

269:   function getKeroseneValue(
         uint id
       ) 
         public 
         view
         returns (uint) {

290:   function getVaults(
         uint id
       ) 
         external 
         view 
         returns (address[] memory) {

299:   function hasVault(
         uint    id,
         address vault
       ) 
         external 
         view 
         returns (bool) {

```
*Github:* [[184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299)]


```solidity
File: ./src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17)]


</details>


<a name="NC-31"></a> 
### [NC-31] Missing NatSpec `@title` from contract declaration
Some contract definitions have an incomplete NatSpec: add a `@title` notation to improve the code documentation.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="NC-32"></a> 
### [NC-32] There is no need to initialize variables with 0
Since the variables are automatically set to 0 when created, it is redundant to initialize it with 0 again.

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="NC-33"></a> 
### [NC-33] Put all system-wide constants in one file
Putting all the system-wide constants in a single file improves code readability, makes it easier to understand the basic configuration and limitations of the system, and makes maintenance easier.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14)]


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="NC-34"></a> 
### [NC-34] Setters should prevent re-setting the same value
Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

29:     unboundedKerosineVault = _unboundedKerosineVault;

```
*Github:* [[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

47:     kerosineDenominator = _kerosineDenominator;

```
*Github:* [[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

63:       keroseneManager = _keroseneManager;

```
*Github:* [[63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63)]



<a name="NC-35"></a> 
### [NC-35] State variables should include comments
Consider adding some comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="NC-36"></a> 
### [NC-36] Unnecessary cast
The variable is being cast to its own type.

<details>
<summary>
There are <b>27</b> instances (click to show):
</summary>

```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

```
*Github:* [[129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280)]


</details>


<a name="NC-37"></a> 
### [NC-37] Unused import
The identifier is imported but never used within the file.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `Dyad`
6: import {Dyad}                   from "./Dyad.sol";

```
*Github:* [[6](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L6)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `BoundedKerosineVault`
9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";

```
*Github:* [[9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L9)]



<a name="NC-38"></a> 
### [NC-38] Unused contract variables
The following state variables are defined but not used. It is recommended to check the code for logical omissions that cause them not to be used. If it's determined that they are not needed anywhere, it's best to remove them from the codebase to improve code clarity and minimize confusion.

*There is one instance of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="NC-39"></a> 
### [NC-39] Expressions for constant values should use `immutable` rather than `constant`
While it doesn't save any gas because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14)]


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="NC-40"></a> 
### [NC-40] Upgrade `openzeppelin` to the latest version (`5.0.2`)
These contracts import contracts from openzeppelin contracts but they are not using the latest version. For more information, please visit: [OpenZeppelin GitHub Releases](https://github.com/OpenZeppelin/openzeppelin-contracts/releases) It is recommended to always use the latest version to take advantage of updates and security fixes.

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="NC-41"></a> 
### [NC-41] Use the latest solidity version for deployment (`0.8.25`)
Upgrading to a newer Solidity release can optimize gas usage, take advantage of new features and improve overall contract efficiency. Where possible, based on compatibility requirements, it is recommended to use newer/latest solidity version to take advantage of the latest optimizations and features.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2)]


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2)]


```solidity
File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2)]



<a name="NC-42"></a> 
### [NC-42] Use the Modern Upgradeable Contract Paradigm
Modern smart contract development often employs upgradeable contract structures, utilizing proxy patterns like OpenZeppelin’s Upgradeable Contracts. This paradigm separates logic and state, allowing developers to amend and enhance the contract's functionality without altering its state or the deployed contract address. Transitioning to this approach enhances long-term maintainability.

Resolution: Adopt a well-established proxy pattern for upgradeability, ensuring proper initialization and employing transparent proxies to mitigate potential risks. Embrace comprehensive testing and audit practices, particularly when updating contract logic, to ensure state consistency and security are preserved across upgrades. This ensures your contract remains robust and adaptable to future requirements.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="NC-43"></a> 
### [NC-43] Consider using modifiers for address control
Modifiers in Solidity can improve code readability and modularity by encapsulating repetitive checks, such as address validity checks, into a reusable construct. For example, an `onlyOwner` modifier can be used to replace repetitive `require(msg.sender == owner)` checks across several functions, reducing code redundancy and enhancing maintainability. To implement, define a modifier with the check, then apply the modifier to relevant functions.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L22)]


```solidity
File: ./src/core/VaultManagerV2.sol

40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40)]



<a name="NC-44"></a> 
### [NC-44] Use of `override` is unnecessary
Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

47:     override

```
*Github:* [[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L47)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

53:     override

```
*Github:* [[53](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L53)]



<a name="NC-45"></a> 
### [NC-45] Empty body - Consider commenting why

*There is one instance of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```
*Github:* [[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L21)]



<a name="NC-46"></a> 
### [NC-46] Names of `private`/`internal` state variables should be prefixed with an underscore
It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;

```
*Github:* [[16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L16)]


```solidity
File: ./src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

```
*Github:* [[34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L35)]



<a name="NC-47"></a> 
### [NC-47] Functions not used internally could be marked `external`

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 

```
*Github:* [[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44)]


```solidity
File: ./src/core/Vault.kerosine.sol

36:   function deposit(

60:   function getUsdValue(

```
*Github:* [[36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 

```
*Github:* [[50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50)]



<a name="NC-48"></a> 
### [NC-48] Don't only depend on Solidity's arithmetic ordering
Relying on Solidity's default arithmetic operator precedence can lead to misunderstood or overlooked nuances in code execution. Misinterpretation risks can be significant, especially when different developers or auditors review the code. To ensure clarity and minimize potential errors, it's recommended to use parentheses. These not only override the default precedence when needed but also emphasize the intended order of operations. By deliberately showing the intended calculation sequence using parentheses, developers make the code's logic explicit, reducing the risk of unintended behaviors and making the codebase more maintainable and understandable for all stakeholders.

*There is one instance of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

67:       return numerator * 1e8 / denominator;

```
*Github:* [[67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67)]



<a name="NC-49"></a> 
### [NC-49] Incorrect comparison against a max value
Comparing a value using `>= MAX_VALUE` is conceptually incorrect when `MAX_VALUE` is defined as the upper limit that a variable can take. According to the definition of a maximum value, the condition should only revert if the variable is greater than `MAX_VALUE`, not equal to it. Using `>=` can introduce unintended behavior, as the condition will trigger a revert even when the variable reaches its legitimate upper bound. This can lead to bugs and vulnerabilities, as well as hamper the contract's intended functionality. The resolution is to strictly use `>` when making comparisons against a defined `MAX_VALUE` to align with its conceptual definition and to prevent unintended reverts or vulnerabilities.

*There are <b>3</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();

```
*Github:* [[24](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L24)]


```solidity
File: ./src/core/VaultManagerV2.sol

74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

```
*Github:* [[74](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L74), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87)]




## Gas Optimizations

<a name="GAS-1"></a> 
### [GAS-1] Optimize gas by using do-while loops
Using `do-while` loops instead of `for` loops can be more gas-efficient. Even if you add an `if` condition to account for the case where the loop doesn't execute at all, a `do-while` loop can still be cheaper in terms of gas.

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-2"></a> 
### [GAS-2] Consider activating via-ir for deploying
By using `--via-ir` or `{"viaIR": true}`, the compiler is able to use more advanced [multi-function optimizations](https://docs.soliditylang.org/en/v0.8.17/ir-breaking-changes.html#solidity-ir-based-codegen-changes), for extra gas savings.

*There is one instance of this issue:*
```solidity

Global finding

```
*Github:* [[Global](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/)]



<a name="GAS-3"></a> 
### [GAS-3] Counting down in for statements is more gas efficient
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-4"></a> 
### [GAS-4] Divisions can be `unchecked` to save gas
The expression `type(int).min/(-1)` is the only case where division causes an overflow. Therefore, uncheck can be used to [save gas](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f) in scenarios where it is certain that such an overflow will not occur.

*There are <b>8</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;

```
*Github:* [[66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L66)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

62:                 / (10**vault.asset().decimals()) 

63:                 / (10**vault.oracle().decimals());

67:       return numerator * 1e8 / denominator;

```
*Github:* [[62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67)]


```solidity
File: ./src/core/VaultManagerV2.sol

148:                   / 10**_vault.oracle().decimals() 

149:                   / 10**_vault.asset().decimals();

197:                     / _vault.assetPrice() 

198:                     / 1e18;

```
*Github:* [[148](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L149), [197](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L197), [198](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L198)]



<a name="GAS-5"></a> 
### [GAS-5] Increments can be `unchecked` to save gas
Using `unchecked` increments can save gas by bypassing the built-in overflow checks. This can save 30-40 gas per iteration. So it is recommended to use unchecked increments when overflow is not possible.

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-6"></a> 
### [GAS-6] Multiple accesses of the same mapping/array key/index should be cached
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `vaults[id]` is also accessed on line 74
76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();

/// @audit `vaultsKerosene[id]` is also accessed on line 87
89:     if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

/// @audit `vaults[id]` is also accessed on line 221
223:           Vault vault      = Vault(vaults[id].at(i));

/// @audit `vaults[id]` is also accessed on line 257
259:         Vault vault = Vault(vaults[id].at(i));

/// @audit `vaultsKerosene[id]` is also accessed on line 276
278:         Vault vault = Vault(vaultsKerosene[id].at(i));

```
*Github:* [[76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76), [89](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L89), [223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223), [259](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L259), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278)]



<a name="GAS-7"></a> 
### [GAS-7] Operator `>=`/`<=` costs less gas than operator `>`/`<`
The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behavior applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`. It can save 3 gas for each. It should be converted to the `<=`/`>=` equivalent when comparing against integer literals.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[150](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L150), [217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217), [222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-8"></a> 
### [GAS-8] Optimize names to save gas
`public`/`external` function names and `public` member variable names can be optimized to save gas. See this [link](https://gist.github.com/IllIllI000/a5d8b486a8259f9f77891a919febd1a9) for an example of how it works. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92)

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

/// @audit `add`, `remove`, `getVaults`, `isLicensed`
7: contract KerosineManager is Owned(msg.sender) {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

/// @audit `setUnboundedKerosineVault`, `withdraw`, `assetPrice`
12: contract BoundedKerosineVault is KerosineVault {

```
*Github:* [[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `withdraw`, `setDenominator`, `assetPrice`
15: contract UnboundedKerosineVault is KerosineVault {

```
*Github:* [[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `setKeroseneManager`, `add`, `addKerosene`, `remove`, `removeKerosene`, `deposit`, `withdraw`, `mintDyad`, `burnDyad`, `redeemDyad`, `liquidate`, `collatRatio`, `getTotalUsdValue`, `getNonKeroseneValue`, `getKeroseneValue`, `getVaults`, `hasVault`
17: contract VaultManagerV2 is IVaultManager, Initializable {

```
*Github:* [[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17)]


```solidity
File: ./src/staking/KerosineDenominator.sol

/// @audit `denominator`
7: contract KerosineDenominator is Parameters {

```
*Github:* [[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7)]



<a name="GAS-9"></a> 
### [GAS-9] Reduce gas usage by moving to Solidity 0.8.19 or later
Solidity version 0.8.19 introduced a number of gas optimizations, refer to the [Solidity 0.8.19 Release Announcement](https://soliditylang.org/blog/2023/02/22/solidity-0.8.19-release-announcement/) for details.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2)]


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2)]


```solidity
File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2)]



<a name="GAS-10"></a> 
### [GAS-10] Remove or replace unused state variables
Saves a storage slot. If the variable is assigned a non-zero value, saves Gsset (20000 gas). If it's assigned a zero value, saves Gsreset (2900 gas). If the variable remains unassigned, there is no gas savings unless the variable is `public`, in which case the compiler-generated non-payable getter deployment cost is saved. If the state variable is overriding an interface's public function, mark the variable as `constant` or `immutable` so that it does not use a storage slot.

*There is one instance of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="GAS-11"></a> 
### [GAS-11] State variables access within a loop
State variable reads and writes are more expensive than local variable reads and writes. Therefore, it is recommended to replace state variable reads and writes within loops with a local variable. Gas savings should be multiplied by the average loop length.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `vaultLicenser`
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit `keroseneManager`
280:         if (keroseneManager.isLicensed(address(vault))) {

```
*Github:* [[261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280)]



<a name="GAS-12"></a> 
### [GAS-12] State variables only set in the constructor should be declared immutable
Accessing state variables within a function involves an `SLOAD` operation, but `immutable` variables can be accessed directly without the need of it, thus reducing gas costs. As these state variables are assigned only in the constructor, consider declaring them `immutable`.

*There is one instance of this issue:*
```solidity
File: ./src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;

```
*Github:* [[9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L9)]



<a name="GAS-13"></a> 
### [GAS-13] Optimize external calls with assembly for memory efficiency
Using interfaces to make external contract calls in Solidity is convenient but can be inefficient in terms of memory utilization. Each such call involves creating a new memory location to store the data being passed, thus incurring memory expansion costs.

Inline assembly allows for optimized memory usage by re-using already allocated memory spaces or using the scratch space for smaller datasets. This can result in notable gas savings, especially for contracts that make frequent external calls.

Additionally, using inline assembly enables important safety checks like verifying if the target address has code deployed to it using `extcodesize(addr)` before making the call, mitigating risks associated with contract interactions.

<details>
<summary>
There are <b>18</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

/// @audit `.safeTransfer(...)`
39:     asset.safeTransfer(to, amount); 

/// @audit `.assetPrice(...)`
61:                 * vault.assetPrice() * 1e18

/// @audit `.asset(...)`
62:                 / (10**vault.asset().decimals()) 

/// @audit `.oracle(...)`
63:                 / (10**vault.oracle().decimals());

```
*Github:* [[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L39), [61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L61), [62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63)]


```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit `.asset(...)`
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit `.deposit(...)`
130:     _vault.deposit(id, amount);

/// @audit `.oracle(...)`
148:                   / 10**_vault.oracle().decimals() 

/// @audit `.asset(...)`
149:                   / 10**_vault.asset().decimals();

/// @audit `.withdraw(...)`
151:     _vault.withdraw(id, to, amount);

/// @audit `.mint(...)`
166:     dyad.mint(id, to, amount);

/// @audit `.burn(...)`
179:     dyad.burn(id, msg.sender, amount);

/// @audit `.burn(...)`
193:       dyad.burn(id, msg.sender, amount);

/// @audit `.oracle(...)`
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 

/// @audit `.asset(...)`
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 

/// @audit `.assetPrice(...)`
197:                     / _vault.assetPrice() 

/// @audit `.mintedDyad(...)`
215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

/// @audit `.burn(...)`
215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

/// @audit `.move(...)`
225:           vault.move(id, to, collateral);

```
*Github:* [[129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [130](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L130), [148](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L149), [151](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L151), [166](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L166), [179](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L179), [193](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L193), [196](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L196), [196](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L196), [197](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L197), [215](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L215), [215](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L215), [225](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L225)]


</details>


<a name="GAS-14"></a> 
### [GAS-14] Use assembly to emit events
To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

<details>
<summary>
There are <b>11</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);

```
*Github:* [[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L57)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40)]


```solidity
File: ./src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

180:     emit BurnDyad(id, amount, msg.sender);

200:       emit RedeemDyad(id, vault, amount, to);

227:       emit Liquidate(id, msg.sender, to);

```
*Github:* [[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L227)]


</details>


<a name="GAS-15"></a> 
### [GAS-15] Use assembly to validate `msg.sender`

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L22)]


```solidity
File: ./src/core/VaultManagerV2.sol

40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

```
*Github:* [[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40)]



<a name="GAS-16"></a> 
### [GAS-16] Use assembly to write address/contract type storage values
Using `assembly { sstore(state.slot, addr)` instead of `state = addr` can save gas.

<details>
<summary>
There are <b>11</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.bounded.sol

29:     unboundedKerosineVault = _unboundedKerosineVault;

```
*Github:* [[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29)]


```solidity
File: ./src/core/Vault.kerosine.sol

31:     vaultManager    = _vaultManager;

32:     asset           = _asset;

33:     kerosineManager = _kerosineManager;

```
*Github:* [[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

27:       dyad = _dyad;

47:     kerosineDenominator = _kerosineDenominator;

```
*Github:* [[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

54:     dNft          = _dNft;

55:     dyad          = _dyad;

56:     vaultLicenser = _licenser;

63:       keroseneManager = _keroseneManager;

```
*Github:* [[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63)]


```solidity
File: ./src/staking/KerosineDenominator.sol

14:     kerosine = _kerosine;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14)]


</details>


<a name="GAS-17"></a> 
### [GAS-17] Use a more recent version of solidity
- Use a solidity version of at least 0.8.2 to get simple compiler automatic inlining.
- Use a solidity version of at least 0.8.3 to get better struct packing and cheaper multiple storage reads.
- Use a solidity version of at least 0.8.4 to get custom errors, which are cheaper at deployment than revert()/require() strings.
- Use a solidity version of at least 0.8.10 to have external calls skip contract existence checks if the external call has a return value.

*There are <b>6</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2)]


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2)]


```solidity
File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;

```
*Github:* [[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2)]



<a name="GAS-18"></a> 
### [GAS-18] Use != 0 instead of > 0
Replace spotted instances with != 0 for uints as this uses less gas.

*There are <b>2</b> instances of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

```
*Github:* [[101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101), [113](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L113)]



<a name="GAS-19"></a> 
### [GAS-19] Consider Using Solady's Gas Optimized Lib for Math
In instances where many similar mathematical operations are performed, consider using Solday's math lib to benefit from the gas saving it can introduce.

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;

```
*Github:* [[66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L66)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

60:         tvl += vault.asset().balanceOf(address(vault)) 

67:       return numerator * 1e8 / denominator;

```
*Github:* [[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67)]


```solidity
File: ./src/core/VaultManagerV2.sol

146:     uint value = amount * _vault.assetPrice() 

195:       uint asset = amount 

```
*Github:* [[146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146), [195](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L195)]



<a name="GAS-20"></a> 
### [GAS-20] Don't initialize variables with default value

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-21"></a> 
### [GAS-21] `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too)
*Saves 5 gas per loop*

*There are <b>4</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58)]


```solidity
File: ./src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```
*Github:* [[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277)]



<a name="GAS-22"></a> 
### [GAS-22] Using `private` rather than `public` for constants, saves gas
If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table

*There are <b>5</b> instances of this issue:*
```solidity
File: ./src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14)]


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```
*Github:* [[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26)]



<a name="GAS-23"></a> 
### [GAS-23] Use assembly to check for `address(0)`
Saves 6 gas per instance.

*There is one instance of this issue:*
```solidity
File: ./src/core/VaultManagerV2.sol

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

```
*Github:* [[43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43)]



<a name="GAS-24"></a> 
### [GAS-24] Avoid updating storage when the value hasn't changed
In Ethereum, updating storage is costly in terms of gas. Therefore, it's beneficial to avoid redundant updates, particularly when the value being written is identical to the existing one. A comparison check before updating can prevent unnecessary operations, thus saving gas. The resolution could involve implementing a conditional check in your function to verify if the new value differs from the current one. If it's the same, the function could simply return without proceeding to the costly storage update. This simple adjustment in your code can lead to significant gas savings in scenarios where redundant updates might occur frequently.

<details>
<summary>
There are <b>16</b> instances (click to show):
</summary>

```solidity
File: ./src/core/Vault.kerosine.bounded.sol

29:     unboundedKerosineVault = _unboundedKerosineVault;

```
*Github:* [[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29)]


```solidity
File: ./src/core/Vault.kerosine.sol

31:     vaultManager    = _vaultManager;

32:     asset           = _asset;

33:     kerosineManager = _kerosineManager;

43:     id2asset[id] += amount;

55:     id2asset[from] -= amount;

56:     id2asset[to]   += amount;

```
*Github:* [[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L43), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L56)]


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

27:       dyad = _dyad;

38:     id2asset[id] -= amount;

47:     kerosineDenominator = _kerosineDenominator;

```
*Github:* [[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27), [38](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L38), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47)]


```solidity
File: ./src/core/VaultManagerV2.sol

54:     dNft          = _dNft;

55:     dyad          = _dyad;

56:     vaultLicenser = _licenser;

63:       keroseneManager = _keroseneManager;

127:     idToBlockOfLastDeposit[id] = block.number;

```
*Github:* [[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63), [127](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L127)]


```solidity
File: ./src/staking/KerosineDenominator.sol

14:     kerosine = _kerosine;

```
*Github:* [[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14)]


</details>


<a name="GAS-25"></a> 
### [GAS-25] Unnecessary casting as variable is already of the same type
Unnecessary casting of a variable to the same type is redundant and can contribute to gas inefficiency and code clutter. This situation commonly arises when developers, perhaps due to oversight or misunderstanding, explicitly cast a variable to its existing type. For example, casting a uint256 variable to uint256 again does not change its type or value but adds unnecessary operations to the code.

Resolution: Developers should scrutinize their code to identify and remove any unnecessary type casting. Utilizing linters or static analysis tools can aid in detecting such redundancies. Ensuring that the code is clean and efficient not only saves gas but also enhances readability and maintainability.

<details>
<summary>
There are <b>27</b> instances (click to show):
</summary>

```solidity
File: ./src/core/VaultManagerV2.sol

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
261:         if (vaultLicenser.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

/// @audit no need to cast `vault` into address
280:         if (keroseneManager.isLicensed(address(vault))) {

```
*Github:* [[129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [129](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L129), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280)]


</details>


<a name="GAS-26"></a> 
### [GAS-26] Variable declared within iteration

*There are <b>7</b> instances of this issue:*
```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

59:         Vault vault = Vault(vaults[i]);

```
*Github:* [[59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L59)]


```solidity
File: ./src/core/VaultManagerV2.sol

223:           Vault vault      = Vault(vaults[id].at(i));

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

259:         Vault vault = Vault(vaults[id].at(i));

260:         uint usdValue;

278:         Vault vault = Vault(vaultsKerosene[id].at(i));

279:         uint usdValue;

```
*Github:* [[223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223), [224](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L224), [259](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L259), [260](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L260), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278), [279](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L279)]



