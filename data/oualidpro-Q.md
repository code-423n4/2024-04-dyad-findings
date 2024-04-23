## Summary

### Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [[L&#x2011;1](#l1-missing-checks-for-address-0-when-assigning-values-to-address-state-variables)] | Missing checks for `address(0)` when assigning values to address state variables | 11 | 
| [[L&#x2011;2](#l2-for-loops-in-public-or-external-functions-should-be-avoided-due-to-high-gas-costs-and-possible-dos)] | For loops in public or external functions should be avoided due to high gas costs and possible DOS | 4 | 
| [[L&#x2011;3](#l3-constant-decimal-values)] | Constant decimal values | 10 | 
| [[L&#x2011;4](#l4-loss-of-precision)] | Loss of precision | 4 | 
| [[L&#x2011;5](#l5-governance-operations-should-be-behind-a-timelock)] | Governance operations should be behind a timelock | 7 | 
| [[L&#x2011;6](#l6-consider-implementing-two-step-procedure-for-updating-protocol-addresses)] | Consider implementing two-step procedure for updating protocol addresses | 3 | 
| [[L&#x2011;7](#l7-upgradeable-contract-uses-non-upgradeable-version-of-the-openzeppelin-libraries-contracts)] | Upgradeable contract uses non-upgradeable version of the OpenZeppelin libraries/contracts | 2 | 
| [[L&#x2011;8](#l8-prevent-re-setting-a-state-variable-with-the-same-value)] | prevent re-setting a state variable with the same value | 3 | 

Total: 44 instances over 8 issues

### Non-critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [[NC&#x2011;1](#nc1-large-or-complicated-code-bases-should-implement-invariant-tests)] | Large or complicated code bases should implement invariant tests | 1 | 
| [[NC&#x2011;2](#nc2-natspec-natspec-author-is-missing-from-contract)] | [NatSpec] Natspec `@author` is missing from `contract` | 7 | 
| [[NC&#x2011;3](#nc3-overly-complicated-arithmetic)] | Overly complicated arithmetic | 2 | 
| [[NC&#x2011;4](#nc4-constants-in-comparisons-should-appear-on-the-left-side)] | Constants in comparisons should appear on the left side | 10 | 
| [[NC&#x2011;5](#nc5-custom-error-has-no-error-details)] | Custom error has no error details | 3 | 
| [[NC&#x2011;6](#nc6-dependence-on-external-protocols)] | Dependence on external protocols | 1 | 
| [[NC&#x2011;7](#nc7-events-are-missing-sender-information)] | Events are missing sender information | 9 | 
| [[NC&#x2011;8](#nc8-events-may-be-emitted-out-of-order-due-to-reentrancy)] | Events may be emitted out of order due to reentrancy | 5 | 
| [[NC&#x2011;9](#nc9-defining-all-external-public-functions-in-contract-interfaces)] | Defining All External/Public Functions in Contract Interfaces | 15 | 
| [[NC&#x2011;10](#nc10-fixed-compiler-version-required-for-non-library-interface-files)] | Fixed Compiler Version Required for Non-Library/Interface Files | 7 | 
| [[NC&#x2011;11](#nc11-imports-could-be-organized-more-systematically)] | Imports could be organized more systematically | 5 | 
| [[NC&#x2011;12](#nc12-import-declarations-should-import-specific-identifiers-rather-than-the-whole-file)] | Import declarations should import specific identifiers, rather than the whole file | 1 | 
| [[NC&#x2011;13](#nc13-inconsistent-spacing-in-comments)] | Inconsistent spacing in comments | 6 | 
| [[NC&#x2011;14](#nc14-incorrect-natspec-syntax)] | Incorrect NatSpec Syntax | 1 | 
| [[NC&#x2011;15](#nc15-long-lines-of-code)] | Long lines of code | 2 | 
| [[NC&#x2011;16](#nc16-mapping-definitions-do-not-follow-the-solidity-style-guide)] | `mapping` definitions do not follow the Solidity Style Guide | 3 | 
| [[NC&#x2011;17](#nc17-file-is-missing-natspec)] | File is missing NatSpec | 5 | 
| [[NC&#x2011;18](#nc18-consider-using-later-versions-of-solidity-for-more-cappabilities)] | Consider using later versions of solidity for more cappabilities | 7 | 
| [[NC&#x2011;19](#nc19-use-of-override-is-unnecessary)] | Use of `override` is unnecessary | 2 | 
| [[NC&#x2011;20](#nc20-remove-forge-std-import)] | Remove `forge-std` import | 1 | 
| [[NC&#x2011;21](#nc21-setters-should-prevent-re-setting-of-the-same-value)] | Setters should prevent re-setting of the same value | 3 | 
| [[NC&#x2011;22](#nc22-state-variables-should-have-natspec-comments)] | State variables should have `Natspec` comments | 21 | 
| [[NC&#x2011;23](#nc23-contracts-should-have-full-test-coverage)] | Contracts should have full test coverage | 1 | 
| [[NC&#x2011;24](#nc24-natspec-natspec-title-is-missing-from-contract)] | [NatSpec] Natspec `@title` is missing from `contract` | 7 | 
| [[NC&#x2011;25](#nc25-top-level-pragma-declarations-should-be-separated-by-two-blank-lines)] | Top level pragma declarations should be separated by two blank lines | 13 | 
| [[NC&#x2011;26](#nc26-critical-functions-should-be-a-two-step-procedure)] | Critical functions should be a two step procedure | 4 | 
| [[NC&#x2011;27](#nc27-uint-variables-should-have-the-bit-size-defined-explicitly)] | uint variables should have the bit size defined explicitly | 72 | 
| [[NC&#x2011;28](#nc28-uncommented-fields-in-a-struct)] | Uncommented fields in a struct | 1 | 
| [[NC&#x2011;29](#nc29-unused-import)] | Unused Import | 3 | 
| [[NC&#x2011;30](#nc30-unused-modifier-definition)] | Unused `modifier` definition | 1 | 
| [[NC&#x2011;31](#nc31-use-the-latest-solidity-prior-to-0-8-20-if-on-l2s-for-deployment)] | Use the latest solidity (prior to 0.8.20 if on L2s) for deployment | 7 | 
| [[NC&#x2011;32](#nc32-use-a-single-file-for-system-wide-constants)] | Use a single file for system wide constants | 2 | 
| [[NC&#x2011;33](#nc33-consider-using-smtchecker)] | Consider using SMTChecker | 7 | 
| [[NC&#x2011;34](#nc34-whitespace-in-expressions)] | Whitespace in Expressions | 12 | 
| [[NC&#x2011;35](#nc35-natspec-natspec-dev-is-missing-from-contract)] | [NatSpec] Natspec `@dev` is missing from `contract` | 54 | 
| [[NC&#x2011;36](#nc36-contract-should-expose-an-interface)] | Contract should expose an `interface` | 15 | 
| [[NC&#x2011;37](#nc37-named-imports-of-parent-contracts-are-missing)] | Named imports of parent contracts are missing | 1 | 
| [[NC&#x2011;38](#nc38-natspec-natspec-notice-is-missing-from-contract)] | [NatSpec] Natspec `@notice` is missing from `contract` | 54 | 
| [[NC&#x2011;39](#nc39-consider-splitting-long-calculations)] | Consider splitting long calculations | 1 | 
| [[NC&#x2011;40](#nc40-top-level-declarations-should-be-separated-by-at-least-two-lines)] | Top-level declarations should be separated by at least two lines | 15 | 
| [[NC&#x2011;41](#nc41-immutable-variable-names-don-t-follow-the-solidity-style-guide)] | `immutable` variable names don\'t follow the Solidity style guide | 7 | 
| [[NC&#x2011;42](#nc42-use-the-latest-solidity-version-for-better-security)] | Use the latest Solidity version for better security | 7 | 
| [[NC&#x2011;43](#nc43-consider-adding-formal-verification-proofs)] | Consider adding formal verification proofs | 1 | 
| [[NC&#x2011;44](#nc44-use-inheritdoc-for-overridden-functions)] | Use `@inheritdoc` for overridden functions | 2 | 
| [[NC&#x2011;45](#nc45-constructor-should-emit-an-event)] | constructor should emit an event | 5 | 
| [[NC&#x2011;46](#nc46-complex-functions-should-include-comments)] | Complex functions should include comments | 1 | 
| [[NC&#x2011;47](#nc47-solidity-all-verbatim-blocks-are-considered-identical-by-deduplicator-and-can-incorrectly-be-unified)] | [Solidity]: All `verbatim` blocks are considered identical by deduplicator and can incorrectly be unified | 7 | 
| [[NC&#x2011;48](#nc48-natspec-natspec-param-is-missing-from-error)] | [NatSpec] Natspec `@param` is missing from `error` | 29 | 
| [[NC&#x2011;49](#nc49-openzeppelin-libraries-should-be-upgraded-to-a-newer-version)] | OpenZeppelin libraries should be upgraded to a newer version | 3 | 
| [[NC&#x2011;50](#nc50-non-constant-immutable-state-variables-are-missing-a-setter-post-deployment)] | Non constant/immutable state variables are missing a setter post deployment | 4 | 
| [[NC&#x2011;51](#nc51-consider-making-private-state-variables-internal-to-increase-flexibility)] | Consider making private state variables internal to increase flexibility | 1 | 
| [[NC&#x2011;52](#nc52-lack-of-space-near-the-operator)] | Lack of space near the operator | 10 | 
| [[NC&#x2011;53](#nc53-incorrect-withdraw-declaration)] | Incorrect withdraw declaration | 3 | 
| [[NC&#x2011;54](#nc54-a-event-should-be-emitted-if-a-non-immutable-state-variable-is-set-in-a-constructor)] | A event should be emitted if a non immutable state variable is set in a constructor | 8 | 
| [[NC&#x2011;55](#nc55-solidity-order-of-argument-evaluation-disrupted-in-non-expression-split-code-by-optimizer-sequences-with-fullinliner)] | [Solidity]: Order of Argument Evaluation Disrupted in Non-Expression-Split Code by Optimizer Sequences with FullInliner | 7 | 
| [[NC&#x2011;56](#nc56-use-named-return-values)] | Use named return values | 14 | 
| [[NC&#x2011;57](#nc57-consider-adding-validation-of-user-inputs)] | Consider adding validation of user inputs | 15 | 
| [[NC&#x2011;58](#nc58-consider-using-named-function-calls)] | Consider using named function calls | 1 | 

Total: 512 instances over 58 issues

## Low Risk Issues

### [L&#x2011;1] Missing checks for `address(0)` when assigning values to address state variables 



*There are 11 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

29:     unboundedKerosineVault = _unboundedKerosineVault;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L29-L29) 


```solidity

File: ./src/core/Vault.kerosine.sol

31:     vaultManager    = _vaultManager;

32:     asset           = _asset;

33:     kerosineManager = _kerosineManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L31-L31) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L32-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L33-L33)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

27:       dyad = _dyad;

47:     kerosineDenominator = _kerosineDenominator;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L27-L27) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L47-L47)


```solidity

File: ./src/core/VaultManagerV2.sol

54:     dNft          = _dNft;

55:     dyad          = _dyad;

56:     vaultLicenser = _licenser;

63:       keroseneManager = _keroseneManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L54-L54) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L55-L55), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L56-L56), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L63-L63)


```solidity

File: ./src/staking/KerosineDenominator.sol

14:     kerosine = _kerosine;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L14-L14) 


</details>


### [L&#x2011;2] For loops in public or external functions should be avoided due to high gas costs and possible DOS 
In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
55:       uint tvl;
56:       address[] memory vaults = kerosineManager.getVaults();
57:       uint numberOfVaults = vaults.length;
58:       for (uint i = 0; i < numberOfVaults; i++) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L58) 


```solidity

File: ./src/core/VaultManagerV2.sol

205:   function liquidate(
206:     uint id,
207:     uint to
208:   ) 
209:     external 
210:       isValidDNft(id)
211:       isValidDNft(to)
212:     {
213:       uint cr = collatRatio(id);
214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
216: 
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
220: 
221:       uint numberOfVaults = vaults[id].length();
222:       for (uint i = 0; i < numberOfVaults; i++) {

250:   function getNonKeroseneValue(
251:     uint id
252:   ) 
253:     public 
254:     view
255:     returns (uint) {
256:       uint totalUsdValue;
257:       uint numberOfVaults = vaults[id].length(); 
258:       for (uint i = 0; i < numberOfVaults; i++) {

269:   function getKeroseneValue(
270:     uint id
271:   ) 
272:     public 
273:     view
274:     returns (uint) {
275:       uint totalUsdValue;
276:       uint numberOfVaults = vaultsKerosene[id].length(); 
277:       for (uint i = 0; i < numberOfVaults; i++) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L205-L222) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L258), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L277)


</details>


### [L&#x2011;3] Constant decimal values 
The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations.Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.
Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts.This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under / overflows that could jeopardize contract integrity and user funds. 


*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L66-L66) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

61:                 * vault.assetPrice() * 1e18

61:                 * vault.assetPrice() * 1e18

61:                 * vault.assetPrice() * 1e18

67:       return numerator * 1e8 / denominator;

67:       return numerator * 1e8 / denominator;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L61-L61) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L61-L61), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L61-L61), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L67-L67), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L67-L67)


```solidity

File: ./src/core/VaultManagerV2.sol

147:                   * 1e18 

147:                   * 1e18 

147:                   * 1e18 

198:                     / 1e18;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L147-L147) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L147-L147), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L147-L147), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L198-L198)


</details>


### [L&#x2011;4] Loss of precision 
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

67:       return numerator * 1e8 / denominator;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L67-L67) 


```solidity

File: ./src/core/VaultManagerV2.sol

146:     uint value = amount * _vault.assetPrice() 

146:     uint value = amount * _vault.assetPrice() 

195:       uint asset = amount 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L146) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L146), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L195)


</details>


### [L&#x2011;5] Governance operations should be behind a timelock 
All critical and governance operations should be protected by a timelock. For example from the point of view of a user, the changing of the owner of a contract is a high risk operation that may have outcomes ranging from an attacker gaining control over the protocol, to the function no longer functioning due to a typo in the destination address. To give users plenty of warning so that they can validate any ownership changes, changes of ownership should be behind a timelock.


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/KerosineManager.sol

28:   function remove(
29:     address vault
30:   ) 
31:     external 
32:       onlyOwner
33:   {
34:     if (!vaults.remove(vault)) revert VaultNotFound();
35:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L35) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }

32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:     view
39:       onlyVaultManager
40:   {
41:     revert NotWithdrawable(id, to, amount);
42:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L30) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L42)


```solidity

File: ./src/core/Vault.kerosine.sol

36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public 
41:       onlyVaultManager
42:   {
43:     id2asset[id] += amount;
44:     emit Deposit(id, amount);
45:   }

47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   {
55:     id2asset[from] -= amount;
56:     id2asset[to]   += amount;
57:     emit Move(from, to, amount);
58:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L36-L45) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L47-L58)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {
38:     id2asset[id] -= amount;
39:     asset.safeTransfer(to, amount); 
40:     emit Withdraw(id, to, amount);
41:   }

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L41) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L48)


</details>


### [L&#x2011;6] Consider implementing two-step procedure for updating protocol addresses 
A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the 'set' functions ensure that the recipient is of the right interface type.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L30) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L48) 


```solidity

File: ./src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L64) 


</details>


### [L&#x2011;7] Upgradeable contract uses non-upgradeable version of the OpenZeppelin libraries/contracts 
OpenZeppelin has an [Upgradeable](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/tree/master/contracts/utils) variants of each of its libraries and contracts, and upgradeable contracts should use those variants.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L14-L14) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L15-L15)


</details>


### [L&#x2011;8] prevent re-setting a state variable with the same value 
Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43) 


```solidity

File: ./src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59) 


</details>


## Non-critical Issues

### [NC&#x2011;1] Large or complicated code bases should implement invariant tests 
Large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts, should implement [invariant fuzzing tests](https://medium.com/coinmonks/smart-contract-fuzzing-d9b88e0b0a05). Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers, with properly and extensively-written invariants, can close this testing gap significantly.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

@audit Should implement invariant tests
1: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L1-L1) 


</details>


### [NC&#x2011;2] [NatSpec] Natspec `@author` is missing from `contract` 



*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L17-L17) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L12-L12) 


```solidity

File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L12-L12) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L15-L15) 


```solidity

File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L7-L7) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L35-L35) 


```solidity

File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L7-L7) 


</details>


### [NC&#x2011;3] Overly complicated arithmetic 
To maintain readability in code, particularly in Solidity which can involve complex mathematical operations, it is often recommended to limit the number of arithmetic operations to a maximum of 2-3 per line. Too many operations in a single line can make the code difficult to read and understand, increase the likelihood of mistakes, and complicate the process of debugging and reviewing the code. Consider splitting such operations over more than one line, take special care when dealing with division however. Try to limit the number of arithmetic operations to a maximum of 3 per line.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();

195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L149) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L198)


</details>


### [NC&#x2011;4] Constants in comparisons should appear on the left side 



*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit `MAX_VAULTS`
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

//@audit `MAX_VAULTS_KEROSENE`
87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();

//@audit `0`
101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

//@audit `0`
113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

//@audit `MIN_COLLATERIZATION_RATIO`
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

//@audit `MIN_COLLATERIZATION_RATIO`
167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); //@audit-info need to be investigated

//@audit `MIN_COLLATERIZATION_RATIO`
214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

//@audit `1e18`
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

//@audit `0`
237:       if (_dyad == 0) return type(uint).max;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L74-L74) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L87-L87), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L101-L101), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L113-L113), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L152-L152), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L167-L167), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L214-L214), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L217-L217), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L237-L237)


```solidity

File: ./src/core/KerosineManager.sol

//@audit `MAX_VAULTS`
24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults(); //@audit VULN: the kerozineManager owner can add more than 5 vaults as the max vaults in this contract is 10 different than the vaultManager contract


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L24-L24) 


</details>


### [NC&#x2011;5] Custom error has no error details 
Consider adding parameters to the error to indicate which user or values caused the failure


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L8-L8) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L9-L9), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L10-L10)


</details>


### [NC&#x2011;6] Dependence on external protocols 
External protocols should be monitored as such dependencies may introduce vulnerabilities if a vulnerability is found /introduced in the external protocol


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./script/deploy/Deploy.V2.s.sol

14: import {IAggregatorV3}          from "../../src/interfaces/IAggregatorV3.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L14-L14) 


</details>


### [NC&#x2011;7] Events are missing sender information 
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.


*There are 9 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

200:       emit RedeemDyad(id, vault, amount, to);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L77-L77) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L90-L90), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L103-L103), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L115-L115), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L168-L168), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L200-L200)


```solidity

File: ./src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L44-L44) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L57-L57)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L40-L40) 


</details>


### [NC&#x2011;8] Events may be emitted out of order due to reentrancy 
Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

168:     emit MintDyad(id, amount, to);

180:     emit BurnDyad(id, amount, msg.sender);

200:       emit RedeemDyad(id, vault, amount, to);

227:       emit Liquidate(id, msg.sender, to);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L168-L168) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L180-L180), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L200-L200), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L227-L227)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

40:     emit Withdraw(id, to, amount);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L40-L40) 


</details>


### [NC&#x2011;9] Defining All External/Public Functions in Contract Interfaces 
It is preferable to have all the external and public function in an interface to make using them easier by developers. This helps ensure the whole API is extracted in a interface.


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L62) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L86), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L106-L112), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L235), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L246), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L255), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L274), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L295), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L305)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L28) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L46) 


```solidity

File: ./src/core/KerosineManager.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L37-L40) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L49)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {
37:     vm.startBroadcast();  // ----------------------


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L36-L37) 


```solidity

File: ./src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {
18:     // @dev: We subtract all the Kerosene in the multi-sig.


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L18) 


</details>


### [NC&#x2011;10] Fixed Compiler Version Required for Non-Library/Interface Files 



*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit `VaultManagerV2` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

//@audit `BoundedKerosineVault` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

//@audit `KerosineVault` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit `UnboundedKerosineVault` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

//@audit `KerosineManager` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

//@audit `DeployV2` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

//@audit `KerosineDenominator` 
2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;11] Imports could be organized more systematically 
The contract used interfaces should be imported first, followed by all other files. The examples below do not follow this layout.


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

8: import {IVaultManager}   from "../interfaces/IVaultManager.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L8-L8) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

5: import {IVaultManager}          from "../interfaces/IVaultManager.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L5-L5) 


```solidity

File: ./src/core/Vault.kerosine.sol

6: import {IVault}          from "../interfaces/IVault.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L6-L6) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

5: import {IVaultManager}        from "../interfaces/IVaultManager.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L5-L5) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

13: import {IWETH}                  from "../../src/interfaces/IWETH.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L13-L13) 


</details>


### [NC&#x2011;12] Import declarations should import specific identifiers, rather than the whole file 
Using import declarations of the form `import {<identifier_name>} from "some/ file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./script/deploy/Deploy.V2.s.sol

4: import "forge-std/Script.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L4-L4) 


</details>


### [NC&#x2011;13] Inconsistent spacing in comments 
Some lines use `// x` and some use `//x`. The instances below point out the usages that don't follow the majority, within each file


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 

128:     Vault _vault = Vault(vault);//@audit VULN: the vault is not checked to see if it is licensed or not (NEED PoC)

151:     _vault.withdraw(id, to, amount); //@audit VULN: it is possible to have a sleepage here ... need more investigations

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); //@audit-info need to be investigated

199:       withdraw(id, vault, asset, to); //@audit VULN: it is possible to have a sleepage here ... need more investigations


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L22) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L128-L128), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L151-L151), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L167-L167), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L199-L199)


```solidity

File: ./src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults(); //@audit VULN: the kerozineManager owner can add more than 5 vaults as the max vaults in this contract is 10 different than the vaultManager contract


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L24-L24) 


</details>


### [NC&#x2011;14] Incorrect NatSpec Syntax 
In Solidity, just like in most other programming languages, regular comments serve to make code more understandable for developers. These are usually denoted by `//` for single line comments, or `/* ... */` for multi-line comments, and are ignored by the compiler.
On the other hand, NatSpec comments in Solidity, denoted by `///` for single - line comments, or`/** ... */` for multi - line comments, serve a different purpose.Besides aiding developer comprehension, they also form a part of the contract's interface, as they can be parsed and used by tools such as automated documentation generators or IDEs to provide users with details about the contract's functions, parameters and behavior.NatSpec comments can also be retrieved via JSON interfaces, and as such, they're included in the contract's ABI.
Thus, using`///` and `/** ... */` appropriately ensures not only proper documentation for developers, but also helps create a richer and more informative interface for users and external tools interacting with your contract.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/staking/KerosineDenominator.sol

18:     // @dev: We subtract all the Kerosene in the multi-sig.


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L18-L18) 


</details>


### [NC&#x2011;15] Long lines of code 
Usually lines in source code are limited to [80](https://softwareengineering.stackexchange.com/questions/148677/why-is-80-characters-the-standard-limit-for-code-width) characters. Today's screens are much larger so it's reasonable to stretch this in some cases. The solidity style guide recommends a maximumum line length of [120 characters](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#maximum-line-length), so the lines below should be split when they reach that length.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L22) 


```solidity

File: ./src/core/KerosineManager.sol

24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults(); //@audit VULN: the kerozineManager owner can add more than 5 vaults as the max vaults in this contract is 10 different than the vaultManager contract


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L24-L24) 


</details>


### [NC&#x2011;16] `mapping` definitions do not follow the Solidity Style Guide 
See the [mappings](https://docs.soliditylang.org/en/latest/style-guide.html#mappings) section of the Solidity Style Guide


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L34-L34) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L35-L35), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L37-L37)


</details>


### [NC&#x2011;17] File is missing NatSpec 



*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

0: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L0-L0) 


```solidity

File: ./src/core/Vault.kerosine.sol

0: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L0-L0) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

0: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L0-L0) 


```solidity

File: ./src/core/KerosineManager.sol

0: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L0-L0) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

0: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L0-L0) 


</details>


### [NC&#x2011;18] Consider using later versions of solidity for more cappabilities 
Consider using solidity 0.8.18 or later to benefit from multiple things including the named mappings [named mappings](https://ethereum.stackexchange.com/a/145555) to make it easier to understand the purpose of each mapping


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;19] Use of `override` is unnecessary 
Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L44-L47) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L53) 


</details>


### [NC&#x2011;20] Remove `forge-std` import 
Logging and debugging libraries such as forge-std are crucial tools during the development phase of a smart contract, as they provide critical insights into the execution of the contract. However, it's essential to remove or disable these libraries in the production version of your contract. Leaving such libraries active in the final version can lead to unnecessary gas costs, as logging operations consume gas, and it can potentially expose sensitive internal state information.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./script/deploy/Deploy.V2.s.sol

4: import "forge-std/Script.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L4-L4) 


</details>


### [NC&#x2011;21] Setters should prevent re-setting of the same value 
This especially problematic when the setter also emits the same value, which may be confusing to offline parsers


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit `keroseneManager` and `_keroseneManager` are never checked for the same value setting
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L63) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

//@audit `unboundedKerosineVault` and `_unboundedKerosineVault` are never checked for the same value setting
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L29) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit `kerosineDenominator` and `_kerosineDenominator` are never checked for the same value setting
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L47) 


</details>


### [NC&#x2011;22] State variables should have `Natspec` comments 
Consider adding some `Natspec` comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.


*There are 21 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit MAX_VAULTS need comments
22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 

//@audit MAX_VAULTS_KEROSENE need comments
23:   uint public constant MAX_VAULTS_KEROSENE = 5;

//@audit MIN_COLLATERIZATION_RATIO need comments
25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

//@audit LIQUIDATION_REWARD need comments
26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

//@audit dNft need comments
28:   DNft     public immutable dNft;

//@audit dyad need comments
29:   Dyad     public immutable dyad;

//@audit vaultLicenser need comments
30:   Licenser public immutable vaultLicenser;

//@audit keroseneManager need comments
32:   KerosineManager public keroseneManager;

//@audit vaults need comments
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

//@audit vaultsKerosene need comments
35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

//@audit idToBlockOfLastDeposit need comments
37:   mapping (uint => uint) public idToBlockOfLastDeposit;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L22) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L23-L23), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L25-L25), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L26-L26), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L28-L28), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L29-L29), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L30-L30), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L32-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L34-L34), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L35-L35), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L37-L37)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

//@audit unboundedKerosineVault need comments
15:   UnboundedKerosineVault public unboundedKerosineVault;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L15-L15) 


```solidity

File: ./src/core/Vault.kerosine.sol

//@audit vaultManager need comments
15:   IVaultManager   public immutable vaultManager;

//@audit asset need comments
16:   ERC20           public immutable asset;

//@audit kerosineManager need comments
17:   KerosineManager public immutable kerosineManager;

//@audit id2asset need comments
19:   mapping(uint => uint) public id2asset;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L15-L15) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L16-L16), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L17-L17), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L19-L19)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit dyad need comments
18:   Dyad                 public immutable dyad;

//@audit kerosineDenominator need comments
19:   KerosineDenominator  public kerosineDenominator;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L18-L18) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L19-L19)


```solidity

File: ./src/core/KerosineManager.sol

//@audit MAX_VAULTS need comments
14:   uint public constant MAX_VAULTS = 10;

//@audit vaults need comments
16:   EnumerableSet.AddressSet private vaults;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L14-L14) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L16-L16)


```solidity

File: ./src/staking/KerosineDenominator.sol

//@audit kerosine need comments
9:   Kerosine public kerosine;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L9-L9) 


</details>


### [NC&#x2011;23] Contracts should have full test coverage 
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

@audit Multiple files
1: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L1-L1) 


</details>


### [NC&#x2011;24] [NatSpec] Natspec `@title` is missing from `contract` 



*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L17-L17) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L12-L12) 


```solidity

File: ./src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L12-L12) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L15-L15) 


```solidity

File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L7-L7) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

35: contract DeployV2 is Script, Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L35-L35) 


```solidity

File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L7-L7) 


</details>


### [NC&#x2011;25] Top level pragma declarations should be separated by two blank lines 



*There are 13 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;
3: 
4: import {DNft}            from "./DNft.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
16: 
17: contract VaultManagerV2 is IVaultManager, Initializable {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L15-L17)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;
3: 
4: import {KerosineVault}          from "./Vault.kerosine.sol";

10: import {ERC20} from "@solmate/src/tokens/ERC20.sol";
11: 
12: contract BoundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L10-L12)


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;
3: 
4: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

10: import {Owned}           from "@solmate/src/auth/Owned.sol";
11: 
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L10-L12)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;
3: 
4: import {KerosineVault}        from "./Vault.kerosine.sol";

13: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
14: 
15: contract UnboundedKerosineVault is KerosineVault {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L13-L15)


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;
3: 
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

5: import {Owned}         from "@solmate/src/auth/Owned.sol";
6: 
7: contract KerosineManager is Owned(msg.sender) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L5-L7)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;
3: 
4: import "forge-std/Script.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L4) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;
3: 
4: import {Parameters} from "../params/Parameters.sol";

5: import {Kerosine} from "../staking/Kerosine.sol";
6: 
7: contract KerosineDenominator is Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L4) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L5-L7)


</details>


### [NC&#x2011;26] Critical functions should be a two step procedure 
Critical functions in Solidity contracts should follow a two-step procedure to enhance security, minimize human error, and ensure proper access control. By dividing sensitive operations into distinct phases, such as initiation and confirmation, developers can introduce a safeguard against unintended actions or unauthorized access.


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/KerosineManager.sol

18:   function add(

28:   function remove(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L18-L18) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L28)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43) 


</details>


### [NC&#x2011;27] uint variables should have the bit size defined explicitly 
Instead of using uint to declare uint258, explicitly define uint258 to ensure there is no confusion


*There are 72 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit `MAX_VAULTS`
22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 

//@audit `MAX_VAULTS_KEROSENE`
23:   uint public constant MAX_VAULTS_KEROSENE = 5;

//@audit `MIN_COLLATERIZATION_RATIO`
25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

//@audit `LIQUIDATION_REWARD`
26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

//@audit `id`
39:   modifier isDNftOwner(uint id) {

//@audit `id`
42:   modifier isValidDNft(uint id) {

//@audit `id`
68:       uint    id,

//@audit `id`
81:       uint    id,

//@audit `id`
95:       uint    id,

//@audit `id`
107:       uint    id,

//@audit `id`
120:     uint    id,

//@audit `amount`
122:     uint    amount

//@audit `id`
135:     uint    id,

//@audit `amount`
137:     uint    amount,

//@audit `id`
157:     uint    id,

//@audit `amount`
158:     uint    amount,

//@audit `id`
173:     uint id,

//@audit `amount`
174:     uint amount

//@audit `id`
185:     uint    id,

//@audit `amount`
187:     uint    amount,

//@audit ``
192:     returns (uint) { 

//@audit `id`
206:     uint id,

//@audit `to`
207:     uint to

//@audit `id`
231:     uint id

//@audit ``
235:     returns (uint) {

//@audit `id`
242:     uint id

//@audit ``
246:     returns (uint) {

//@audit `id`
251:     uint id

//@audit ``
255:     returns (uint) {

//@audit `id`
270:     uint id

//@audit ``
274:     returns (uint) {

//@audit `id`
291:     uint id

//@audit `id`
300:     uint    id,

//@audit `dyadMinted`
144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

//@audit `value`
146:     uint value = amount * _vault.assetPrice() 

//@audit `newDyadMinted`
164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

//@audit `asset`
195:       uint asset = amount 

//@audit `cr`
213:       uint cr = collatRatio(id);

//@audit `cappedCr`
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

//@audit `liquidationEquityShare`
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

//@audit `liquidationAssetShare`
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

//@audit `numberOfVaults`
221:       uint numberOfVaults = vaults[id].length();

//@audit `_dyad`
236:       uint _dyad = dyad.mintedDyad(address(this), id);

//@audit `totalUsdValue`
256:       uint totalUsdValue;

//@audit `numberOfVaults`
257:       uint numberOfVaults = vaults[id].length(); 

//@audit `totalUsdValue`
275:       uint totalUsdValue;

//@audit `numberOfVaults`
276:       uint numberOfVaults = vaultsKerosene[id].length(); 

//@audit `collateral`
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

//@audit `usdValue`
260:         uint usdValue;

//@audit `usdValue`
279:         uint usdValue;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L22) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L23-L23), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L25-L25), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L26-L26), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L39-L39), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L42-L42), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L68-L68), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L81-L81), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L95-L95), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L107-L107), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L120-L120), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L122-L122), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L135-L135), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L137-L137), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L157-L157), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L158-L158), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L173-L173), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L174-L174), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L185-L185), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L187-L187), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L192-L192), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L206-L206), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L207-L207), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L231-L231), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L235-L235), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L242-L242), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L246-L246), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L251-L251), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L255-L255), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L270-L270), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L274-L274), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L291-L291), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L300-L300), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L144-L144), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L146), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L164-L164), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L195), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L213-L213), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L217-L217), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L218-L218), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L219-L219), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L221-L221), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L236-L236), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L256-L256), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L257-L257), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L275-L275), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L276-L276), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L224-L224), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L260-L260), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L279-L279)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

//@audit `id`
13:   error NotWithdrawable(uint id, address to, uint amount);

//@audit `amount`
13:   error NotWithdrawable(uint id, address to, uint amount);

//@audit `id`
33:     uint    id,

//@audit `amount`
35:     uint    amount

//@audit ``
48:     returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L13-L13) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L13-L13), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L33-L33), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L35-L35), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L48-L48)


```solidity

File: ./src/core/Vault.kerosine.sol

//@audit `id`
37:     uint id,

//@audit `amount`
38:     uint amount

//@audit `from`
48:     uint from,

//@audit `to`
49:     uint to,

//@audit `amount`
50:     uint amount

//@audit `id`
61:     uint id

//@audit ``
65:     returns (uint) {

//@audit ``
73:     returns (uint); 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L37-L37) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L38-L38), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L48-L48), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L49-L49), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L50-L50), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L61-L61), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L65-L65), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L73-L73)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit `id`
31:     uint    id,

//@audit `amount`
33:     uint    amount

//@audit ``
54:     returns (uint) {

//@audit `tvl`
55:       uint tvl;

//@audit `numberOfVaults`
57:       uint numberOfVaults = vaults.length;

//@audit `numerator`
65:       uint numerator   = tvl - dyad.totalSupply();

//@audit `denominator`
66:       uint denominator = kerosineDenominator.denominator();


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L31-L31) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L33-L33), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L54-L54), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L55-L55), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L57-L57), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L65-L65), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L66-L66)


```solidity

File: ./src/core/KerosineManager.sol

//@audit `MAX_VAULTS`
14:   uint public constant MAX_VAULTS = 10;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L14-L14) 


```solidity

File: ./src/staking/KerosineDenominator.sol

//@audit ``
17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L17) 


</details>


### [NC&#x2011;28] Uncommented fields in a struct 
Consider adding comments for all the fields in a struct to improve the readability of the codebase.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./script/deploy/Deploy.V2.s.sol

//@audit Add explanational comments to the following items `kerosene`, `vaultLicenser`, `vaultManager`, `ethVault`, `wstEth`, `kerosineManager`, `unboundedKerosineVault`, `boundedKerosineVault`, `kerosineDenominator`, 
23: struct Contracts {
24:   Kerosine               kerosene;
25:   Licenser               vaultLicenser;
26:   VaultManagerV2         vaultManager;
27:   Vault                  ethVault;
28:   VaultWstEth            wstEth;
29:   KerosineManager        kerosineManager;
30:   UnboundedKerosineVault unboundedKerosineVault;
31:   BoundedKerosineVault   boundedKerosineVault;
32:   KerosineDenominator    kerosineDenominator;
33: }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L23-L33) 


</details>


### [NC&#x2011;29] Unused Import 
Some files/Items are imported but never used


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

//@audit `Dyad` is not used
6: import {Dyad}                   from "./Dyad.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L6-L6) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit `BoundedKerosineVault` is not used
9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L9-L9) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

//@audit `IWETH` is not used
13: import {IWETH}                  from "../../src/interfaces/IWETH.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L13-L13) 


</details>


### [NC&#x2011;30] Unused `modifier` definition 
The following modifier are never used, consider to remove them.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit isLicensed is never used
45:   modifier isLicensed(address vault) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L45-L45) 


</details>


### [NC&#x2011;31] Use the latest solidity (prior to 0.8.20 if on L2s) for deployment 
```
When deploying contracts, you should use the latest released version of Solidity.Apart from exceptional cases, only the latest version receives security fixes.
```
https://docs.soliditylang.org/en/v0.8.20/


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;32] Use a single file for system wide constants 
Consider grouping all the system constants under a single file. This finding shows only the first constant for each file.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L22) 


```solidity

File: ./src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L14-L14) 


</details>


### [NC&#x2011;33] Consider using SMTChecker 
The SMTChecker is a valuable tool for Solidity developers as it helps detect potential vulnerabilities and logical errors in the contract's code. By utilizing Satisfiability Modulo Theories (SMT) solvers, it can reason about the potential states a contract can be in, and therefore, identify conditions that could lead to undesirable behavior. This automatic formal verification can catch issues that might otherwise be missed in manual code reviews or standard testing, enhancing the overall contract's security and reliability.


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;34] Whitespace in Expressions 
See the [Whitespace in Expressions](https://docs.soliditylang.org/en/latest/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide


*There are 12 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit reduce the number of whiteSpace before the '=' char
22:   uint public constant MAX_VAULTS          = 5; //@audit VULN: the value here is different than the one in KerosineManager, one of them is wrong 
23:   uint public constant MAX_VAULTS_KEROSENE = 5;

//@audit reduce the number of whiteSpace before the '=' char
26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
27: 

//@audit reduce the number of whiteSpace before the '=' char
54:     dNft          = _dNft;
55:     dyad          = _dyad;

//@audit reduce the number of whiteSpace before the '=' char
55:     dyad          = _dyad;
56:     vaultLicenser = _licenser;

//@audit reduce the number of whiteSpace before the '=' char
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

//@audit reduce the number of whiteSpace before the '=' char
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
220: 

//@audit reduce the number of whiteSpace before the '=' char
223:           Vault vault      = Vault(vaults[id].at(i));
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L22-L23) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L26-L27), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L54-L55), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L55-L56), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L217-L218), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L219-L220), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L223-L224)


```solidity

File: ./src/core/Vault.kerosine.sol

//@audit reduce the number of whiteSpace before the '=' char
31:     vaultManager    = _vaultManager;
32:     asset           = _asset;

//@audit reduce the number of whiteSpace before the '=' char
32:     asset           = _asset;
33:     kerosineManager = _kerosineManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L31-L32) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L32-L33)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit reduce the number of whiteSpace before the '=' char
65:       uint numerator   = tvl - dyad.totalSupply();
66:       uint denominator = kerosineDenominator.denominator();


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L65-L66) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

//@audit reduce the number of whiteSpace before the '=' char
78:     BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault(
79:       vaultManager,

//@audit reduce the number of whiteSpace before the '=' char
84:     KerosineDenominator kerosineDenominator       = new KerosineDenominator(
85:       Kerosine(MAINNET_KEROSENE)


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L78-L79) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L84-L85)


</details>


### [NC&#x2011;35] [NatSpec] Natspec `@dev` is missing from `contract` 



*There are 54 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

66:   /// @inheritdoc IVaultManager

80:   function addKerosene(

93:   /// @inheritdoc IVaultManager

106:   function removeKerosene(

118:   /// @inheritdoc IVaultManager

133:   /// @inheritdoc IVaultManager

155:   /// @inheritdoc IVaultManager

171:   /// @inheritdoc IVaultManager

183:   /// @inheritdoc IVaultManager

204:   /// @inheritdoc IVaultManager

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L17-L17) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L39-L39), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L42-L42), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L45-L45), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L49-L49), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L66-L66), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L80), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L93-L93), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L106-L106), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L118-L118), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L133-L133), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L155-L155), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L171-L171), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L183-L183), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L204-L204), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L230), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L241), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L250), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L269), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L290), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L299)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

13:   error NotWithdrawable(uint id, address to, uint amount);

17:   constructor(

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L12-L12) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L13-L13), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L17-L17), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L44-L44)


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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L12-L12) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L21-L21), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L26-L26), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L36-L36), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L47-L47), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L60-L60), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L69-L69)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

21:   constructor(

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

50:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L15-L15) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L21-L21), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L30), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L50)


```solidity

File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L7-L7) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L8-L8), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L9-L9), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L10-L10), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L18-L18), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L28), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L37-L37), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L44)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

23: struct Contracts {

35: contract DeployV2 is Script, Parameters {

36:   function run() public returns (Contracts memory) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L23-L23) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L35-L35), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L36-L36)


```solidity

File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

11:   constructor(

17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L7-L7) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L11-L11), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L17)


