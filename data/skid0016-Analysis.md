## Medium

### [M-01] Uninitialized Local Variable (Risk of Unintended Behavior)

**Description:**
In the `VaultManagerV2::getNonKeroseneValue` function, the local variable `usdValue` is declared but not initialized with a default value before use. This can lead to unintended behavior or incorrect calculations. If the condition `vaultLicenser.isLicensed(address(vault))` evaluates to `false`, the `usdValue` variable remains uninitialized, causing it to hold an unpredictable value or be incorrectly added to `totalUsdValue`.

**Impact:**
An uninitialized variable can cause unpredictable outcomes, affecting the accuracy of calculations or state changes. This inconsistency could lead to incorrect totals, affecting the contract's business logic, and potentially causing miscalculations or incorrect data being used elsewhere in the contract.

**Proof of Concept:**
Below is the code snippet with the issue. Notice that `usdValue` is declared without initialization, potentially leading to erroneous behavior if the conditional check isn't satisfied:
```javascript
function getNonKeroseneValue(
    uint id
) 
  public 
  view
  returns (uint) {
    uint totalUsdValue;
    uint numberOfVaults = vaults[id].length(); 
    for (uint i = 0; i < numberOfVaults; i++) {
      Vault vault = Vault(vaults[id].at(i));
      uint usdValue;
      if (vaultLicenser.isLicensed(address(vault))) {
        usdValue = vault.getUsdValue(id);        
      }
      totalUsdValue += usdValue;
    }
    return totalUsdValue;
}
```
If `vaultLicenser.isLicensed(address(vault))` is false, the `usdValue` variable remains uninitialized, leading to unexpected results in totalUsdValue.

**Recommended Mitigation:** To prevent unintended behavior, initialize `usdValue` with a default value. This ensures consistent behavior even if the condition is not met. Here is the corrected code snippet:

```javascript
    function getNonKeroseneValue(
    uint id
) 
  public 
  view
  returns (uint) {
    uint totalUsdValue;
    uint numberOfVaults = vaults[id].length(); 
    for (uint i = 0; i < numberOfVaults; i++) {
      Vault vault = Vault(vaults[id].at(i));
      uint usdValue = 0; // Initialization to avoid uninitialized issues
      if (vaultLicenser.isLicensed(address(vault))) {
        usdValue = vault.getUsdValue(id);        
      }
      totalUsdValue += usdValue;
    }
    return totalUsdValue;
}
```
Initializing `usdValue` to `0` prevents any unpredictable behavior and maintains proper calculation logic, thus reducing the risk of unintended outcomes.

### [M-02] Dangerous Strict Equality Check in `withdraw` Function

**Description:**
The `withdraw` function in the `VaultManagerV2` contract checks whether a withdrawal is being attempted in the same block where a deposit occurred. This is achieved through a strict equality check:

```Javascript
if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
```
Strict equality checks like this can be risky because of the high likelihood of state changes, especially in complex systems with external interactions. This check could lead to unintended revertions, potentially disrupting expected behavior.

**Impact:**

*   **Unintended Reverts:** If a user attempts to withdraw after a deposit within the same block, the transaction will revert. This could be exploited to disrupt legitimate operations or prevent certain transactions from occurring.
*   **Race Conditions:** In high-volume environments, strict equality checks can be prone to race conditions, leading to inconsistent behavior or errors.

**Proof of Concept:** Consider a scenario where a user deposits into a vault and then attempts to withdraw within the same block. Given the strict equality check, the withdrawal will revert, leading to unexpected behavior or user frustration.

**Recommended Mitigation:** To mitigate this issue, consider implementing a more robust check that accounts for potential race conditions or varying block times:

*   **Block Buffer:** Instead of checking if the deposit and withdrawal occur in the same block, consider implementing a buffer to allow a certain number of blocks between operations.
*   **Timestamp-Based Checks:** Use block timestamps to determine if sufficient time has passed between deposit and withdrawal. This approach is less prone to race conditions.
*   **Explicit User Confirmation:** Require explicit user confirmation for potentially risky operations to ensure that users are aware of the consequences.

Here's a refactor that introduces a block buffer to reduce the risk of race conditions:

```javascript
    function withdraw(
    uint id,
    address vault,
    uint amount,
    address to
) 
    public
    isDNftOwner(id)
{
    if (block.number - idToBlockOfLastDeposit[id] < 2) revert DepositedInSameBlock();
    ...
}
```
By implementing these changes, the system becomes less prone to strict equality issues, reducing the risk of unintended reverts or race conditions.


## Low

### [L-01] Function Does Not Follow Check-Effects-Interactions (CEI) Pattern

**Description:** 
In the `mintDyad` function, the code makes an external call to `dyad.mint()` before emitting the event `MintDyad`. The typical pattern for functions involving external calls is Check-Effects-Interactions (CEI), where state changes and event emissions are done before interacting with external contracts. Deviating from this pattern might lead to unexpected behaviors, especially if reentrancy vulnerabilities or state inconsistencies could occur.

