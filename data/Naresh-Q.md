This report includes additional instances of an issue listed in the automated findings report

## Summary

| |Issue|Instances| Gas Savings
|-|:-|:-:|:-:|
| [[M-01](#m-01)] | Large transfers may not work with some `ERC20` tokens | 1| 0|
| [[M-02](#m-02)] | Some `ERC20` can revert on a zero value `transfer` | 2| 0|
| [[L-01](#l-01)] | `decimals()` not part of ERC20 standard | 5| 0|
| [[L-02](#l-02)] | Events may be emitted out of order due to reentrancy | 5| 0|
| [[L-03](#l-03)] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 4| 0|
| [[L-04](#l-04)] | Missing zero address check in constructor | 5| 0|
| [[N-01](#n-01)] | Consider adding validation of user inputs | 17| 0|
| [[N-02](#n-02)] | Contracts should have all `public`/`external` functions exposed by `interface`s | 6| 0|
| [[N-03](#n-03)] | Contracts should have full test coverage | 6| 0|
| [[N-04](#n-04)] | Control structures do not follow the Solidity Style Guide | 24| 0|
| [[N-05](#n-05)] | Constants in comparisons should appear on the left side | 9| 0|
| [[N-06](#n-06)] | Critical Changes Should Use Two-step Procedure | 3| 0|
| [[N-07](#n-07)] | Division by zero not prevented | 4| 0|
| [[N-08](#n-08)] | Consider adding emergency-stop functionality | 6| 0|
| [[N-09](#n-09)] | Consider emitting an event at the end of the constructor | 4| 0|
| [[N-10](#n-10)] | Empty constructor body | 1| 0|
| [[N-11](#n-11)] | Events are missing sender information | 9| 0|
| [[N-12](#n-12)] | For loops in public or external functions should be avoided due to high gas costs and possible DOS | 4| 0|
| [[N-13](#n-13)] | Consider adding formal verification proofs | 6| 0|
| [[N-14](#n-14)] | No equate comparison checks between to and from address parameters | 1| 0|
| [[N-15](#n-15)] | Functions within contracts are not ordered according to the solidity style guide | 6| 0|
| [[N-16](#n-16)] | Functions should not be longer than 50 lines | 3| 0|
| [[N-17](#n-17)] | Governance operations should be behind a timelock | 8| 0|
| [[N-18](#n-18)] | Use a ternary statement instead of `if`/`else` when appropriate | 26| 0|
| [[N-19](#n-19)] | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES | 7| 0|
| [[N-20](#n-20)] | Inconsistent comment spacing | 6| 0|
| [[N-21](#n-21)] | Interface imports should be declared first | 6| 0|
| [[N-22](#n-22)] | Lack Of Brace Spacing | 36| 0|
| [[N-23](#n-23)] | It is best practice to use linear inheritance | 6| 0|
| [[N-24](#n-24)] | `constant`s should be defined rather than using magic numbers | 3| 0|
| [[N-25](#n-25)] | `mapping` definitions do not follow the Solidity Style Guide | 3| 0|
| [[N-26](#n-26)] | `type(uint<n>).max` should be used instead of `uint<n>(-1)` | 1| 0|
| [[N-27](#n-27)] | Consider checking that transfer to `address(this)` is disabled | 1| 0|
| [[N-28](#n-28)] | Custom errors has no error details | 3| 0|
| [[N-29](#n-29)] | Missing events in sensitive functions | 3| 0|
| [[N-30](#n-30)] | Use a struct to encapsulate multiple function parameters | 3| 0|
| [[N-31](#n-31)] | Consider using named mappings | 4| 0|
| [[N-32](#n-32)] | Missing `@inheritdoc` on override functions | 2| 0|
| [[N-33](#n-33)] | Natspec `@author` is missing from abstract contract | 1| 0|
| [[N-34](#n-34)] | Natspec `@dev` is missing from abstract contract | 1| 0|
| [[N-35](#n-35)] | Natspec `@notice` is missing from abstract contract | 1| 0|
| [[N-36](#n-36)] | Natspec `@title` is missing from abstract contract | 1| 0|
| [[N-37](#n-37)] | NatSpec: Contract declarations should have `@author` tags | 5| 0|
| [[N-38](#n-38)] | NatSpec: Contract declarations should have `@dev` tags | 5| 0|
| [[N-39](#n-39)] | NatSpec: Contract declarations should have `@notice` tags | 5| 0|
| [[N-40](#n-40)] | NatSpec: Contract declarations should have `@title` tags | 5| 0|
| [[N-41](#n-41)] | NatSpec: Constructor missing NatSpec `@dev` tag | 5| 0|
| [[N-42](#n-42)] | NatSpec: Constructor missing NatSpec `@notice` tag | 5| 0|
| [[N-43](#n-43)] | NatSpec: Constructor missing NatSpec `@param` tag | 5| 0|
| [[N-44](#n-44)] | NatSpec: Error missing NatSpec `@dev` tag | 4| 0|
| [[N-45](#n-45)] | NatSpec: Error missing NatSpec `@param` tag | 1| 0|
| [[N-46](#n-46)] | NatSpec: Functions missing NatSpec `@dev` tag | 31| 0|
| [[N-47](#n-47)] | NatSpec: Functions missing NatSpec `@notice` tag | 31| 0|
| [[N-48](#n-48)] | NatSpec: Functions missing NatSpec `@param` tag | 27| 0|
| [[N-49](#n-49)] | NatSpec: Functions missing NatSpec `@return` tag | 13| 0|
| [[N-50](#n-50)] | NatSpec: Modifier missing NatSpec `@dev` tag | 4| 0|
| [[N-51](#n-51)] | NatSpec: Modifier missing NatSpec `@notice` tag | 4| 0|
| [[N-52](#n-52)] | NatSpec: Modifier missing NatSpec `@param` tag | 3| 0|
| [[N-53](#n-53)] | Use recent version of solidity | 6| 0|
| [[N-54](#n-54)] | Use of `override` is unnecessary | 2| 0|
| [[N-55](#n-55)] | Consider making `private` state variables `internal` to increase flexibility | 1| 0|
| [[N-56](#n-56)] | `private` and `internal` state variables should have a preceding _ in their name unless they are `constant`/`immutable` | 1| 0|
| [[N-57](#n-57)] | Public variable declarations should have NatSpec descriptions | 18| 0|
| [[N-58](#n-58)] | Take advantage of Custom Error's return value property | 23| 0|
| [[N-59](#n-59)] | Setters should prevent re-setting the same value | 3| 0|
| [[N-60](#n-60)] | Use a single file for system wide constants | 5| 0|
| [[N-61](#n-61)] | Consider using SMTChecker | 6| 0|
| [[N-62](#n-62)] | Contract does not follow the Solidity style guide's suggested layout ordering | 5| 0|
| [[N-63](#n-63)] | Change `uint` to `uint256` | 81| 0|
| [[N-64](#n-64)] | Use the Modern Upgradeable Contract Paradigm | 6| 0|
| [[N-65](#n-65)] | Upgrade openzeppelin to the Latest Version - 5.0.0 | 3| 0|
| [[N-66](#n-66)] | Consider using named returns | 14| 0|
| [[N-67](#n-67)] | Consider using a format prettier or forge fmt | 6| 0|
| [[N-68](#n-68)] | Variable/Parameters names don't follow the Solidity naming convention | 101| 0|
| [[N-69](#n-69)] | Incorrect withdraw declaration | 3| 0|
| [[N-70](#n-70)] | Invalid NatSpec comment style | 1| 0|

### Medium Risk Issues

### [M-01]<a name="m-01"></a> Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued transferred is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20#revert-on-large-approvals--transfers)

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

39:     asset.safeTransfer(to, amount); 

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L39-L39)

### [M-02]<a name="m-02"></a> Some `ERC20` can revert on a zero value `transfer`

In spite of the fact that [EIP-20](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) states that zero-valued transfers must be accepted, some tokens, such as `LEND` will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

39:     asset.safeTransfer(to, amount); 

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L39-L39)

```solidity
📁 File: src/core/VaultManagerV2.sol

129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

```


*GitHub* : [129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L129-L129)

### Low Risk Issues

### [L-01]<a name="l-01"></a> `decimals()` not part of ERC20 standard

`decimals()` is not part of the official ERC20 standard and might fail for tokens that do not implement it. While in practice it is very unlikely, as usually most of the tokens implement it, this should still be considered as a potential issue.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

62:                 / (10**vault.asset().decimals()) 

63:                 / (10**vault.oracle().decimals());

```


*GitHub* : [62](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L62-L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L63-L63)

```solidity
📁 File: src/core/VaultManagerV2.sol

148:                   / 10**_vault.oracle().decimals() 

149:                   / 10**_vault.asset().decimals();

196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 

```


*GitHub* : [148](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L148-L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L149-L149), [196](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L196-L196)

### [L-02]<a name="l-02"></a> Events may be emitted out of order due to reentrancy

If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events are emitted before external calls and follow the best practice of CEI.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);

```


*GitHub* : [40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L40-L40)

```solidity
📁 File: src/core/VaultManagerV2.sol

168:     emit MintDyad(id, amount, to);

180:     emit BurnDyad(id, amount, msg.sender);

200:       emit RedeemDyad(id, vault, amount, to);

227:       emit Liquidate(id, msg.sender, to);

```


*GitHub* : [168](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L168-L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L180-L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L200-L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L227-L227)

### [L-03]<a name="l-03"></a> Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

// @audit function 'withdraw()' is missing Reentrancy guard
39:     asset.safeTransfer(to, amount); 

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L39-L39)

```solidity
📁 File: src/core/VaultManagerV2.sol

// @audit function 'deposit()' is missing Reentrancy guard
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

// @audit function 'withdraw()' is missing Reentrancy guard
151:     _vault.withdraw(id, to, amount);

// @audit function 'redeemDyad()' is missing Reentrancy guard
199:       withdraw(id, vault, asset, to);

```


*GitHub* : [129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L129-L129), [151](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L151-L151), [199](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L199-L199)

### [L-04]<a name="l-04"></a> Missing zero address check in constructor

Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address `(0x0)`. This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

// @audit missing checks for -->  _vaultManager, _asset, _kerosineManager
17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
📁 File: src/core/Vault.kerosine.sol

// @audit missing checks for -->  _vaultManager, _asset, _kerosineManager
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {

```


*GitHub* : [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

// @audit missing checks for -->  _vaultManager, _asset, _dyad, _kerosineManager
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L26)

```solidity
📁 File: src/core/VaultManagerV2.sol

// @audit missing checks for -->  _dNft, _dyad, _licenser
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49-L53)

```solidity
📁 File: src/staking/KerosineDenominator.sol

// @audit missing checks for -->  _kerosine
11:   constructor(
12:     Kerosine _kerosine
13:   ) {

```


*GitHub* : [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11-L13)

### NonCritical Risk Issues

### [N-01]<a name="n-01"></a> Consider adding validation of user inputs

There are no validations done on the arguments below. Consider that the Solidity [documentation](https://docs.soliditylang.org/en/latest/control-structures.html#panic-via-assert-and-error-via-require) states that `Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix`. This means that there should be explicit checks for expected ranges of inputs. Underflows/overflows result in panics should not be used as range checks, and allowing funds to be sent to `0x0`, which is the default value of address variables and has many gotchas, should be avoided.

*There are 17 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

// @audit missing checks for -->  vault
18:   function add(
19:     address vault
20:   ) 
21:     external 
22:       onlyOwner
23:   {

// @audit missing checks for -->  vault
28:   function remove(
29:     address vault
30:   ) 
31:     external 
32:       onlyOwner
33:   {

// @audit missing checks for -->  vault
44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) {

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28-L33), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

// @audit missing checks for -->  _unboundedKerosineVault
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

// @audit missing checks for -->  to
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


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

// @audit missing checks for -->  to
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {

// @audit missing checks for -->  _kerosineDenominator
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {

```


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46)

```solidity
📁 File: src/core/VaultManagerV2.sol

// @audit missing checks for -->  _keroseneManager
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {

// @audit missing checks for -->  vault
67:   function add(
68:       uint    id,
69:       address vault
70:   ) 
71:     external
72:       isDNftOwner(id)
73:   {

// @audit missing checks for -->  vault
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   ) 
84:     external
85:       isDNftOwner(id)
86:   {

// @audit missing checks for -->  vault
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 
98:     external
99:       isDNftOwner(id)
100:   {

// @audit missing checks for -->  vault
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 
110:     external
111:       isDNftOwner(id)
112:   {

// @audit missing checks for -->  vault
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   {

// @audit missing checks for -->  vault, to
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {

// @audit missing checks for -->  to
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   {

// @audit missing checks for -->  vault, to
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 

// @audit missing checks for -->  vault
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   ) 
303:     external 
304:     view 
305:     returns (bool) {

```


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L163), [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

### [N-02]<a name="n-02"></a> Contracts should have all `public`/`external` functions exposed by `interface`s

The `contract`s should expose an `interface` so that other projects can more easily integrate with it, without having to develop their own non-standard variants.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

// @audit  add(), remove(), getVaults(), isLicensed()
7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

// @audit  setUnboundedKerosineVault(), withdraw(), assetPrice()
12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

// @audit  deposit(), move(), getUsdValue(), assetPrice()
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

// @audit  withdraw(), setDenominator(), assetPrice()
15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

// @audit  setKeroseneManager(), add(), addKerosene(), remove(), removeKerosene(), deposit(), withdraw(), mintDyad(), burnDyad(), redeemDyad(), liquidate(), collatRatio(), getTotalUsdValue(), getNonKeroseneValue(), getKeroseneValue(), getVaults(), hasVault()
17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

// @audit  denominator()
7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-03]<a name="n-03"></a> Contracts should have full test coverage

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-04]<a name="n-04"></a> Control structures do not follow the Solidity Style Guide

See the [control structures](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) section of the Solidity Style Guide

*There are 24 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();

25:     if (!vaults.add(vault))            revert VaultAlreadyAdded();

34:     if (!vaults.remove(vault)) revert VaultNotFound();

```


*GitHub* : [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L25-L25), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L34-L34)

```solidity
📁 File: src/core/Vault.kerosine.sol

22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L22-L22)

```solidity
📁 File: src/core/VaultManagerV2.sol

40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;

74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();

76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();

87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

88:     if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();

89:     if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

114:     if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();

143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

237:       if (_dyad == 0) return type(uint).max;

```


*GitHub* : [40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L46-L46), [74](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L114-L114), [143](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L143-L143), [150](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L214-L214), [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L237-L237)

### [N-05]<a name="n-05"></a> Constants in comparisons should appear on the left side

Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html) where the first `!`, `>`, `<`, or `=` at the beginning of the operator is missing.

*There are 9 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();

```


*GitHub* : [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24-L24)

```solidity
📁 File: src/core/VaultManagerV2.sol

74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

237:       if (_dyad == 0) return type(uint).max;

```


*GitHub* : [74](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74-L74), [87](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L87-L87), [101](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L101-L101), [113](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L113-L113), [152](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L152-L152), [167](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L214-L214), [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L237-L237)

### [N-06]<a name="n-06"></a> Critical Changes Should Use Two-step Procedure

The critical procedures should be two step process.

See similar findings in previous Code4rena contests for reference: <https://code4rena.com/reports/2022-06-illuminate/#2-critical-changes-should-use-two-step-procedure>

**Recommended Mitigation Steps**

Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }

```


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }

```


*GitHub* : [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L48)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }

```


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L64)

### [N-07]<a name="n-07"></a> Division by zero not prevented

The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

62:                 / (10**vault.asset().decimals()) 

63:                 / (10**vault.oracle().decimals());

67:       return numerator * 1e8 / denominator;

```


*GitHub* : [62](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L62-L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L63-L63), [67](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L67-L67)

```solidity
📁 File: src/core/VaultManagerV2.sol

197:                     / _vault.assetPrice() 

```


*GitHub* : [197](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L197-L197)

### [N-08]<a name="n-08"></a> Consider adding emergency-stop functionality

Adding a way to quickly halt protocol functionality in an emergency, rather than having to pause individual contracts one-by-one, will make in-progress hack mitigation faster and much less stressful.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-09]<a name="n-09"></a> Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
31:     vaultManager    = _vaultManager;
32:     asset           = _asset;
33:     kerosineManager = _kerosineManager;
34:   }

```


*GitHub* : [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26-L34)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27:       dyad = _dyad;
28:   }

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L28)

```solidity
📁 File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
54:     dNft          = _dNft;
55:     dyad          = _dyad;
56:     vaultLicenser = _licenser;
57:   }

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49-L57)

```solidity
📁 File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }

```


*GitHub* : [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11-L15)

### [N-10]<a name="n-10"></a> Empty constructor body

A void constructor in Solidity refers to a constructor that has no logic or code within it. It can be redundant and should be avoided because it unnecessarily increases the contract's bytecode, leading to higher deployment and gas costs. In a contract, a constructor is often used to initialize state variables or set specific conditions at the time of deployment. If no such initialization or conditions are required, the empty or void constructor serves no functional purpose. The resolution is simply to omit the constructor if it is not needed, thereby optimizing the contract for efficiency and readability.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L17-L21)

### [N-11]<a name="n-11"></a> Events are missing sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

*There are 9 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);

```


*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L44-L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L57-L57)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);

```


*GitHub* : [40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L40-L40)

```solidity
📁 File: src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

200:       emit RedeemDyad(id, vault, amount, to);

```


*GitHub* : [77](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L77-L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L90-L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L103-L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L115-L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L168-L168), [200](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L200-L200)

### [N-12]<a name="n-12"></a> For loops in public or external functions should be avoided due to high gas costs and possible DOS

For loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
64:       }

```


*GitHub* : [58](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L58-L64)

```solidity
📁 File: src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {
223:           Vault vault      = Vault(vaults[id].at(i));
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225:           vault.move(id, to, collateral);
226:       }

258:       for (uint i = 0; i < numberOfVaults; i++) {
259:         Vault vault = Vault(vaults[id].at(i));
260:         uint usdValue;
261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }
264:         totalUsdValue += usdValue;
265:       }

277:       for (uint i = 0; i < numberOfVaults; i++) {
278:         Vault vault = Vault(vaultsKerosene[id].at(i));
279:         uint usdValue;
280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }
283:         totalUsdValue += usdValue;
284:       }

```


*GitHub* : [222](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L222-L226), [258](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L258-L265), [277](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L277-L284)

### [N-13]<a name="n-13"></a> Consider adding formal verification proofs

Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-14]<a name="n-14"></a> No equate comparison checks between to and from address parameters

The function lacks a standard check: it does not validate if the 'to' and 'from' addresses are identical. This omission can lead to unintended outcomes if the same address is used in both parameters. To rectify this, we recommend implementing a comparison check at the beginning of the function. In the context of Solidity, the command `require(to != from, 'To and From addresses can't be the same');` could be utilized. This addition will generate an error if the 'to' and 'from' addresses are the same, thereby fortifying the function's robustness and security.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

// @audit missing checks for -> from != to
47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {

```


*GitHub* : [47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L54)

### [N-15]<a name="n-15"></a> Functions within contracts are not ordered according to the solidity style guide

Order of Functions; ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier. But there are contracts in the project that do not comply with this.

<https://docs.soliditylang.org/en/v0.8.17/style-guide.html>

Functions should be grouped according to their visibility and ordered:

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private
- within a grouping, place the view and pure functions last

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-16]<a name="n-16"></a> Functions should not be longer than 50 lines

Overly complex code can make understanding functionality more difficult, try to further modularize your code to ensure readability 

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

```


*GitHub* : [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L43)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

```


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L59)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-17]<a name="n-17"></a> Governance operations should be behind a timelock

All critical and governance operations should be protected by a timelock. For example from the point of view of a user, the changing of the owner of a contract is a high risk operation that may have outcomes ranging from an attacker gaining control over the protocol, to the function no longer functioning due to a typo in the destination address. To give users plenty of warning so that they can validate any ownership changes, changes of ownership should be behind a timelock.

*There are 8 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28-L33)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

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


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40)

```solidity
📁 File: src/core/Vault.kerosine.sol

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

```


*GitHub* : [36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L54)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

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


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46)

### [N-18]<a name="n-18"></a> Use a ternary statement instead of `if`/`else` when appropriate

The `if`/`else` statement can be written in a shorthand way using the ternary operator, as it increases readability and reduces the number of lines of code.

*There are 26 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();

25:     if (!vaults.add(vault))            revert VaultAlreadyAdded();

34:     if (!vaults.remove(vault)) revert VaultNotFound();

```


*GitHub* : [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L25-L25), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L34-L34)

```solidity
📁 File: src/core/Vault.kerosine.sol

22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L22-L22)

```solidity
📁 File: src/core/VaultManagerV2.sol

40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;

74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();

76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();

87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

88:     if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();

89:     if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

114:     if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();

143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

237:       if (_dyad == 0) return type(uint).max;

261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }

280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }

```


*GitHub* : [40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L46-L46), [74](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L114-L114), [143](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L143-L143), [150](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L214-L214), [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L237-L237), [261](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L261-L263), [280](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L280-L282)

### [N-19]<a name="n-19"></a> Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

*There are 7 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L17-L17)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L18-L18)

```solidity
📁 File: src/core/VaultManagerV2.sol

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;

```


*GitHub* : [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L28-L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L29-L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L30-L30)

### [N-20]<a name="n-20"></a> Inconsistent comment spacing

Some comments use // X and others //X Amend comments to use only use // X or //X consistently

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L1-L1)

```solidity
📁 File: src/core/VaultManagerV2.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L1-L1)

```solidity
📁 File: src/staking/KerosineDenominator.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L1-L1)

### [N-21]<a name="n-21"></a> Interface imports should be declared first

Amend the ordering of imports to import interfaces first followed by other imports

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
5: import {Owned}         from "@solmate/src/auth/Owned.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L4-L5)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

4: import {KerosineVault}          from "./Vault.kerosine.sol";
5: import {IVaultManager}          from "../interfaces/IVaultManager.sol";
6: import {Dyad}                   from "./Dyad.sol";
7: import {KerosineManager}        from "./KerosineManager.sol";
8: import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";
9: 
10: import {ERC20} from "@solmate/src/tokens/ERC20.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L4-L10)

```solidity
📁 File: src/core/Vault.kerosine.sol

4: import {IVaultManager}   from "../interfaces/IVaultManager.sol";
5: import {KerosineManager} from "./KerosineManager.sol";
6: import {IVault}          from "../interfaces/IVault.sol";
7: 
8: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
9: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
10: import {Owned}           from "@solmate/src/auth/Owned.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L4-L10)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

4: import {KerosineVault}        from "./Vault.kerosine.sol";
5: import {IVaultManager}        from "../interfaces/IVaultManager.sol";
6: import {Vault}                from "./Vault.sol";
7: import {Dyad}                 from "./Dyad.sol";
8: import {KerosineManager}      from "./KerosineManager.sol";
9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
10: import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
11: 
12: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
13: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L4-L13)

```solidity
📁 File: src/core/VaultManagerV2.sol

4: import {DNft}            from "./DNft.sol";
5: import {Dyad}            from "./Dyad.sol";
6: import {Licenser}        from "./Licenser.sol";
7: import {Vault}           from "./Vault.sol";
8: import {IVaultManager}   from "../interfaces/IVaultManager.sol";
9: import {KerosineManager} from "../../src/core/KerosineManager.sol";
10: 
11: import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
12: import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
13: import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L4-L15)

```solidity
📁 File: src/staking/KerosineDenominator.sol

4: import {Parameters} from "../params/Parameters.sol";
5: import {Kerosine} from "../staking/Kerosine.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L4-L5)

### [N-22]<a name="n-22"></a> Lack Of Brace Spacing

Lack of brace spacing in coding refers to the absence of spaces around braces, which can hinder code readability. In Solidity, as in many programming languages, spacing can enhance the visual distinction between different parts of the code, making it easier to follow. A lack of spacing can lead to a dense, confusing appearance. The resolution to this issue is to follow a consistent style guide that defines rules for brace spacing. By including spaces around braces, such as `{ statement }` instead of `{statement}`, developers can ensure that the code is more legible and maintainable, especially in larger codebases.

*There are 36 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

5: import {Owned}         from "@solmate/src/auth/Owned.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L5-L5)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

4: import {KerosineVault}          from "./Vault.kerosine.sol";

5: import {IVaultManager}          from "../interfaces/IVaultManager.sol";

6: import {Dyad}                   from "./Dyad.sol";

7: import {KerosineManager}        from "./KerosineManager.sol";

8: import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";

10: import {ERC20} from "@solmate/src/tokens/ERC20.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L5-L5), [6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L6-L6), [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L7-L7), [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L8-L8), [10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L10-L10)

```solidity
📁 File: src/core/Vault.kerosine.sol

4: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

5: import {KerosineManager} from "./KerosineManager.sol";

6: import {IVault}          from "../interfaces/IVault.sol";

8: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

9: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";

10: import {Owned}           from "@solmate/src/auth/Owned.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L5-L5), [6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L6-L6), [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L10-L10)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

4: import {KerosineVault}        from "./Vault.kerosine.sol";

5: import {IVaultManager}        from "../interfaces/IVaultManager.sol";

6: import {Vault}                from "./Vault.sol";

7: import {Dyad}                 from "./Dyad.sol";

8: import {KerosineManager}      from "./KerosineManager.sol";

9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";

10: import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";

12: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";

13: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L5-L5), [6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L6-L6), [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L7-L7), [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L10-L10), [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L13-L13)

```solidity
📁 File: src/core/VaultManagerV2.sol

4: import {DNft}            from "./DNft.sol";

5: import {Dyad}            from "./Dyad.sol";

6: import {Licenser}        from "./Licenser.sol";

7: import {Vault}           from "./Vault.sol";

8: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

9: import {KerosineManager} from "../../src/core/KerosineManager.sol";

11: import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";

12: import {ERC20}             from "@solmate/src/tokens/ERC20.sol";

13: import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";

14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L5-L5), [6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L6-L6), [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L7-L7), [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L9-L9), [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L11-L11), [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L13-L13), [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L14-L14), [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L15-L15)

```solidity
📁 File: src/staking/KerosineDenominator.sol

4: import {Parameters} from "../params/Parameters.sol";

5: import {Kerosine} from "../staking/Kerosine.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L5-L5)

### [N-23]<a name="n-23"></a> It is best practice to use linear inheritance

In Solidity, complex inheritance structures can obfuscate code understanding, introducing potential security risks. Multiple inheritance, especially with overlapping function names or state variables, can cause unintentional overrides or ambiguous behavior. Resolution: Strive for linear and simple inheritance chains. Avoid diamond or circular inheritance patterns. Clearly document the purpose and relationships of base contracts, ensuring that overrides are intentional. Tools like Remix or Hardhat can visualize inheritance chains, assisting in verification. Keeping inheritance streamlined aids in better code readability, reduces potential errors, and ensures smoother audits and upgrades.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-24]<a name="n-24"></a> `constant`s should be defined rather than using magic numbers

Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

49:       return unboundedKerosineVault.assetPrice() * 2;

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L49-L49)

```solidity
📁 File: src/core/VaultManagerV2.sol

148:                   / 10**_vault.oracle().decimals() 

149:                   / 10**_vault.asset().decimals();

```


*GitHub* : [148](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L148-L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L149-L149)

### [N-25]<a name="n-25"></a> `mapping` definitions do not follow the Solidity Style Guide

See the [mappings](https://docs.soliditylang.org/en/latest/style-guide.html#mappings) section of the Solidity Style Guide

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```


*GitHub* : [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L35-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L37-L37)

### [N-26]<a name="n-26"></a> `type(uint<n>).max` should be used instead of `uint<n>(-1)`



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/VaultManagerV2.sol

237:       if (_dyad == 0) return type(uint).max;

```


*GitHub* : [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L237-L237)

### [N-27]<a name="n-27"></a> Consider checking that transfer to `address(this)` is disabled

Functions allowing users to specify the receiving address should check whether the referenced address is not `address(this)`. This would prevent tokens to remain lock inside the contract due to an incorrect `transfer` or `mint`.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/VaultManagerV2.sol

// @audit missing checks for -->  to
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   {

```


*GitHub* : [156](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L163)

### [N-28]<a name="n-28"></a> Custom errors has no error details

Consider adding parameters to the error to indicate which user or values caused the failure.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

```


*GitHub* : [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L10-L10)

### [N-29]<a name="n-29"></a> Missing events in sensitive functions

Sensitive setter functions in smart contracts often alter critical state variables. Without events emitted in these functions, external observers or dApps cannot easily track or react to these state changes. Missing events can obscure contract activity, hampering transparency and making integration more challenging. To resolve this, incorporate appropriate event emissions within these functions. Events offer an efficient way to log crucial changes, aiding in real-time tracking and post-transaction verification.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }

```


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }

```


*GitHub* : [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L48)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }

```


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L64)

### [N-30]<a name="n-30"></a> Use a struct to encapsulate multiple function parameters

Using a struct to encapsulate multiple parameters in Solidity functions can significantly enhance code readability and maintainability. Instead of passing a long list of arguments, which can be error-prone and hard to manage, a struct allows grouping related data into a single, coherent entity. This approach simplifies function signatures and makes the code more organized. It also enhances code clarity, as developers can easily understand the relationship between the parameters. Moreover, it aids in future code modifications and expansions, as adding or modifying a parameter only requires changes in the struct definition, rather than in every function that uses these parameters.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L26)

```solidity
📁 File: src/core/VaultManagerV2.sol

134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {

184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 

```


*GitHub* : [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142), [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192)

### [N-31]<a name="n-31"></a> Consider using named mappings

Consider using [named mappings](https://ethereum.stackexchange.com/questions/51629/how-to-name-the-arguments-in-mapping/145555#145555) to make it easier to understand the purpose of each mapping

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;

```


*GitHub* : [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19-L19)

```solidity
📁 File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```


*GitHub* : [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L35-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L37-L37)

### [N-32]<a name="n-32"></a> Missing `@inheritdoc` on override functions

In Solidity, using `@inheritdoc` on overridden functions is crucial for maintaining comprehensive and understandable NatSpec documentation. It ensures that when a function overrides an external interface or contract function, the original documentation is preserved. This not only helps developers understand the purpose and usage of the function but also aids in keeping documentation consistent and accurate across different versions of the codebase. Neglecting to use `@inheritdoc` can lead to incomplete or confusing documentation, making code maintenance and usage more challenging.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {

```


*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {

```


*GitHub* : [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

### [N-33]<a name="n-33"></a> Natspec `@author` is missing from abstract contract



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

### [N-34]<a name="n-34"></a> Natspec `@dev` is missing from abstract contract



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

### [N-35]<a name="n-35"></a> Natspec `@notice` is missing from abstract contract



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

### [N-36]<a name="n-36"></a> Natspec `@title` is missing from abstract contract



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

### [N-37]<a name="n-37"></a> NatSpec: Contract declarations should have `@author` tags



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-38]<a name="n-38"></a> NatSpec: Contract declarations should have `@dev` tags



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-39]<a name="n-39"></a> NatSpec: Contract declarations should have `@notice` tags



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-40]<a name="n-40"></a> NatSpec: Contract declarations should have `@title` tags



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-41]<a name="n-41"></a> NatSpec: Constructor missing NatSpec `@dev` tag



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
📁 File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {

```


*GitHub* : [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L26)

```solidity
📁 File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49-L53)

```solidity
📁 File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {

```


*GitHub* : [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11-L13)

### [N-42]<a name="n-42"></a> NatSpec: Constructor missing NatSpec `@notice` tag



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
📁 File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {

```


*GitHub* : [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L26)

```solidity
📁 File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49-L53)

```solidity
📁 File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {

```


*GitHub* : [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11-L13)

### [N-43]<a name="n-43"></a> NatSpec: Constructor missing NatSpec `@param` tag



*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
📁 File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {

```


*GitHub* : [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26-L30)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21-L26)

```solidity
📁 File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

```


*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49-L53)

```solidity
📁 File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {

```


*GitHub* : [11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11-L13)

### [N-44]<a name="n-44"></a> NatSpec: Error missing NatSpec `@dev` tag



*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

```


*GitHub* : [8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L10-L10)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

```


*GitHub* : [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L13-L13)

### [N-45]<a name="n-45"></a> NatSpec: Error missing NatSpec `@param` tag



*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

```


*GitHub* : [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L13-L13)

### [N-46]<a name="n-46"></a> NatSpec: Functions missing NatSpec `@dev` tag



*There are 31 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28-L33), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

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


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.sol

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


*GitHub* : [36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L65)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

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


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46), [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {

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


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L163), [172](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172-L178), [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [205](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L205-L212), [230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-47]<a name="n-47"></a> NatSpec: Functions missing NatSpec `@notice` tag



*There are 31 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28-L33), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

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


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.sol

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


*GitHub* : [36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L65)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

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


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46), [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {

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


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L163), [172](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172-L178), [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [205](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L205-L212), [230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-48]<a name="n-48"></a> NatSpec: Functions missing NatSpec `@param` tag



*There are 27 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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

44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) {

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28-L33), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

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


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40)

```solidity
📁 File: src/core/Vault.kerosine.sol

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


*GitHub* : [36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L65)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

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


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {

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


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L163), [172](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172-L178), [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [205](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L205-L212), [230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

### [N-49]<a name="n-49"></a> NatSpec: Functions missing NatSpec `@return` tag



*There are 13 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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


*GitHub* : [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {

```


*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.sol

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view 
65:     returns (uint) {

```


*GitHub* : [60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L65)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {

```


*GitHub* : [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

```solidity
📁 File: src/core/VaultManagerV2.sol

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


*GitHub* : [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-50]<a name="n-50"></a> NatSpec: Modifier missing NatSpec `@dev` tag



*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

21:   modifier onlyVaultManager() {
22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();
23:     _;
24:   }

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L21-L24)

```solidity
📁 File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41:   }

42:   modifier isValidDNft(uint id) {
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44:   }

45:   modifier isLicensed(address vault) {
46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47:   }

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L39-L41), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L42-L44), [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47)

### [N-51]<a name="n-51"></a> NatSpec: Modifier missing NatSpec `@notice` tag



*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.sol

21:   modifier onlyVaultManager() {
22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();
23:     _;
24:   }

```


*GitHub* : [21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L21-L24)

```solidity
📁 File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41:   }

42:   modifier isValidDNft(uint id) {
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44:   }

45:   modifier isLicensed(address vault) {
46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47:   }

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L39-L41), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L42-L44), [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47)

### [N-52]<a name="n-52"></a> NatSpec: Modifier missing NatSpec `@param` tag



*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41:   }

42:   modifier isValidDNft(uint id) {
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44:   }

45:   modifier isLicensed(address vault) {
46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47:   }

```


*GitHub* : [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L39-L41), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L42-L44), [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47)

### [N-53]<a name="n-53"></a> Use recent version of solidity

Use a more [recent version](https://github.com/ethereum/solc-js/tags) of Solidity; it's safer to use newer versions to get the latest bugfixes and features when deploying on L2.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L2-L2)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L2-L2)

```solidity
📁 File: src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L2-L2)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L2-L2)

```solidity
📁 File: src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L2-L2)

```solidity
📁 File: src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L2-L2)

### [N-54]<a name="n-54"></a> Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the override keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {

```


*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {

```


*GitHub* : [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

### [N-55]<a name="n-55"></a> Consider making `private` state variables `internal` to increase flexibility

In Solidity, `private` state variables are strictly confined to the contract they are defined in and can't be accessed or modified by its derived contracts. While this offers strong encapsulation, it can limit contract extensibility and modification in inheritance chains. On the other hand, `internal` variables can be accessed and potentially overridden by child contracts, granting more flexibility in contract development and upgrades. Therefore, it's recommended to use `private` only when you explicitly want to prevent child contract access. Otherwise, prefer `internal` to maintain a balance between encapsulation and the flexibility offered by inheritance patterns in Solidity.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;

```


*GitHub* : [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L16-L16)

### [N-56]<a name="n-56"></a> `private` and `internal` state variables should have a preceding _ in their name unless they are `constant`/`immutable`

Add a preceding underscore to the state variable name, take care to refactor where there variables are read/wrote

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;

```


*GitHub* : [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L16-L16)

### [N-57]<a name="n-57"></a> Public variable declarations should have NatSpec descriptions

Public variable declarations in smart contracts should ideally be accompanied by NatSpec comments to enhance code readability and provide clear documentation. NatSpec (Natural Language Specification) is a standard for writing comments in Ethereum smart contracts that can generate user-friendly documentation, improving the transparency of the contract's functionality. This is particularly crucial for public variables, as they are accessible externally, and understanding their role and impact is vital for both developers and users interacting with the contract

*There are 18 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```


*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14-L14)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

15:   UnboundedKerosineVault public unboundedKerosineVault;

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L15-L15)

```solidity
📁 File: src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

19:   mapping(uint => uint) public id2asset;

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L17-L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19-L19)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

19:   KerosineDenominator  public kerosineDenominator;

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L18-L18), [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L19-L19)

```solidity
📁 File: src/core/VaultManagerV2.sol

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


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L26-L26), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L28-L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L29-L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L30-L30), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L32-L32), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L37-L37)

```solidity
📁 File: src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;

```


*GitHub* : [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L9-L9)

### [N-58]<a name="n-58"></a> Take advantage of Custom Error's return value property

An important feature of Custom Error is that values such as address, tokenID, msg.value can be written inside the () sign, this kind of approach provides a serious advantage in debugging and examining the revert details of dapps such as tenderly.

*There are 23 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();

25:     if (!vaults.add(vault))            revert VaultAlreadyAdded();

34:     if (!vaults.remove(vault)) revert VaultNotFound();

```


*GitHub* : [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L25-L25), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L34-L34)

```solidity
📁 File: src/core/Vault.kerosine.sol

22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L22-L22)

```solidity
📁 File: src/core/VaultManagerV2.sol

40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;

74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();

76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();

87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

88:     if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();

89:     if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

114:     if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();

143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

```


*GitHub* : [40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L46-L46), [74](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L114-L114), [143](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L143-L143), [150](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L214-L214)

### [N-59]<a name="n-59"></a> Setters should prevent re-setting the same value

Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {

```


*GitHub* : [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23-L28)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {

```


*GitHub* : [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L46)

```solidity
📁 File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {

```


*GitHub* : [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L62)

### [N-60]<a name="n-60"></a> Use a single file for system wide constants

Consider grouping all the system constants under a single file.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```


*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14-L14)

```solidity
📁 File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L26-L26)

### [N-61]<a name="n-61"></a> Consider using SMTChecker

The SMTChecker is a valuable tool for Solidity developers as it helps detect potential vulnerabilities and logical errors in the contract's code. By utilizing Satisfiability Modulo Theories (SMT) solvers, it can reason about the potential states a contract can be in, and therefore, identify conditions that could lead to undesirable behavior. This automatic formal verification can catch issues that might otherwise be missed in manual code reviews or standard testing, enhancing the overall contract's security and reliability.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L1-L1)

```solidity
📁 File: src/core/VaultManagerV2.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L1-L1)

```solidity
📁 File: src/staking/KerosineDenominator.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L1-L1)

### [N-62]<a name="n-62"></a> Contract does not follow the Solidity style guide's suggested layout ordering

The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be:

1) Type declarations
2) State variables
3) Events
4) Modifiers
5) Functions

However, the contract(s) below do not follow this ordering

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

1: 
2: Current order:
3: CustomErrorDefinition.TooManyVaults
4: CustomErrorDefinition.VaultAlreadyAdded
5: CustomErrorDefinition.VaultNotFound
6: UsingForDeclaration.undefined
7: StateVariableDeclaration.undefined
8: StateVariableDeclaration.undefined
9: FunctionDefinition.add
10: FunctionDefinition.remove
11: FunctionDefinition.getVaults
12: FunctionDefinition.isLicensed
13: 
14: Suggested order:
15: StateVariableDeclaration.undefined
16: StateVariableDeclaration.undefined
17: CustomErrorDefinition.TooManyVaults
18: CustomErrorDefinition.VaultAlreadyAdded
19: CustomErrorDefinition.VaultNotFound
20: FunctionDefinition.add
21: FunctionDefinition.remove
22: FunctionDefinition.getVaults
23: FunctionDefinition.isLicensed

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L1-L23)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

1: 
2: Current order:
3: CustomErrorDefinition.NotWithdrawable
4: StateVariableDeclaration.undefined
5: FunctionDefinition.undefined
6: FunctionDefinition.setUnboundedKerosineVault
7: FunctionDefinition.withdraw
8: FunctionDefinition.assetPrice
9: 
10: Suggested order:
11: StateVariableDeclaration.undefined
12: CustomErrorDefinition.NotWithdrawable
13: FunctionDefinition.undefined
14: FunctionDefinition.setUnboundedKerosineVault
15: FunctionDefinition.withdraw
16: FunctionDefinition.assetPrice

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L1-L16)

```solidity
📁 File: src/core/Vault.kerosine.sol

1: 
2: Current order:
3: UsingForDeclaration.undefined
4: StateVariableDeclaration.undefined
5: StateVariableDeclaration.undefined
6: StateVariableDeclaration.undefined
7: StateVariableDeclaration.undefined
8: ModifierDefinition.onlyVaultManager
9: FunctionDefinition.undefined
10: FunctionDefinition.deposit
11: FunctionDefinition.move
12: FunctionDefinition.getUsdValue
13: FunctionDefinition.assetPrice
14: 
15: Suggested order:
16: StateVariableDeclaration.undefined
17: StateVariableDeclaration.undefined
18: StateVariableDeclaration.undefined
19: StateVariableDeclaration.undefined
20: ModifierDefinition.onlyVaultManager
21: FunctionDefinition.undefined
22: FunctionDefinition.deposit
23: FunctionDefinition.move
24: FunctionDefinition.getUsdValue
25: FunctionDefinition.assetPrice

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L1-L25)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

1: 
2: Current order:
3: UsingForDeclaration.undefined
4: StateVariableDeclaration.undefined
5: StateVariableDeclaration.undefined
6: FunctionDefinition.undefined
7: FunctionDefinition.withdraw
8: FunctionDefinition.setDenominator
9: FunctionDefinition.assetPrice
10: 
11: Suggested order:
12: StateVariableDeclaration.undefined
13: StateVariableDeclaration.undefined
14: FunctionDefinition.undefined
15: FunctionDefinition.withdraw
16: FunctionDefinition.setDenominator
17: FunctionDefinition.assetPrice

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L1-L17)

```solidity
📁 File: src/core/VaultManagerV2.sol

1: 
2: Current order:
3: UsingForDeclaration.undefined
4: UsingForDeclaration.undefined
5: UsingForDeclaration.undefined
6: StateVariableDeclaration.undefined
7: StateVariableDeclaration.undefined
8: StateVariableDeclaration.undefined
9: StateVariableDeclaration.undefined
10: StateVariableDeclaration.undefined
11: StateVariableDeclaration.undefined
12: StateVariableDeclaration.undefined
13: StateVariableDeclaration.undefined
14: StateVariableDeclaration.undefined
15: StateVariableDeclaration.undefined
16: StateVariableDeclaration.undefined
17: ModifierDefinition.isDNftOwner
18: ModifierDefinition.isValidDNft
19: ModifierDefinition.isLicensed
20: FunctionDefinition.undefined
21: FunctionDefinition.setKeroseneManager
22: FunctionDefinition.add
23: FunctionDefinition.addKerosene
24: FunctionDefinition.remove
25: FunctionDefinition.removeKerosene
26: FunctionDefinition.deposit
27: FunctionDefinition.withdraw
28: FunctionDefinition.mintDyad
29: FunctionDefinition.burnDyad
30: FunctionDefinition.redeemDyad
31: FunctionDefinition.liquidate
32: FunctionDefinition.collatRatio
33: FunctionDefinition.getTotalUsdValue
34: FunctionDefinition.getNonKeroseneValue
35: FunctionDefinition.getKeroseneValue
36: FunctionDefinition.getVaults
37: FunctionDefinition.hasVault
38: 
39: Suggested order:
40: StateVariableDeclaration.undefined
41: StateVariableDeclaration.undefined
42: StateVariableDeclaration.undefined
43: StateVariableDeclaration.undefined
44: StateVariableDeclaration.undefined
45: StateVariableDeclaration.undefined
46: StateVariableDeclaration.undefined
47: StateVariableDeclaration.undefined
48: StateVariableDeclaration.undefined
49: StateVariableDeclaration.undefined
50: StateVariableDeclaration.undefined
51: ModifierDefinition.isDNftOwner
52: ModifierDefinition.isValidDNft
53: ModifierDefinition.isLicensed
54: FunctionDefinition.undefined
55: FunctionDefinition.setKeroseneManager
56: FunctionDefinition.add
57: FunctionDefinition.addKerosene
58: FunctionDefinition.remove
59: FunctionDefinition.removeKerosene
60: FunctionDefinition.deposit
61: FunctionDefinition.withdraw
62: FunctionDefinition.mintDyad
63: FunctionDefinition.burnDyad
64: FunctionDefinition.redeemDyad
65: FunctionDefinition.liquidate
66: FunctionDefinition.collatRatio
67: FunctionDefinition.getTotalUsdValue
68: FunctionDefinition.getNonKeroseneValue
69: FunctionDefinition.getKeroseneValue
70: FunctionDefinition.getVaults
71: FunctionDefinition.hasVault

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L1-L71)

### [N-63]<a name="n-63"></a> Change `uint` to `uint256`

Throughout the code base, some variables are declared as `uint`. To favor explicitness, consider changing all instances of `uint` to `uint256`

*There are 81 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```


*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14-L14)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

33:     uint    id,

35:     uint    amount

48:     returns (uint) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L13-L13), [33](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L33-L33), [35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L35-L35), [48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L48-L48)

```solidity
📁 File: src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;

37:     uint id,

38:     uint amount

48:     uint from,

49:     uint to,

50:     uint amount

61:     uint id

65:     returns (uint) {

73:     returns (uint); 

```


*GitHub* : [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19-L19), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L37-L37), [38](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L38-L38), [48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L48-L48), [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L49-L49), [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L50-L50), [61](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L61-L61), [65](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L65-L65), [73](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L73-L73)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

31:     uint    id,

33:     uint    amount

54:     returns (uint) {

55:       uint tvl;

57:       uint numberOfVaults = vaults.length;

58:       for (uint i = 0; i < numberOfVaults; i++) {

65:       uint numerator   = tvl - dyad.totalSupply();

66:       uint denominator = kerosineDenominator.denominator();

```


*GitHub* : [31](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L31-L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L33-L33), [54](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L54-L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L55-L55), [57](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L57-L57), [58](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L58-L58), [65](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L66-L66)

```solidity
📁 File: src/core/VaultManagerV2.sol

19:   using FixedPointMathLib for uint;

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

68:       uint    id,

81:       uint    id,

95:       uint    id,

107:       uint    id,

120:     uint    id,

122:     uint    amount

135:     uint    id,

137:     uint    amount,

144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

146:     uint value = amount * _vault.assetPrice() 

157:     uint    id,

158:     uint    amount,

164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

173:     uint id,

174:     uint amount

185:     uint    id,

187:     uint    amount,

192:     returns (uint) { 

195:       uint asset = amount 

206:     uint id,

207:     uint to

213:       uint cr = collatRatio(id);

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

221:       uint numberOfVaults = vaults[id].length();

222:       for (uint i = 0; i < numberOfVaults; i++) {

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

231:     uint id

235:     returns (uint) {

236:       uint _dyad = dyad.mintedDyad(address(this), id);

237:       if (_dyad == 0) return type(uint).max;

242:     uint id

246:     returns (uint) {

251:     uint id

255:     returns (uint) {

256:       uint totalUsdValue;

257:       uint numberOfVaults = vaults[id].length(); 

258:       for (uint i = 0; i < numberOfVaults; i++) {

260:         uint usdValue;

270:     uint id

274:     returns (uint) {

275:       uint totalUsdValue;

276:       uint numberOfVaults = vaultsKerosene[id].length(); 

277:       for (uint i = 0; i < numberOfVaults; i++) {

279:         uint usdValue;

291:     uint id

300:     uint    id,

```


*GitHub* : [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L19-L19), [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L26-L26), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L35-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L37-L37), [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L42-L42), [68](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L68-L68), [81](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L81-L81), [95](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L95-L95), [107](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L107-L107), [120](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L120-L120), [122](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L122-L122), [135](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L135-L135), [137](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L137-L137), [144](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L144-L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L146-L146), [157](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L157-L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L158-L158), [164](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L164-L164), [173](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L173-L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L174-L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L185-L185), [187](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L187-L187), [192](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L192-L192), [195](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L195-L195), [206](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L206-L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L207-L207), [213](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L213-L213), [217](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L217-L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L218-L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L219-L219), [221](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L221-L221), [222](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L222-L222), [224](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L224-L224), [231](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L231-L231), [235](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L235-L235), [236](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L236-L236), [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L237-L237), [242](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L242-L242), [246](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L246-L246), [251](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L251-L251), [255](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L255-L255), [256](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L256-L256), [257](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L257-L257), [258](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L258-L258), [260](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L260-L260), [270](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L270-L270), [274](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L274-L274), [275](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L275-L275), [276](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L276-L276), [277](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L277-L277), [279](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L279-L279), [291](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L291-L291), [300](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L300-L300)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-64]<a name="n-64"></a> Use the Modern Upgradeable Contract Paradigm

Modern smart contract development often employs upgradeable contract structures, utilizing proxy patterns like OpenZeppelin’s Upgradeable Contracts. This paradigm separates logic and state, allowing developers to amend and enhance the contract's functionality without altering its state or the deployed contract address. Transitioning to this approach enhances long-term maintainability.

Resolution: Adopt a well-established proxy pattern for upgradeability, ensuring proper initialization and employing transparent proxies to mitigate potential risks. Embrace comprehensive testing and audit practices, particularly when updating contract logic, to ensure state consistency and security are preserved across upgrades. This ensures your contract remains robust and adaptable to future requirements.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7-L7)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12-L12)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```


*GitHub* : [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15-L15)

```solidity
📁 File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L17-L17)

```solidity
📁 File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```


*GitHub* : [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L7-L7)

### [N-65]<a name="n-65"></a> Upgrade openzeppelin to the Latest Version - 5.0.0



*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L4-L4)

```solidity
📁 File: src/core/VaultManagerV2.sol

14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

```


*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L14-L14), [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L15-L15)

### [N-66]<a name="n-66"></a> Consider using named returns

Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

*There are 14 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

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


*GitHub* : [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L49)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {

```


*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44-L48)

```solidity
📁 File: src/core/Vault.kerosine.sol

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


*GitHub* : [60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L65), [69](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L69-L73)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {

```


*GitHub* : [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L54)

```solidity
📁 File: src/core/VaultManagerV2.sol

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


*GitHub* : [184](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L192), [230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L299-L305)

```solidity
📁 File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17-L17)

### [N-67]<a name="n-67"></a> Consider using a format prettier or forge fmt

Some comments use // X and others //X Amend comments to use only use // X or //X consistently such style inconsistencies can be resolved by running the project through a format prettier or by using forge fmt.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L1-L1)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L1-L1)

```solidity
📁 File: src/core/VaultManagerV2.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L1-L1)

```solidity
📁 File: src/staking/KerosineDenominator.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L1-L1)

### [N-68]<a name="n-68"></a> Variable/Parameters names don't follow the Solidity naming convention

Use `mixedCase` for local and state variables that are not constants, and add a trailing underscore for non-external variables. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#local-and-state-variable-names)

*There are 101 instance(s) of this issue:*

```solidity
📁 File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

16:   EnumerableSet.AddressSet private vaults;

19:     address vault

29:     address vault

45:     address vault

```


*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14-L14), [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L16-L16), [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L19-L19), [29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L29-L29), [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L45-L45)

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

18:     IVaultManager   _vaultManager,

19:     ERC20           _asset, 

20:     KerosineManager _kerosineManager

24:     UnboundedKerosineVault _unboundedKerosineVault

33:     uint    id,

34:     address to,

35:     uint    amount

```


*GitHub* : [13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L13-L13), [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L18-L18), [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L19-L19), [20](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L20-L20), [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L24-L24), [33](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L33-L33), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L35-L35)

```solidity
📁 File: src/core/Vault.kerosine.sol

16:   ERC20           public immutable asset;

19:   mapping(uint => uint) public id2asset;

27:     IVaultManager   _vaultManager,

28:     ERC20           _asset, 

29:     KerosineManager _kerosineManager 

37:     uint id,

38:     uint amount

48:     uint from,

49:     uint to,

50:     uint amount

61:     uint id

```


*GitHub* : [16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L16-L16), [19](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19-L19), [27](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L27-L27), [28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L28-L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L29-L29), [37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L37-L37), [38](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L38-L38), [48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L48-L48), [49](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L49-L49), [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L50-L50), [61](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L61-L61)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

22:       IVaultManager   _vaultManager,

23:       ERC20           _asset, 

24:       Dyad            _dyad, 

25:       KerosineManager _kerosineManager

31:     uint    id,

32:     address to,

33:     uint    amount

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

55:       uint tvl;

56:       address[] memory vaults = kerosineManager.getVaults();

58:       for (uint i = 0; i < numberOfVaults; i++) {

59:         Vault vault = Vault(vaults[i]);

65:       uint numerator   = tvl - dyad.totalSupply();

66:       uint denominator = kerosineDenominator.denominator();

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L18-L18), [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L23-L23), [24](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L25-L25), [31](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L31-L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L32-L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L33-L33), [43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43-L43), [55](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L55-L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L56-L56), [58](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L58-L58), [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L59-L59), [65](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L66-L66)

```solidity
📁 File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

29:   Dyad     public immutable dyad;

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

50:     DNft          _dNft,

51:     Dyad          _dyad,

52:     Licenser      _licenser

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

68:       uint    id,

69:       address vault

81:       uint    id,

82:       address vault

95:       uint    id,

96:       address vault

107:       uint    id,

108:       address vault

120:     uint    id,

121:     address vault,

122:     uint    amount

128:     Vault _vault = Vault(vault);

135:     uint    id,

136:     address vault,

137:     uint    amount,

138:     address to

145:     Vault _vault = Vault(vault);

146:     uint value = amount * _vault.assetPrice() 

157:     uint    id,

158:     uint    amount,

159:     address to

173:     uint id,

174:     uint amount

185:     uint    id,

186:     address vault,

187:     uint    amount,

188:     address to

194:       Vault _vault = Vault(vault);

195:       uint asset = amount 

206:     uint id,

207:     uint to

213:       uint cr = collatRatio(id);

222:       for (uint i = 0; i < numberOfVaults; i++) {

223:           Vault vault      = Vault(vaults[id].at(i));

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

231:     uint id

236:       uint _dyad = dyad.mintedDyad(address(this), id);

242:     uint id

251:     uint id

258:       for (uint i = 0; i < numberOfVaults; i++) {

259:         Vault vault = Vault(vaults[id].at(i));

270:     uint id

277:       for (uint i = 0; i < numberOfVaults; i++) {

278:         Vault vault = Vault(vaultsKerosene[id].at(i));

291:     uint id

300:     uint    id,

301:     address vault

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L26-L26), [29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L29-L29), [34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L34-L34), [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L42-L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L45), [50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L50-L50), [51](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L51-L51), [52](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L52-L52), [59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L59), [68](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L68-L68), [69](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L69-L69), [81](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L81-L81), [82](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L82-L82), [95](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L95-L95), [96](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L96-L96), [107](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L107-L107), [108](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L108-L108), [120](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L120-L120), [121](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L121-L121), [122](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L122-L122), [128](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L128-L128), [135](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L135-L135), [136](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L136-L136), [137](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L137-L137), [138](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L138-L138), [145](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L145-L145), [146](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L146-L146), [157](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L157-L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L158-L158), [159](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L159-L159), [173](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L173-L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L174-L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L185-L185), [186](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L186-L186), [187](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L187-L187), [188](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L188-L188), [194](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L194-L194), [195](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L195-L195), [206](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L206-L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L207-L207), [213](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L213-L213), [222](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L222-L222), [223](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L223-L223), [224](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L224-L224), [231](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L231-L231), [236](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L236-L236), [242](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L242-L242), [251](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L251-L251), [258](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L258-L258), [259](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L259-L259), [270](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L270-L270), [277](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L277-L277), [278](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L278-L278), [291](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L291-L291), [300](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L300-L300), [301](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L301-L301)

```solidity
📁 File: src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;

12:     Kerosine _kerosine

```


*GitHub* : [9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L9-L9), [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L12-L12)

### [N-69]<a name="n-69"></a> Incorrect withdraw declaration

In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for `withdraw` should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/core/Vault.kerosine.bounded.sol

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


*GitHub* : [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L40)

```solidity
📁 File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {

```


*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30-L37)

```solidity
📁 File: src/core/VaultManagerV2.sol

134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {

```


*GitHub* : [134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L142)

### [N-70]<a name="n-70"></a> Invalid NatSpec comment style

NatSpec [must](https://docs.soliditylang.org/en/latest/natspec-format.html#documentation-example) begin with `///`, or use the `/* ... */` syntax.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/staking/KerosineDenominator.sol

18:     // @dev: We subtract all the Kerosene in the multi-sig.

```


*GitHub* : [18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L18-L18)