</details>


### [NC&#x2011;36] Contract should expose an `interface` 
The `contract`s should expose an `interface` so that other projects can more easily integrate with it, without having to develop their own non-standard variants.


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

80:   function addKerosene(

106:   function removeKerosene(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L80), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L106-L106), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L230), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L241), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L250), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L269), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L290), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L299)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43) 


```solidity

File: ./src/core/KerosineManager.sol

37:   function getVaults() 

44:   function isLicensed(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L37-L37) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L44)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L36-L36) 


```solidity

File: ./src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L17) 


</details>


### [NC&#x2011;37] Named imports of parent contracts are missing 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./script/deploy/Deploy.V2.s.sol

//@audit `Script`
35: contract DeployV2 is Script, Parameters {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L35-L35) 


</details>


### [NC&#x2011;38] [NatSpec] Natspec `@notice` is missing from `contract` 



*There are 54 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

66:   /// @inheritdoc IVaultManager

80:   function addKerosene(

93:   /// @inheritdoc IVaultManager

106:   function removeKerosene(

118:   /// @inheritdoc IVaultManager

133:   /// @inheritdoc IVaultManager

155:   /// @inheritdoc IVaultManager

171:   /// @inheritdoc IVaultManager

183:   /// @inheritdoc IVaultManager

204:   /// @inheritdoc IVaultManager

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L17-L17) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L39-L39), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L42-L42), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L45-L45), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L49-L49), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L66-L66), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L80), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L93-L93), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L106-L106), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L118-L118), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L133-L133), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L155-L155), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L171-L171), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L183-L183), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L204-L204), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L230), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L241), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L250), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L269), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L290), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L299)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

