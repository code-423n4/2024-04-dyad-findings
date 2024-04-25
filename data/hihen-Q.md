# QA Report

## Summary

### Low Issues

Total **63 instances** over **15 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[L-01]](#l-01-missing-storage-gap-for-upgradeable-contracts) | Missing storage gap for upgradeable contracts | 1 |
| [[L-02]](#l-02-events-may-be-emitted-out-of-order-due-to-reentrancy) | Events may be emitted out of order due to reentrancy | 8 |
| [[L-03]](#l-03-upgradable-contracts-need-a-constructor-to-init-and-lock-the-implementation-contract) | Upgradable contracts need a constructor to init and lock the implementation contract | 1 |
| [[L-04]](#l-04-missing-zero-address-check-in-constructor) | Missing zero address check in constructor | 8 |
| [[L-05]](#l-05-missing-zero-address-check-in-initializer) | Missing zero address check in initializer | 1 |
| [[L-06]](#l-06-revert-on-transfer-to-the-zero-address) | Revert on transfer to the zero address | 2 |
| [[L-07]](#l-07-consider-implementing-two-step-procedure-for-updating-protocol-addresses) | Consider implementing two-step procedure for updating protocol addresses | 2 |
| [[L-08]](#l-08-use-ownable2step-instead-of-ownable) | Use Ownable2Step instead of Ownable | 4 |
| [[L-09]](#l-09-vulnerable-versions-of-packages-are-being-used) | Vulnerable versions of packages are being used | 5 |
| [[L-10]](#l-10-constructor--initialization-function-lacks-parameter-validation) | Constructor / initialization function lacks parameter validation | 12 |
| [[L-11]](#l-11-contracts-are-vulnerable-to-fee-on-transfer-accounting-related-issues) | Contracts are vulnerable to fee-on-transfer accounting-related issues | 2 |
| [[L-12]](#l-12-functions-calling-contractsaddresses-with-transfer-hooks-should-be-protected-by-reentrancy-guard) | Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard | 2 |
| [[L-13]](#l-13-critical-functions-should-be-controlled-by-time-locks) | Critical functions should be controlled by time locks | 8 |
| [[L-14]](#l-14-tokens-may-be-minted-to-the-zero-address) | Tokens may be minted to the zero address | 4 |
| [[L-15]](#l-15-code-does-not-follow-the-best-practice-of-check-effects-interaction) | Code does not follow the best practice of check-effects-interaction | 3 |

### Non Critical Issues

Total **196 instances** over **35 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[N-01]](#n-01-names-of-privateinternal-state-variables-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` state variables should be prefixed with an underscore | 3 |
| [[N-02]](#n-02-use-of-override-is-unnecessary) | Use of `override` is unnecessary | 2 |
| [[N-03]](#n-03-complex-math-should-be-split-into-multiple-steps) | Complex math should be split into multiple steps | 3 |
| [[N-04]](#n-04-consider-adding-a-blockdeny-list) | Consider adding a block/deny-list | 2 |
| [[N-05]](#n-05-constantsimmutables-redefined-elsewhere) | Constants/Immutables redefined elsewhere | 4 |
| [[N-06]](#n-06-contract-name-does-not-match-its-filename) | Contract name does not match its filename | 3 |
| [[N-07]](#n-07-consider-emitting-an-event-at-the-end-of-the-constructor) | Consider emitting an event at the end of the constructor | 5 |
| [[N-08]](#n-08-empty-function-body-without-comments) | Empty function body without comments | 1 |
| [[N-09]](#n-09-events-are-emitted-without-the-sender-information) | Events are emitted without the sender information | 9 |
| [[N-10]](#n-10-imports-could-be-organized-more-systematically) | Imports could be organized more systematically | 4 |
| [[N-11]](#n-11-invalid-natspec-comment-style) | Invalid NatSpec comment style | 1 |
| [[N-12]](#n-12-openzeppelincontracts-should-be-upgraded-to-a-newer-version) | @openzeppelin/contracts should be upgraded to a newer version | 3 |
| [[N-13]](#n-13-variable-names-for-immutables-should-use-upper_case_with_underscores) | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES | 7 |
| [[N-14]](#n-14-modifiers-should-be-named-in-mixedcase-style) | Modifiers should be named in mixedCase style | 2 |
| [[N-15]](#n-15-consider-adding-validation-of-user-inputs) | Consider adding validation of user inputs | 15 |
| [[N-16]](#n-16-constants-should-be-put-on-the-left-side-of-comparisons) | Constants should be put on the left side of comparisons | 2 |
| [[N-17]](#n-17-unnecessary-casting) | Unnecessary casting | 1 |
| [[N-18]](#n-18-unused-import) | Unused import | 34 |
| [[N-19]](#n-19-unused-modifiers) | Unused modifiers | 1 |
| [[N-20]](#n-20-use-the-latest-solidity-version) | Use the latest Solidity version | 6 |
| [[N-21]](#n-21-contract-variables-should-have-comments) | Contract variables should have comments | 3 |
| [[N-22]](#n-22-missing-event-when-a-state-variables-is-set-in-constructor) | Missing event when a state variables is set in constructor | 1 |
| [[N-23]](#n-23-multiple-mappings-with-same-keys-can-be-combined-into-a-single-struct-mapping-for-readability) | Multiple mappings with same keys can be combined into a single struct mapping for readability | 3 |
| [[N-24]](#n-24-missing-event-for-critical-changes) | Missing event for critical changes | 2 |
| [[N-25]](#n-25-duplicated-requirerevert-checks-should-be-refactored) | Duplicated `require()`/`revert()` checks should be refactored | 6 |
| [[N-26]](#n-26-consider-adding-emergency-stop-functionality) | Consider adding emergency-stop functionality | 4 |
| [[N-27]](#n-27-missing-checks-for-uint-state-variable-assignments) | Missing checks for uint state variable assignments | 1 |
| [[N-28]](#n-28-use-the-modern-upgradeable-contract-paradigm) | Use the Modern Upgradeable Contract Paradigm | 4 |
| [[N-29]](#n-29-large-or-complicated-code-bases-should-implement-invariant-tests) | Large or complicated code bases should implement invariant tests | 1 |
| [[N-30]](#n-30-the-default-value-is-manually-set-when-it-is-declared) | The default value is manually set when it is declared | 4 |
| [[N-31]](#n-31-contracts-should-have-all-publicexternal-functions-exposed-by-interfaces) | Contracts should have all `public`/`external` functions exposed by `interface`s | 5 |
| [[N-32]](#n-32-top-level-declarations-should-be-separated-by-at-least-two-lines) | Top-level declarations should be separated by at least two lines | 36 |
| [[N-33]](#n-33-consider-adding-formal-verification-proofs) | Consider adding formal verification proofs | 6 |
| [[N-34]](#n-34-prevent-re-setting-a-state-variable-with-the-same-value) | Prevent re-setting a state variable with the same value | 2 |
| [[N-35]](#n-35-whitespace-in-expressions) | Whitespace in Expressions | 10 |

## Low Issues

### [L-01] Missing storage gap for upgradeable contracts

Each upgradeable contract (even for most derived) should include a state variable of type fixed-size array (usually named [`__gap`](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/f4b309ae37dc650efa7523dd1230d230e3f452d7/contracts/token/ERC20/ERC20Upgradeable.sol#L383) and placed after all other variables) to provide reserved space in storage.
It allows the team to freely add new state variables in the future upgrades without compromising the storage compatibility with existing deployments.

There is 1 instance:

- *VaultManagerV2.sol* ( [17-17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L17-L17) ):

```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable {
```

### [L-02] Events may be emitted out of order due to reentrancy

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls.

<details>
<summary>There are 8 instances (click to show):</summary>

- *Vault.kerosine.unbounded.sol* ( [40-40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L40-L40) ):

```solidity
/// @audit safeTransfer() is called prior to this emission in withdraw()
40:     emit Withdraw(id, to, amount);
```

- *VaultManagerV2.sol* ( [77-77](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L77-L77), [103-103](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L103-L103), [115-115](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L115-L115), [168-168](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L168-L168), [180-180](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L180-L180), [200-200](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L200-L200), [227-227](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L227-L227) ):

```solidity
/// @audit isLicensed() is called prior to this emission in add()
77:     emit Added(id, vault);

/// @audit id2asset() is called prior to this emission in remove()
103:     emit Removed(id, vault);

/// @audit id2asset() is called prior to this emission in removeKerosene()
115:     emit Removed(id, vault);

/// @audit mint() is called prior to this emission in mintDyad()
168:     emit MintDyad(id, amount, to);

/// @audit burn() is called prior to this emission in burnDyad()
180:     emit BurnDyad(id, amount, msg.sender);

/// @audit burn() is called prior to this emission in redeemDyad()
200:       emit RedeemDyad(id, vault, amount, to);

/// @audit collatRatio() is called prior to this emission in liquidate(), which will call `mintedDyad()`
227:       emit Liquidate(id, msg.sender, to);
```

</details>

### [L-03] Upgradable contracts need a constructor to init and lock the implementation contract

An uninitialized contract can be taken over by an attacker. For an upgradable contract, this applies to both the proxy and its implementation contract, which may impact the proxy.
To prevent the implementation contract from being used, we should trigger the initialization in the constructor to automatically lock it when it is deployed.
For contracts that inherit `Initializable`, the `_disableInitializers()` function [is suggested to do this job](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/4d9d9073b84f56fe3eea360e5067c6ffd864c43d/contracts/proxy/utils/Initializable.sol#L43-L56).

There is 1 instance:

- *VaultManagerV2.sol* ( [49-53](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L49-L53) ):

```solidity
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
```

### [L-04] Missing zero address check in constructor

Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address (0x0). This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

<details>
<summary>There are 8 instances (click to show):</summary>

- *Vault.kerosine.sol* ( [26-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L26-L30) ):

```solidity
/// @audit `_vaultManager not checked`
/// @audit `_asset not checked`
/// @audit `_kerosineManager not checked`
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
```

- *Vault.kerosine.unbounded.sol* ( [21-26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L21-L26) ):

```solidity
/// @audit `_dyad not checked`
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

- *VaultManagerV2.sol* ( [49-53](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L49-L53) ):

```solidity
/// @audit `_dNft not checked`
/// @audit `_dyad not checked`
/// @audit `_licenser not checked`
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
```

- *KerosineDenominator.sol* ( [11-13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L11-L13) ):

```solidity
/// @audit `_kerosine not checked`
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

</details>

### [L-05] Missing zero address check in initializer

Consider adding a zero address check for each address type parameter in initializer.

There is 1 instance:

- *VaultManagerV2.sol* ( [59-59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L59-L59) ):

```solidity
/// @audit `_keroseneManager not checked`
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
```

### [L-06] Revert on transfer to the zero address

It's good practice to revert a token transfer transaction if the recipient's address is the zero address. This can prevent unintentional transfers to the zero address due to accidental operations or programming errors. Many token contracts implement such a safeguard, such as [OpenZeppelin - ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC20/ERC20.sol#L232), [OpenZeppelin - ERC721](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC721/ERC721.sol#L142).

There are 2 instances:

- *Vault.kerosine.unbounded.sol* ( [39-39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L39-L39) ):

```solidity
39:     asset.safeTransfer(to, amount); 
```

- *VaultManagerV2.sol* ( [129-129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L129-L129) ):

```solidity
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

### [L-07] Consider implementing two-step procedure for updating protocol addresses

A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the 'set' functions ensure that the recipient is of the right interface type.

There are 2 instances:

- *Vault.kerosine.bounded.sol* ( [23-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L23-L30) ):

```solidity
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }
```

- *Vault.kerosine.unbounded.sol* ( [43-48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L43-L48) ):

```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }
```

### [L-08] Use Ownable2Step instead of Ownable

[`Ownable2Step`](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/3d7a93876a2e5e1d7fe29b5a0e96e222afdc4cfa/contracts/access/Ownable2Step.sol#L31-L56) and [`Ownable2StepUpgradeable`](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/25aabd286e002a1526c345c8db259d57bdf0ad28/contracts/access/Ownable2StepUpgradeable.sol#L47-L63) prevent the contract ownership from mistakenly being transferred to an address that cannot handle it (e.g. due to a typo in the address), by requiring that the recipient of the owner permissions actively accept via a contract call of its own.

There are 4 instances:

- *KerosineManager.sol* ( [7-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L7-L7) ):

```solidity
7: contract KerosineManager is Owned(msg.sender) {
```

- *Vault.kerosine.bounded.sol* ( [12-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L12-L12) ):

```solidity
12: contract BoundedKerosineVault is KerosineVault {
```

- *Vault.kerosine.sol* ( [12-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L12-L12) ):

```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
```

- *Vault.kerosine.unbounded.sol* ( [15-15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15-L15) ):

```solidity
15: contract UnboundedKerosineVault is KerosineVault {
```

### [L-09] Vulnerable versions of packages are being used

This project is using specific package versions which are vulnerable to the specific CVEs listed below. Consider switching to more recent versions of these packages that don't have these vulnerabilities.
- [CVE-2023-40014](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-40014) - **MEDIUM** - (`openzeppelin-solidity >=4.0.0 <4.9.3`): OpenZeppelin Contracts is a library for secure smart contract development. Starting in version 4.0.0 and prior to version 4.9.3, contracts using `ERC2771Context` along with a custom trusted forwarder may see `_msgSender` return `address(0)` in calls that originate from the forwarder with calldata shorter than 20 bytes. This combination of circumstances does not appear to be common, in particular it is not the case for `MinimalForwarder` from OpenZeppelin Contracts, or any deployed forwarder the team is aware of, given that the signer address is appended to all calls that originate from these forwarders. The problem has been patched in v4.9.3.

- [CVE-2023-34459](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-34459) - **MEDIUM** - (`openzeppelin-solidity >=4.7.0 <4.9.2`): OpenZeppelin Contracts is a library for smart contract development. Starting in version 4.7.0 and prior to version 4.9.2, when the `verifyMultiProof`, `verifyMultiProofCalldata`, `procesprocessMultiProof`, or `processMultiProofCalldat` functions are in use, it is possible to construct merkle trees that allow forging a valid multiproof for an arbitrary set of leaves. A contract may be vulnerable if it uses multiproofs for verification and the merkle tree that is processed includes a node with value 0 at depth 1 (just under the root). This could happen inadvertedly for balanced trees with 3 leaves or less, if the leaves are not hashed. This could happen deliberately if a malicious tree builder includes such a node in the tree. A contract is not vulnerable if it uses single-leaf proving (`verify`, `verifyCalldata`, `processProof`, or `processProofCalldata`), or if it uses multiproofs with a known tree that has hashed leaves. Standard merkle trees produced or validated with the @openzeppelin/merkle-tree library are safe. The problem has been patched in version 4.9.2. Some workarounds are available. For those using multiproofs: When constructing merkle trees hash the leaves and do not insert empty nodes in your trees. Using the @openzeppelin/merkle-tree package eliminates this issue. Do not accept user-provided merkle roots without reconstructing at least the first level of the tree. Verify the merkle tree structure by reconstructing it from the leaves.

- [CVE-2023-30542](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-30542) - **HIGH** - (`openzeppelin-solidity >=4.7.0 <4.8.2`): OpenZeppelin Contracts is a library for secure smart contract development. The proposal creation entrypoint (`propose`) in `GovernorCompatibilityBravo` allows the creation of proposals with a `signatures` array shorter than the `calldatas` array. This causes the additional elements of the latter to be ignored, and if the proposal succeeds the corresponding actions would eventually execute without any calldata. The `ProposalCreated` event correctly represents what will eventually execute, but the proposal parameters as queried through `getActions` appear to respect the original intended calldata. This issue has been patched in 4.8.3. As a workaround, ensure that all proposals that pass through governance have equal length `signatures` and `calldatas` parameters.

- [CVE-2023-30541](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-30541) - **MEDIUM** - (`openzeppelin-solidity >=3.2.0 <4.8.3`): OpenZeppelin Contracts is a library for secure smart contract development. A function in the implementation contract may be inaccessible if its selector clashes with one of the proxy's own selectors. Specifically, if the clashing function has a different signature with incompatible ABI encoding, the proxy could revert while attempting to decode the arguments from calldata. The probability of an accidental clash is negligible, but one could be caused deliberately and could cause a reduction in availability. The issue has been fixed in version 4.8.3. As a workaround if a function appears to be inaccessible for this reason, it may be possible to craft the calldata such that ABI decoding does not fail at the proxy and the function is properly proxied through.

- [CVE-2023-26488](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-26488) - **MEDIUM** - (`openzeppelin-solidity >=4.8.0 <4.8.2`): OpenZeppelin Contracts is a library for secure smart contract development. The ERC721Consecutive contract designed for minting NFTs in batches does not update balances when a batch has size 1 and consists of a single token. Subsequent transfers from the receiver of that token may overflow the balance as reported by `balanceOf`. The issue exclusively presents with batches of size 1. The issue has been patched in 4.8.2.

There are 5 instances:

- Global finding

### [L-10] Constructor / initialization function lacks parameter validation

Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

<details>
<summary>There are 12 instances (click to show):</summary>

- *Vault.kerosine.bounded.sol* ( [17-21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L17-L21) ):

```solidity
/// @audit `_vaultManager`
/// @audit `_asset`
/// @audit `_kerosineManager`
17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

- *Vault.kerosine.sol* ( [26-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L26-L30) ):

```solidity
/// @audit `_vaultManager`
/// @audit `_asset`
/// @audit `_kerosineManager`
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
```

- *Vault.kerosine.unbounded.sol* ( [21-26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L21-L26) ):

```solidity
/// @audit `_dyad`
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

- *VaultManagerV2.sol* ( [49-53](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L49-L53), [59-62](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L59-L62) ):

```solidity
/// @audit `_dNft`
/// @audit `_dyad`
/// @audit `_licenser`
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {

/// @audit `_keroseneManager`
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
```

- *KerosineDenominator.sol* ( [11-13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L11-L13) ):

```solidity
/// @audit `_kerosine`
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

</details>

### [L-11] Contracts are vulnerable to fee-on-transfer accounting-related issues

Some tokens take a transfer fee (e.g. STA, PAXG), some do not currently charge a fee but may do so in the future (e.g. USDT, USDC).
The functions below transfer funds from the caller to the receiver via `transferFrom()`, but do not ensure that the actual number of tokens received is the same as the input amount to the transfer. If the token is a fee-on-transfer token, the balance after the transfer will be smaller than expected, leading to accounting issues. Even if there are checks later, related to a secondary transfer, an attacker may be able to use latent funds (e.g. mistakenly sent by another user) in order to get a free credit.
One way to solve this problem is to measure the balance before and after the transfer, and use the difference as the amount, rather than the stated amount.

There are 2 instances:

- *Vault.kerosine.unbounded.sol* ( [39-39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L39-L39) ):

```solidity
39:     asset.safeTransfer(to, amount); 
```

- *VaultManagerV2.sol* ( [129-129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L129-L129) ):

```solidity
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

### [L-12] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to [read-only reentrancy vulnerability](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect them except by block-listing the entire protocol.

There are 2 instances:

- *Vault.kerosine.unbounded.sol* ( [39-39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L39-L39) ):

```solidity
39:     asset.safeTransfer(to, amount); 
```

- *VaultManagerV2.sol* ( [129-129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L129-L129) ):

```solidity
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

### [L-13] Critical functions should be controlled by time locks

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user).

<details>
<summary>There are 8 instances (click to show):</summary>

- *KerosineManager.sol* ( [18-23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L18-L23), [28-33](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L28-L33) ):

```solidity
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

- *Vault.kerosine.bounded.sol* ( [23-28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L23-L28) ):

```solidity
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
```

- *Vault.kerosine.unbounded.sol* ( [43-46](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L43-L46) ):

```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
```

- *VaultManagerV2.sol* ( [67-73](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L67-L73), [80-86](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L80-L86), [94-100](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L94-L100), [106-112](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L106-L112) ):

```solidity
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
```

</details>

### [L-14] Tokens may be minted to the zero address

Neither the listed functions, nor `_mint()` prevent minting to `address(0x0)`

There are 4 instances:

- *VaultManagerV2.sol* ( [144-144](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L144-L144), [156-163](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L156-L163), [215-215](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L215-L215), [236-236](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L236-L236) ):

```solidity
144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   {

215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

236:       uint _dyad = dyad.mintedDyad(address(this), id);
```

### [L-15] Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

There are 3 instances:

- *VaultManagerV2.sol* ( [222-222](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L222-L222), [262-262](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L262-L262), [264-264](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L264-L264) ):

```solidity
/// @audit `collatRatio()` is called on line 213, triggering an external call - `mintedDyad()`
222:       for (uint i = 0; i < numberOfVaults; i++) {

/// @audit `isLicensed()` is called on line 261
262:           usdValue = vault.getUsdValue(id);        

/// @audit `isLicensed()` is called on line 261
264:         totalUsdValue += usdValue;
```

## Non Critical Issues

### [N-01] Names of `private`/`internal` state variables should be prefixed with an underscore

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

There are 3 instances:

- *KerosineManager.sol* ( [16-16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L16-L16) ):

```solidity
16:   EnumerableSet.AddressSet private vaults;
```

- *VaultManagerV2.sol* ( [34-34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L34-L34), [35-35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L35-L35) ):

```solidity
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
```

### [N-02] Use of `override` is unnecessary

[Starting from Solidity 0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), the override keyword is not required when overriding an interface function, except for the case where the function is defined in multiple bases.

There are 2 instances:

- *Vault.kerosine.bounded.sol* ( [44-48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L44-L48) ):

```solidity
44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {
```

- *Vault.kerosine.unbounded.sol* ( [50-54](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L50-L54) ):

```solidity
50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
```

### [N-03] Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

There are 3 instances:

- *Vault.kerosine.unbounded.sol* ( [60-63](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L60-L63) ):

```solidity
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
```

- *VaultManagerV2.sol* ( [146-149](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L146-L149), [195-198](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L195-L198) ):

```solidity
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();

195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;
```

### [N-04] Consider adding a block/deny-list

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

There are 2 instances:

- *Vault.kerosine.unbounded.sol* ( [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15) ):

```solidity
15: contract UnboundedKerosineVault is KerosineVault {
```

- *VaultManagerV2.sol* ( [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L17) ):

```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable {
```

### [N-05] Constants/Immutables redefined elsewhere

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants/immutables in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

There are 4 instances:

- *KerosineManager.sol* ( [14-14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L14-L14) ):

```solidity
/// @audit Seen in ./src/core/VaultManagerV2.sol#22
14:   uint public constant MAX_VAULTS = 10;
```

- *Vault.kerosine.unbounded.sol* ( [18-18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L18-L18) ):

```solidity
/// @audit Seen in ./src/core/VaultManagerV2.sol#29
18:   Dyad                 public immutable dyad;
```

- *VaultManagerV2.sol* ( [22-22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L22-L22), [29-29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L29-L29) ):

```solidity
/// @audit Seen in ./src/core/KerosineManager.sol#14
22:   uint public constant MAX_VAULTS          = 5;

/// @audit Seen in ./src/core/Vault.kerosine.unbounded.sol#18
29:   Dyad     public immutable dyad;
```

### [N-06] Contract name does not match its filename

According to the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names), contract and library names should also match their filenames.

There are 3 instances:

- *Vault.kerosine.bounded.sol* ( [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L12) ):

```solidity
/// @audit Not match filename `Vault.kerosine.bounded.sol`
12: contract BoundedKerosineVault is KerosineVault {
```

- *Vault.kerosine.sol* ( [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L12) ):

```solidity
/// @audit Not match filename `Vault.kerosine.sol`
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
```

- *Vault.kerosine.unbounded.sol* ( [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15) ):

```solidity
/// @audit Not match filename `Vault.kerosine.unbounded.sol`
15: contract UnboundedKerosineVault is KerosineVault {
```

### [N-07] Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed.

<details>
<summary>There are 5 instances (click to show):</summary>

- *Vault.kerosine.bounded.sol* ( [17-21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L17-L21) ):

```solidity
17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

- *Vault.kerosine.sol* ( [26-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L26-L30) ):

```solidity
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
```

- *Vault.kerosine.unbounded.sol* ( [21-26](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L21-L26) ):

```solidity
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```

- *VaultManagerV2.sol* ( [49-53](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L49-L53) ):

```solidity
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
```

- *KerosineDenominator.sol* ( [11-13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L11-L13) ):

```solidity
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
```

</details>

### [N-08] Empty function body without comments

Empty function body in solidity is not recommended, consider adding some comments to the body.

There is 1 instance:

- *Vault.kerosine.bounded.sol* ( [17-21](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L17-L21) ):

```solidity
17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```

### [N-09] Events are emitted without the sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

There are 9 instances:

- *Vault.kerosine.sol* ( [44-44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L44-L44), [57-57](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L57-L57) ):

```solidity
44:     emit Deposit(id, amount);

57:     emit Move(from, to, amount);
```

- *Vault.kerosine.unbounded.sol* ( [40-40](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L40-L40) ):

```solidity
40:     emit Withdraw(id, to, amount);
```

- *VaultManagerV2.sol* ( [77-77](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L77-L77), [90-90](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L90-L90), [103-103](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L103-L103), [115-115](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L115-L115), [168-168](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L168-L168), [200-200](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L200-L200) ):

```solidity
77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

168:     emit MintDyad(id, amount, to);

200:       emit RedeemDyad(id, vault, amount, to);
```

### [N-10] Imports could be organized more systematically

The contract's interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout.

There are 4 instances:

- *Vault.kerosine.bounded.sol* ( [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IVaultManager}          from "../interfaces/IVaultManager.sol";
```

- *Vault.kerosine.sol* ( [6-6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IVault}          from "../interfaces/IVault.sol";
```

- *Vault.kerosine.unbounded.sol* ( [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IVaultManager}        from "../interfaces/IVaultManager.sol";
```

- *VaultManagerV2.sol* ( [8-8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L8-L8) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
8: import {IVaultManager}   from "../interfaces/IVaultManager.sol";
```

### [N-11] Invalid NatSpec comment style

NatSpec comment in solidity should use `///` or `/* ... */` syntax.

There is 1 instance:

- *KerosineDenominator.sol* ( [18-18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L18-L18) ):

```solidity
18:     // @dev: We subtract all the Kerosene in the multi-sig.
```

### [N-12] @openzeppelin/contracts should be upgraded to a newer version

These contracts import contracts from `@openzeppelin/contracts`, but they are not using [the latest version](https://github.com/OpenZeppelin/openzeppelin-contracts/releases). Using the latest version ensures contract security with fixes for known vulnerabilities, access to the latest feature updates, and enhanced community support and engagement.

The imported version is `4.8.0`.

There are 3 instances:

- *KerosineManager.sol* ( [4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L4) ):

```solidity
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
```

- *VaultManagerV2.sol* ( [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L14), [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L15) ):

```solidity
14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

### [N-13] Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

There are 7 instances:

- *Vault.kerosine.sol* ( [15-15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L15-L15), [16-16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L16-L16), [17-17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L17-L17) ):

```solidity
15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;
```

- *Vault.kerosine.unbounded.sol* ( [18-18](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L18-L18) ):

```solidity
18:   Dyad                 public immutable dyad;
```

- *VaultManagerV2.sol* ( [28-28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L28-L28), [29-29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L29-L29), [30-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L30-L30) ):

```solidity
28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;
```

### [N-14] Modifiers should be named in mixedCase style

As the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#modifier-names) suggests: modifiers should be named in mixedCase style. Use mixedCase. Examples: `onlyBy`, `onlyAfter`, `onlyDuringThePreSale`.

There are 2 instances:

- *VaultManagerV2.sol* ( [39](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L42) ):

```solidity
39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {
```

### [N-15] Consider adding validation of user inputs

There are no validations done on the arguments below. Consider that the Solidity [documentation](https://docs.soliditylang.org/en/latest/control-structures.html#panic-via-assert-and-error-via-require) states that `Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix`. This means that there should be explicit checks for expected ranges of inputs. Underflows/overflows result in panics should not be used as range checks, and allowing funds to be sent to  `0x0`, which is the default value of address variables and has many gotchas, should be avoided.

<details>
<summary>There are 15 instances (click to show):</summary>

- *KerosineManager.sol* ( [18-20](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L18-L20), [28-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L28-L30) ):

```solidity
/// @audit `vault not checked`
18:   function add(
19:     address vault
20:   ) 

/// @audit `vault not checked`
28:   function remove(
29:     address vault
30:   ) 
```

- *Vault.kerosine.bounded.sol* ( [23-25](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L23-L25) ):

```solidity
/// @audit `_unboundedKerosineVault not checked`
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
```

- *Vault.kerosine.unbounded.sol* ( [30-34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L30-L34), [43-43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L43-L43) ):

```solidity
/// @audit `to not checked`
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 

/// @audit `_kerosineDenominator not checked`
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
```

- *VaultManagerV2.sol* ( [67-70](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L67-L70), [80-83](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L80-L83), [94-97](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L94-L97), [106-109](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L106-L109), [119-123](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L119-L123), [134-139](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L134-L139), [156-160](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L156-L160), [184-189](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L184-L189) ):

```solidity
/// @audit `vault not checked`
67:   function add(
68:       uint    id,
69:       address vault
70:   ) 

/// @audit `vault not checked`
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   ) 

/// @audit `vault not checked`
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 

/// @audit `vault not checked`
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 

/// @audit `vault not checked`
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 

/// @audit `vault not checked`
/// @audit `to not checked`
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 

/// @audit `to not checked`
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )

/// @audit `vault not checked`
/// @audit `to not checked`
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
```

</details>

### [N-16] Constants should be put on the left side of comparisons

Putting constants on the left side of comparison statements is a best practice known as [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions).
Although solidity's static typing system prevents accidental assignments within conditionals, adopting this practice can improve code readability and consistency, especially when working across multiple languages.

There are 2 instances:

- *VaultManagerV2.sol* ( [214](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L214), [237](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L237) ):

```solidity
/// @audit put `MIN_COLLATERIZATION_RATIO` on the left
214:       if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

/// @audit put `0` on the left
237:       if (_dyad == 0) return type(uint).max;
```

### [N-17] Unnecessary casting

Unnecessary castings can be removed.

There is 1 instance:

- *VaultManagerV2.sol* ( [129-129](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L129-L129) ):

```solidity
/// @audit address(vault)
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```

### [N-18] Unused import

The identifier is imported but never used within the file.

<details>
<summary>There are 34 instances (click to show):</summary>

- *KerosineManager.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L5-L5) ):

```solidity
/// @audit EnumerableSet
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

/// @audit Owned
5: import {Owned}         from "@solmate/src/auth/Owned.sol";
```

- *Vault.kerosine.bounded.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L6-L6), [7-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L7-L7), [8-8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L8-L8), [10-10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L10-L10) ):

```solidity
/// @audit KerosineVault
4: import {KerosineVault}          from "./Vault.kerosine.sol";

/// @audit IVaultManager
5: import {IVaultManager}          from "../interfaces/IVaultManager.sol";

/// @audit Dyad
6: import {Dyad}                   from "./Dyad.sol";

/// @audit KerosineManager
7: import {KerosineManager}        from "./KerosineManager.sol";

/// @audit UnboundedKerosineVault
8: import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";

/// @audit ERC20
10: import {ERC20} from "@solmate/src/tokens/ERC20.sol";
```

- *Vault.kerosine.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L6-L6), [8-8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L8-L8), [9-9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L9-L9), [10-10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L10-L10) ):

```solidity
/// @audit IVaultManager
4: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

/// @audit KerosineManager
5: import {KerosineManager} from "./KerosineManager.sol";

/// @audit IVault
6: import {IVault}          from "../interfaces/IVault.sol";

/// @audit SafeTransferLib
8: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

/// @audit ERC20
9: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";

/// @audit Owned
10: import {Owned}           from "@solmate/src/auth/Owned.sol";
```

- *Vault.kerosine.unbounded.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L5-L5), [7-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L7-L7), [8-8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L8-L8), [9-9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L9-L9), [10-10](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L10-L10), [12-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L12-L12), [13-13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L13-L13) ):

```solidity
/// @audit KerosineVault
4: import {KerosineVault}        from "./Vault.kerosine.sol";

/// @audit IVaultManager
5: import {IVaultManager}        from "../interfaces/IVaultManager.sol";

/// @audit Dyad
7: import {Dyad}                 from "./Dyad.sol";

/// @audit KerosineManager
8: import {KerosineManager}      from "./KerosineManager.sol";

/// @audit BoundedKerosineVault
9: import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";

/// @audit KerosineDenominator
10: import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";

/// @audit ERC20
12: import {ERC20}           from "@solmate/src/tokens/ERC20.sol";

/// @audit SafeTransferLib
13: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
```

- *VaultManagerV2.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L5-L5), [6-6](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L6-L6), [8-8](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L8-L8), [9-9](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L9-L9), [11-11](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L11-L11), [12-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L12-L12), [13-13](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L13-L13), [14-14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L14-L14), [15-15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L15-L15) ):

```solidity
/// @audit DNft
4: import {DNft}            from "./DNft.sol";

/// @audit Dyad
5: import {Dyad}            from "./Dyad.sol";

/// @audit Licenser
6: import {Licenser}        from "./Licenser.sol";

/// @audit IVaultManager
8: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

/// @audit KerosineManager
9: import {KerosineManager} from "../../src/core/KerosineManager.sol";

/// @audit FixedPointMathLib
11: import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";

/// @audit ERC20
12: import {ERC20}             from "@solmate/src/tokens/ERC20.sol";

/// @audit SafeTransferLib
13: import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";

/// @audit EnumerableSet
14: import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

/// @audit Initializable
15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

- *KerosineDenominator.sol* ( [4-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L4-L4), [5-5](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L5-L5) ):

```solidity
/// @audit Parameters
4: import {Parameters} from "../params/Parameters.sol";

/// @audit Kerosine
5: import {Kerosine} from "../staking/Kerosine.sol";
```

</details>

### [N-19] Unused modifiers

The following `modifier`s are not used. It is recommended to check the code for logical omissions that cause them not to be used. If it's determined that they are not needed anywhere, it's best to remove them from the codebase to improve code clarity and minimize confusion.

There is 1 instance:

- *VaultManagerV2.sol* ( [45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L45) ):

```solidity
45:   modifier isLicensed(address vault) {
```

### [N-20] Use the latest Solidity version

Upgrading to the [latest solidity version](https://github.com/ethereum/solc-js/tags) (0.8.19 for L2s) can optimize gas usage, take advantage of new features and improve overall contract efficiency. Where possible, based on compatibility requirements, it is recommended to use newer/latest solidity version to take advantage of the latest optimizations and features.

<details>
<summary>There are 6 instances (click to show):</summary>

- *KerosineManager.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

- *Vault.kerosine.bounded.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

- *Vault.kerosine.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

- *Vault.kerosine.unbounded.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

- *VaultManagerV2.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

- *KerosineDenominator.sol* ( [2](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L2) ):

```solidity
2: pragma solidity =0.8.17;
```

</details>

### [N-21] Contract variables should have comments

Consider adding some comments on non-public contract variables to explain what they are supposed to do. This will help for future code reviews.

There are 3 instances:

- *KerosineManager.sol* ( [16-16](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L16-L16) ):

```solidity
16:   EnumerableSet.AddressSet private vaults;
```

- *VaultManagerV2.sol* ( [34-34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L34-L34), [35-35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L35-L35) ):

```solidity
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
```

### [N-22] Missing event when a state variables is set in constructor

The initial states set in a constructor are important and should be recorded in the event.

There is 1 instance:

- *KerosineDenominator.sol* ( [14](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L14) ):

```solidity
14:     kerosine = _kerosine;
```

### [N-23] Multiple mappings with same keys can be combined into a single struct mapping for readability

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related.

There are 3 instances:

- *VaultManagerV2.sol* ( [34-34](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L34-L34), [35-35](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L35-L35), [37-37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L37-L37) ):

```solidity
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;
```

### [N-24] Missing event for critical changes

Events should be emitted when critical changes are made to the contracts.

There are 2 instances:

- *Vault.kerosine.bounded.sol* ( [23-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L23-L30) ):

```solidity
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }
```

- *Vault.kerosine.unbounded.sol* ( [43-48](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L43-L48) ):

```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }
```

### [N-25] Duplicated `require()`/`revert()` checks should be refactored

Refactoring duplicate `require()`/`revert()` checks into a modifier or function can make the code more concise, readable and maintainable, and less likely to make errors or omissions when modifying the `require()` or `revert()`.

There are 6 instances:

- *VaultManagerV2.sol* ( [74-74](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L74-L74), [75-75](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L75-L75), [76-76](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L76-L76), [101-101](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L101-L101), [102-102](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L102-L102), [150-150](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L150-L150) ):

```solidity
/// @audit Duplicated on line 87
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

/// @audit Duplicated on line 88
75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();

/// @audit Duplicated on line 89
76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();

/// @audit Duplicated on line 113
101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

/// @audit Duplicated on line 114
102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();

/// @audit Duplicated on line 165
150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
```

### [N-26] Consider adding emergency-stop functionality

Adding a way to quickly halt protocol functionality in an emergency, rather than having to pause individual contracts one-by-one, will make in-progress hack mitigation faster and much less stressful.

There are 4 instances:

- *KerosineManager.sol* ( [7-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L7-L7) ):

```solidity
7: contract KerosineManager is Owned(msg.sender) {
```

- *Vault.kerosine.bounded.sol* ( [12-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L12-L12) ):

```solidity
12: contract BoundedKerosineVault is KerosineVault {
```

- *Vault.kerosine.unbounded.sol* ( [15-15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15-L15) ):

```solidity
15: contract UnboundedKerosineVault is KerosineVault {
```

- *VaultManagerV2.sol* ( [17-17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L17-L17) ):

```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable {
```

### [N-27] Missing checks for uint state variable assignments

Consider whether reasonable bounds checks for variables would be useful.

There is 1 instance:

- *VaultManagerV2.sol* ( [127-127](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L127-L127) ):

```solidity
127:     idToBlockOfLastDeposit[id] = block.number;
```

### [N-28] Use the Modern Upgradeable Contract Paradigm

Modern smart contract development often employs upgradeable contract structures, utilizing proxy patterns like OpenZeppelin’s Upgradeable Contracts. This paradigm separates logic and state, allowing developers to amend and enhance the contract's functionality without altering its state or the deployed contract address. Transitioning to this approach enhances long-term maintainability.
Resolution: Adopt a well-established proxy pattern for upgradeability, ensuring proper initialization and employing transparent proxies to mitigate potential risks. Embrace comprehensive testing and audit practices, particularly when updating contract logic, to ensure state consistency and security are preserved across upgrades. This ensures your contract remains robust and adaptable to future requirements.

There are 4 instances:

- *KerosineManager.sol* ( [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L7) ):

```solidity
7: contract KerosineManager is Owned(msg.sender) {
```

- *Vault.kerosine.bounded.sol* ( [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L12) ):

```solidity
12: contract BoundedKerosineVault is KerosineVault {
```

- *Vault.kerosine.unbounded.sol* ( [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15) ):

```solidity
15: contract UnboundedKerosineVault is KerosineVault {
```

- *KerosineDenominator.sol* ( [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L7) ):

```solidity
7: contract KerosineDenominator is Parameters {
```

### [N-29] Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.
Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.
Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

There is 1 instance:

- Global finding

### [N-30] The default value is manually set when it is declared

In instances where a new variable is defined, there is no need to set it to it's default value.

There are 4 instances:

- *Vault.kerosine.unbounded.sol* ( [58-58](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L58-L58) ):

```solidity
58:       for (uint i = 0; i < numberOfVaults; i++) {
```

- *VaultManagerV2.sol* ( [222-222](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L222-L222), [258-258](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L258-L258), [277-277](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L277-L277) ):

```solidity
222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {
```

### [N-31] Contracts should have all `public`/`external` functions exposed by `interface`s

All `external`/`public` functions should extend an `interface`. This is useful to ensure that the whole API is extracted and can be more easily integrated by other projects.

There are 5 instances:

- *KerosineManager.sol* ( [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L7) ):

```solidity
7: contract KerosineManager is Owned(msg.sender) {
```

- *Vault.kerosine.bounded.sol* ( [12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L12) ):

```solidity
12: contract BoundedKerosineVault is KerosineVault {
```

- *Vault.kerosine.unbounded.sol* ( [15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L15) ):

```solidity
15: contract UnboundedKerosineVault is KerosineVault {
```

- *VaultManagerV2.sol* ( [17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L17) ):

```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable {
```

- *KerosineDenominator.sol* ( [7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L7) ):

```solidity
7: contract KerosineDenominator is Parameters {
```

### [N-32] Top-level declarations should be separated by at least two lines

-

<details>
<summary>There are 36 instances (click to show):</summary>

- *KerosineManager.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L2-L4), [5-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L5-L7), [26-28](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L26-L28), [35-37](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L35-L37), [42-44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol#L42-L44) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

5: import {Owned}         from "@solmate/src/auth/Owned.sol";
6: 
7: contract KerosineManager is Owned(msg.sender) {

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

- *Vault.kerosine.bounded.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L2-L4), [10-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L10-L12), [21-23](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L21-L23), [30-32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L30-L32), [42-44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L42-L44) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {KerosineVault}          from "./Vault.kerosine.sol";

10: import {ERC20} from "@solmate/src/tokens/ERC20.sol";
11: 
12: contract BoundedKerosineVault is KerosineVault {

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

- *Vault.kerosine.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L2-L4), [10-12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L10-L12), [34-36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L34-L36), [45-47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L45-L47), [58-60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L58-L60), [67-69](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L67-L69) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {IVaultManager}   from "../interfaces/IVaultManager.sol";

10: import {Owned}           from "@solmate/src/auth/Owned.sol";
11: 
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

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

- *Vault.kerosine.unbounded.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L2-L4), [13-15](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L13-L15), [28-30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L28-L30), [41-43](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L41-L43), [48-50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L48-L50) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {KerosineVault}        from "./Vault.kerosine.sol";

13: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
14: 
15: contract UnboundedKerosineVault is KerosineVault {

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

- *VaultManagerV2.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L2-L4), [15-17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L15-L17), [41-42](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L41-L42), [44-45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L44-L45), [57-59](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L57-L59), [78-80](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L78-L80), [104-106](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L104-L106), [228-230](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L228-L230), [239-241](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L239-L241), [248-250](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L248-L250), [267-269](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L267-L269), [297-299](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L297-L299) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {DNft}            from "./DNft.sol";

15: import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
16: 
17: contract VaultManagerV2 is IVaultManager, Initializable {

41:   }
42:   modifier isValidDNft(uint id) {

44:   }
45:   modifier isLicensed(address vault) {

57:   }
58: 
59:   function setKeroseneManager(KerosineManager _keroseneManager) 

78:   }
79: 
80:   function addKerosene(

104:   }
105: 
106:   function removeKerosene(

228:   }
229: 
230:   function collatRatio(

239:   }
240: 
241:   function getTotalUsdValue(

248:   }
249: 
250:   function getNonKeroseneValue(

267:   }
268: 
269:   function getKeroseneValue(

297:   }
298: 
299:   function hasVault(
```

- *KerosineDenominator.sol* ( [2-4](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L2-L4), [5-7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L5-L7), [15-17](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol#L15-L17) ):

```solidity
2: pragma solidity =0.8.17;
3: 
4: import {Parameters} from "../params/Parameters.sol";

5: import {Kerosine} from "../staking/Kerosine.sol";
6: 
7: contract KerosineDenominator is Parameters {

15:   }
16: 
17:   function denominator() external view returns (uint) {
```

</details>

### [N-33] Consider adding formal verification proofs

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

There are 6 instances:

- [*KerosineManager.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/KerosineManager.sol)

- [*Vault.kerosine.bounded.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol)

- [*Vault.kerosine.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol)

- [*Vault.kerosine.unbounded.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol)

- [*VaultManagerV2.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol)

- [*KerosineDenominator.sol*](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/staking/KerosineDenominator.sol)

### [N-34] Prevent re-setting a state variable with the same value

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers.

There are 2 instances:

- *Vault.kerosine.bounded.sol* ( [29-29](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.bounded.sol#L29-L29) ):

```solidity
29:     unboundedKerosineVault = _unboundedKerosineVault;
```

- *Vault.kerosine.unbounded.sol* ( [47-47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L47-L47) ):

```solidity
47:     kerosineDenominator = _kerosineDenominator;
```

### [N-35] Whitespace in Expressions

See the [whitespace](https://docs.soliditylang.org/en/latest/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide.

<details>
<summary>There are 10 instances (click to show):</summary>

- *Vault.kerosine.sol* ( [31](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L32), [56](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.sol#L56) ):

```solidity
/// @audit More than one space around an operator
31:     vaultManager    = _vaultManager;

/// @audit More than one space around an operator
32:     asset           = _asset;

/// @audit More than one space around an operator
56:     id2asset[to]   += amount;
```

- *Vault.kerosine.unbounded.sol* ( [65](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/Vault.kerosine.unbounded.sol#L65) ):

```solidity
/// @audit More than one space around an operator
65:       uint numerator   = tvl - dyad.totalSupply();
```

- *VaultManagerV2.sol* ( [22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L22), [54](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L55), [217](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L217), [219](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L219), [223](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/./src/core/VaultManagerV2.sol#L223) ):

```solidity
/// @audit More than one space around an operator
22:   uint public constant MAX_VAULTS          = 5;

/// @audit More than one space around an operator
54:     dNft          = _dNft;

/// @audit More than one space around an operator
55:     dyad          = _dyad;

/// @audit More than one space around an operator
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

/// @audit More than one space around an operator
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

/// @audit More than one space around an operator
223:           Vault vault      = Vault(vaults[id].at(i));
```

</details>
