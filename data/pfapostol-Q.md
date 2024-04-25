The content section shows only 10 examples, subsequent cases are listed as links.

## Low Risk Issues

|Index|Issue|Instances|
|:---:|:---|:---:|
| [L-01](#L-01) | [Consider disabling `renounceOwnership()`](#L-01) | 4 |
| [L-02](#L-02) | [Functions calling contracts/addresses with transfer hooks are missing reentrancy guards](#L-02) | 2 |
| [L-03](#L-03) | [Code does not follow the best practice of check-effects-interaction](#L-03) | 2 |
| [L-04](#L-04) | [Must approve or increase allowance first](#L-04) | 1 |

9 instances over 4 issues

---

## NonCritical Risk Issues

|Index|Issue|Instances|
|:---:|:---|:---:|
| [N-01](#N-01) | [Events should be emitted before external calls](#N-01) | 9 |
| [N-02](#N-02) | [Complex math should be split into multiple steps](#N-02) | 7 |
| [N-03](#N-03) | [Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES](#N-03) | 7 |
| [N-04](#N-04) | [Duplicated `require/if` statements should be refactored](#N-04) | 6 |
| [N-05](#N-05) | [Use a single file for system wide constants](#N-05) | 5 |
| [N-06](#N-06) | [`constructor` missing zero address check](#N-06) | 4 |
| [N-07](#N-07) | [Private and internal state variables should have a preceding _ in their name unless they are constants](#N-07) | 3 |
| [N-08](#N-08) | [Missing event and or timelock for critical parameter change](#N-08) | 3 |
| [N-09](#N-09) | [Setters should prevent re-setting of the same value](#N-09) | 3 |
| [N-10](#N-10) | [Use of `override` is unnecessary](#N-10) | 2 |
| [N-11](#N-11) | [Use `@inheritdoc` for overridden functions](#N-11) | 2 |
| [N-12](#N-12) | [Contract name does not follow the Solidity Style Guide](#N-12) | 2 |
| [N-13](#N-13) | [State variables not capped at reasonable values](#N-13) | 2 |
| [N-14](#N-14) | [Consider adding a block/deny-list](#N-14) | 2 |
| [N-15](#N-15) | [Empty function blocks](#N-15) | 1 |
| [N-16](#N-16) | [Emits without `msg.sender` parameter](#N-16) | 1 |
| [N-17](#N-17) | [Unused `modifier`](#N-17) | 1 |
| [N-18](#N-18) | [Consider disallowing transfers to `address(this)`](#N-18) | 1 |
| [N-19](#N-19) | [Named imports of parent contracts are missing](#N-19) | 1 |

62 instances over 19 issues

---



## Low Risk Issues

### [L-01] Consider disabling `renounceOwnership()`
<a name="L-01"></a>
[To the top](#TOP)

Typically, the contract's owner is the account that deploys the contract. As a result, the owner is able to perform certain privileged activities. The OpenZeppelin's `Ownable` is used in this project contract implements `renounceOwnership`. This can represent a certain risk if the ownership is renounced for any other reason than by design. Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 4 instances</summary>


---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
23	  function setUnboundedKerosineVault(
24	    UnboundedKerosineVault _unboundedKerosineVault
25	  )
26	    external
27	    onlyOwner
28	  {
```
[23..28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
43	  function setDenominator(KerosineDenominator _kerosineDenominator) 
44	    external 
45	      onlyOwner
46	  {
```
[43..46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46)

---

	 - src/core/KerosineManager.sol

```solidity
18	  function add(
19	    address vault
20	  ) 
21	    external 
22	      onlyOwner
23	  {
...
28	  function remove(
29	    address vault
30	  ) 
31	    external 
32	      onlyOwner
33	  {
```
[18..23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L23)
[28..33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L33)


</details>

-------
### [L-02] Functions calling contracts/addresses with transfer hooks are missing reentrancy guards
<a name="L-02"></a>
[To the top](#TOP)

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.`

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
119	  function deposit(
120	    uint    id,
121	    address vault,
122	    uint    amount
123	  ) 
124	    external 
125	      isValidDNft(id)
126	  {
...
// @audit Function `deposit` doesn't  have the `nonReentrant` modifier
129	    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```
[129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
30	  function withdraw(
31	    uint    id,
32	    address to,
33	    uint    amount
34	  ) 
35	    external 
36	      onlyVaultManager
37	  {
...
// @audit Function `withdraw` doesn't  have the `nonReentrant` modifier
39	    asset.safeTransfer(to, amount); 
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L39)


</details>

-------
### [L-03] Code does not follow the best practice of check-effects-interaction
<a name="L-03"></a>
[To the top](#TOP)

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
// @audit Some statements does not follow CEI
134	  function withdraw(
135	    uint    id,
136	    address vault,
137	    uint    amount,
138	    address to
139	  ) 
140	    public
141	      isDNftOwner(id)
142	  {
...
// @audit Statement out of CEI order
152	    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
...
// @audit Some statements does not follow CEI
156	  function mintDyad(
157	    uint    id,
158	    uint    amount,
159	    address to
160	  )
161	    external 
162	      isDNftOwner(id)
163	  {
...
// @audit Statement out of CEI order
167	    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
```
[152](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L152)
[167](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L167)


</details>

-------
### [L-04] Must approve or increase allowance first
<a name="L-04"></a>
[To the top](#TOP)

In the context of ERC20 tokens, a token holder needs to "approve" another account to transfer a certain amount of their tokens on their behalf. This is accomplished by calling the `approve()` function, which takes the address of the spender and the amount they're allowed to spend as parameters. 

This approval step is a crucial part of the ERC20 standard because it allows for secure delegated transfers. A common use case for this feature is in decentralized exchanges or DeFi protocols, where a user can approve a smart contract to transfer tokens on their behalf. 

After the approval step, the approved account (or contract) can then transfer tokens up to the approved amount from the token holder's account by calling the `transferFrom()` function. This function takes three parameters: the address of the token holder, the recipient's address, and the amount to transfer.

If an account tries to call `transferFrom()` before the token holder has called `approve()`, the transaction will fail because the ERC20 contract checks whether the `transferFrom()` caller has an adequate allowance. 

In summary, if a contract or user needs to move ERC20 tokens on behalf of another account, it's necessary to ensure that the token holder has first called `approve()` to set a sufficient allowance. This is a key aspect of ERC20 token security and functionality. 

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
 // @audit function call transfer from, but not approve
119	  function deposit(
120	    uint    id,
121	    address vault,
122	    uint    amount
123	  ) 
124	    external 
125	      isValidDNft(id)
126	  {
...
129	    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
```
[129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129)


</details>


## NonCritical Risk Issues

### [N-01] Events should be emitted before external calls
<a name="N-01"></a>
[To the top](#TOP)

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 9 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
// @audit functions: `length`, `isLicensed`, `add` called before this event
77	    emit Added(id, vault);
...
// @audit functions: `length`, `isLicensed`, `add` called before this event
90	    emit Added(id, vault);
...
// @audit functions: `id2asset`, `remove` called before this event
103	    emit Removed(id, vault);
...
// @audit functions: `id2asset`, `remove` called before this event
115	    emit Removed(id, vault);
...
// @audit functions: `mintedDyad`, `mint` called before this event
168	    emit MintDyad(id, amount, to);
...
// @audit functions: `burn` called before this event
180	    emit BurnDyad(id, amount, msg.sender);
...
// @audit functions: `burn`, `decimals`, `oracle`, `decimals`, `asset`, `assetPrice` called before this event
200	      emit RedeemDyad(id, vault, amount, to);
...
// @audit functions: `burn`, `mintedDyad`, `mulWadDown`, `divWadDown`, `length`, `at`, `mulWadUp`, `id2asset`, `move` called before this event
227	      emit Liquidate(id, msg.sender, to);
```
[77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77)
[90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90)
[103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103)
[115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115)
[168](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L168)
[180](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L180)
[200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200)
[227](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L227)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
// @audit functions: `safeTransfer` called before this event
40	    emit Withdraw(id, to, amount);
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L40)


</details>

-------
### [N-02] Complex math should be split into multiple steps
<a name="N-02"></a>
[To the top](#TOP)

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 7 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
146	    uint value = amount * _vault.assetPrice() 
147	                  * 1e18 
148	                  / 10**_vault.oracle().decimals() 
149	                  / 10**_vault.asset().decimals();
...
146	    uint value = amount * _vault.assetPrice() 
147	                  * 1e18 
148	                  / 10**_vault.oracle().decimals() 
...
195	      uint asset = amount 
196	                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197	                    / _vault.assetPrice() 
198	                    / 1e18;
...
195	      uint asset = amount 
196	                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197	                    / _vault.assetPrice() 
...
195	      uint asset = amount 
196	                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
```
[146..149](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L149)
[146..148](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L148)
[195..198](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L198)
[195..197](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L197)
[195..196](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L196)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
60	        tvl += vault.asset().balanceOf(address(vault)) 
61	                * vault.assetPrice() * 1e18
62	                / (10**vault.asset().decimals()) 
63	                / (10**vault.oracle().decimals());
...
60	        tvl += vault.asset().balanceOf(address(vault)) 
61	                * vault.assetPrice() * 1e18
62	                / (10**vault.asset().decimals()) 
```
[60..63](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60-L63)
[60..62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60-L62)


</details>

-------
### [N-03] Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES
<a name="N-03"></a>
[To the top](#TOP)

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 7 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
28	  DNft     public immutable dNft;
...
29	  Dyad     public immutable dyad;
...
30	  Licenser public immutable vaultLicenser;
```
[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28)
[29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L29)
[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L30)

---

	 - src/core/Vault.kerosine.sol

```solidity
15	  IVaultManager   public immutable vaultManager;
...
16	  ERC20           public immutable asset;
...
17	  KerosineManager public immutable kerosineManager;
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15)
[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L16)
[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L17)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
18	  Dyad                 public immutable dyad;
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18)


</details>

-------
### [N-04] Duplicated `require/if` statements should be refactored
<a name="N-04"></a>
[To the top](#TOP)

These statements should be refactored to a separate function, as there are multiple parts of the codebase that use the same logic, to improve the code readability and reduce code duplication.



#### <ins>Proof Of Concept</ins>

<details>

<summary>see 6 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
46	    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
...
75	    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
...
101	    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
...
113	    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
...
152	    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
...
167	    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
```
[46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L46)
[75](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L75)
[101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101)
[113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113)
[152](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L152)
[167](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L167)


</details>

-------
### [N-05] Use a single file for system wide constants
<a name="N-05"></a>
[To the top](#TOP)

Consider grouping all the system constants under a single file.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 5 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
22	  uint public constant MAX_VAULTS          = 5;
...
23	  uint public constant MAX_VAULTS_KEROSENE = 5;
...
25	  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%
...
26	  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22)
[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23)
[25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25)
[26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26)

---

	 - src/core/KerosineManager.sol

```solidity
14	  uint public constant MAX_VAULTS = 10;
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14)


</details>

-------
### [N-06] `constructor` missing zero address check
<a name="N-06"></a>
[To the top](#TOP)

It is important to ensure that the constructor does not allow zero address to be set.
    This is a common mistake that can lead to loss of funds or redeployment of the contract.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 4 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
49	  constructor(
50	    DNft          _dNft,
51	    Dyad          _dyad,
52	    Licenser      _licenser
53	  ) {
```
[49..53](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L53)

---

	 - src/core/Vault.kerosine.sol

```solidity
26	  constructor(
27	    IVaultManager   _vaultManager,
28	    ERC20           _asset, 
29	    KerosineManager _kerosineManager 
30	  ) {
```
[26..30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L30)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
21	  constructor(
22	      IVaultManager   _vaultManager,
23	      ERC20           _asset, 
24	      Dyad            _dyad, 
25	      KerosineManager _kerosineManager
26	  ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
```
[21..26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L26)

---

	 - src/staking/KerosineDenominator.sol

```solidity
11	  constructor(
12	    Kerosine _kerosine
13	  ) {
```
[11..13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L13)


</details>

-------
### [N-07] Private and internal state variables should have a preceding _ in their name unless they are constants
<a name="N-07"></a>
[To the top](#TOP)

Add a preceding underscore to the state variable name, take care to refactor where there variables are read/wrote

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 3 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
34	  mapping (uint => EnumerableSet.AddressSet) internal vaults; 
...
35	  mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
```
[34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34)
[35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35)

---

	 - src/core/KerosineManager.sol

```solidity
16	  EnumerableSet.AddressSet private vaults;
```
[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16)


</details>

-------
### [N-08] Missing event and or timelock for critical parameter change
<a name="N-08"></a>
[To the top](#TOP)

Events help non-contract tools to track changes, and timelocks prevent users from being surprised by changes

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 3 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
59	  function setKeroseneManager(KerosineManager _keroseneManager) 
60	    external
61	      initializer 
62	    {
```
[59..62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L62)

---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
23	  function setUnboundedKerosineVault(
24	    UnboundedKerosineVault _unboundedKerosineVault
25	  )
26	    external
27	    onlyOwner
28	  {
```
[23..28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
43	  function setDenominator(KerosineDenominator _kerosineDenominator) 
44	    external 
45	      onlyOwner
46	  {
```
[43..46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46)


</details>

-------
### [N-09] Setters should prevent re-setting of the same value
<a name="N-09"></a>
[To the top](#TOP)

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 3 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
59	  function setKeroseneManager(KerosineManager _keroseneManager) 
60	    external
61	      initializer 
62	    {
```
[59..62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L62)

---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
23	  function setUnboundedKerosineVault(
24	    UnboundedKerosineVault _unboundedKerosineVault
25	  )
26	    external
27	    onlyOwner
28	  {
```
[23..28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L28)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
43	  function setDenominator(KerosineDenominator _kerosineDenominator) 
44	    external 
45	      onlyOwner
46	  {
```
[43..46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L46)


</details>

-------
### [N-10] Use of `override` is unnecessary
<a name="N-10"></a>
[To the top](#TOP)

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
44	  function assetPrice() 
45	    public 
46	    view 
47	    override
48	    returns (uint) {
```
[44..48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
50	  function assetPrice() 
51	    public 
52	    view 
53	    override
54	    returns (uint) {
```
[50..54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54)


</details>

-------
### [N-11] Use `@inheritdoc` for overridden functions
<a name="N-11"></a>
[To the top](#TOP)

It is recommended to use `@inheritdoc` for overridden functions.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
44	  function assetPrice() 
45	    public 
46	    view 
47	    override
48	    returns (uint) {
```
[44..48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L48)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
50	  function assetPrice() 
51	    public 
52	    view 
53	    override
54	    returns (uint) {
```
[50..54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L54)


</details>

-------
### [N-12] Contract name does not follow the Solidity Style Guide
<a name="N-12"></a>
[To the top](#TOP)

According to the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names), contracts and libraries should be named using the CapWords style.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
17	contract VaultManagerV2 is IVaultManager, Initializable {
18	  using EnumerableSet     for EnumerableSet.AddressSet;
```
[17..18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L18)

---

	 - script/deploy/Deploy.V2.s.sol

```solidity
35	contract DeployV2 is Script, Parameters {
36	  function run() public returns (Contracts memory) {
```
[35..36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35-L36)


</details>

-------
### [N-13] State variables not capped at reasonable values
<a name="N-13"></a>
[To the top](#TOP)

Consider adding minimum/maximum value checks to ensure that the state variables below can never be used to excessively harm users, including via griefing

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
// @audit: parameter `amount` is not limited in function body
137	    uint    amount,
...
// @audit: parameter `amount` is not limited in function body
158	    uint    amount,
```
[137](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L137)
[158](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L158)


</details>

-------
### [N-14] Consider adding a block/deny-list
<a name="N-14"></a>
[To the top](#TOP)

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 2 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
17	contract VaultManagerV2 is IVaultManager, Initializable {
18	  using EnumerableSet     for EnumerableSet.AddressSet;
```
[17..18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17-L18)

---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
15	contract UnboundedKerosineVault is KerosineVault {
16	  using SafeTransferLib for ERC20;
```
[15..16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15-L16)


</details>

-------
### [N-15] Empty function blocks
<a name="N-15"></a>
[To the top](#TOP)

Empty code blocks (i.e., {}) in a Solidity contract can be harmful as they can lead to ambiguity, misinterpretation, and unintended behavior. When developers encounter empty code blocks, it may be unclear whether the absence of code is intentional or the result of an oversight. This uncertainty can cause confusion during development, testing, and debugging, increasing the likelihood of introducing errors or vulnerabilities. Moreover, empty code blocks may give a false impression of implemented functionality or security measures, creating a misleading sense of assurance. To ensure clarity and maintainability, it is essential to avoid empty code blocks and explicitly document the intended behavior or any intentional omissions.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - src/core/Vault.kerosine.bounded.sol

```solidity
17	  constructor(
18	    IVaultManager   _vaultManager,
19	    ERC20           _asset, 
20	    KerosineManager _kerosineManager
21	  ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```
[17..21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21)


</details>

-------
### [N-16] Emits without `msg.sender` parameter
<a name="N-16"></a>
[To the top](#TOP)

If `msg.sender` play a part in the functionality of a function, any emits of this function should include msg.sender to ensure transparency with users

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
200	      emit RedeemDyad(id, vault, amount, to);
```
[200](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L200)


</details>

-------
### [N-17] Unused `modifier`
<a name="N-17"></a>
[To the top](#TOP)

Consider removing unused modifier or moving it to a higher level contract.

#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - src/core/VaultManagerV2.sol

```solidity
45	  modifier isLicensed(address vault) {
46	    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47	  }
```
[45..47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45-L47)


</details>

-------
### [N-18] Consider disallowing transfers to `address(this)`
<a name="N-18"></a>
[To the top](#TOP)



#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - src/core/Vault.kerosine.unbounded.sol

```solidity
30	  function withdraw(
31	    uint    id,
32	    address to,
33	    uint    amount
34	  ) 
35	    external 
36	      onlyVaultManager
37	  {
```
[30..37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L37)


</details>

-------
### [N-19] Named imports of parent contracts are missing
<a name="N-19"></a>
[To the top](#TOP)



#### <ins>Proof Of Concept</ins>

<details>

<summary>see 1 instances</summary>


---

	 - script/deploy/Deploy.V2.s.sol

```solidity
35	contract DeployV2 is Script, Parameters {
36	  function run() public returns (Contracts memory) {
```
[35..36](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35-L36)


</details>