13:   error NotWithdrawable(uint id, address to, uint amount);

17:   constructor(

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L12-L12) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L13-L13), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L17-L17), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L44-L44)


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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L12-L12) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L21-L21), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L26-L26), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L36-L36), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L47-L47), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L60-L60), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L69-L69)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

21:   constructor(

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

50:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L15-L15) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L21-L21), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L30), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L50)


```solidity

File: ./src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L7-L7) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L8-L8), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L9-L9), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L10-L10), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L18-L18), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L28), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L37-L37), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L44)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

23: struct Contracts {

35: contract DeployV2 is Script, Parameters {

36:   function run() public returns (Contracts memory) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L23-L23) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L35-L35), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L36-L36)


```solidity

File: ./src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

11:   constructor(

17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L7-L7) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L11-L11), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L17)


</details>


### [NC&#x2011;39] Consider splitting long calculations 
The longer a string of operations is, the harder it is to understand it. Consider splitting the full calculation into more steps, with more descriptive temporary variable names, and add extensive comments.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.unbounded.sol

60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L60-L63) 


</details>


### [NC&#x2011;40] Top-level declarations should be separated by at least two lines 



*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

57:   }
58: 
59:   function setKeroseneManager(KerosineManager _keroseneManager) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L57-L59) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
22: 
23:   function setUnboundedKerosineVault(

30:   }
31: 
32:   function withdraw(

42:   }
43: 
44:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L21-L23) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L30-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L42-L44)