**Impact:** 
The deviation from the CEI pattern, while not inherently leading to a security risk, could result in unexpected behavior or difficulty in tracking changes. Although not critical, following the CEI pattern helps ensure proper sequencing and minimizes potential vulnerabilities.

**Proof of Concept:**
Here is the code snippet from the `mintDyad` function where the deviation occurs:

```javascript
function mintDyad(
    uint    id,
    uint    amount,
    address to
) 
  external 
    isDNftOwner(id)
{
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted) revert NotEnoughExoCollat();
    dyad.mint(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();
    emit MintDyad(id, amount, to);
}
```
**Recommended Mitigation:** 

To follow the CEI pattern, refactor the function to ensure state changes and event emissions occur before any external interactions. Here is the corrected version of the mintDyad function following the CEI pattern:
```javascript
function mintDyad(
    uint    id,
    uint    amount,
    address to
) 
  external 
    isDNftOwner(id)
{
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted) revert NotEnoughExoCollat();
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();
    
    emit MintDyad(id, amount, to);
    dyad.mint(id, to, amount);
}
```
By placing the event emission and checks before the external interaction, the function better aligns with the CEI pattern, reducing the risk of unexpected behavior.

NOTE: The following functions also does not follow CEI:
`VaultManagerV2::mintDyad`, `VaultManagerV2::redeemDyad`,  `VaultManagerV2::liquidate`. I will love you to follow the best practice there also

### [L-02] Insufficient Documentation (Lack of Comments and Annotations)

**Description:**
The codebase lacks adequate documentation, including side notes, comments, and explanatory annotations. While the code itself may function correctly, the absence of comments makes it difficult for auditors and other developers to understand the code's intent, structure, and critical logic. Proper documentation is essential for code maintainability, auditability, and ease of understanding, especially in complex smart contracts.

**Impact:**
The lack of comments and documentation can lead to several issues:
- **Increased Audit Time:** Without comments, auditors must spend more time understanding the code's functionality and logic, potentially overlooking crucial details.
- **Reduced Maintainability:** Developers maintaining or extending the code may struggle to understand its structure, leading to longer development times and an increased risk of introducing bugs.
- **Decreased Collaboration:** Teams collaborating on the codebase may find it challenging to understand each other's work without clear comments and documentation.

**Proof of Concept:**
In the following code snippet, there's a lack of comments explaining the purpose of each function, variable, or complex logic. Without these explanations, it is challenging to understand the rationale behind certain operations, which can lead to misinterpretation or errors during audits.

```javascript
// Example function with no comments or explanation
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
```
This snippet lacks comments describing what the function is doing, what the variables represent, and the context in which it operates. This absence of documentation can lead to confusion and misinterpretation.

**Recommended Mitigation:** To improve documentation and ease of understanding:

*   **Add Comments to Functions:** Each function should have a brief description of its purpose, the expected inputs and outputs, and any important side effects.
*   **Comment Complex Logic:** For sections of code with intricate logic, include comments to explain the reasoning and expected behavior.
*   **Document State Variables:** Provide descriptions for state variables, explaining their purpose and how they are used throughout the contract.
*   **Use NatSpec Comments for Functions:** Employ Ethereum Natural Language Specification (NatSpec) comments for external functions to facilitate automated documentation tools and improve readability for auditors.

By implementing these suggestions, the codebase will become more understandable, easier to audit, and simpler to maintain, leading to reduced risk of errors and improved collaboration among developers and auditors.

## GAS

### [G-01] External Calls Within a Loop (Gas Inefficiency)

**Description:** 
The `VaultManagerV2` contract has a pattern where external calls are made within a loop. Specifically, in the `getNonKeroseneValue` function, there is an external call to `vaultLicenser.isLicensed(address(vault))` in each iteration of the loop. This design can lead to higher gas costs due to multiple external calls, which could be avoided by caching the results or rethinking the loop structure.

**Impact:** 
- **Higher Gas Costs**: Repeated external calls within a loop significantly increase transaction gas costs, potentially making some operations prohibitively expensive.
- **Reduced Efficiency**: Increased gas consumption reduces the contract's overall efficiency, affecting its usability in real-world scenarios.

**Proof of Concept:**
In the following snippet, the external call to `vaultLicenser.isLicensed(address(vault))` occurs within a loop, increasing gas consumption with each iteration:

```javascript
function getNonKeroseneValue(uint id) public view returns (uint) {
    uint totalUsdValue;
    uint numberOfVaults = vaults[id].length(); 
    for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[id].at(i));
        if (vaultLicenser.isLicensed(address(vault))) {  // External call within loop
            totalUsdValue += vault.getUsdValue(id);
        }
    }
    return totalUsdValue;
}
```
**Recommended Mitigation:** To reduce gas costs and improve efficiency, consider the following:

