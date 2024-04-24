




# Summary



## Identification Method

These issues were identified manually, not by the Code4rena 4naly3r bot.
In the manual analysis of the Solidity codebase, the following issues were identified:

- **8 Low-Risk Issues**
- **51 Non-Critical Issues**




### Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [[L001](#l001---loss-of-precision-due-to-division-by-large-numbers)] | Loss of precision due to division by large numbers | 1 |
| [[L002](#l002---upgradeable-contract-is-missing-a-__gap50-storage-variable-to-allow-for-new-storage-variables-in-later-versions)] | Upgradeable contract is missing a __gap[50] storage variable to allow for new storage variables in later versions | 1 |
| [[L003](#l003---constant-decimal-values)] | Constant decimal values | 5 |
| [[L004](#l004---constructor-contains-no-validation)] | Constructor contains no validation | 4 |
| [[L005](#l005---for-loops-in-public-or-external-functions-should-be-avoided-due-to-high-gas-costs-and-possible-dos)] | For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS | 1 |
| [[L006](#l006---contracts-are-not-using-their-oz-upgradeable-counterparts)] | Contracts are not using their OZ Upgradeable counterparts | 3 |
| [[L007](#l007---governance-functions-should-be-controlled-by-time-locks)] | Governance functions should be controlled by time locks | 4 |
| [[L008](#l008---unbounded-state-array-which-is-iterated-upon)] | Unbounded state array which is iterated upon | 3 |



### Non-critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [[NC001](#nc001---use-scientific-notation-eg-1e18-rather-than-exponentiation-eg-1018)] | Use scientific notation (e.g. 1e18) rather than exponentiation (e.g. 10**18) | 5 |
| [[NC002](#nc002---imports-could-be-organized-more-systematically)] | Imports could be organized more systematically | 4 |
| [[NC003](#nc003---constants-in-comparisons-should-appear-on-the-left-side)] | Constants in comparisons should appear on the left side | 4 |
| [[NC004](#nc004---events-may-be-emitted-out-of-order-due-to-reentrancy)] | Events may be emitted out of order due to reentrancy | 1 |
| [[NC005](#nc005---public-functions-not-called-by-the-contract-should-be-declared-external-instead)] | Public functions not called by the contract should be declared external instead | 2 |
| [[NC006](#nc006---constant-redefined-elsewhere)] | Constant redefined elsewhere | 2 |
| [[NC007](#nc007---multiple-addressid-mappings-can-be-combined-into-a-single-mapping-of-an-addressid-to-a-struct-for-readability)] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability | 1 |
| [[NC008](#nc008---variable-names-for-immutables-should-use-constant_case)] | Variable names for `immutable`s should use CONSTANT_CASE | 7 |
| [[NC009](#nc009---file-is-missing-natspec-comments)] | File is missing NatSpec comments | 5 |
| [[NC010](#nc010---function-declarations-should-have-natspec-descriptions)] | Function declarations should have NatSpec descriptions | 29 |
| [[NC011](#nc011---contract-declarations-should-have-notice-tags)] | Contract declarations should have `@notice` tags | 6 |
| [[NC012](#nc012---invalid-natspec-comment-style)] | Invalid NatSpec comment style | 1 |
| [[NC013](#nc013---error-declarations-should-have-natspec-descriptions)] | Error declarations should have NatSpec descriptions | 4 |
| [[NC014](#nc014---contracts-should-have-full-test-coverage)] | Contracts should have full test coverage | 1 |
| [[NC015](#nc015---large-or-complicated-code-bases-should-implement-invariant-tests)] | Large or complicated code bases should implement invariant tests | 1 |
| [[NC016](#nc016---consider-adding-a-deny-list)] | Consider adding a deny-list | 5 |
| [[NC017](#nc017---custom-error-has-no-error-details)] | Custom error has no error details | 3 |
| [[NC018](#nc018---contract-uses-both-requirerevert-as-well-as-custom-errors)] | Contract uses both `require()`/`revert()` as well as custom errors | 2 |
| [[NC019](#nc019---events-are-missing-sender-information)] | Events are missing sender information | 8 |
| [[NC020](#nc020---function-names-should-differ-to-make-the-code-more-readable)] | Function names should differ to make the code more readable | 14 |
| [[NC021](#nc021---it-is-standard-for-all-external-and-public-functions-to-be-override-from-an-interface)] | It is standard for all external and public functions to be override from an interface | 28 |
| [[NC022](#nc022---consider-adding-formal-verification-proofs)] | Consider adding formal verification proofs | 1 |
| [[NC023](#nc023---missing-timelock-for-critical-parameter-change)] | Missing timelock for critical parameter change | 3 |
| [[NC024](#nc024---setters-should-prevent-re-setting-of-the-same-value)] | Setters should prevent re-setting of the same value | 3 |
| [[NC025](#nc025---consider-splitting-long-calculations)] | Consider splitting long calculations | 2 |
| [[NC026](#nc026---use-of-override-is-unnecessary)] | Use of override is unnecessary | 2 |
| [[NC027](#nc027---unused-import)] | Unused import | 2 |
| [[NC028](#nc028---put-all-system-wide-constants-in-one-file)] | Put all system-wide constants in one file | 5 |
| [[NC029](#nc029---consider-adding-emergency-stop-functionality)] | Consider adding emergency-stop functionality | 3 |
| [[NC030](#nc030---unnecessary-cast)] | Unnecessary cast | 1 |
| [[NC031](#nc031---use-the-latest-solidity-prior-to-0820-if-on-l2s-for-deployment)] | Use the latest solidity (prior to 0.8.20 if on L2s) for deployment | 6 |
| [[NC032](#nc032---function-definitions-should-have-natspec-dev-annotations)] | Function definitions should have NatSpec @dev annotations | 37 |
| [[NC033](#nc033---function-definitions-should-have-natspec-notice-annotations)] | Function definitions should have NatSpec @notice annotations | 37 |
| [[NC034](#nc034---abstract-contract-declarations-should-have-natspec-title-annotations)] | Abstract contract declarations should have NatSpec @title annotations | 1 |
| [[NC035](#nc035---abstract-contract-declarations-should-have-natspec-author-annotations)] | Abstract contract declarations should have NatSpec @author annotations | 1 |
| [[NC036](#nc036---abstract-contract-declarations-should-have-natspec-notice-annotations)] | Abstract contract declarations should have NatSpec @notice annotations | 1 |
| [[NC037](#nc037---abstract-contract-declarations-should-have-natspec-dev-annotations)] | Abstract contract declarations should have Natspec @dev annotations | 1 |
| [[NC038](#nc038---modifier-definitions-should-have-natspec-notice-annotations)] | Modifier definitions should have Natspec @notice annotations | 4 |
| [[NC039](#nc039---modifier-definitions-should-have-natspec-dev-annotations)] | Modifier definitions should have Natspec @dev annotations | 4 |
| [[NC040](#nc040---contract-definitions-should-have-natspec-title-annotations)] | Contract definitions should have Natspec @title annotations | 5 |
| [[NC041](#nc041---contract-definitions-should-have-natspec-author-annotations)] | Contract definitions should have Natspec @author annotations | 5 |
| [[NC042](#nc042---contract-definitions-should-have-natspec-notice-annotations)] | Contract definitions should have Natspec @notice annotations | 5 |
| [[NC043](#nc043---contract-definitions-should-have-natspec-dev-annotations)] | Contract definitions should have Natspec @dev annotations | 5 |
| [[NC044](#nc044---state-variable-declarations-should-have-natspec-notice-annotations)] | State variable declarations should have Natspec @notice annotations | 21 |
| [[NC045](#nc045---state-variable-declarations-should-have-natspec-dev-annotations)] | State variable declarations should have Natspec @dev annotations | 21 |
| [[NC046](#nc046---functions-should-have-natspec-return-annotations)] | Functions should have Natspec @return annotations | 14 |
| [[NC047](#nc047---functions-should-have-natspec-param-annotations)] | Functions should have Natspec @param annotations | 36 |
| [[NC048](#nc048---missing-events-in-sensitive-functions)] | Missing events in sensitive functions | 3 |
| [[NC049](#nc049---if-statement-control-structures-do-not-comply-with-best-practices)] | If statement control structures do not comply with best practices | 24 |
| [[NC050](#nc050---a-event-should-be-emitted-if-a-non-immutable-state-variable-is-set-in-a-constructor)] | A event should be emitted if a non immutable state variable is set in a constructor | 1 |
| [[NC051](#nc052---defining-all-externalpublic-functions-in-contract-interfaces)] | Defining All External/Public Functions in Contract Interfaces | 5 |

Total: 413 instances over 51 issues



## L001 - Loss of precision due to division by large numbers:

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator.


```solidity
File: src/core/Vault.kerosine.unbounded.sol


67            return numerator * 1e8 / denominator;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67:67


## L002 - Upgradeable contract is missing a __gap[50] storage variable to allow for new storage variables in later versions:

This issue arises when an upgradeable contract doesn't include a __gap[50] storage variable. This variable is crucial for facilitating future upgrades and preserving storage layout.


```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17


## L003 - Constant decimal values:

The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations. Always retrieve and use the decimals() function from the token contract itself when performing calculations involving token amounts.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


66            return id2asset[id] * assetPrice() / 1e8;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L66:66

```solidity
File: src/core/Vault.kerosine.unbounded.sol


60              tvl += vault.asset().balanceOf(address(vault)) 
61                      * vault.assetPrice() * 1e18


67            return numerator * 1e8 / denominator;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67:67

```solidity
File: src/core/VaultManagerV2.sol


146         uint value = amount * _vault.assetPrice() 
147                       * 1e18 


195           uint asset = amount 
196                         * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197                         / _vault.assetPrice() 
198                         / 1e18;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195:198

</details>

## L004 - Constructor contains no validation:

In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


26        constructor(
27          IVaultManager   _vaultManager,
28          ERC20           _asset, 
29          KerosineManager _kerosineManager 
30        ) {
31          vaultManager    = _vaultManager;
32          asset           = _asset;
33          kerosineManager = _kerosineManager;
34        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26:34

```solidity
File: src/core/Vault.kerosine.unbounded.sol


21        constructor(
22            IVaultManager   _vaultManager,
23            ERC20           _asset, 
24            Dyad            _dyad, 
25            KerosineManager _kerosineManager
26        ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27            dyad = _dyad;
28        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21:28

```solidity
File: src/core/VaultManagerV2.sol


49        constructor(
50          DNft          _dNft,
51          Dyad          _dyad,
52          Licenser      _licenser
53        ) {
54          dNft          = _dNft;
55          dyad          = _dyad;
56          vaultLicenser = _licenser;
57        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49:57

```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(
12          Kerosine _kerosine
13        ) {
14          kerosine = _kerosine;
15        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11:15

</details>

## L005 - For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS:

In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly.


```solidity
File: src/core/VaultManagerV2.sol


205       function liquidate(
206         uint id,
207         uint to
208       ) 
209         external 
210           isValidDNft(id)
211           isValidDNft(to)
212         {
213           uint cr = collatRatio(id);
214           if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
215           dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
216     
217           uint cappedCr               = cr < 1e18 ? 1e18 : cr;
218           uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219           uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
220     
221           uint numberOfVaults = vaults[id].length();
222           for (uint i = 0; i < numberOfVaults; i++) {
223               Vault vault      = Vault(vaults[id].at(i));
224               uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225               vault.move(id, to, collateral);
226           }
227           emit Liquidate(id, msg.sender, to);
228       }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205:228

## L006 - Contracts are not using their OZ Upgradeable counterparts:

The non-upgradeable standard version of OpenZeppelin’s library is inherited/used by the contracts. It would be safer to use the upgradeable versions of the library contracts to avoid unexpected behavior.

Use the contracts from `@openzeppelin/contracts-upgradeable` instead of `@openzeppelin/contracts` where applicable. See https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/tree/master/contracts for a list of available upgradeable contracts


```solidity
File: src/core/KerosineManager.sol


4       import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L4:4

```solidity
File: src/core/VaultManagerV2.sol


14      import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";


15      import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L15:15

## L007 - Governance functions should be controlled by time locks:

Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/KerosineManager.sol


28        function remove(
29          address vault
30        ) 
31          external 
32            onlyOwner
33        {

18        function add(
19          address vault
20        ) 
21          external 
22            onlyOwner
23        {

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18:26

```solidity
File: src/core/Vault.kerosine.bounded.sol


23        function setUnboundedKerosineVault(
24          UnboundedKerosineVault _unboundedKerosineVault
25        )
26          external
27          onlyOwner
28        {

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23:30

```solidity
File: src/core/Vault.kerosine.unbounded.sol


43        function setDenominator(KerosineDenominator _kerosineDenominator) 
44          external 
45            onlyOwner
46        {

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43:48

</details>

## L008 - Unbounded state array which is iterated upon:

Iterating over an unbounded state array in Solidity can result in excessive gas consumption, especially if the array size exceeds the block gas limit. This issue commonly arises in tasks like token distribution. To address this, it is recommended to limit array sizes for iteration, consider alternative data structures like linked lists, adopt paginated processing for smaller batches over multiple transactions, or use a 'state array' with a separate index-tracking array to manage large datasets and avoid gas-related problems.


```solidity
File: src/core/VaultManagerV2.sol


223               Vault vault      = Vault(vaults[id].at(i));


259             Vault vault = Vault(vaults[id].at(i));


278             Vault vault = Vault(vaultsKerosene[id].at(i));


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L278:278




## Total: 52 Non-Critical Issues Identified



## NC001 - Use scientific notation (e.g. 1e18) rather than exponentiation (e.g. 10**18):

While the compiler knows to optimize away the exponentiation, it's still better coding practice to use idioms that do not require compiler optimization, if they exist.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol


62                      / (10**vault.asset().decimals()) 


63                      / (10**vault.oracle().decimals());


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L63:63

```solidity
File: src/core/VaultManagerV2.sol


148                       / 10**_vault.oracle().decimals() 


149                       / 10**_vault.asset().decimals();


196                         * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L196:196

</details>

## NC002 - Imports could be organized more systematically:

This issue arises when the contract's interface is not imported first, followed by each of the interfaces it uses, followed by all other files.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol


5       import {IVaultManager}          from "../interfaces/IVaultManager.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L5:5

```solidity
File: src/core/Vault.kerosine.sol


6       import {IVault}          from "../interfaces/IVault.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L6:6

```solidity
File: src/core/Vault.kerosine.unbounded.sol


5       import {IVaultManager}        from "../interfaces/IVaultManager.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L5:5

```solidity
File: src/core/VaultManagerV2.sol


8       import {IVaultManager}   from "../interfaces/IVaultManager.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L8:8

</details>

## NC003 - Constants in comparisons should appear on the left side:

This issue arises when constants in comparisons appear on the right side, which can lead to typo bugs.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/VaultManagerV2.sol


101         if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();


113         if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();


217           uint cappedCr               = cr < 1e18 ? 1e18 : cr;


237           if (_dyad == 0) return type(uint).max;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237:237

</details>

## NC004 Total: 52 Non-Critical Issues Identified - Events may be emitted out of order due to reentrancy:

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls


```solidity
File: src/core/Vault.kerosine.unbounded.sol


/// @audit safeTransfer() called before event
40          emit Withdraw(id, to, amount);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40:40

## NC005 - Public functions not called by the contract should be declared external instead:

Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from `external` to `public`.


```solidity
File: src/core/Vault.kerosine.sol


36        function deposit(
37          uint id,
38          uint amount
39        )
40          public 
41            onlyVaultManager
42        {
43          id2asset[id] += amount;
44          emit Deposit(id, amount);
45        }


60        function getUsdValue(
61          uint id
62        )
63          public
64          view 
65          returns (uint) {
66            return id2asset[id] * assetPrice() / 1e8;
67        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60:67

## NC006 - Constant redefined elsewhere:

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A cheap way to store constants in a single location is to create an internal constant in a library. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.


```solidity
File: src/core/VaultManagerV2.sol


  uint public constant MAX_VAULTS          = 5;

  Dyad     public immutable dyad;

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L29:29

## NC007 - Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability:

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related


```solidity
File: src/core/VaultManagerV2.sol


34        mapping (uint => EnumerableSet.AddressSet) internal vaults; 
35        mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
36      
37        mapping (uint => uint) public idToBlockOfLastDeposit;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34:37

## NC008 - Variable names for `immutable`s should use CONSTANT_CASE:

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE).


<details>
<summary>Click to show 7 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


15        IVaultManager   public immutable vaultManager;


16        ERC20           public immutable asset;


17        KerosineManager public immutable kerosineManager;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L17:17

```solidity
File: src/core/Vault.kerosine.unbounded.sol


18        Dyad                 public immutable dyad;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18:18

```solidity
File: src/core/VaultManagerV2.sol


28        DNft     public immutable dNft;


29        Dyad     public immutable dyad;


30        Licenser public immutable vaultLicenser;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L30:30

</details>

## NC009 - File is missing NatSpec comments:

The file does not contain any of the NatSpec comments (@inheritdoc, @param, @return, @notice), which are important for documentation and user confirmation.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


// SPDX-License-Identifier: MIT
pragma solidity =0.8.17;

import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Owned}         from "@solmate/src/auth/Owned.sol";

contract KerosineManager is Owned(msg.sender) {
  error TooManyVaults();
  error VaultAlreadyAdded();
  error VaultNotFound();

  using EnumerableSet for EnumerableSet.AddressSet;

  uint public constant MAX_VAULTS = 10;

  EnumerableSet.AddressSet private vaults;

  function add(
    address vault
  ) 
    external 
      onlyOwner
  {
    if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
    if (!vaults.add(vault))            revert VaultAlreadyAdded();
  }

  function remove(
    address vault
  ) 
    external 
      onlyOwner
  {
    if (!vaults.remove(vault)) revert VaultNotFound();
  }

  function getVaults() 
    external 
    view 
    returns (address[] memory) {
      return vaults.values();
  }

  function isLicensed(
    address vault
  ) 
    external 
    view 
    returns (bool) {
      return vaults.contains(vault);
  }
}


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L1:1

```solidity
File: src/core/Vault.kerosine.bounded.sol


// SPDX-License-Identifier: MIT
pragma solidity =0.8.17;

import {KerosineVault}          from "./Vault.kerosine.sol";
import {IVaultManager}          from "../interfaces/IVaultManager.sol";
import {Dyad}                   from "./Dyad.sol";
import {KerosineManager}        from "./KerosineManager.sol";
import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";

import {ERC20} from "@solmate/src/tokens/ERC20.sol";

contract BoundedKerosineVault is KerosineVault {
  error NotWithdrawable(uint id, address to, uint amount);

  UnboundedKerosineVault public unboundedKerosineVault;

  constructor(
    IVaultManager   _vaultManager,
    ERC20           _asset, 
    KerosineManager _kerosineManager
  ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

  function setUnboundedKerosineVault(
    UnboundedKerosineVault _unboundedKerosineVault
  )
    external
    onlyOwner
  {
    unboundedKerosineVault = _unboundedKerosineVault;
  }

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

  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }
}


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L1:1

```solidity
File: src/core/Vault.kerosine.sol


// SPDX-License-Identifier: MIT
pragma solidity =0.8.17;

import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "./KerosineManager.sol";
import {IVault}          from "../interfaces/IVault.sol";

import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {Owned}           from "@solmate/src/auth/Owned.sol";

abstract contract KerosineVault is IVault, Owned(msg.sender) {
  using SafeTransferLib for ERC20;

  IVaultManager   public immutable vaultManager;
  ERC20           public immutable asset;
  KerosineManager public immutable kerosineManager;

  mapping(uint => uint) public id2asset;

  modifier onlyVaultManager() {
    if (msg.sender != address(vaultManager)) revert NotVaultManager();
    _;
  }

  constructor(
    IVaultManager   _vaultManager,
    ERC20           _asset, 
    KerosineManager _kerosineManager 
  ) {
    vaultManager    = _vaultManager;
    asset           = _asset;
    kerosineManager = _kerosineManager;
  }

  function deposit(
    uint id,
    uint amount
  )
    public 
      onlyVaultManager
  {
    id2asset[id] += amount;
    emit Deposit(id, amount);
  }

  function move(
    uint from,
    uint to,
    uint amount
  )
    external
      onlyVaultManager
  {
    id2asset[from] -= amount;
    id2asset[to]   += amount;
    emit Move(from, to, amount);
  }

  function getUsdValue(
    uint id
  )
    public
    view 
    returns (uint) {
      return id2asset[id] * assetPrice() / 1e8;
  }

  function assetPrice() 
    public 
    view 
    virtual
    returns (uint); 
}


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L1:1

```solidity
File: src/core/Vault.kerosine.unbounded.sol


// SPDX-License-Identifier: MIT
pragma solidity =0.8.17;

import {KerosineVault}        from "./Vault.kerosine.sol";
import {IVaultManager}        from "../interfaces/IVaultManager.sol";
import {Vault}                from "./Vault.sol";
import {Dyad}                 from "./Dyad.sol";
import {KerosineManager}      from "./KerosineManager.sol";
import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";

import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

contract UnboundedKerosineVault is KerosineVault {
  using SafeTransferLib for ERC20;

  Dyad                 public immutable dyad;
  KerosineDenominator  public kerosineDenominator;

  constructor(
      IVaultManager   _vaultManager,
      ERC20           _asset, 
      Dyad            _dyad, 
      KerosineManager _kerosineManager
  ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
      dyad = _dyad;
  }

  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
      onlyVaultManager
  {
    id2asset[id] -= amount;
    asset.safeTransfer(to, amount); 
    emit Withdraw(id, to, amount);
  }

  function setDenominator(KerosineDenominator _kerosineDenominator) 
    external 
      onlyOwner
  {
    kerosineDenominator = _kerosineDenominator;
  }

  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }
}


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L1:1

```solidity
File: src/staking/KerosineDenominator.sol


// SPDX-License-Identifier: MIT
pragma solidity =0.8.17;

import {Parameters} from "../params/Parameters.sol";
import {Kerosine} from "../staking/Kerosine.sol";

contract KerosineDenominator is Parameters {

  Kerosine public kerosine;

  constructor(
    Kerosine _kerosine
  ) {
    kerosine = _kerosine;
  }

  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
}


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L1:1

</details>

## NC010 - Function declarations should have NatSpec descriptions:

Function declarations should be preceded by a NatSpec comment.


<details>
<summary>Click to show 29 findings</summary>

```solidity
File: src/core/KerosineManager.sol


18        function add(


28        function remove(


37        function getVaults() 


44        function isLicensed(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:44

```solidity
File: src/core/Vault.kerosine.bounded.sol


17        constructor(


23        function setUnboundedKerosineVault(


32        function withdraw(


44        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:44

```solidity
File: src/core/Vault.kerosine.sol


26        constructor(


36        function deposit(


47        function move(


60        function getUsdValue(


69        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69:69

```solidity
File: src/core/Vault.kerosine.unbounded.sol


21        constructor(


30        function withdraw(


43        function setDenominator(KerosineDenominator _kerosineDenominator) 


50        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:50

```solidity
File: src/core/VaultManagerV2.sol


49        constructor(


59        function setKeroseneManager(KerosineManager _keroseneManager) 


80        function addKerosene(


106       function removeKerosene(


230       function collatRatio(


241       function getTotalUsdValue(


250       function getNonKeroseneValue(


269       function getKeroseneValue(


290       function getVaults(


299       function hasVault(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:299

```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(


17        function denominator() external view returns (uint) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:17

</details>

## NC011 - Contract declarations should have `@notice` tags:

`@notice` is used to explain to end users what the contract does, and the compiler interprets `///` or `/**` comments as this tag if one wasn't explicitly provided.


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.sol


12      abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>

## NC012 - Invalid NatSpec comment style:

NatSpec must begin with `///`, or use `/* ... */` syntax. 


```solidity
File: src/staking/KerosineDenominator.sol


18          // @dev: We subtract all the Kerosene in the multi-sig.


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L18:18

## NC013 - Error declarations should have NatSpec descriptions:




<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/KerosineManager.sol


8         error TooManyVaults();


9         error VaultAlreadyAdded();


10        error VaultNotFound();


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L10:10

```solidity
File: src/core/Vault.kerosine.bounded.sol


13        error NotWithdrawable(uint id, address to, uint amount);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13:13

</details>



## NC014 - Contracts should have full test coverage:

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.


```solidity
File: Various Files


None

```

## NC015 - Large or complicated code bases should implement invariant tests:

Large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts, should implement invariant fuzzing tests. Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers, with properly and extensively-written invariants, can close this testing gap significantly.


```solidity
File: Various Files


None

```

## NC016 - Consider adding a deny-list:

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>



## NC017 - Custom error has no error details:

Consider adding parameters to the error to indicate which user or values caused the failure.


```solidity
File: src/core/KerosineManager.sol


8         error TooManyVaults();


9         error VaultAlreadyAdded();


10        error VaultNotFound();


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L10:10

## NC018 - Contract uses both `require()`/`revert()` as well as custom errors:

Consider using just one method in a single file


```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

## NC019 - Events are missing sender information:

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the msg.sender the events of these types of action will make events much more useful to end users. Include `msg.sender` in the event output.


<details>
<summary>Click to show 8 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


57          emit Move(from, to, amount);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L57:57

```solidity
File: src/core/Vault.kerosine.unbounded.sol


40          emit Withdraw(id, to, amount);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40:40

```solidity
File: src/core/VaultManagerV2.sol


77          emit Added(id, vault);


90          emit Added(id, vault);


103         emit Removed(id, vault);


115         emit Removed(id, vault);


168         emit MintDyad(id, amount, to);


200           emit RedeemDyad(id, vault, amount, to);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200:200

</details>

## NC020 - Function names should differ to make the code more readable:

In Solidity, while function overriding allows for functions with the same name to coexist, it is advisable to avoid this practice to enhance code readability and maintainability. Having multiple functions with the same name, even with different parameters or in inherited contracts, can cause confusion and increase the likelihood of errors during development, testing, and debugging. Using distinct and descriptive function names not only clarifies the purpose and behavior of each function, but also helps prevent unintended function calls or incorrect overriding. By adopting a clear and consistent naming convention, developers can create more comprehensible and maintainable smart contracts.


<details>
<summary>Click to show 14 findings</summary>

```solidity
File: src/core/KerosineManager.sol


  function add(
    address vault
  ) 
    external 
      onlyOwner
  {
    if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
    if (!vaults.add(vault))            revert VaultAlreadyAdded();
  }

  function remove(
    address vault
  ) 
    external 
      onlyOwner
  {
    if (!vaults.remove(vault)) revert VaultNotFound();
  }

  function getVaults() 
    external 
    view 
    returns (address[] memory) {
      return vaults.values();
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37:42

```solidity
File: src/core/VaultManagerV2.sol


  function add(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();
    emit Added(id, vault);
  }

  function remove(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
    if (!vaults[id].remove(vault))     revert VaultNotAdded();
    emit Removed(id, vault);
  }

  function getVaults(
    uint id
  ) 
    external 
    view 
    returns (address[] memory) {
      return vaults[id].values();
  }

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
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }

  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119:131

```solidity
File: src/core/Vault.kerosine.bounded.sol


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

  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:50

```solidity
File: src/core/Vault.kerosine.unbounded.sol


  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
      onlyVaultManager
  {
    id2asset[id] -= amount;
    asset.safeTransfer(to, amount); 
    emit Withdraw(id, to, amount);
  }

  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:68

```solidity
File: src/core/Vault.kerosine.sol


  function assetPrice() 
    public 
    view 
    virtual
    returns (uint); 

  function deposit(
    uint id,
    uint amount
  )
    public 
      onlyVaultManager
  {
    id2asset[id] += amount;
    emit Deposit(id, amount);
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36:45

</details>

## NC021 - It is standard for all external and public functions to be override from an interface:

This is to ensure the whole API is extracted in an interface


<details>
<summary>Click to show 28 findings</summary>

```solidity
File: src/core/KerosineManager.sol


18        function add(
19          address vault
20        ) 
21          external 
22            onlyOwner
23        {
24          if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
25          if (!vaults.add(vault))            revert VaultAlreadyAdded();
26        }


28        function remove(
29          address vault
30        ) 
31          external 
32            onlyOwner
33        {
34          if (!vaults.remove(vault)) revert VaultNotFound();
35        }


37        function getVaults() 
38          external 
39          view 
40          returns (address[] memory) {
41            return vaults.values();
42        }


44        function isLicensed(
45          address vault
46        ) 
47          external 
48          view 
49          returns (bool) {
50            return vaults.contains(vault);
51        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:51

```solidity
File: src/core/Vault.kerosine.bounded.sol


23        function setUnboundedKerosineVault(
24          UnboundedKerosineVault _unboundedKerosineVault
25        )
26          external
27          onlyOwner
28        {
29          unboundedKerosineVault = _unboundedKerosineVault;
30        }


32        function withdraw(
33          uint    id,
34          address to,
35          uint    amount
36        ) 
37          external 
38          view
39            onlyVaultManager
40        {
41          revert NotWithdrawable(id, to, amount);
42        }


44        function assetPrice() 
45          public 
46          view 
47          override
48          returns (uint) {
49            return unboundedKerosineVault.assetPrice() * 2;
50        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:50

```solidity
File: src/core/Vault.kerosine.unbounded.sol


30        function withdraw(
31          uint    id,
32          address to,
33          uint    amount
34        ) 
35          external 
36            onlyVaultManager
37        {
38          id2asset[id] -= amount;
39          asset.safeTransfer(to, amount); 
40          emit Withdraw(id, to, amount);
41        }


43        function setDenominator(KerosineDenominator _kerosineDenominator) 
44          external 
45            onlyOwner
46        {
47          kerosineDenominator = _kerosineDenominator;
48        }


50        function assetPrice() 
51          public 
52          view 
53          override
54          returns (uint) {
55            uint tvl;
56            address[] memory vaults = kerosineManager.getVaults();
57            uint numberOfVaults = vaults.length;
58            for (uint i = 0; i < numberOfVaults; i++) {
59              Vault vault = Vault(vaults[i]);
60              tvl += vault.asset().balanceOf(address(vault)) 
61                      * vault.assetPrice() * 1e18
62                      / (10**vault.asset().decimals()) 
63                      / (10**vault.oracle().decimals());
64            }
65            uint numerator   = tvl - dyad.totalSupply();
66            uint denominator = kerosineDenominator.denominator();
67            return numerator * 1e8 / denominator;
68        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:68

```solidity
File: src/core/VaultManagerV2.sol


59        function setKeroseneManager(KerosineManager _keroseneManager) 
60          external
61            initializer 
62          {
63            keroseneManager = _keroseneManager;
64        }


67        function add(
68            uint    id,
69            address vault
70        ) 
71          external
72            isDNftOwner(id)
73        {
74          if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
75          if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
76          if (!vaults[id].add(vault))            revert VaultAlreadyAdded();
77          emit Added(id, vault);
78        }


80        function addKerosene(
81            uint    id,
82            address vault
83        ) 
84          external
85            isDNftOwner(id)
86        {
87          if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
88          if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
89          if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
90          emit Added(id, vault);
91        }


94        function remove(
95            uint    id,
96            address vault
97        ) 
98          external
99            isDNftOwner(id)
100       {
101         if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
102         if (!vaults[id].remove(vault))     revert VaultNotAdded();
103         emit Removed(id, vault);
104       }


106       function removeKerosene(
107           uint    id,
108           address vault
109       ) 
110         external
111           isDNftOwner(id)
112       {
113         if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
114         if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
115         emit Removed(id, vault);
116       }


119       function deposit(
120         uint    id,
121         address vault,
122         uint    amount
123       ) 
124         external 
125           isValidDNft(id)
126       {
127         idToBlockOfLastDeposit[id] = block.number;
128         Vault _vault = Vault(vault);
129         _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
130         _vault.deposit(id, amount);
131       }


134       function withdraw(
135         uint    id,
136         address vault,
137         uint    amount,
138         address to
139       ) 
140         public
141           isDNftOwner(id)
142       {
143         if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
144         uint dyadMinted = dyad.mintedDyad(address(this), id);
145         Vault _vault = Vault(vault);
146         uint value = amount * _vault.assetPrice() 
147                       * 1e18 
148                       / 10**_vault.oracle().decimals() 
149                       / 10**_vault.asset().decimals();
150         if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
151         _vault.withdraw(id, to, amount);
152         if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
153       }


156       function mintDyad(
157         uint    id,
158         uint    amount,
159         address to
160       )
161         external 
162           isDNftOwner(id)
163       {
164         uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
165         if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
166         dyad.mint(id, to, amount);
167         if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
168         emit MintDyad(id, amount, to);
169       }


172       function burnDyad(
173         uint id,
174         uint amount
175       ) 
176         external 
177           isValidDNft(id)
178       {
179         dyad.burn(id, msg.sender, amount);
180         emit BurnDyad(id, amount, msg.sender);
181       }


184       function redeemDyad(
185         uint    id,
186         address vault,
187         uint    amount,
188         address to
189       )
190         external 
191           isDNftOwner(id)
192         returns (uint) { 
193           dyad.burn(id, msg.sender, amount);
194           Vault _vault = Vault(vault);
195           uint asset = amount 
196                         * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197                         / _vault.assetPrice() 
198                         / 1e18;
199           withdraw(id, vault, asset, to);
200           emit RedeemDyad(id, vault, amount, to);
201           return asset;
202       }


205       function liquidate(
206         uint id,
207         uint to
208       ) 
209         external 
210           isValidDNft(id)
211           isValidDNft(to)
212         {
213           uint cr = collatRatio(id);
214           if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
215           dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
216     
217           uint cappedCr               = cr < 1e18 ? 1e18 : cr;
218           uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219           uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
220     
221           uint numberOfVaults = vaults[id].length();
222           for (uint i = 0; i < numberOfVaults; i++) {
223               Vault vault      = Vault(vaults[id].at(i));
224               uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225               vault.move(id, to, collateral);
226           }
227           emit Liquidate(id, msg.sender, to);
228       }


230       function collatRatio(
231         uint id
232       )
233         public 
234         view
235         returns (uint) {
236           uint _dyad = dyad.mintedDyad(address(this), id);
237           if (_dyad == 0) return type(uint).max;
238           return getTotalUsdValue(id).divWadDown(_dyad);
239       }


241       function getTotalUsdValue(
242         uint id
243       ) 
244         public 
245         view
246         returns (uint) {
247           return getNonKeroseneValue(id) + getKeroseneValue(id);
248       }


250       function getNonKeroseneValue(
251         uint id
252       ) 
253         public 
254         view
255         returns (uint) {
256           uint totalUsdValue;
257           uint numberOfVaults = vaults[id].length(); 
258           for (uint i = 0; i < numberOfVaults; i++) {
259             Vault vault = Vault(vaults[id].at(i));
260             uint usdValue;
261             if (vaultLicenser.isLicensed(address(vault))) {
262               usdValue = vault.getUsdValue(id);        
263             }
264             totalUsdValue += usdValue;
265           }
266           return totalUsdValue;
267       }


269       function getKeroseneValue(
270         uint id
271       ) 
272         public 
273         view
274         returns (uint) {
275           uint totalUsdValue;
276           uint numberOfVaults = vaultsKerosene[id].length(); 
277           for (uint i = 0; i < numberOfVaults; i++) {
278             Vault vault = Vault(vaultsKerosene[id].at(i));
279             uint usdValue;
280             if (keroseneManager.isLicensed(address(vault))) {
281               usdValue = vault.getUsdValue(id);        
282             }
283             totalUsdValue += usdValue;
284           }
285           return totalUsdValue;
286       }


290       function getVaults(
291         uint id
292       ) 
293         external 
294         view 
295         returns (address[] memory) {
296           return vaults[id].values();
297       }


299       function hasVault(
300         uint    id,
301         address vault
302       ) 
303         external 
304         view 
305         returns (bool) {
306           return vaults[id].contains(vault);
307       }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:307

```solidity
File: src/staking/KerosineDenominator.sol


17        function denominator() external view returns (uint) {
18          // @dev: We subtract all the Kerosene in the multi-sig.
19          //       We are aware that this is not a great solution. That is
20          //       why we can switch out Denominator contracts.
21          return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
22        } 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:22

</details>

## NC022 - Consider adding formal verification proofs:

Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in based off of SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification).


```solidity
File: Various Files


None

```

## NC023 - Missing timelock for critical parameter change:

Timelocks prevent users from being surprised by changes.


```solidity
File: src/core/Vault.kerosine.bounded.sol


29          unboundedKerosineVault = _unboundedKerosineVault;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L29:29

```solidity
File: src/core/Vault.kerosine.unbounded.sol


47          kerosineDenominator = _kerosineDenominator;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L47:47

```solidity
File: src/core/VaultManagerV2.sol


63            keroseneManager = _keroseneManager;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63:63

## NC024 - Setters should prevent re-setting of the same value:

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers.


```solidity
File: src/core/Vault.kerosine.bounded.sol


23        function setUnboundedKerosineVault(
24          UnboundedKerosineVault _unboundedKerosineVault
25        )
26          external
27          onlyOwner
28        {
29          unboundedKerosineVault = _unboundedKerosineVault;
30        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23:30

```solidity
File: src/core/Vault.kerosine.unbounded.sol


43        function setDenominator(KerosineDenominator _kerosineDenominator) 
44          external 
45            onlyOwner
46        {
47          kerosineDenominator = _kerosineDenominator;
48        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43:48

```solidity
File: src/core/VaultManagerV2.sol


59        function setKeroseneManager(KerosineManager _keroseneManager) 
60          external
61            initializer 
62          {
63            keroseneManager = _keroseneManager;
64        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59:64

## NC025 - Consider splitting long calculations:

The longer a string of operations is, the harder it is to understand it. Consider splitting the full calculation into more steps, with more descriptive temporary variable names, and add extensive comments.


```solidity
File: src/core/VaultManagerV2.sol


146         uint value = amount * _vault.assetPrice() 
147                       * 1e18 
148                       / 10**_vault.oracle().decimals() 
149                       / 10**_vault.asset().decimals();


195           uint asset = amount 
196                         * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197                         / _vault.assetPrice() 
198                         / 1e18;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195:198

## NC026 - Use of override is unnecessary:

Starting with Solidity version 0.8.8, using the override keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.


```solidity
File: src/core/Vault.kerosine.bounded.sol


  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:50

```solidity
File: src/core/Vault.kerosine.unbounded.sol


  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:68

## NC027 - Unused import:

The identifier is imported but never used within the file


```solidity
File: src/core/Vault.kerosine.bounded.sol


6       import {Dyad}                   from "./Dyad.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L6:6

```solidity
File: src/core/Vault.kerosine.unbounded.sol


9       import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L9:9

## NC028 - Put all system-wide constants in one file:

Putting all the system-wide constants in a single file improves code readability, makes it easier to understand the basic configuration and limitations of the system, and makes maintenance easier.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


14        uint public constant MAX_VAULTS = 10;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14:14

```solidity
File: src/core/VaultManagerV2.sol


22        uint public constant MAX_VAULTS          = 5;


23        uint public constant MAX_VAULTS_KEROSENE = 5;


25        uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%


26        uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26:26

</details>

## NC029 - Consider adding emergency-stop functionality:

Adding a way to quickly halt protocol functionality in an emergency, rather than having to pause individual contracts one-by-one, will make in-progress hack mitigation faster and much less stressful.


```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

## NC030 - Unnecessary cast:

The variable is being cast to its own type


```solidity
File: src/core/VaultManagerV2.sol


129         _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129:129

## NC031 - Use the latest solidity (prior to 0.8.20 if on L2s) for deployment:

Since deployed contracts should not use floating pragmas, I've flagged all instances where a version prior to 0.8.19 is allowed by the version pragma


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: src/core/KerosineManager.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L2:2

```solidity
File: src/core/Vault.kerosine.bounded.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2:2

```solidity
File: src/core/Vault.kerosine.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2:2

```solidity
File: src/core/Vault.kerosine.unbounded.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2:2

```solidity
File: src/core/VaultManagerV2.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2:2

```solidity
File: src/staking/KerosineDenominator.sol


2       pragma solidity =0.8.17;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L2:2

</details>

## NC032 - Function definitions should have NatSpec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 37 findings</summary>

```solidity
File: src/core/KerosineManager.sol


18        function add(


28        function remove(


37        function getVaults() 


44        function isLicensed(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:44

```solidity
File: src/core/Vault.kerosine.bounded.sol


17        constructor(


23        function setUnboundedKerosineVault(


32        function withdraw(


44        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:44

```solidity
File: src/core/Vault.kerosine.sol


26        constructor(


36        function deposit(


47        function move(


60        function getUsdValue(


69        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69:69

```solidity
File: src/core/Vault.kerosine.unbounded.sol


21        constructor(


30        function withdraw(


43        function setDenominator(KerosineDenominator _kerosineDenominator) 


50        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:50

```solidity
File: src/core/VaultManagerV2.sol


49        constructor(


59        function setKeroseneManager(KerosineManager _keroseneManager) 


67        function add(


80        function addKerosene(


94        function remove(


106       function removeKerosene(


119       function deposit(


134       function withdraw(


156       function mintDyad(


172       function burnDyad(


184       function redeemDyad(


205       function liquidate(


230       function collatRatio(


241       function getTotalUsdValue(


250       function getNonKeroseneValue(


269       function getKeroseneValue(


290       function getVaults(


299       function hasVault(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:299

```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(


17        function denominator() external view returns (uint) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:17

</details>

## NC033 - Function definitions should have NatSpec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 37 findings</summary>

```solidity
File: src/core/KerosineManager.sol


18        function add(


28        function remove(


37        function getVaults() 


44        function isLicensed(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:44

```solidity
File: src/core/Vault.kerosine.bounded.sol


17        constructor(


23        function setUnboundedKerosineVault(


32        function withdraw(


44        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:44

```solidity
File: src/core/Vault.kerosine.sol


26        constructor(


36        function deposit(


47        function move(


60        function getUsdValue(


69        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69:69

```solidity
File: src/core/Vault.kerosine.unbounded.sol


21        constructor(


30        function withdraw(


43        function setDenominator(KerosineDenominator _kerosineDenominator) 


50        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:50

```solidity
File: src/core/VaultManagerV2.sol


49        constructor(


59        function setKeroseneManager(KerosineManager _keroseneManager) 


67        function add(


80        function addKerosene(


94        function remove(


106       function removeKerosene(


119       function deposit(


134       function withdraw(


156       function mintDyad(


172       function burnDyad(


184       function redeemDyad(


205       function liquidate(


230       function collatRatio(


241       function getTotalUsdValue(


250       function getNonKeroseneValue(


269       function getKeroseneValue(


290       function getVaults(


299       function hasVault(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:299

```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(


17        function denominator() external view returns (uint) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:17

</details>

## NC034 - Abstract contract declarations should have NatSpec @title annotations:

A title that should describe the contract/interface


```solidity
File: src/core/Vault.kerosine.sol


12      abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12:12

## NC035 - Abstract contract declarations should have NatSpec @author annotations:

The name of the author


```solidity
File: src/core/Vault.kerosine.sol


12      abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12:12

## NC036 - Abstract contract declarations should have NatSpec @notice annotations:

Explain to an end user what this does


```solidity
File: src/core/Vault.kerosine.sol


12      abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12:12

## NC037 - Abstract contract declarations should have Natspec @dev annotations:

Explain to a developer any extra details


```solidity
File: src/core/Vault.kerosine.sol


12      abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12:12

## NC038 - Modifier definitions should have Natspec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


21        modifier onlyVaultManager() {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21:21

```solidity
File: src/core/VaultManagerV2.sol


39        modifier isDNftOwner(uint id) {


42        modifier isValidDNft(uint id) {


45        modifier isLicensed(address vault) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45:45

</details>

## NC039 - Modifier definitions should have Natspec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: src/core/Vault.kerosine.sol


21        modifier onlyVaultManager() {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21:21

```solidity
File: src/core/VaultManagerV2.sol


39        modifier isDNftOwner(uint id) {


42        modifier isValidDNft(uint id) {


45        modifier isLicensed(address vault) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45:45

</details>

## NC040 - Contract definitions should have Natspec @title annotations:

 title that should describe the contract


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>

## NC041 - Contract definitions should have Natspec @author annotations:

The name of the author


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>

## NC042 - Contract definitions should have Natspec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>

## NC043 - Contract definitions should have Natspec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/KerosineManager.sol


7       contract KerosineManager is Owned(msg.sender) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7:7

```solidity
File: src/core/Vault.kerosine.bounded.sol


12      contract BoundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12:12

```solidity
File: src/core/Vault.kerosine.unbounded.sol


15      contract UnboundedKerosineVault is KerosineVault {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15:15

```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

```solidity
File: src/staking/KerosineDenominator.sol


7       contract KerosineDenominator is Parameters {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7:7

</details>

## NC044 - State variable declarations should have Natspec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 21 findings</summary>

```solidity
File: src/core/KerosineManager.sol


14        uint public constant MAX_VAULTS = 10;


16        EnumerableSet.AddressSet private vaults;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16:16

```solidity
File: src/core/Vault.kerosine.bounded.sol


15        UnboundedKerosineVault public unboundedKerosineVault;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L15:15

```solidity
File: src/core/Vault.kerosine.sol


15        IVaultManager   public immutable vaultManager;


16        ERC20           public immutable asset;


17        KerosineManager public immutable kerosineManager;


19        mapping(uint => uint) public id2asset;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19:19

```solidity
File: src/core/Vault.kerosine.unbounded.sol


18        Dyad                 public immutable dyad;


19        KerosineDenominator  public kerosineDenominator;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L19:19

```solidity
File: src/core/VaultManagerV2.sol


22        uint public constant MAX_VAULTS          = 5;


23        uint public constant MAX_VAULTS_KEROSENE = 5;


25        uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%


26        uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%


28        DNft     public immutable dNft;


29        Dyad     public immutable dyad;


30        Licenser public immutable vaultLicenser;


32        KerosineManager public keroseneManager;


34        mapping (uint => EnumerableSet.AddressSet) internal vaults; 


35        mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 


37        mapping (uint => uint) public idToBlockOfLastDeposit;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37:37

```solidity
File: src/staking/KerosineDenominator.sol


9         Kerosine public kerosine;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9:9

</details>

## NC045 - State variable declarations should have Natspec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 21 findings</summary>

```solidity
File: src/core/KerosineManager.sol


14        uint public constant MAX_VAULTS = 10;


16        EnumerableSet.AddressSet private vaults;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16:16

```solidity
File: src/core/Vault.kerosine.bounded.sol


15        UnboundedKerosineVault public unboundedKerosineVault;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L15:15

```solidity
File: src/core/Vault.kerosine.sol


15        IVaultManager   public immutable vaultManager;


16        ERC20           public immutable asset;


17        KerosineManager public immutable kerosineManager;


19        mapping(uint => uint) public id2asset;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19:19

```solidity
File: src/core/Vault.kerosine.unbounded.sol


18        Dyad                 public immutable dyad;


19        KerosineDenominator  public kerosineDenominator;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L19:19

```solidity
File: src/core/VaultManagerV2.sol


22        uint public constant MAX_VAULTS          = 5;


23        uint public constant MAX_VAULTS_KEROSENE = 5;


25        uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%


26        uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%


28        DNft     public immutable dNft;


29        Dyad     public immutable dyad;


30        Licenser public immutable vaultLicenser;


32        KerosineManager public keroseneManager;


34        mapping (uint => EnumerableSet.AddressSet) internal vaults; 


35        mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 


37        mapping (uint => uint) public idToBlockOfLastDeposit;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37:37

```solidity
File: src/staking/KerosineDenominator.sol


9         Kerosine public kerosine;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9:9

</details>

## NC046 - Functions should have Natspec @return annotations:

Documents the return variables of a contract’s function


<details>
<summary>Click to show 14 findings</summary>

```solidity
File: src/core/KerosineManager.sol


37        function getVaults() 


44        function isLicensed(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:44

```solidity
File: src/core/Vault.kerosine.bounded.sol


44        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:44

```solidity
File: src/core/Vault.kerosine.sol


60        function getUsdValue(


69        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69:69

```solidity
File: src/core/Vault.kerosine.unbounded.sol


50        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:50

```solidity
File: src/core/VaultManagerV2.sol


184       function redeemDyad(


230       function collatRatio(


241       function getTotalUsdValue(


250       function getNonKeroseneValue(


269       function getKeroseneValue(


290       function getVaults(


299       function hasVault(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:299

```solidity
File: src/staking/KerosineDenominator.sol


17        function denominator() external view returns (uint) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:17

</details>

## NC047 - Functions should have Natspec @param annotations:

Documents a parameter just like in Doxygen (must be followed by parameter name)


<details>
<summary>Click to show 36 findings</summary>

```solidity
File: src/core/KerosineManager.sol


18        function add(


28        function remove(


37        function getVaults() 


44        function isLicensed(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44:44

```solidity
File: src/core/Vault.kerosine.bounded.sol


17        constructor(


23        function setUnboundedKerosineVault(


32        function withdraw(


44        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44:44

```solidity
File: src/core/Vault.kerosine.sol


26        constructor(


36        function deposit(


47        function move(


60        function getUsdValue(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60:60

```solidity
File: src/core/Vault.kerosine.unbounded.sol


21        constructor(


30        function withdraw(


43        function setDenominator(KerosineDenominator _kerosineDenominator) 


50        function assetPrice() 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50:50

```solidity
File: src/core/VaultManagerV2.sol


49        constructor(


59        function setKeroseneManager(KerosineManager _keroseneManager) 


67        function add(


80        function addKerosene(


94        function remove(


106       function removeKerosene(


119       function deposit(


134       function withdraw(


156       function mintDyad(


172       function burnDyad(


184       function redeemDyad(


205       function liquidate(


230       function collatRatio(


241       function getTotalUsdValue(


250       function getNonKeroseneValue(


269       function getKeroseneValue(


290       function getVaults(


299       function hasVault(


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299:299

```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(


17        function denominator() external view returns (uint) {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17:17

</details>


## NC048 - If statement control structures do not comply with best practices:

If statements which include a single line do not need to have curly brackets, however according to the Solidiity style guide the line of code executed upon the if statement condition being met should still be on the next line, not on the same line as the if statement declaration.


<details>
<summary>Click to show 24 findings</summary>

```solidity
File: src/core/KerosineManager.sol


24          if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();


25          if (!vaults.add(vault))            revert VaultAlreadyAdded();


34          if (!vaults.remove(vault)) revert VaultNotFound();


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L34:34

```solidity
File: src/core/Vault.kerosine.sol


22          if (msg.sender != address(vaultManager)) revert NotVaultManager();


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L22:22

```solidity
File: src/core/VaultManagerV2.sol


40          if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;


43          if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;


46          if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;


74          if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();


75          if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();


76          if (!vaults[id].add(vault))            revert VaultAlreadyAdded();


87          if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();


88          if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();


89          if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();


101         if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();


102         if (!vaults[id].remove(vault))     revert VaultNotAdded();


113         if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();


114         if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();


143         if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();


150         if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();


152         if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 


165         if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();


167         if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 


214           if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();


237           if (_dyad == 0) return type(uint).max;


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237:237

</details>

## NC049 - A event should be emitted if a non immutable state variable is set in a constructor:




```solidity
File: src/staking/KerosineDenominator.sol


11        constructor(
12          Kerosine _kerosine
13        ) {
14          kerosine = _kerosine;
15        }


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11:15

## NC050 - It is best practice to use linear inheritance:

In Solidity, complex inheritance structures can obfuscate code understanding, introducing potential security risks. Multiple inheritance, especially with overlapping function names or state variables, can cause unintentional overrides or ambiguous behavior. Resolution: Strive for linear and simple inheritance chains. Avoid diamond or circular inheritance patterns. Clearly document the purpose and relationships of base contracts, ensuring that overrides are intentional. Tools like Remix or Hardhat can visualize inheritance chains, assisting in verification. Keeping inheritance streamlined aids in better code readability, reduces potential errors, and ensures smoother audits and upgrades.


```solidity
File: src/core/VaultManagerV2.sol


17      contract VaultManagerV2 is IVaultManager, Initializable {


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17:17

## NC051 - Defining All External/Public Functions in Contract Interfaces:

It is preferable to have all the external and public function in an interface to make using them easier by developers. This helps ensure the whole API is extracted in a interface.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: src/core/VaultManagerV2.sol


134       function withdraw(
135         uint    id,
136         address vault,
137         uint    amount,
138         address to
139       ) 


230       function collatRatio(
231         uint id
232       )


241       function getTotalUsdValue(
242         uint id
243       ) 


250       function getNonKeroseneValue(
251         uint id
252       ) 


269       function getKeroseneValue(
270         uint id
271       ) 


```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269:271

</details>