```solidity

File: ./src/core/Vault.kerosine.sol

34:   }
35: 
36:   function deposit(

45:   }
46: 
47:   function move(

58:   }
59: 
60:   function getUsdValue(

67:   }
68: 
69:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L34-L36) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L45-L47), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L58-L60), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L67-L69)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

28:   }
29: 
30:   function withdraw(

41:   }
42: 
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

48:   }
49: 
50:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L28-L30) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L41-L43), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L48-L50)


```solidity

File: ./src/core/KerosineManager.sol

26:   }
27: 
28:   function remove(

35:   }
36: 
37:   function getVaults() 

42:   }
43: 
44:   function isLicensed(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L26-L28) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L35-L37), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L42-L44)


```solidity

File: ./src/staking/KerosineDenominator.sol

15:   }
16: 
17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L15-L17) 


</details>


### [NC&#x2011;41] `immutable` variable names don\'t follow the Solidity style guide 
For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L28-L28) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L29-L29), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L30-L30)


```solidity

File: ./src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L15-L15) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L16-L16), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L17-L17)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L18-L18) 


</details>


### [NC&#x2011;42] Use the latest Solidity version for better security 
Using the latest solidity version will help avoid old compiler related vulnerabilities


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;43] Consider adding formal verification proofs 
Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

@audit Should implement invariant tests
1: 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L1-L1) 