*   **Cache External Results**: Before entering the loop, cache the results of external calls to avoid repetitive interactions.
*   **Restructure the Loop**: Minimize or eliminate external calls within the loop, if possible.

The following refactor demonstrates caching the license status before entering the loop, reducing repeated external calls:

```javascript
    function getNonKeroseneValue(uint id) public view returns (uint) {
    uint totalUsdValue;
    uint numberOfVaults = vaults[id].length();
    bool[] memory isLicensed = new bool[](numberOfVaults);

    // Cache license status
    for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[id].at(i));
        isLicensed[i] = vaultLicenser.isLicensed(address(vault));
    }

    // Now use cached results to calculate total USD value
    for (uint i = 0; i < numberOfVaults; i++) {
        if (isLicensed[i]) {
            Vault vault = Vault(vaults[id].at(i));
            totalUsdValue += vault.getUsdValue(id);
        }
    }
    return totalUsdValue;
}

```

Implementing these mitigations can significantly reduce gas costs and improve the contract's efficiency.

**Note**: The following functions also have external calls within a loop:

*   `VaultManagerV2::getNonKeroseneValue`
*   `VaultManagerV2::getKeroseneValue`
*   `Vault.kerosine.unbounded::assetPrice`

### [G-02] Non-Immutable Variable in `KerosineDenominator` (Optimization Impact)

**Description:**
The `KerosineDenominator` contract has a `Kerosine` reference named `kerosine` that is initialized in the constructor and does not change afterward. In Solidity, variables that are set in the constructor and remain constant can be marked as `immutable`. Using `immutable` reduces gas costs during contract execution and indicates to readers that the variable's value won't change.

**Impact:**
- **Gas Costs:** Marking a variable as `immutable` can lower gas costs for reads and ensure the variable value is known at compile time, leading to optimization.
- **Clarity:** The `immutable` keyword makes it clear that a variable is set once and won't change, improving the code's readability and maintainability.

**Proof of Concept:**
```javascript
contract KerosineDenominator is Parameters {
  Kerosine public kerosine;

  constructor(
    Kerosine _kerosine
  ) {
    kerosine = _kerosine;
  }

  function denominator() external view returns (uint) {
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
}
```
In this code snippet, `kerosine` is set in the constructor and doesn't change, indicating it should be marked as `immutable`.

**Recommended Mitigation:** To improve gas efficiency and provide clarity, mark the `kerosine` variable as `immutable`. This change can reduce the gas cost for read operations and make it clear that this variable's value won't change after initialization.

```javascript
    contract KerosineDenominator is Parameters {
  Kerosine public immutable kerosine;  // Marked as immutable

  constructor(
    Kerosine _kerosine
  ) {
    kerosine = _kerosine;
  }

  function denominator() external view returns (uint) {
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
}

```
This change adds the `immutable` keyword to `kerosine`, indicating that the value is set once and never changes, leading to better gas efficiency and clarity.



## Informational

### [I-1] Improve Naming Conventions for Storage and Immutable Variables

**Description:**
In Solidity codebases, variable naming conventions are essential for code readability, maintainability, and reducing the likelihood of errors. Using consistent prefixes for storage and immutable variables helps distinguish between them at a glance, aiding in understanding and debugging. The current codebase does not follow consistent naming conventions for storage and immutable variables, which might lead to confusion for developers and auditors.

**Impact:**
- **Readability:** Inconsistent naming conventions can make it harder for developers and auditors to understand the purpose and scope of a variable.
- **Maintainability:** Proper naming conventions reduce the risk of misinterpretation when modifying or extending the codebase.
- **Debugging:** Clear conventions help identify variable types and their expected behavior, simplifying troubleshooting.

**Proof of Concept:**
In the codebase, storage and immutable variables do not follow a consistent naming convention. This can be seen in the following example from the `VaultManagerV2` contract:

```javascript
DNft public immutable dNft;  // Immutable variable
Dyad public immutable dyad;  // Immutable variable
Licenser public immutable vaultLicenser;  // Immutable variable

mapping(uint => EnumerableSet.AddressSet) internal vaults;  // Storage variable
```
In this example, there's no clear indication that `vaults` is a storage variable or that `dNft`, `dyad`, and `vaultLicenser` are immutable variables.

**Recommended Mitigation:** To improve readability and maintainability, consider adopting a consistent naming convention for storage and immutable variables. A common approach is to prefix storage variables with `s_` and immutable variables with `i_`. This convention makes it easier to identify the variable's purpose at a glance.

Here's an example of how you might refactor the code to follow this convention:

```javascript
    DNft public immutable i_dNft;
Dyad public immutable i_dyad;
Licenser public immutable i_vaultLicenser;

mapping(uint => EnumerableSet.AddressSet) internal s_vaults;

```
This change would improve code clarity and aid future developers in understanding the structure of the codebase.

### Time spent:
29 hours