# Report


## QA Report


| |Issue|Severity|
|-|:-|:-:|
| [L-01](#L-01) | `VaultManagerV2.withdraw` uses a dangerous strict equality | Low |
| [L-02](#L-02) | Local variables never initialized | Low |
| [NC-01](#NC-01) | Pragma version=0.8.17 allows old versions | Non-Critical |
| [NC-02](#NC-02) | KerosineDenominator.kerosine should be immutable | Non-Critical |

## <a name="L-01"></a>[L-01] `VaultManagerV2.withdraw` uses a dangerous strict equality

The function `VaultManagerV2.withdraw(uint256,address,uint256,address)` in `VaultManagerV2.sol` at lines 134-153 contains a dangerous strict equality check. Specifically, the line `idToBlockOfLastDeposit[id] == block.number` at line 143 uses strict equality (`==`) to compare the `idToBlockOfLastDeposit` value with the current block number (`block.number`).

### Recommendation:
Avoid using strict equality checks (==) in situations where precise values are crucial for security or critical logic. Instead, consider using range checks or other validation mechanisms that are less susceptible to manipulation by attackers.


*Instances (1)*:
```solidity
File: /src/core/VaultManagerV2.sol

143:        idToBlockOfLastDeposit[id] == block.number

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L143)


## <a name="L-02"></a>[L-02] Local variables never initialized

The functions `VaultManager.getTotalUsdValue(uint256).usdValue` in `VaultManager.sol` at line 191, `VaultManagerV2.getKeroseneValue(uint256).usdValue` in `VaultManagerV2.sol` at line 279, and `VaultManagerV2.getNonKeroseneValue(uint256).usdValue` in `VaultManagerV2.sol` at line 260 all contain local variables (usdValue) that are never initialized.

### Recommendation:
Always initialize local variables before use to ensure predictable behavior and avoid potential vulnerabilities. If a variable is meant to be initialized to zero or a specific value, explicitly set it to that value during declaration. This not only improves code readability but also reduces the risk of unintended consequences due to uninitialized variables.

*Instances (3)*:
```solidity
File: /src/core/VaultManagerV2.sol

279:        uint usdValue;

```

```solidity
File: /src/core/VaultManager.sol

191:        uint usdValue;

```

```solidity
File: /src/core/VaultManagerV2.sol

260:        uint usdValue;

```

[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L279)
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L260)
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManager.sol#L191)

### <a name="NC-01"></a>[NC-01] Pragma version=0.8.17 allows old versions

The contracts listed are using an outdated version of Solidity (`0.8.17`) specified in their pragma statements. These instances are flagged because they are not using a recent version of Solidity, potentially missing out on important security updates and features introduced in newer compiler versions.

### Recommendation

- Deploy with Recent Solidity Version: Update the pragma statement to use a recent version of Solidity (at least 0.8.0) to ensure access to the latest security features and optimizations.
- Simplify Pragma Statements: Avoid complex pragma statements unless absolutely necessary. Use a simple pragma version that allows for compatibility with a range of recent Solidity versions.
- Testing with Latest Solidity: Consider using the latest stable version of Solidity for testing and development to leverage the most recent advancements and security checks provided by the compiler.

*Instances (6)*:

```solidity
File: /src/core/Vault.kerosine.unbounded.sol

39:         pragma solidity =0.8.17;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2)

```solidity
File: /src/core/Vault.kerosine.bounded.sol

2:         pragma solidity =0.8.17;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2)

```solidity
File: /src/core/Vault.kerosine.sol

2:         pragma solidity =0.8.17;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2)

```solidity
File: /src/core/VaultManagerV2.sol

2:         pragma solidity =0.8.17;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2)

```solidity
File: /src/staking/KerosineDenominator.sol

2:         pragma solidity =0.8.17;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L2)


### <a name="NC-02"></a>[NC-02] KerosineDenominator.kerosine should be immutable 

The state variable `kerosine` in the contract `KerosineDenominator` defined in `KerosineDenominator.sol` at line 9 is not declared as immutable. Since this variable is not updated after deployment, declaring it as immutable can optimize the code.

### Recommendation

Declare State Variable as Immutable: Add the `immutable` attribute to the `kerosine` state variable in the contract `KerosineDenominator` since it is never updated after deployment.

*Instances (1)*:
```solidity
File: /src/staking/KerosineDenominator.sol

9:        Kerosine public kerosine;

```
[Link to code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9)