</details>


### [NC&#x2011;44] Use `@inheritdoc` for overridden functions 



*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L44-L44) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L50) 


</details>


### [NC&#x2011;45] constructor should emit an event 
Use events to signal significant changes to off-chain monitoring tools.


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L49-L57) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L17-L21) 


```solidity

File: ./src/core/Vault.kerosine.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L26-L34) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27:       dyad = _dyad;
28:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L21-L28) 


```solidity

File: ./src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L11-L15) 


</details>


### [NC&#x2011;46] Complex functions should include comments 
Large and/or complex functions should include comments to make them easier to understand and reduce margin for error.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

205:   function liquidate(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L205-L205) 


</details>


### [NC&#x2011;47] [Solidity]: All `verbatim` blocks are considered identical by deduplicator and can incorrectly be unified 
The block deduplicator is a step of the opcode-based optimizer which identifies equivalent assembly blocks and merges them into a single one. However, when blocks contained `verbatim`, their comparison was performed incorrectly, leading to the collapse of assembly blocks which are identical except for the contents of the ``verbatim`` items. Since `verbatim` is only available in Yul, compilation of Solidity sources is not affected. For more details check the following [link](https://blog.soliditylang.org/2023/11/08/verbatim-invalid-deduplication-bug/)


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;48] [NatSpec] Natspec `@param` is missing from `error` 



