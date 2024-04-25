### Low

|Number|Issue|Instances|
|-|:-|:-:|
| [L&#x2011;1](#L1-constant-decimal-values) | Constant decimal values | 8 |
| [L&#x2011;2](#L2-constructor-/-initialization-function-lacks-parameter-validation) | Constructor / initialization function lacks parameter validation | 4 |
| [L&#x2011;3](#L3-critical-functions-should-be-controlled-by-time-locks) | Critical functions should be controlled by time locks | 2 |
| [L&#x2011;4](#L4-external-calls-in-an-un-bounded-for-loop-may-result-in-a-dos) | External calls in an un-bounded `for-`loop may result in a DOS | 4 |
| [L&#x2011;5](#L5-missing-_disableinitializer-in-upgradeable-constructor-body) | Missing `_disableInitializer()` in upgradeable constructor body | 1 |
| [L&#x2011;6](#L6-missing-zero-address-check-in-functions-with-address-parameters) | Missing zero address check in functions with address parameters | 14 |
| [L&#x2011;7](#L7-some-tokens-may-revert-when-zero-value-transfers-are-made) | Some tokens may revert when zero value transfers are made | 2 |
| [L&#x2011;8](#L8-upgradable-contracts-should-have-an-initialization-function) | Upgradable contracts should have an initialization function | 1 |


### NonCritical

|Number|Issue|Instances|
|-|:-|:-:|
| [NC&#x2011;01](#NC01-@openzeppelin/contracts-should-be-upgraded-to-a-newer-version) | `@openzeppelin/contracts` should be upgraded to a newer version | 3 |
| [NC&#x2011;02](#NC02-avoid-external-calls-in-modifiers) | Avoid external calls in modifiers | 3 |
| [NC&#x2011;03](#NC03-consider-adding-formal-verification-proofs) | Consider adding formal verification proofs | 1 |
| [NC&#x2011;04](#NC04-consider-adding-a-block/deny-list) | Consider adding a block/deny-list | 5 |
| [NC&#x2011;05](#NC05-consider-disallowing-transfers-to-addressthis) | Consider disallowing transfers to `address(this)` | 4 |
| [NC&#x2011;06](#NC06-consider-enabling---via-ir-for-enhanced-code-transparency-and-auditability) | Consider enabling `--via-ir` for enhanced code transparency and auditability | 1 |
| [NC&#x2011;07](#NC07-use-the-modern-upgradeable-contract-paradigm) | Use the Modern Upgradeable Contract Paradigm | 6 |
| [NC&#x2011;08](#NC08-use-named-function-calls) | Use named function calls | 6 |
| [NC&#x2011;09](#NC09-constants-should-be-put-on-the-left-side-of-comparisons) | Constants should be put on the left side of comparisons | 2 |
| [NC&#x2011;10](#NC10-constructor-should-emit-an-event) | `constructor` should emit an event | 4 |
| [NC&#x2011;11](#NC11-contract-implements-interface-without-extending-the-interface) | Contract implements interface without extending the interface | 1 |
| [NC&#x2011;12](#NC12-contract-functions-should-be-exposed-by-an-interface) | Contract functions should be exposed by an `interface` | 31 |
| [NC&#x2011;13](#NC13-contracts-should-have-full-test-coverage) | Contracts should have full test coverage | 1 |
| [NC&#x2011;14](#NC14-empty-function-body-without-comments) | Empty function body without comments | 1 |
| [NC&#x2011;15](#NC15-events-are-missing-sender-information) | Events are missing sender information | 6 |
| [NC&#x2011;16](#NC16-events-may-be-emitted-out-of-order-due-to-reentrancy) | Events may be emitted out of order due to reentrancy | 1 |
| [NC&#x2011;17](#NC17-events-should-be-emitted-before-external-calls) | Events should be emitted before external calls | 9 |
| [NC&#x2011;18](#NC18-extraneous-whitespace) | Extraneous whitespace | 3 |
| [NC&#x2011;19](#NC19-file-names-should-match-the-contract-name) | File names should match the contract name | 3 |
| [NC&#x2011;20](#NC20-for-loops-in-public-or-external-functions-should-be-avoided-due-to-high-gas-costs-and-possible-dos) | For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS | 4 |
| [NC&#x2011;21](#NC21-imports-could-be-organized-more-systematically) | Imports could be organized more systematically | 5 |
| [NC&#x2011;22](#NC22-incorrect-withdraw-declaration) | Incorrect withdraw declaration | 3 |
| [NC&#x2011;23](#NC23-invalid-natspec-comment-style) | Invalid NatSpec comment style | 1 |
| [NC&#x2011;24](#NC24-it-is-best-practice-to-use-linear-inheritance) | It is best practice to use linear inheritance | 2 |
| [NC&#x2011;25](#NC25-large-or-complicated-code-bases-should-implement-invariant-tests) | Large or complicated code bases should implement invariant tests | 1 |
| [NC&#x2011;26](#NC26-minting-to-the-zero-address-should-be-avoided) | Minting to the zero address should be avoided | 1 |
| [NC&#x2011;27](#NC27-state-variable-assignments-are-missing-checks-for-uints) | State variable assignments are missing checks for uints | 4 |
| [NC&#x2011;28](#NC28-natspec-documentation-for-constructor-is-missing) | NatSpec documentation for `constructor` is missing | 5 |
| [NC&#x2011;29](#NC29-constructors-should-have-@notice-tags) | Constructors should have `@notice` tags | 5 |
| [NC&#x2011;30](#NC30-contract-declarations-should-have-@author-tags) | Contract declarations should have `@author` tags | 6 |
| [NC&#x2011;31](#NC31-contract-declarations-should-have-@dev-tags) | Contract declarations should have `@dev` tags | 6 |
| [NC&#x2011;32](#NC32-contract-declarations-should-have-@notice-tags) | Contract declarations should have `@notice` tags | 6 |
| [NC&#x2011;33](#NC33-contract-declarations-should-have-@title-tags) | Contract declarations should have `@title` tags | 6 |
| [NC&#x2011;34](#NC34-contract-declarations-should-have-natspec-descriptions) | Contract declarations should have NatSpec descriptions | 6 |
| [NC&#x2011;35](#NC35-errors-should-have-@notice-tags) | Errors should have `@notice` tags | 4 |
| [NC&#x2011;36](#NC36-errormodifier-declarations-should-have-natspec-descriptions) | ErrorModifier declarations should have NatSpec descriptions | 4 |
| [NC&#x2011;37](#NC37-error-missing-natspec-@dev-tag) | Error missing NatSpec `@dev` tag | 4 |
| [NC&#x2011;38](#NC38-error-declaration-missing-natspec-@param-tag) | Error declaration missing NatSpec `@param` tag | 1 |
| [NC&#x2011;39](#NC39-file-is-missing-natspec) | File is missing NatSpec | 6 |
| [NC&#x2011;40](#NC40-functions-should-have-@notice-tags) | Functions should have `@notice` tags | 24 |
| [NC&#x2011;41](#NC41-natspec-documentation-for-function-is-missing) | NatSpec documentation for function is missing | 24 |
| [NC&#x2011;42](#NC42-functions-missing-natspec-@dev-tag) | Functions missing NatSpec `@dev` tag | 37 |
| [NC&#x2011;43](#NC43-functions-missing-natspec-@param-tag) | Functions missing NatSpec `@param` tag | 24 |
| [NC&#x2011;44](#NC44-functions-missing-natspec-@return-tag) | Functions missing NatSpec `@return` tag | 14 |
| [NC&#x2011;45](#NC45-modifier-declarations-should-have-natspec-descriptions) | Modifier declarations should have NatSpec descriptions | 4 |
| [NC&#x2011;46](#NC46-modifier-missing-natspec-@dev-tag) | Modifier missing NatSpec `@dev` tag | 4 |
| [NC&#x2011;47](#NC47-modifier-missing-natspec-@param-tag) | Modifier missing NatSpec `@param` tag | 3 |
| [NC&#x2011;48](#NC48-names-of-private/internal-state-variables-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` state variables should be prefixed with an underscore | 3 |
| [NC&#x2011;49](#NC49-update-project-dependencies-to-their-latest-versions) | Update project dependencies to their latest versions | 1 |
| [NC&#x2011;50](#NC50-use-the-latest-solidity-version-0819-for-l2s) | Use the latest Solidity version (0.8.19 for L2s) | 6 |
| [NC&#x2011;51](#NC51-consider-splitting-long-calculations) | Consider splitting long calculations | 3 |
| [NC&#x2011;52](#NC52-public-variable-declarations-should-have-natspec-descriptions) | Public variable declarations should have NatSpec descriptions | 19 |
| [NC&#x2011;53](#NC53-style-guide-mapping-definitions-do-not-follow-the-solidity-style-guide) | Style guide: `mapping` definitions do not follow the Solidity Style Guide | 3 |
| [NC&#x2011;54](#NC54-top-level-declarations-should-be-separated-by-at-least-two-lines) | Top-level declarations should be separated by at least two lines | 33 |
| [NC&#x2011;55](#NC55-unnecessary-cast) | Unnecessary cast | 1 |
| [NC&#x2011;56](#NC56-use-@inheritdoc-for-overridden-functions) | Use `@inheritdoc` for overridden functions | 2 |
| [NC&#x2011;57](#NC57-variable-names-for-immutables-should-use-constant_case) | Variable names for `immutable`s should use CONSTANT_CASE | 7 |
| [NC&#x2011;58](#NC58-state-and-local-variables-should-be-named-using-lowercamelcase) | State and local variables should be named using lowerCamelCase | 17 |

## Low

### [L&#x2011;1] Constant decimal values
The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.

<details>
<summary><i>There are 8 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

66       return id2asset[id] * assetPrice() / 1e8; 
```
([66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L66))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

60         tvl += vault.asset().balanceOf(address(vault))  
61                 * vault.assetPrice() * 1e18

67       return numerator * 1e8 / denominator; 
```
([60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60-L61), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67))

```solidity
File: src/core/VaultManagerV2.sol

146     uint value = amount * _vault.assetPrice()  
147                   * 1e18 

195       uint asset = amount  
196                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197                     / _vault.assetPrice() 
198                     / 1e18;

217       uint cappedCr               = cr < 1e18 ? 1e18 : cr; 
218       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
```
([146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L147), [195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L198), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217-L219))

</details>

### [L&#x2011;2] Constructor / initialization function lacks parameter validation
Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

// @audit _vaultManager , _asset , _kerosineManager 
26   constructor( 
27     IVaultManager   _vaultManager,
28     ERC20           _asset, 
29     KerosineManager _kerosineManager 
30   ) {
```
([26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit _dyad 
21   constructor( 
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
26   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26))

```solidity
File: src/core/VaultManagerV2.sol

// @audit _dNft , _dyad , _licenser 
49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53))

```solidity
File: src/staking/KerosineDenominator.sol

// @audit _kerosine 
11   constructor( 
12     Kerosine _kerosine
13   ) {
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13))

</details>

### [L&#x2011;3] Critical functions should be controlled by time locks
It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user).


<i>There are 2 instaces of this issue:</i>

```solidity
File: src/core/KerosineManager.sol

18   function add( 
19     address vault
20   ) 
21     external 
22       onlyOwner
23   {
24     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
25     if (!vaults.add(vault))            revert VaultAlreadyAdded();
26   }

28   function remove( 
29     address vault
30   ) 
31     external 
32       onlyOwner
33   {
34     if (!vaults.remove(vault)) revert VaultNotFound();
35   }
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L26), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L35))

### [L&#x2011;4] External calls in an un-bounded `for-`loop may result in a DOS
Consider limiting the number of iterations in `for`-loops that make external calls

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit L63
// @audit L60
// @audit L61
// @audit L62
// @audit L63
// @audit L60
// @audit L62
58       for (uint i = 0; i < numberOfVaults; i++) { 
59         Vault vault = Vault(vaults[i]);
60         tvl += vault.asset().balanceOf(address(vault)) 
61                 * vault.assetPrice() * 1e18
62                 / (10**vault.asset().decimals()) 
63                 / (10**vault.oracle().decimals());
64       }
```
([58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58-L64))

```solidity
File: src/core/VaultManagerV2.sol

// @audit L225
// @audit L224
222       for (uint i = 0; i < numberOfVaults; i++) { 
223           Vault vault      = Vault(vaults[id].at(i));
224           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225           vault.move(id, to, collateral);
226       }

// @audit L261
// @audit L262
258       for (uint i = 0; i < numberOfVaults; i++) { 
259         Vault vault = Vault(vaults[id].at(i));
260         uint usdValue;
261         if (vaultLicenser.isLicensed(address(vault))) {
262           usdValue = vault.getUsdValue(id);        
263         }
264         totalUsdValue += usdValue;
265       }

// @audit L280
// @audit L281
277       for (uint i = 0; i < numberOfVaults; i++) { 
278         Vault vault = Vault(vaultsKerosene[id].at(i));
279         uint usdValue;
280         if (keroseneManager.isLicensed(address(vault))) {
281           usdValue = vault.getUsdValue(id);        
282         }
283         totalUsdValue += usdValue;
284       }
```
([222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222-L226), [258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258-L265), [277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277-L284))

</details>

### [L&#x2011;5] Missing `_disableInitializer()` in upgradeable constructor body
Avoid leaving a contract uninitialized.
An uninitialized contract can be taken over by an attacker. This applies to both a proxy and its implementation contract, which may impact the proxy. To prevent the implementation contract from being used, you should invoke the `_disableInitializers()` function in the constructor to automatically lock it when it is deployed.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {
54     dNft          = _dNft;
55     dyad          = _dyad;
56     vaultLicenser = _licenser;
57   }
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L57))

### [L&#x2011;6] Missing zero address check in functions with address parameters
Adding a zero address check for each address type parameter can prevent errors.

<details>
<summary><i>There are 14 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

// @audit vault
18   function add( 
19     address vault
20   ) 
21     external 
22       onlyOwner
23   {

// @audit vault
28   function remove( 
29     address vault
30   ) 
31     external 
32       onlyOwner
33   {

// @audit vault
44   function isLicensed( 
45     address vault
46   ) 
47     external 
48     view 
49     returns (bool) {
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L33), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44-L49))

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit to
32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {
```
([32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit to
30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37))

```solidity
File: src/core/VaultManagerV2.sol

// @audit vault
67   function add( 
68       uint    id,
69       address vault
70   ) 
71     external
72       isDNftOwner(id)
73   {

// @audit vault
80   function addKerosene( 
81       uint    id,
82       address vault
83   ) 
84     external
85       isDNftOwner(id)
86   {

// @audit vault
94   function remove( 
95       uint    id,
96       address vault
97   ) 
98     external
99       isDNftOwner(id)
100   {

// @audit vault
106   function removeKerosene( 
107       uint    id,
108       address vault
109   ) 
110     external
111       isDNftOwner(id)
112   {

// @audit vault
119   function deposit( 
120     uint    id,
121     address vault,
122     uint    amount
123   ) 
124     external 
125       isValidDNft(id)
126   {

// @audit vault, to
134   function withdraw( 
135     uint    id,
136     address vault,
137     uint    amount,
138     address to
139   ) 
140     public
141       isDNftOwner(id)
142   {

// @audit to
156   function mintDyad( 
157     uint    id,
158     uint    amount,
159     address to
160   )
161     external 
162       isDNftOwner(id)
163   {

// @audit vault, to
184   function redeemDyad( 
185     uint    id,
186     address vault,
187     uint    amount,
188     address to
189   )
190     external 
191       isDNftOwner(id)
192     returns (uint) { 

// @audit vault
299   function hasVault( 
300     uint    id,
301     address vault
302   ) 
303     external 
304     view 
305     returns (bool) {
```
([67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L163), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L192), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299-L305))

</details>

### [L&#x2011;7] Some tokens may revert when zero value transfers are made
In spite of the fact that EIP-20 [states](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) that zero-valued transfers must be accepted, some tokens, such as LEND will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

<details>
<summary><i>There are 2 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

39     asset.safeTransfer(to, amount);  
```
([39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L39))

```solidity
File: src/core/VaultManagerV2.sol

129     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount); 
```
([129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129))

</details>

### [L&#x2011;8] Upgradable contracts should have an initialization function
Upgradable Solidity contracts utilize a proxy pattern to separate logic from data storage, allowing smooth logic updates without affecting data. To ensure consistency and security, an initialization function is crucial during deployment. This safeguards against vulnerabilities and maintains a proper contract setup.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

// @audit Initializable
17 contract VaultManagerV2 is IVaultManager, Initializable { 
18   using EnumerableSet     for EnumerableSet.AddressSet;
19   using FixedPointMathLib for uint;
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L19))

## NonCritical

### [NC&#x2011;01] `@openzeppelin/contracts` should be upgraded to a newer version
These contracts import contracts from `@openzeppelin/contracts`, but they are not using the [latest version](https://github.com/OpenZeppelin/openzeppelin-contracts/releases).

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

4 import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol"; 
```
([4](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L4))

```solidity
File: src/core/VaultManagerV2.sol

14 import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol"; 
15 import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```
([14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L14-L15))

</details>

### [NC&#x2011;02] Avoid external calls in modifiers
It is unusual to have external calls in modifiers, and doing so will make reviewers more likely to miss important external interactions. Consider moving the external call to an internal function, and calling that function from the modifier.


<i>There are 3 instaces of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

// @audit dNft.ownerOf()
39   modifier isDNftOwner(uint id) { 
40     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41   }
// @audit dNft.ownerOf()
42   modifier isValidDNft(uint id) {
43     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44   }
// @audit vaultLicenser.isLicensed()
45   modifier isLicensed(address vault) {
46     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47   }
```
([39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39-L47))

### [NC&#x2011;03] Consider adding formal verification proofs
Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

### [NC&#x2011;04] Consider adding a block/deny-list
Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

<details>
<summary><i>There are 5 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
8   error TooManyVaults();
9   error VaultAlreadyAdded();
10   error VaultNotFound();
11 
12   using EnumerableSet for EnumerableSet.AddressSet;
13 
14   uint public constant MAX_VAULTS = 10;
15 
16   EnumerableSet.AddressSet private vaults;
17 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7-L17))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
13   error NotWithdrawable(uint id, address to, uint amount);
14 
15   UnboundedKerosineVault public unboundedKerosineVault;
16 
17   constructor(
18     IVaultManager   _vaultManager,
19     ERC20           _asset, 
20     KerosineManager _kerosineManager
21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
22 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12-L22))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15 contract UnboundedKerosineVault is KerosineVault { 
16   using SafeTransferLib for ERC20;
17 
18   Dyad                 public immutable dyad;
19   KerosineDenominator  public kerosineDenominator;
20 
21   constructor(
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15-L25))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
18   using EnumerableSet     for EnumerableSet.AddressSet;
19   using FixedPointMathLib for uint;
20   using SafeTransferLib   for ERC20;
21 
22   uint public constant MAX_VAULTS          = 5;
23   uint public constant MAX_VAULTS_KEROSENE = 5;
24 
25   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%
26   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
27 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L27))

```solidity
File: src/staking/KerosineDenominator.sol

7 contract KerosineDenominator is Parameters { 
8 
9   Kerosine public kerosine;
10 
11   constructor(
12     Kerosine _kerosine
13   ) {
14     kerosine = _kerosine;
15   }
16 
17   function denominator() external view returns (uint) {
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L17))

</details>

### [NC&#x2011;05] Consider disallowing transfers to `address(this)`
<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {
```
([32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37))

```solidity
File: src/core/VaultManagerV2.sol

134   function withdraw( 
135     uint    id,
136     address vault,
137     uint    amount,
138     address to
139   ) 
140     public
141       isDNftOwner(id)
142   {

184   function redeemDyad( 
185     uint    id,
186     address vault,
187     uint    amount,
188     address to
189   )
190     external 
191       isDNftOwner(id)
192     returns (uint) { 
```
([134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L142), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L192))

</details>

### [NC&#x2011;06] Consider enabling `--via-ir` for enhanced code transparency and auditability
The `--via-ir` command line option enables Solidity's IR-based code generator, offering a level of transparency and auditability superior to the traditional, direct-to-EVM method. The Intermediate Representation (IR) in Yul serves as an intermediary, offering a more transparent view of how the Solidity code is transformed into EVM bytecode.

While it does introduce slight semantic variations, these are mostly in areas unlikely to impact the typical contract's behavior.
It is encouraged to test this feature to gain its benefits, which include making the code generation process more transparent and auditable.

[Solidity Documentation](https://docs.soliditylang.org/en/v0.8.20/ir-breaking-changes.html#solidity-ir-based-codegen-changes).

### [NC&#x2011;07] Use the Modern Upgradeable Contract Paradigm
Contract uses a non-upgradeable design.
Transitioning to an upgradeable contract structure is more aligned with contemporary smart contract practices.
This approach not only enhances flexibility but also allows for continuous improvement and adaptation, ensuring the contract stays relevant and robust in an ever-evolving ecosystem.

<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12))

```solidity
File: src/core/Vault.kerosine.sol

12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15 contract UnboundedKerosineVault is KerosineVault { 
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17))

```solidity
File: src/staking/KerosineDenominator.sol

7 contract KerosineDenominator is Parameters { 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7))

</details>

### [NC&#x2011;08] Use named function calls
When calling a function, use named parameters to improve readability and reduce the chance of making mistakes. For example: `_mint({account: msg.sender, amount: _amount})`


<i>There are 6 instaces of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

151     _vault.withdraw(id, to, amount); 

166     dyad.mint(id, to, amount); 

179     dyad.burn(id, msg.sender, amount); 

193       dyad.burn(id, msg.sender, amount); 

215       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id)); 

225           vault.move(id, to, collateral); 
```
([151](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L151), [166](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L166), [179](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L179), [193](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L193), [215](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L215), [225](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L225))

### [NC&#x2011;09] Constants should be put on the left side of comparisons
Putting constants on the left side of comparison statements is a best practice known as [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions). Although solidity's static typing system prevents accidental assignments within conditionals, adopting this practice can improve code readability and consistency, especially when working across multiple languages.


<i>There are 2 instaces of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

143     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock(); 

237       if (_dyad == 0) return type(uint).max; 
```
([143](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L143), [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237))

### [NC&#x2011;10] `constructor` should emit an event
Use events to signal significant changes to off-chain monitoring tools.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

26   constructor( 
27     IVaultManager   _vaultManager,
28     ERC20           _asset, 
29     KerosineManager _kerosineManager 
30   ) {
```
([26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

21   constructor( 
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
26   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26))

```solidity
File: src/core/VaultManagerV2.sol

49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53))

```solidity
File: src/staking/KerosineDenominator.sol

11   constructor( 
12     Kerosine _kerosine
13   ) {
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13))

</details>

### [NC&#x2011;11] Contract implements interface without extending the interface
Not extending the interface may lead to the wrong function signature being used, leading to unexpected behavior. If the interface is in fact being implemented, use the `override` keyword to indicate that fact.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/Vault.kerosine.sol

// @audit withdraw() from IVault
12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12))

### [NC&#x2011;12] Contract functions should be exposed by an `interface`
The `contract`s should expose an `interface` so that other projects can more easily integrate with it, without having to develop their own non-standard variants.

<details>
<summary><i>There are 31 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

18   function add( 
19     address vault
20   ) 
21     external 
22       onlyOwner
23   {

28   function remove( 
29     address vault
30   ) 
31     external 
32       onlyOwner
33   {

37   function getVaults()  
38     external 
39     view 
40     returns (address[] memory) {

44   function isLicensed( 
45     address vault
46   ) 
47     external 
48     view 
49     returns (bool) {
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L33), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44-L49))

```solidity
File: src/core/Vault.kerosine.bounded.sol

23   function setUnboundedKerosineVault( 
24     UnboundedKerosineVault _unboundedKerosineVault
25   )
26     external
27     onlyOwner
28   {

32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {

44   function assetPrice()  
45     public 
46     view 
47     override
48     returns (uint) {
```
([23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48))

```solidity
File: src/core/Vault.kerosine.sol

36   function deposit( 
37     uint id,
38     uint amount
39   )
40     public 
41       onlyVaultManager
42   {

47   function move( 
48     uint from,
49     uint to,
50     uint amount
51   )
52     external
53       onlyVaultManager
54   {

60   function getUsdValue( 
61     uint id
62   )
63     public
64     view 
65     returns (uint) {
```
([36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60-L65))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {

43   function setDenominator(KerosineDenominator _kerosineDenominator)  
44     external 
45       onlyOwner
46   {

50   function assetPrice()  
51     public 
52     view 
53     override
54     returns (uint) {
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54))

```solidity
File: src/core/VaultManagerV2.sol

59   function setKeroseneManager(KerosineManager _keroseneManager)  
60     external
61       initializer 
62     {

67   function add( 
68       uint    id,
69       address vault
70   ) 
71     external
72       isDNftOwner(id)
73   {

80   function addKerosene( 
81       uint    id,
82       address vault
83   ) 
84     external
85       isDNftOwner(id)
86   {

94   function remove( 
95       uint    id,
96       address vault
97   ) 
98     external
99       isDNftOwner(id)
100   {

106   function removeKerosene( 
107       uint    id,
108       address vault
109   ) 
110     external
111       isDNftOwner(id)
112   {

119   function deposit( 
120     uint    id,
121     address vault,
122     uint    amount
123   ) 
124     external 
125       isValidDNft(id)
126   {

134   function withdraw( 
135     uint    id,
136     address vault,
137     uint    amount,
138     address to
139   ) 
140     public
141       isDNftOwner(id)
142   {

156   function mintDyad( 
157     uint    id,
158     uint    amount,
159     address to
160   )
161     external 
162       isDNftOwner(id)
163   {

172   function burnDyad( 
173     uint id,
174     uint amount
175   ) 
176     external 
177       isValidDNft(id)
178   {

184   function redeemDyad( 
185     uint    id,
186     address vault,
187     uint    amount,
188     address to
189   )
190     external 
191       isDNftOwner(id)
192     returns (uint) { 

205   function liquidate( 
206     uint id,
207     uint to
208   ) 
209     external 
210       isValidDNft(id)
211       isValidDNft(to)
212     {

230   function collatRatio( 
231     uint id
232   )
233     public 
234     view
235     returns (uint) {

241   function getTotalUsdValue( 
242     uint id
243   ) 
244     public 
245     view
246     returns (uint) {

250   function getNonKeroseneValue( 
251     uint id
252   ) 
253     public 
254     view
255     returns (uint) {

269   function getKeroseneValue( 
270     uint id
271   ) 
272     public 
273     view
274     returns (uint) {

290   function getVaults( 
291     uint id
292   ) 
293     external 
294     view 
295     returns (address[] memory) {

299   function hasVault( 
300     uint    id,
301     address vault
302   ) 
303     external 
304     view 
305     returns (bool) {
```
([59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67-L73), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L86), [94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94-L100), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L112), [119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L126), [134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L142), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L163), [172](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L172-L178), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L192), [205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L212), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299-L305))

```solidity
File: src/staking/KerosineDenominator.sol

17   function denominator() external view returns (uint) { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17))

</details>

### [NC&#x2011;13] Contracts should have full test coverage
A 100% test coverage is not foolproof, but it helps immensely in reducing the amount of bugs that may occur.

### [NC&#x2011;14] Empty function body without comments
Empty function body in solidity is not recommended, consider adding some comments to the body.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/Vault.kerosine.bounded.sol

17   constructor( 
18     IVaultManager   _vaultManager,
19     ERC20           _asset, 
20     KerosineManager _kerosineManager
21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21))

### [NC&#x2011;15] Events are missing sender information
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the msg.sender the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

40     emit Withdraw(id, to, amount); 
```
([40](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40))

```solidity
File: src/core/VaultManagerV2.sol

77     emit Added(id, vault); 

90     emit Added(id, vault); 

103     emit Removed(id, vault); 

115     emit Removed(id, vault); 

168     emit MintDyad(id, amount, to); 
```
([77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L168))

</details>

### [NC&#x2011;16] Events may be emitted out of order due to reentrancy
If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events follow the best practice of CEI.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

200       emit RedeemDyad(id, vault, amount, to); 
```
([200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200))

### [NC&#x2011;17] Events should be emitted before external calls
Make sure that events adhere to the check-effects-interaction best practice and are emitted prior to external calls.

<details>
<summary><i>There are 9 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit safeTransfer(), L39
40     emit Withdraw(id, to, amount); 
```
([40](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40))

```solidity
File: src/core/VaultManagerV2.sol

// @audit add(), L76
77     emit Added(id, vault); 

// @audit add(), L89
90     emit Added(id, vault); 

// @audit remove(), L102
103     emit Removed(id, vault); 

// @audit remove(), L114
115     emit Removed(id, vault); 

// @audit mint(), L166
168     emit MintDyad(id, amount, to); 

// @audit burn(), L179
180     emit BurnDyad(id, amount, msg.sender); 

// @audit assetPrice(), L197
200       emit RedeemDyad(id, vault, amount, to); 

// @audit move(), L225
227       emit Liquidate(id, msg.sender, to); 
```
([77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L168), [180](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L180), [200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200), [227](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L227))

</details>

### [NC&#x2011;18] Extraneous whitespace
See the [whitespace](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

31     vaultManager    = _vaultManager; 

56     id2asset[to]   += amount; 
```
([31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L31), [56](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L56))

```solidity
File: src/core/VaultManagerV2.sol

54     dNft          = _dNft; 
```
([54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L54))

</details>

### [NC&#x2011;19] File names should match the contract name
According to the Solidity [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names) contract and library names should match their filenames.

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit Vault.kerosine.bounded
12 contract BoundedKerosineVault is KerosineVault { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12))

```solidity
File: src/core/Vault.kerosine.sol

// @audit Vault.kerosine
12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit Vault.kerosine.unbounded
15 contract UnboundedKerosineVault is KerosineVault { 
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15))

</details>

### [NC&#x2011;20] For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS
In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit L58
50   function assetPrice()  
51     public 
52     view 
53     override
54     returns (uint) {
55       uint tvl;
56       address[] memory vaults = kerosineManager.getVaults();
57       uint numberOfVaults = vaults.length;
58       for (uint i = 0; i < numberOfVaults; i++) {
59         Vault vault = Vault(vaults[i]);
60         tvl += vault.asset().balanceOf(address(vault)) 
61                 * vault.assetPrice() * 1e18
62                 / (10**vault.asset().decimals()) 
63                 / (10**vault.oracle().decimals());
64       }
65       uint numerator   = tvl - dyad.totalSupply();
66       uint denominator = kerosineDenominator.denominator();
67       return numerator * 1e8 / denominator;
68   }
```
([50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L68))

```solidity
File: src/core/VaultManagerV2.sol

// @audit L222
205   function liquidate( 
206     uint id,
207     uint to
208   ) 
209     external 
210       isValidDNft(id)
211       isValidDNft(to)
212     {
213       uint cr = collatRatio(id);
214       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
215       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
216 
217       uint cappedCr               = cr < 1e18 ? 1e18 : cr;
218       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
220 
221       uint numberOfVaults = vaults[id].length();
222       for (uint i = 0; i < numberOfVaults; i++) {
223           Vault vault      = Vault(vaults[id].at(i));
224           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225           vault.move(id, to, collateral);
226       }
227       emit Liquidate(id, msg.sender, to);
228   }

// @audit L258
250   function getNonKeroseneValue( 
251     uint id
252   ) 
253     public 
254     view
255     returns (uint) {
256       uint totalUsdValue;
257       uint numberOfVaults = vaults[id].length(); 
258       for (uint i = 0; i < numberOfVaults; i++) {
259         Vault vault = Vault(vaults[id].at(i));
260         uint usdValue;
261         if (vaultLicenser.isLicensed(address(vault))) {
262           usdValue = vault.getUsdValue(id);        
263         }
264         totalUsdValue += usdValue;
265       }
266       return totalUsdValue;
267   }

// @audit L277
269   function getKeroseneValue( 
270     uint id
271   ) 
272     public 
273     view
274     returns (uint) {
275       uint totalUsdValue;
276       uint numberOfVaults = vaultsKerosene[id].length(); 
277       for (uint i = 0; i < numberOfVaults; i++) {
278         Vault vault = Vault(vaultsKerosene[id].at(i));
279         uint usdValue;
280         if (keroseneManager.isLicensed(address(vault))) {
281           usdValue = vault.getUsdValue(id);        
282         }
283         totalUsdValue += usdValue;
284       }
285       return totalUsdValue;
286   }
```
([205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L267), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L286))

</details>

### [NC&#x2011;21] Imports could be organized more systematically
The contract's interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout.

<details>
<summary><i>There are 5 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

2 pragma solidity =0.8.17; 
3 
4 import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
5 import {Owned}         from "@solmate/src/auth/Owned.sol";
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L2-L5))

```solidity
File: src/core/Vault.kerosine.bounded.sol

2 pragma solidity =0.8.17; 
3 
4 import {KerosineVault}          from "./Vault.kerosine.sol";
5 import {IVaultManager}          from "../interfaces/IVaultManager.sol";
6 import {Dyad}                   from "./Dyad.sol";
7 import {KerosineManager}        from "./KerosineManager.sol";
8 import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";
9 
10 import {ERC20} from "@solmate/src/tokens/ERC20.sol";
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2-L10))

```solidity
File: src/core/Vault.kerosine.sol

2 pragma solidity =0.8.17; 
3 
4 import {IVaultManager}   from "../interfaces/IVaultManager.sol";
5 import {KerosineManager} from "./KerosineManager.sol";
6 import {IVault}          from "../interfaces/IVault.sol";
7 
8 import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
9 import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
10 import {Owned}           from "@solmate/src/auth/Owned.sol";
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2-L10))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

2 pragma solidity =0.8.17; 
3 
4 import {KerosineVault}        from "./Vault.kerosine.sol";
5 import {IVaultManager}        from "../interfaces/IVaultManager.sol";
6 import {Vault}                from "./Vault.sol";
7 import {Dyad}                 from "./Dyad.sol";
8 import {KerosineManager}      from "./KerosineManager.sol";
9 import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
10 import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
11 
12 import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
13 import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2-L13))

```solidity
File: src/core/VaultManagerV2.sol

2 pragma solidity =0.8.17; 
3 
4 import {DNft}            from "./DNft.sol";
5 import {Dyad}            from "./Dyad.sol";
6 import {Licenser}        from "./Licenser.sol";
7 import {Vault}           from "./Vault.sol";
8 import {IVaultManager}   from "../interfaces/IVaultManager.sol";
9 import {KerosineManager} from "../../src/core/KerosineManager.sol";
10 
11 import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
12 import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
13 import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
14 import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
15 import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2-L15))

</details>

### [NC&#x2011;22] Incorrect withdraw declaration
If the `withdraw` function is expected to return a bool to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions.

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {
```
([32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37))

```solidity
File: src/core/VaultManagerV2.sol

134   function withdraw( 
135     uint    id,
136     address vault,
137     uint    amount,
138     address to
139   ) 
140     public
141       isDNftOwner(id)
142   {
```
([134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L142))

</details>

### [NC&#x2011;23] Invalid NatSpec comment style
NatSpec [must](https://docs.soliditylang.org/en/latest/natspec-format.html#documentation-example) begin with `///`, or use the `/* ... */` syntax.


<i>There is one instance of this issue:</i>

```solidity
File: src/staking/KerosineDenominator.sol

18     // @dev: We subtract all the Kerosene in the multi-sig. 
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L18))

### [NC&#x2011;24] It is best practice to use linear inheritance
In Solidity, complex inheritance structures can obfuscate code understanding, introducing potential security risks. Multiple inheritance, especially with overlapping function names or state variables, can cause unintentional overrides or ambiguous behavior. Resolution: Strive for linear and simple inheritance chains. Avoid diamond or circular inheritance patterns. Clearly document the purpose and relationships of base contracts, ensuring that overrides are intentional. Tools like Remix or Hardhat can visualize inheritance chains, assisting in verification. Keeping inheritance streamlined aids in better code readability, reduces potential errors, and ensures smoother audits and upgrades.

<details>
<summary><i>There are 2 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17))

</details>

### [NC&#x2011;25] Large or complicated code bases should implement invariant tests
Large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts, should implement [invariant fuzzing tests](https://medium.com/coinmonks/smart-contract-fuzzing-d9b88e0b0a05). Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers, with properly and extensively-written invariants, can close this testing gap significantly.

### [NC&#x2011;26] Minting to the zero address should be avoided
Minting tokens to the zero address in Solidity is a potential pitfall. The zero address (0x0) is commonly used as a default value and sending tokens there effectively burns them, leading to unintended token loss. To prevent this, include a check in the minting function to ensure the target address is not zero. Using OpenZeppelin's Address library with the requireNonZero function simplifies this check and enhances security.


<i>There is one instance of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

156   function mintDyad( 
157     uint    id,
158     uint    amount,
159     address to
160   )
161     external 
162       isDNftOwner(id)
163   {
164     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
165     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
166     dyad.mint(id, to, amount);
167     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
168     emit MintDyad(id, amount, to);
169   }
```
([156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169))

### [NC&#x2011;27] State variable assignments are missing checks for uints
<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

43     id2asset[id] += amount; 

55     id2asset[from] -= amount; 
56     id2asset[to]   += amount;
```
([43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L43), [55](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L55-L56))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

38     id2asset[id] -= amount; 
```
([38](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L38))

</details>

### [NC&#x2011;28] NatSpec documentation for `constructor` is missing
<details>
<summary><i>There are 5 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

17   constructor( 
18     IVaultManager   _vaultManager,
19     ERC20           _asset, 
20     KerosineManager _kerosineManager
21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21))

```solidity
File: src/core/Vault.kerosine.sol

26   constructor( 
27     IVaultManager   _vaultManager,
28     ERC20           _asset, 
29     KerosineManager _kerosineManager 
30   ) {
```
([26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

21   constructor( 
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
26   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26))

```solidity
File: src/core/VaultManagerV2.sol

49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53))

```solidity
File: src/staking/KerosineDenominator.sol

11   constructor( 
12     Kerosine _kerosine
13   ) {
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13))

</details>

### [NC&#x2011;29] Constructors should have `@notice` tags
<details>
<summary><i>There are 5 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

17   constructor( 
18     IVaultManager   _vaultManager,
19     ERC20           _asset, 
20     KerosineManager _kerosineManager
21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21))

```solidity
File: src/core/Vault.kerosine.sol

26   constructor( 
27     IVaultManager   _vaultManager,
28     ERC20           _asset, 
29     KerosineManager _kerosineManager 
30   ) {
```
([26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

21   constructor( 
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
26   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26))

```solidity
File: src/core/VaultManagerV2.sol

49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53))

```solidity
File: src/staking/KerosineDenominator.sol

11   constructor( 
12     Kerosine _kerosine
13   ) {
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13))

</details>

### [NC&#x2011;30] Contract declarations should have `@author` tags
<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

6  
7 contract KerosineManager is Owned(msg.sender) {
8   error TooManyVaults();
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L6-L8))

```solidity
File: src/core/Vault.kerosine.bounded.sol

11  
12 contract BoundedKerosineVault is KerosineVault {
13   error NotWithdrawable(uint id, address to, uint amount);
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.sol

11  
12 abstract contract KerosineVault is IVault, Owned(msg.sender) {
13   using SafeTransferLib for ERC20;
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

14  
15 contract UnboundedKerosineVault is KerosineVault {
16   using SafeTransferLib for ERC20;
```
([14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L14-L16))

```solidity
File: src/core/VaultManagerV2.sol

16  
17 contract VaultManagerV2 is IVaultManager, Initializable {
18   using EnumerableSet     for EnumerableSet.AddressSet;
```
([16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L16-L18))

```solidity
File: src/staking/KerosineDenominator.sol

6  
7 contract KerosineDenominator is Parameters {
8 
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L6-L8))

</details>

### [NC&#x2011;31] Contract declarations should have `@dev` tags
<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

6  
7 contract KerosineManager is Owned(msg.sender) {
8   error TooManyVaults();
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L6-L8))

```solidity
File: src/core/Vault.kerosine.bounded.sol

11  
12 contract BoundedKerosineVault is KerosineVault {
13   error NotWithdrawable(uint id, address to, uint amount);
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.sol

11  
12 abstract contract KerosineVault is IVault, Owned(msg.sender) {
13   using SafeTransferLib for ERC20;
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

14  
15 contract UnboundedKerosineVault is KerosineVault {
16   using SafeTransferLib for ERC20;
```
([14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L14-L16))

```solidity
File: src/core/VaultManagerV2.sol

16  
17 contract VaultManagerV2 is IVaultManager, Initializable {
18   using EnumerableSet     for EnumerableSet.AddressSet;
```
([16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L16-L18))

```solidity
File: src/staking/KerosineDenominator.sol

6  
7 contract KerosineDenominator is Parameters {
8 
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L6-L8))

</details>

### [NC&#x2011;32] Contract declarations should have `@notice` tags
`@notice` is used to explain to end users what the contract does, and the compiler interprets `///` or `/**` comments as this tag if one was't explicitly provided

<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
8   error TooManyVaults();
9   error VaultAlreadyAdded();
10   error VaultNotFound();
11 
12   using EnumerableSet for EnumerableSet.AddressSet;
13 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7-L13))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
13   error NotWithdrawable(uint id, address to, uint amount);
14 
15   UnboundedKerosineVault public unboundedKerosineVault;
16 
17   constructor(
18     IVaultManager   _vaultManager,
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12-L18))

```solidity
File: src/core/Vault.kerosine.sol

12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
13   using SafeTransferLib for ERC20;
14 
15   IVaultManager   public immutable vaultManager;
16   ERC20           public immutable asset;
17   KerosineManager public immutable kerosineManager;
18 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12-L18))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15 contract UnboundedKerosineVault is KerosineVault { 
16   using SafeTransferLib for ERC20;
17 
18   Dyad                 public immutable dyad;
19   KerosineDenominator  public kerosineDenominator;
20 
21   constructor(
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15-L21))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
18   using EnumerableSet     for EnumerableSet.AddressSet;
19   using FixedPointMathLib for uint;
20   using SafeTransferLib   for ERC20;
21 
22   uint public constant MAX_VAULTS          = 5;
23   uint public constant MAX_VAULTS_KEROSENE = 5;
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L23))

```solidity
File: src/staking/KerosineDenominator.sol

7 contract KerosineDenominator is Parameters { 
8 
9   Kerosine public kerosine;
10 
11   constructor(
12     Kerosine _kerosine
13   ) {
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L13))

</details>

### [NC&#x2011;33] Contract declarations should have `@title` tags
<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

6  
7 contract KerosineManager is Owned(msg.sender) {
8   error TooManyVaults();
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L6-L8))

```solidity
File: src/core/Vault.kerosine.bounded.sol

11  
12 contract BoundedKerosineVault is KerosineVault {
13   error NotWithdrawable(uint id, address to, uint amount);
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.sol

11  
12 abstract contract KerosineVault is IVault, Owned(msg.sender) {
13   using SafeTransferLib for ERC20;
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L11-L13))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

14  
15 contract UnboundedKerosineVault is KerosineVault {
16   using SafeTransferLib for ERC20;
```
([14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L14-L16))

```solidity
File: src/core/VaultManagerV2.sol

16  
17 contract VaultManagerV2 is IVaultManager, Initializable {
18   using EnumerableSet     for EnumerableSet.AddressSet;
```
([16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L16-L18))

```solidity
File: src/staking/KerosineDenominator.sol

6  
7 contract KerosineDenominator is Parameters {
8 
```
([6](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L6-L8))

</details>

### [NC&#x2011;34] Contract declarations should have NatSpec descriptions
It is recommended that Solidity libraries and contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
8   error TooManyVaults();
9   error VaultAlreadyAdded();
10   error VaultNotFound();
11 
12   using EnumerableSet for EnumerableSet.AddressSet;
13 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7-L13))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
13   error NotWithdrawable(uint id, address to, uint amount);
14 
15   UnboundedKerosineVault public unboundedKerosineVault;
16 
17   constructor(
18     IVaultManager   _vaultManager,
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12-L18))

```solidity
File: src/core/Vault.kerosine.sol

12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
13   using SafeTransferLib for ERC20;
14 
15   IVaultManager   public immutable vaultManager;
16   ERC20           public immutable asset;
17   KerosineManager public immutable kerosineManager;
18 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12-L18))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15 contract UnboundedKerosineVault is KerosineVault { 
16   using SafeTransferLib for ERC20;
17 
18   Dyad                 public immutable dyad;
19   KerosineDenominator  public kerosineDenominator;
20 
21   constructor(
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15-L21))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
18   using EnumerableSet     for EnumerableSet.AddressSet;
19   using FixedPointMathLib for uint;
20   using SafeTransferLib   for ERC20;
21 
22   uint public constant MAX_VAULTS          = 5;
23   uint public constant MAX_VAULTS_KEROSENE = 5;
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L23))

```solidity
File: src/staking/KerosineDenominator.sol

7 contract KerosineDenominator is Parameters { 
8 
9   Kerosine public kerosine;
10 
11   constructor(
12     Kerosine _kerosine
13   ) {
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L13))

</details>

### [NC&#x2011;35] Errors should have `@notice` tags
The `@notice` is used to explain to users what the error does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

8   error TooManyVaults(); 
9   error VaultAlreadyAdded();
10   error VaultNotFound();
```
([8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L8-L10))

```solidity
File: src/core/Vault.kerosine.bounded.sol

13   error NotWithdrawable(uint id, address to, uint amount); 
```
([13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13))

</details>

### [NC&#x2011;36] ErrorModifier declarations should have NatSpec descriptions
It is recommended that errors are fully annotated using NatSpec. It is clearly stated in the Solidity official documentation.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

8   error TooManyVaults(); 
9   error VaultAlreadyAdded();
10   error VaultNotFound();
```
([8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L8-L10))

```solidity
File: src/core/Vault.kerosine.bounded.sol

13   error NotWithdrawable(uint id, address to, uint amount); 
```
([13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13))

</details>

### [NC&#x2011;37] Error missing NatSpec `@dev` tag
<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
8   error TooManyVaults();
9   error VaultAlreadyAdded();
10   error VaultNotFound();
11 
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7-L11))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
13   error NotWithdrawable(uint id, address to, uint amount);
14 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12-L14))

</details>

### [NC&#x2011;38] Error declaration missing NatSpec `@param` tag

<i>There is one instance of this issue:</i>

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit all error parameters
13   error NotWithdrawable(uint id, address to, uint amount); 
```
([13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13))

### [NC&#x2011;39] File is missing NatSpec
<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L1))

```solidity
File: src/core/Vault.kerosine.bounded.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L1))

```solidity
File: src/core/Vault.kerosine.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L1))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L1))

```solidity
File: src/core/VaultManagerV2.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L1))

```solidity
File: src/staking/KerosineDenominator.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L1))

</details>

### [NC&#x2011;40] Functions should have `@notice` tags
The `@notice` is used to explain to users what the function does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

<details>
<summary><i>There are 24 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

18   function add( 
19     address vault
20   ) 
21     external 
22       onlyOwner
23   {

28   function remove( 
29     address vault
30   ) 
31     external 
32       onlyOwner
33   {

37   function getVaults()  
38     external 
39     view 
40     returns (address[] memory) {

44   function isLicensed( 
45     address vault
46   ) 
47     external 
48     view 
49     returns (bool) {
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L33), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44-L49))

```solidity
File: src/core/Vault.kerosine.bounded.sol

23   function setUnboundedKerosineVault( 
24     UnboundedKerosineVault _unboundedKerosineVault
25   )
26     external
27     onlyOwner
28   {

32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {

44   function assetPrice()  
45     public 
46     view 
47     override
48     returns (uint) {
```
([23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48))

```solidity
File: src/core/Vault.kerosine.sol

36   function deposit( 
37     uint id,
38     uint amount
39   )
40     public 
41       onlyVaultManager
42   {

47   function move( 
48     uint from,
49     uint to,
50     uint amount
51   )
52     external
53       onlyVaultManager
54   {

60   function getUsdValue( 
61     uint id
62   )
63     public
64     view 
65     returns (uint) {

69   function assetPrice()  
```
([36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60-L65), [69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {

43   function setDenominator(KerosineDenominator _kerosineDenominator)  
44     external 
45       onlyOwner
46   {

50   function assetPrice()  
51     public 
52     view 
53     override
54     returns (uint) {
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54))

```solidity
File: src/core/VaultManagerV2.sol

59   function setKeroseneManager(KerosineManager _keroseneManager)  
60     external
61       initializer 
62     {

80   function addKerosene( 
81       uint    id,
82       address vault
83   ) 
84     external
85       isDNftOwner(id)
86   {

106   function removeKerosene( 
107       uint    id,
108       address vault
109   ) 
110     external
111       isDNftOwner(id)
112   {

230   function collatRatio( 
231     uint id
232   )
233     public 
234     view
235     returns (uint) {

241   function getTotalUsdValue( 
242     uint id
243   ) 
244     public 
245     view
246     returns (uint) {

250   function getNonKeroseneValue( 
251     uint id
252   ) 
253     public 
254     view
255     returns (uint) {

269   function getKeroseneValue( 
270     uint id
271   ) 
272     public 
273     view
274     returns (uint) {

290   function getVaults( 
291     uint id
292   ) 
293     external 
294     view 
295     returns (address[] memory) {

299   function hasVault( 
300     uint    id,
301     address vault
302   ) 
303     external 
304     view 
305     returns (bool) {
```
([59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L62), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L86), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L112), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299-L305))

```solidity
File: src/staking/KerosineDenominator.sol

17   function denominator() external view returns (uint) { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17))

</details>

### [NC&#x2011;41] NatSpec documentation for function is missing
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 24 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

18   function add( 

28   function remove( 

37   function getVaults()  

44   function isLicensed( 
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44))

```solidity
File: src/core/Vault.kerosine.bounded.sol

23   function setUnboundedKerosineVault( 

32   function withdraw( 

44   function assetPrice()  
```
([23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44))

```solidity
File: src/core/Vault.kerosine.sol

36   function deposit( 

47   function move( 

60   function getUsdValue( 

69   function assetPrice()  
```
([36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30   function withdraw( 

43   function setDenominator(KerosineDenominator _kerosineDenominator)  

50   function assetPrice()  
```
([30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50))

```solidity
File: src/core/VaultManagerV2.sol

59   function setKeroseneManager(KerosineManager _keroseneManager)  

80   function addKerosene( 

106   function removeKerosene( 

230   function collatRatio( 

241   function getTotalUsdValue( 

250   function getNonKeroseneValue( 

269   function getKeroseneValue( 

290   function getVaults( 

299   function hasVault( 
```
([59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299))

```solidity
File: src/staking/KerosineDenominator.sol

17   function denominator() external view returns (uint) { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17))

</details>

### [NC&#x2011;42] Functions missing NatSpec `@dev` tag
<details>
<summary><i>There are 37 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

17  
18   function add(
19     address vault

27  
28   function remove(
29     address vault

36  
37   function getVaults() 
38     external 

43  
44   function isLicensed(
45     address vault
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L17-L19), [27](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L27-L29), [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L36-L38), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L43-L45))

```solidity
File: src/core/Vault.kerosine.bounded.sol

16  
17   constructor(
18     IVaultManager   _vaultManager,

22  
23   function setUnboundedKerosineVault(
24     UnboundedKerosineVault _unboundedKerosineVault

31  
32   function withdraw(
33     uint    id,

43  
44   function assetPrice() 
45     public 
```
([16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L16-L18), [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L22-L24), [31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L31-L33), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L43-L45))

```solidity
File: src/core/Vault.kerosine.sol

25  
26   constructor(
27     IVaultManager   _vaultManager,

35  
36   function deposit(
37     uint id,

46  
47   function move(
48     uint from,

59  
60   function getUsdValue(
61     uint id

68  
69   function assetPrice() 
70     public 
```
([25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L25-L27), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L35-L37), [46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L46-L48), [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L59-L61), [68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L68-L70))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

20  
21   constructor(
22       IVaultManager   _vaultManager,

29  
30   function withdraw(
31     uint    id,

42  
43   function setDenominator(KerosineDenominator _kerosineDenominator) 
44     external 

49  
50   function assetPrice() 
51     public 
```
([20](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L20-L22), [29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L29-L31), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L42-L44), [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L49-L51))

```solidity
File: src/core/VaultManagerV2.sol

48  
49   constructor(
50     DNft          _dNft,

58  
59   function setKeroseneManager(KerosineManager _keroseneManager) 
60     external

66   /// @inheritdoc IVaultManager 
67   function add(
68       uint    id,

79  
80   function addKerosene(
81       uint    id,

93   /// @inheritdoc IVaultManager 
94   function remove(
95       uint    id,

105  
106   function removeKerosene(
107       uint    id,

118   /// @inheritdoc IVaultManager 
119   function deposit(
120     uint    id,

133   /// @inheritdoc IVaultManager 
134   function withdraw(
135     uint    id,

155   /// @inheritdoc IVaultManager 
156   function mintDyad(
157     uint    id,

171   /// @inheritdoc IVaultManager 
172   function burnDyad(
173     uint id,

183   /// @inheritdoc IVaultManager 
184   function redeemDyad(
185     uint    id,

204   /// @inheritdoc IVaultManager 
205   function liquidate(
206     uint id,

229  
230   function collatRatio(
231     uint id

240  
241   function getTotalUsdValue(
242     uint id

249  
250   function getNonKeroseneValue(
251     uint id

268  
269   function getKeroseneValue(
270     uint id

289  
290   function getVaults(
291     uint id

298  
299   function hasVault(
300     uint    id,
```
([48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L48-L50), [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L58-L60), [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L66-L68), [79](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L79-L81), [93](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L93-L95), [105](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L105-L107), [118](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L118-L120), [133](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L133-L135), [155](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L155-L157), [171](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L171-L173), [183](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L183-L185), [204](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L204-L206), [229](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L229-L231), [240](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L240-L242), [249](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L249-L251), [268](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L268-L270), [289](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L289-L291), [298](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L298-L300))

```solidity
File: src/staking/KerosineDenominator.sol

10  
11   constructor(
12     Kerosine _kerosine

16  
17   function denominator() external view returns (uint) {
18     // @dev: We subtract all the Kerosene in the multi-sig.
```
([10](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L10-L12), [16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L16-L18))

</details>

### [NC&#x2011;43] Functions missing NatSpec `@param` tag
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 24 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

// @audit all function parameters
18   function add( 
19     address vault
20   ) 
21     external 
22       onlyOwner
23   {

// @audit all function parameters
28   function remove( 
29     address vault
30   ) 
31     external 
32       onlyOwner
33   {

// @audit all function parameters
44   function isLicensed( 
45     address vault
46   ) 
47     external 
48     view 
49     returns (bool) {
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L33), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44-L49))

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit all function parameters
17   constructor( 
18     IVaultManager   _vaultManager,
19     ERC20           _asset, 
20     KerosineManager _kerosineManager
21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

// @audit all function parameters
23   function setUnboundedKerosineVault( 
24     UnboundedKerosineVault _unboundedKerosineVault
25   )
26     external
27     onlyOwner
28   {

// @audit all function parameters
32   function withdraw( 
33     uint    id,
34     address to,
35     uint    amount
36   ) 
37     external 
38     view
39       onlyVaultManager
40   {
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21), [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L40))

```solidity
File: src/core/Vault.kerosine.sol

// @audit all function parameters
26   constructor( 
27     IVaultManager   _vaultManager,
28     ERC20           _asset, 
29     KerosineManager _kerosineManager 
30   ) {

// @audit all function parameters
36   function deposit( 
37     uint id,
38     uint amount
39   )
40     public 
41       onlyVaultManager
42   {

// @audit all function parameters
47   function move( 
48     uint from,
49     uint to,
50     uint amount
51   )
52     external
53       onlyVaultManager
54   {

// @audit all function parameters
60   function getUsdValue( 
61     uint id
62   )
63     public
64     view 
65     returns (uint) {
```
([26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30), [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36-L42), [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47-L54), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60-L65))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit all function parameters
21   constructor( 
22       IVaultManager   _vaultManager,
23       ERC20           _asset, 
24       Dyad            _dyad, 
25       KerosineManager _kerosineManager
26   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {

// @audit all function parameters
30   function withdraw( 
31     uint    id,
32     address to,
33     uint    amount
34   ) 
35     external 
36       onlyVaultManager
37   {

// @audit all function parameters
43   function setDenominator(KerosineDenominator _kerosineDenominator)  
44     external 
45       onlyOwner
46   {
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26), [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46))

```solidity
File: src/core/VaultManagerV2.sol

// @audit all function parameters
49   constructor( 
50     DNft          _dNft,
51     Dyad          _dyad,
52     Licenser      _licenser
53   ) {

// @audit all function parameters
59   function setKeroseneManager(KerosineManager _keroseneManager)  
60     external
61       initializer 
62     {

// @audit all function parameters
80   function addKerosene( 
81       uint    id,
82       address vault
83   ) 
84     external
85       isDNftOwner(id)
86   {

// @audit all function parameters
106   function removeKerosene( 
107       uint    id,
108       address vault
109   ) 
110     external
111       isDNftOwner(id)
112   {

// @audit all function parameters
230   function collatRatio( 
231     uint id
232   )
233     public 
234     view
235     returns (uint) {

// @audit all function parameters
241   function getTotalUsdValue( 
242     uint id
243   ) 
244     public 
245     view
246     returns (uint) {

// @audit all function parameters
250   function getNonKeroseneValue( 
251     uint id
252   ) 
253     public 
254     view
255     returns (uint) {

// @audit all function parameters
269   function getKeroseneValue( 
270     uint id
271   ) 
272     public 
273     view
274     returns (uint) {

// @audit all function parameters
290   function getVaults( 
291     uint id
292   ) 
293     external 
294     view 
295     returns (address[] memory) {

// @audit all function parameters
299   function hasVault( 
300     uint    id,
301     address vault
302   ) 
303     external 
304     view 
305     returns (bool) {
```
([49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53), [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L62), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L86), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L112), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299-L305))

```solidity
File: src/staking/KerosineDenominator.sol

// @audit all function parameters
11   constructor( 
12     Kerosine _kerosine
13   ) {
```
([11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13))

</details>

### [NC&#x2011;44] Functions missing NatSpec `@return` tag
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 14 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

// @audit all function parameters
37   function getVaults()  
38     external 
39     view 
40     returns (address[] memory) {

// @audit all function parameters
44   function isLicensed( 
45     address vault
46   ) 
47     external 
48     view 
49     returns (bool) {
```
([37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37-L40), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44-L49))

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit all function parameters
44   function assetPrice()  
45     public 
46     view 
47     override
48     returns (uint) {
```
([44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48))

```solidity
File: src/core/Vault.kerosine.sol

// @audit all function parameters
60   function getUsdValue( 
61     uint id
62   )
63     public
64     view 
65     returns (uint) {

// @audit all function parameters
69   function assetPrice()  
```
([60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60-L65), [69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit all function parameters
50   function assetPrice()  
51     public 
52     view 
53     override
54     returns (uint) {
```
([50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54))

```solidity
File: src/core/VaultManagerV2.sol

// @audit  all function parameters
184   function redeemDyad( 
185     uint    id,
186     address vault,
187     uint    amount,
188     address to
189   )
190     external 
191       isDNftOwner(id)
192     returns (uint) { 

// @audit all function parameters
230   function collatRatio( 
231     uint id
232   )
233     public 
234     view
235     returns (uint) {

// @audit all function parameters
241   function getTotalUsdValue( 
242     uint id
243   ) 
244     public 
245     view
246     returns (uint) {

// @audit all function parameters
250   function getNonKeroseneValue( 
251     uint id
252   ) 
253     public 
254     view
255     returns (uint) {

// @audit all function parameters
269   function getKeroseneValue( 
270     uint id
271   ) 
272     public 
273     view
274     returns (uint) {

// @audit all function parameters
290   function getVaults( 
291     uint id
292   ) 
293     external 
294     view 
295     returns (address[] memory) {

// @audit all function parameters
299   function hasVault( 
300     uint    id,
301     address vault
302   ) 
303     external 
304     view 
305     returns (bool) {
```
([184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L192), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230-L235), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241-L246), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L255), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L274), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290-L295), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299-L305))

```solidity
File: src/staking/KerosineDenominator.sol

// @audit all function parameters
17   function denominator() external view returns (uint) { 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17))

</details>

### [NC&#x2011;45] Modifier declarations should have NatSpec descriptions
It is recommended that modifiers are fully annotated using NatSpec.

<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

21   modifier onlyVaultManager() { 
```
([21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21))

```solidity
File: src/core/VaultManagerV2.sol

39   modifier isDNftOwner(uint id) { 

42   modifier isValidDNft(uint id) { 

45   modifier isLicensed(address vault) { 
```
([39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45))

</details>

### [NC&#x2011;46] Modifier missing NatSpec `@dev` tag
<details>
<summary><i>There are 4 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

20  
21   modifier onlyVaultManager() {
22     if (msg.sender != address(vaultManager)) revert NotVaultManager();
```
([20](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L20-L22))

```solidity
File: src/core/VaultManagerV2.sol

38  
39   modifier isDNftOwner(uint id) {
40     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41   }
42   modifier isValidDNft(uint id) {
43     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44   }
45   modifier isLicensed(address vault) {
46     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
```
([38](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L38-L46))

</details>

### [NC&#x2011;47] Modifier missing NatSpec `@param` tag
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.


<i>There are 3 instaces of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

// @audit all modifier parameters
39   modifier isDNftOwner(uint id) { 

// @audit all modifier parameters
42   modifier isValidDNft(uint id) { 

// @audit all modifier parameters
45   modifier isLicensed(address vault) { 
```
([39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45))

### [NC&#x2011;48] Names of `private`/`internal` state variables should be prefixed with an underscore
According to the Solidity Style Guide, Non-`external`/`public` state variables should begin with an <a href="https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables">underscore</a>.

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

// @audit _vaults
16   EnumerableSet.AddressSet private vaults; 
```
([16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16))

```solidity
File: src/core/VaultManagerV2.sol

// @audit _vaults
34   mapping (uint => EnumerableSet.AddressSet) internal vaults;  
// @audit _vaultsKerosene
35   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
```
([34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34-L35))

</details>

### [NC&#x2011;49] Update project dependencies to their latest versions
**forge-std** - Latest: 1.8.1 - Current: 1.2.0**openzeppelin-contracts** - Latest: 5.0.2 - Current: 4.8.0**solmate** - Latest: 6 - Current: 6.6.2


<i>There is one instance of this issue:</i>

```solidity
File: src/staking/KerosineDenominator.sol

1 // SPDX-License-Identifier: MIT 
```
([1](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L1))

### [NC&#x2011;50] Use the latest Solidity version (0.8.19 for L2s)
The latest version of Solidity is 0.8.25

<details>
<summary><i>There are 6 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L2))

```solidity
File: src/core/Vault.kerosine.bounded.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2))

```solidity
File: src/core/Vault.kerosine.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2))

```solidity
File: src/core/VaultManagerV2.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2))

```solidity
File: src/staking/KerosineDenominator.sol

2 pragma solidity =0.8.17; 
```
([2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L2))

</details>

### [NC&#x2011;51] Consider splitting long calculations
The longer a string of operations is, the harder it is to understand it. Consider splitting the full calculation into more steps, with more descriptive temporary variable names, and add extensive comments.

<details>
<summary><i>There are 3 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

60         tvl += vault.asset().balanceOf(address(vault))  
61                 * vault.assetPrice() * 1e18
62                 / (10**vault.asset().decimals()) 
63                 / (10**vault.oracle().decimals());
```
([60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60-L63))

```solidity
File: src/core/VaultManagerV2.sol

146     uint value = amount * _vault.assetPrice()  
147                   * 1e18 
148                   / 10**_vault.oracle().decimals() 
149                   / 10**_vault.asset().decimals();

195       uint asset = amount  
196                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197                     / _vault.assetPrice() 
198                     / 1e18;
```
([146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L149), [195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L198))

</details>

### [NC&#x2011;52] Public variable declarations should have NatSpec descriptions
It is [recommended](https://docs.soliditylang.org/en/v0.8.20/natspec-format.html#tags) to use the NatSpec tags `@notice`, `@dev`, `@return`, `@inheritdoc` for public state variables.

<details>
<summary><i>There are 19 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

14   uint public constant MAX_VAULTS = 10; 

16   EnumerableSet.AddressSet private vaults; 
```
([14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14), [16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16))

```solidity
File: src/core/Vault.kerosine.bounded.sol

15   UnboundedKerosineVault public unboundedKerosineVault; 
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L15))

```solidity
File: src/core/Vault.kerosine.sol

15   IVaultManager   public immutable vaultManager; 
16   ERC20           public immutable asset;
17   KerosineManager public immutable kerosineManager;

19   mapping(uint => uint) public id2asset; 
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15-L17), [19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

18   Dyad                 public immutable dyad; 
19   KerosineDenominator  public kerosineDenominator;
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18-L19))

```solidity
File: src/core/VaultManagerV2.sol

22   uint public constant MAX_VAULTS          = 5; 
23   uint public constant MAX_VAULTS_KEROSENE = 5;

28   DNft     public immutable dNft; 
29   Dyad     public immutable dyad;
30   Licenser public immutable vaultLicenser;

32   KerosineManager public keroseneManager; 

34   mapping (uint => EnumerableSet.AddressSet) internal vaults;  
35   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37   mapping (uint => uint) public idToBlockOfLastDeposit; 
```
([22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22-L23), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28-L30), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L32), [34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37))

```solidity
File: src/staking/KerosineDenominator.sol

9   Kerosine public kerosine; 
```
([9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9))

</details>

### [NC&#x2011;53] Style guide: `mapping` definitions do not follow the Solidity Style Guide
See the [mappings](https://docs.soliditylang.org/en/latest/style-guide.html#mappings) section of the Solidity Style Guide


<i>There are 3 instaces of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

34   mapping (uint => EnumerableSet.AddressSet) internal vaults;  
35   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37   mapping (uint => uint) public idToBlockOfLastDeposit; 
```
([34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37))

### [NC&#x2011;54] Top-level declarations should be separated by at least two lines
<details>
<summary><i>There are 33 instances (click to view)</i></summary>

```solidity
File: src/core/KerosineManager.sol

7 contract KerosineManager is Owned(msg.sender) { 
8   error TooManyVaults();

26   } 
27 
28   function remove(

35   } 
36 
37   function getVaults() 

42   } 
43 
44   function isLicensed(
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7-L8), [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L26-L28), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L35-L37), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L42-L44))

```solidity
File: src/core/Vault.kerosine.bounded.sol

12 contract BoundedKerosineVault is KerosineVault { 
13   error NotWithdrawable(uint id, address to, uint amount);
14 
15   UnboundedKerosineVault public unboundedKerosineVault;
16 
17   constructor(

21   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {} 
22 
23   function setUnboundedKerosineVault(

30   } 
31 
32   function withdraw(

42   } 
43 
44   function assetPrice() 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12-L17), [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L21-L23), [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L30-L32), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L42-L44))

```solidity
File: src/core/Vault.kerosine.sol

12 abstract contract KerosineVault is IVault, Owned(msg.sender) { 
13   using SafeTransferLib for ERC20;
14 
15   IVaultManager   public immutable vaultManager;

24   } 
25 
26   constructor(

34   } 
35 
36   function deposit(

45   } 
46 
47   function move(

58   } 
59 
60   function getUsdValue(

67   } 
68 
69   function assetPrice() 

73     returns (uint);  
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12-L15), [24](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L24-L26), [34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L34-L36), [45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L45-L47), [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L58-L60), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L67-L69), [73](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L73-L19))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15 contract UnboundedKerosineVault is KerosineVault { 
16   using SafeTransferLib for ERC20;
17 
18   Dyad                 public immutable dyad;

28   } 
29 
30   function withdraw(

41   } 
42 
43   function setDenominator(KerosineDenominator _kerosineDenominator) 

48   } 
49 
50   function assetPrice() 
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15-L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L28-L30), [41](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L41-L43), [48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L48-L50))

```solidity
File: src/core/VaultManagerV2.sol

17 contract VaultManagerV2 is IVaultManager, Initializable { 
18   using EnumerableSet     for EnumerableSet.AddressSet;
19   using FixedPointMathLib for uint;
20   using SafeTransferLib   for ERC20;
21 
22   uint public constant MAX_VAULTS          = 5;

57   } 
58 
59   function setKeroseneManager(KerosineManager _keroseneManager) 

78   } 
79 
80   function addKerosene(

104   } 
105 
106   function removeKerosene(

228   } 
229 
230   function collatRatio(

239   } 
240 
241   function getTotalUsdValue(

248   } 
249 
250   function getNonKeroseneValue(

267   } 
268 
269   function getKeroseneValue(

297   } 
298 
299   function hasVault(

307   } 
```
([17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L22), [57](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L57-L59), [78](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L78-L80), [104](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L104-L106), [228](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L228-L230), [239](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L239-L241), [248](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L248-L250), [267](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L267-L269), [297](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L297-L299), [307](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L307-L34))

```solidity
File: src/staking/KerosineDenominator.sol

7 contract KerosineDenominator is Parameters { 
8 
9   Kerosine public kerosine;
10 
11   constructor(
```
([7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L11))

</details>

### [NC&#x2011;55] Unnecessary cast
The variable is being cast to its own type


<i>There is one instance of this issue:</i>

```solidity
File: src/core/VaultManagerV2.sol

// @audit vault
129     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount); 
```
([129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129))

### [NC&#x2011;56] Use `@inheritdoc` for overridden functions
<details>
<summary><i>There are 2 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

44   function assetPrice()  
45     public 
46     view 
47     override
48     returns (uint) {
```
([44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

50   function assetPrice()  
51     public 
52     view 
53     override
54     returns (uint) {
```
([50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54))

</details>

### [NC&#x2011;57] Variable names for `immutable`s should use CONSTANT_CASE
Immutables should be in uppercase as stated [Solidity style guide](https://docs.soliditylang.org/en/latest/style-guide.html#constants).

<details>
<summary><i>There are 7 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

15   IVaultManager   public immutable vaultManager; 
16   ERC20           public immutable asset;
17   KerosineManager public immutable kerosineManager;
```
([15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15-L17))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

18   Dyad                 public immutable dyad; 
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18))

```solidity
File: src/core/VaultManagerV2.sol

28   DNft     public immutable dNft; 
29   Dyad     public immutable dyad;
30   Licenser public immutable vaultLicenser;
```
([28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28-L30))

</details>

### [NC&#x2011;58] State and local variables should be named using lowerCamelCase
The Solidity style guide [says](https://docs.soliditylang.org/en/latest/style-guide.html#local-and-state-variable-names) to use mixedCase for local and state variable names. Note that while OpenZeppelin may not follow this advice, it still is the recommended way of naming variables.

<details>
<summary><i>There are 17 instances (click to view)</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

// @audit _vaultManager
18     IVaultManager   _vaultManager, 
// @audit _asset
19     ERC20           _asset, 
// @audit _kerosineManager
20     KerosineManager _kerosineManager

// @audit _unboundedKerosineVault
24     UnboundedKerosineVault _unboundedKerosineVault 
```
([18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L18-L20), [24](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L24))

```solidity
File: src/core/Vault.kerosine.sol

// @audit _vaultManager
27     IVaultManager   _vaultManager, 
// @audit _asset
28     ERC20           _asset, 
// @audit _kerosineManager
29     KerosineManager _kerosineManager 
```
([27](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L27-L29))

```solidity
File: src/core/Vault.kerosine.unbounded.sol

// @audit _vaultManager
22       IVaultManager   _vaultManager, 
// @audit _asset
23       ERC20           _asset, 
// @audit _dyad
24       Dyad            _dyad, 
// @audit _kerosineManager
25       KerosineManager _kerosineManager

// @audit _kerosineDenominator
43   function setDenominator(KerosineDenominator _kerosineDenominator)  
```
([22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L22-L25), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43))

```solidity
File: src/core/VaultManagerV2.sol

// @audit _dNft
50     DNft          _dNft, 
// @audit _dyad
51     Dyad          _dyad,
// @audit _licenser
52     Licenser      _licenser

// @audit _keroseneManager
59   function setKeroseneManager(KerosineManager _keroseneManager)  
```
([50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L50-L52), [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59))

```solidity
File: src/staking/KerosineDenominator.sol

// @audit _kerosine
12     Kerosine _kerosine 
```
([12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L12))

</details>