*There are 29 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

49:   constructor(

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

80:   function addKerosene(

106:   function removeKerosene(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L39-L39) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L42-L42), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L45-L45), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L49-L49), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L80), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L106-L106), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L230), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L241), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L250), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L269), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L290), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L299)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

17:   constructor(

23:   function setUnboundedKerosineVault(

32:   function withdraw(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L13-L13) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L17-L17), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L23), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L32)


```solidity

File: ./src/core/Vault.kerosine.sol

26:   constructor(

36:   function deposit(

47:   function move(

60:   function getUsdValue(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L26-L26) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L36-L36), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L47-L47), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L60-L60)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

21:   constructor(

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L21-L21) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L30), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43)


```solidity

File: ./src/core/KerosineManager.sol

18:   function add(

28:   function remove(

44:   function isLicensed(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L18-L18) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L28), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L44)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

23: struct Contracts {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L23-L23) 


```solidity

File: ./src/staking/KerosineDenominator.sol

11:   constructor(


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L11-L11) 


</details>


### [NC&#x2011;49] OpenZeppelin libraries should be upgraded to a newer version 
These contracts import some OpenZeppelin libraries, but they are using an old version.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L14-L14) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L15-L15)


```solidity

File: ./src/core/KerosineManager.sol

4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L4-L4) 


</details>


### [NC&#x2011;50] Non constant/immutable state variables are missing a setter post deployment 
Non-constant or non-immutable state variables lacking a setter function can create inflexibility in contract operations. If there's no way to update these variables post-deployment, the contract might not adapt to changing conditions or requirements, which can be a significant drawback, especially in upgradable or long-lived contracts. To resolve this, implement setter functions guarded by appropriate access controls, like `onlyOwner` or similar modifiers, so that these variables can be updated as required while maintaining security. This enables smoother contract maintenance and feature upgrades.


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L34-L34) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L35-L35)


```solidity

File: ./src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L16-L16) 


```solidity

File: ./src/staking/KerosineDenominator.sol

9:   Kerosine public kerosine;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L9-L9) 


</details>


### [NC&#x2011;51] Consider making private state variables internal to increase flexibility 
In Solidity, `private` state variables are strictly confined to the contract they are defined in and can't be accessed or modified by its derived contracts. While this offers strong encapsulation, it can limit contract extensibility and modification in inheritance chains. On the other hand, `internal` variables can be accessed and potentially overridden by child contracts, granting more flexibility in contract development and upgrades. Therefore, it's recommended to use `private` only when you explicitly want to prevent child contract access. Otherwise, prefer `internal` to maintain a balance between encapsulation and the flexibility offered by inheritance patterns in Solidity.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L16-L16) 


</details>


### [NC&#x2011;52] Lack of space near the operator 
Lack of space near operators in code can lead to reduced readability, making it more challenging to distinguish between different elements and understand the logic quickly. As a resolution, always include spaces around operators to ensure a clear visual separation, which promotes better maintainability and comprehension of the code.


*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit operator : /
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();

//@audit operator : /
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();

//@audit operator : /
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;

//@audit operator : /
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 

//@audit operator : /
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 

//@audit operator : *
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 

//@audit operator : +
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L149) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L149), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L198), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L146-L148), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L197), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L195-L196), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L196-L196)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit operator : /
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());

//@audit operator : /
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());

//@audit operator : /
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L60-L63) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L60-L63), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L60-L62)


</details>


### [NC&#x2011;53] Incorrect withdraw declaration 
In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for `withdraw` should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {
143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
144:     uint dyadMinted = dyad.mintedDyad(address(this), id);
145:     Vault _vault = Vault(vault);
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();
150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
151:     _vault.withdraw(id, to, amount); //@audit VULN: it is possible to have a sleepage here ... need more investigations
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
153:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L134-L153) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:     view
39:       onlyVaultManager
40:   {
41:     revert NotWithdrawable(id, to, amount);
42:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L42) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {
38:     id2asset[id] -= amount;
39:     asset.safeTransfer(to, amount); 
40:     emit Withdraw(id, to, amount);
41:   }


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L41) 


</details>


### [NC&#x2011;54] A event should be emitted if a non immutable state variable is set in a constructor 



*There are 8 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

54:     dNft          = _dNft;

55:     dyad          = _dyad;

56:     vaultLicenser = _licenser;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L54-L54) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L55-L55), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L56-L56)


```solidity

File: ./src/core/Vault.kerosine.sol

31:     vaultManager    = _vaultManager;

32:     asset           = _asset;

33:     kerosineManager = _kerosineManager;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L31-L31) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L32-L32), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L33-L33)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

27:       dyad = _dyad;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L27-L27) 


```solidity

File: ./src/staking/KerosineDenominator.sol

14:     kerosine = _kerosine;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L14-L14) 


</details>


### [NC&#x2011;55] [Solidity]: Order of Argument Evaluation Disrupted in Non-Expression-Split Code by Optimizer Sequences with FullInliner 
Function call arguments in Yul are evaluated right to left. This order matters when the argument expressions have side-effects, and changing it may change contract behavior. FullInliner is an optimizer step that can replace a function call with the body of that function. The transformation involves assigning argument expressions to temporary variables, which imposes an explicit evaluation order. FullInliner was written with the assumption that this order does not necessarily have to match usual argument evaluation order because the argument expressions have no side-effects. In most circumstances this assumption is true because the default optimization step sequence contains the ExpressionSplitter step. ExpressionSplitter ensures that the code is in *expression-split form*, which means that function calls cannot appear nested inside expressions, and all function call arguments have to be variables. The assumption is, however, not guaranteed to be true in general. Version 0.6.7 introduced a setting allowing users to specify an arbitrary optimization step sequence, making it possible for the FullInliner to actually encounter argument expressions with side-effects, which can result in behavior differences between optimized and unoptimized bytecode. Contracts compiled without optimization or with the default optimization sequence are not affected. To trigger the bug the user has to explicitly choose compiler settings that contain a sequence with FullInliner step not preceded by ExpressionSplitter. [Ref](https://blog.soliditylang.org/2023/07/19/full-inliner-non-expression-split-argument-evaluation-order-bug/)


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L2-L2) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L2-L2) 


```solidity

File: ./src/core/KerosineManager.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L2-L2) 


```solidity

File: ./script/deploy/Deploy.V2.s.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L2-L2) 


```solidity

File: ./src/staking/KerosineDenominator.sol

2: pragma solidity =0.8.17;


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L2-L2) 


</details>


### [NC&#x2011;56] Use named return values 
Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.


*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L184-L192) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L230-L235), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L241-L246), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L250-L255), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L269-L274), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L290-L295), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L305)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L44-L48) 


```solidity

File: ./src/core/Vault.kerosine.sol

60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view 
65:     returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.sol#L60-L65) 


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L50-L54) 


```solidity

File: ./src/core/KerosineManager.sol

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

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L37-L40) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L49)


```solidity

File: ./script/deploy/Deploy.V2.s.sol

36:   function run() public returns (Contracts memory) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./script/deploy/Deploy.V2.s.sol#L36-L36) 


```solidity

File: ./src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/staking/KerosineDenominator.sol#L17-L17) 


</details>


### [NC&#x2011;57] Consider adding validation of user inputs 



*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

//@audit these parameters `_keroseneManager`, are not checked
59:   function setKeroseneManager(KerosineManager _keroseneManager) 

//@audit these parameters `vault`, are not checked
67:   function add(
68:       uint    id,
69:       address vault

//@audit these parameters `vault`, are not checked
80:   function addKerosene(
81:       uint    id,
82:       address vault

//@audit these parameters `vault`, are not checked
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount

//@audit these parameters `vault`,`to`, are not checked
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to

//@audit these parameters `to`, are not checked
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to

//@audit these parameters `vault`,`to`, are not checked
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to

//@audit these parameters `vault`, are not checked
299:   function hasVault(
300:     uint    id,
301:     address vault


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L59-L59) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L67-L69), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L80-L82), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L119-L122), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L134-L138), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L156-L159), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L184-L188), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L299-L301)


```solidity

File: ./src/core/Vault.kerosine.bounded.sol

//@audit these parameters `_unboundedKerosineVault`, are not checked
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault

//@audit these parameters `to`, are not checked
32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L23-L24) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.bounded.sol#L32-L35)


```solidity

File: ./src/core/Vault.kerosine.unbounded.sol

//@audit these parameters `to`, are not checked
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount

//@audit these parameters `_kerosineDenominator`, are not checked
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L30-L33) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/Vault.kerosine.unbounded.sol#L43-L43)


```solidity

File: ./src/core/KerosineManager.sol

//@audit these parameters `vault`, are not checked
18:   function add(
19:     address vault

//@audit these parameters `vault`, are not checked
28:   function remove(
29:     address vault

//@audit these parameters `vault`, are not checked
44:   function isLicensed(
45:     address vault


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L18-L19) , [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L28-L29), [link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/KerosineManager.sol#L44-L45)


</details>


### [NC&#x2011;58] Consider using named function calls 
Named function calls in Solidity greatly improve code readability by explicitly mapping arguments to their respective parameter names. This clarity becomes critical when dealing with functions that have numerous or complex parameters, reducing potential errors due to misordered arguments. Therefore, adopting named function calls contributes to more maintainable and less error-prone code.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./src/core/VaultManagerV2.sol

199:       withdraw(id, vault, asset, to); //@audit VULN: it is possible to have a sleepage here ... need more investigations


```

[link](https://github.com/code-423n4/2024-04-dyad/blob/main//./src/core/VaultManagerV2.sol#L199-L199) 


</details>
