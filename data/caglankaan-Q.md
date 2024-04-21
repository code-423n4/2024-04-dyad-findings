### Consider implementing two-step procedure for updating protocol addresses
Implementing a two-step procedure for updating protocol addresses adds an extra layer of security. In such a system, the first step initiates the change, and the second step, after a predefined delay, confirms and finalizes it. This delay allows stakeholders or monitoring tools to observe and react to unintended or malicious changes. If an unauthorized change is detected, corrective actions can be taken before the change is finalized. To achieve this, introduce a "proposed address" state variable and a "delay period". Upon an update request, set the "proposed address". After the delay, if not contested, the main protocol address can be updated.

```solidity
Path: ./src/core/VaultManagerV2.sol

63:      keroseneManager = _keroseneManager;	// @audit-issue
```
[63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63-L63), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

29:    unboundedKerosineVault = _unboundedKerosineVault;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29-L29), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

47:    kerosineDenominator = _kerosineDenominator;	// @audit-issue
```
[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47-L47), 


#### Recommendation

Introduce two state variables in your contract: one to hold the proposed new address (`address public proposedAddress`) and another to timestamp the proposal (`uint public addressChangeInitiated`). Implement two functions: one to propose a new address, recording the current timestamp, and another to finalize the address change after the delay period has elapsed.


### Missing checks for `address(0)` in constructor/initializers
In Solidity, the Ethereum address `0x0000000000000000000000000000000000000000` is known as the "zero address". This address has significance because it's the default value for uninitialized address variables and is often used to represent an invalid or non-existent address. The "
Missing zero address control" issue arises when a Solidity smart contract does not properly check or prevent interactions with the zero address, leading to unintended behavior.
For instance, a contract might allow tokens to be sent to the zero address without any checks, which essentially burns those tokens as they become irretrievable. While sometimes this is intentional, without proper control or checks, accidental transfers could occur.    
        

```solidity
Path: ./src/staking/KerosineDenominator.sol

14:    kerosine = _kerosine;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14-L14), 


```solidity
Path: ./src/core/VaultManagerV2.sol

54:    dNft          = _dNft;	// @audit-issue

55:    dyad          = _dyad;	// @audit-issue

56:    vaultLicenser = _licenser;	// @audit-issue
```
[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54-L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55-L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56-L56), 


```solidity
Path: ./src/core/Vault.kerosine.sol

31:    vaultManager    = _vaultManager;	// @audit-issue

32:    asset           = _asset;	// @audit-issue

33:    kerosineManager = _kerosineManager;	// @audit-issue
```
[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31-L31), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L32-L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33-L33), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

27:      dyad = _dyad;	// @audit-issue
```
[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27-L27), 


#### Recommendation

It is strongly recommended to implement checks to prevent the zero address from being set during the initialization of contracts. This can be achieved by adding require statements that ensure address parameters are not the zero address. 

### Missing checks for `address(0)`  when updating state variables
In Solidity, the Ethereum address `0x0000000000000000000000000000000000000000` is known as the "zero address". This address has significance because it's the default value for uninitialized address variables and is often used to represent an invalid or non-existent address. The "
Missing zero address control" issue arises when a Solidity smart contract does not properly check or prevent interactions with the zero address, leading to unintended behavior.
For instance, a contract might allow tokens to be sent to the zero address without any checks, which essentially burns those tokens as they become irretrievable. While sometimes this is intentional, without proper control or checks, accidental transfers could occur.    
        

```solidity
Path: ./src/core/VaultManagerV2.sol

63:      keroseneManager = _keroseneManager;	// @audit-issue

102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();	// @audit-issue

114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();	// @audit-issue
```
[63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L63-L63), [102](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L102-L102), [114](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L114-L114), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

29:    unboundedKerosineVault = _unboundedKerosineVault;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L29-L29), 


```solidity
Path: ./src/core/KerosineManager.sol

34:    if (!vaults.remove(vault)) revert VaultNotFound();	// @audit-issue
```
[34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L34-L34), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

47:    kerosineDenominator = _kerosineDenominator;	// @audit-issue
```
[47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L47-L47), 


#### Recommendation

It is strongly recommended to implement checks to prevent the zero address from being set during the initialization of contracts. This can be achieved by adding require statements that ensure address parameters are not the zero address. 


### The `constructor`/`initialize` function lacks parameter validation.
Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

```solidity
Path: ./src/staking/KerosineDenominator.sol

14:    kerosine = _kerosine;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L14-L14), 


```solidity
Path: ./src/core/VaultManagerV2.sol

54:    dNft          = _dNft;	// @audit-issue

55:    dyad          = _dyad;	// @audit-issue

56:    vaultLicenser = _licenser;	// @audit-issue
```
[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L54-L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L55-L55), [56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L56-L56), 


```solidity
Path: ./src/core/Vault.kerosine.sol

31:    vaultManager    = _vaultManager;	// @audit-issue

33:    kerosineManager = _kerosineManager;	// @audit-issue
```
[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L31-L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L33-L33), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

27:      dyad = _dyad;	// @audit-issue
```
[27](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L27-L27), 


#### Recommendation

Incorporate comprehensive parameter validation in your contract's constructor and initialization functions. This should include checks for value ranges, address validity, and any other condition that defines a parameter as valid. Use `require` statements for validation, providing clear error messages for each condition. If any validation fails, the `require` statement will revert the transaction, preventing the contract from being deployed or initialized with invalid parameters.
Example:
```solidity
contract MyContract {
    address public owner;
    uint256 public someValue;

    constructor(address _owner, uint256 _someValue) {
        require(_owner != address(0), "Owner cannot be the zero address");
        require(_someValue > 0 && _someValue < 100, "SomeValue must be between 1 and 99");

        owner = _owner;
        someValue = _someValue;
    }
}

// For contracts using the proxy pattern and requiring initialization functions:
function initialize(address _owner, uint256 _someValue) public {
    require(_owner != address(0), "Owner cannot be the zero address");
    require(_someValue > 0 && _someValue < 100, "SomeValue must be between 1 and 99");

    owner = _owner;
    someValue = _someValue;
}
```



### Functions calling contracts/addresses with transfer hooks are missing reentrancy guards
Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.

```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

39:    asset.safeTransfer(to, amount); 	// @audit-issue
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L39-L39), 


#### Recommendation

To ensure the security of your protocol and protect users from potential vulnerabilities, consider implementing reentrancy guards in functions that call contracts or addresses with transfer hooks. Even if your function follows the check-effects-interaction pattern, using reentrancy guards is essential to prevent read-only reentrancy attacks, as demonstrated in incidents like the [Curve LP Oracle Manipulation](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/). Implementing reentrancy guards adds an extra layer of protection and safeguards your protocol against such attacks.


### External calls in an unbounded loop can result in a DoS
Consider limiting the number of iterations in loops that make external calls, as just a single one of them failing will result in a revert.

```solidity
Path: ./src/core/VaultManagerV2.sol

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue

224:          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);	// @audit-issue

225:          vault.move(id, to, collateral);	// @audit-issue

259:        Vault vault = Vault(vaults[id].at(i));	// @audit-issue

261:        if (vaultLicenser.isLicensed(address(vault))) {	// @audit-issue

262:          usdValue = vault.getUsdValue(id);        	// @audit-issue

278:        Vault vault = Vault(vaultsKerosene[id].at(i));	// @audit-issue

280:        if (keroseneManager.isLicensed(address(vault))) {	// @audit-issue

281:          usdValue = vault.getUsdValue(id);        	// @audit-issue
```
[223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), [224](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L224-L224), [225](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L225-L225), [259](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L259-L259), [261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261-L261), [262](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L262-L262), [278](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L278-L278), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280-L280), [281](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L281-L281), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue

61:                * vault.assetPrice() * 1e18	// @audit-issue

62:                / (10**vault.asset().decimals()) 	// @audit-issue

63:                / (10**vault.oracle().decimals());	// @audit-issue
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L60), [61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L61-L61), [62](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L62-L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L63-L63), 


#### Recommendation

To mitigate the risk of Denial-of-Service (DoS) attacks in your Solidity code, it's important to limit the number of iterations in loops that involve external calls. A single failed external call in an unbounded loop can lead to a revert, causing disruptions in contract execution. Consider implementing safeguards, such as setting a maximum loop iteration count or employing strategies like batch processing, to reduce the impact of potential external call failures.

### Possible loss of precision
Division by large numbers may result in precision loss due to rounding down, or even the result being erroneously equal to zero. Consider adding checks on the numerator to ensure precision loss is handled appropriately.


```solidity
Path: ./src/core/VaultManagerV2.sol

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue
147:                  * 1e18 
148:                  / 10**_vault.oracle().decimals() 
149:                  / 10**_vault.asset().decimals();

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue
147:                  * 1e18 
148:                  / 10**_vault.oracle().decimals() 

195:      uint asset = amount 	// @audit-issue
196:                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                    / _vault.assetPrice() 
```
[146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L149), [146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L148), [195](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L195-L197), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue
61:                * vault.assetPrice() * 1e18
62:                / (10**vault.asset().decimals()) 
63:                / (10**vault.oracle().decimals());

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue
61:                * vault.assetPrice() * 1e18
62:                / (10**vault.asset().decimals()) 

67:      return numerator * 1e8 / denominator;	// @audit-issue
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L63), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L62), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L67-L67), 


#### Recommendation

Incorporate strategies in your Solidity contracts to mitigate precision loss in division operations. This can include:
1. Performing checks on the numerator and denominator to ensure they are within a reasonable range to avoid significant rounding errors.
2. Considering the use of fixed-point arithmetic libraries or scaling factors to handle divisions with higher precision.
3. Clearly documenting any inherent limitations of your division logic and providing guidelines for inputs to minimize unexpected behavior.
Always thoroughly test division operations under various scenarios to ensure that the outcomes are consistent with your contract's intended logic and accuracy requirements.



### Non-compliant `IERC20` tokens may revert with `transfer`
Some `IERC20` tokens (e.g. `BNB`, `OMG`, `USDT`) do not implement the standard properly, but they are still accepted by most code that accepts `ERC20` tokens.

For example, `USDT` transfer functions on L1 do not return booleans: when casted to `IERC20`, their function signatures do not match, and therefore the calls made will revert.

```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

39:    asset.safeTransfer(to, amount); 	// @audit-issue
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L39-L39), 


#### Recommendation

When dealing with tokens that may not fully comply with the `IERC20` standard, it's important to exercise caution and carefully verify the behavior of the specific token in question. In cases where tokens do not return booleans for transfer functions, consider implementing additional error-handling mechanisms to account for potential failures. This may include checking the token balance before and after the transfer to detect any discrepancies or using try-catch blocks to handle potential exceptions. Ensuring robust error handling can help your smart contract interact more gracefully with non-compliant tokens while maintaining security and reliability.

### Unneeded initializations of integer variable to `0`.
In Solidity, it is common practice to initialize variables with default values when declaring them. However, initializing integer variables to `0` when they are not subsequently used in the code can lead to unnecessary gas consumption and code clutter. This issue points out instances where such initializations are present but serve no functional purpose.

```solidity
Path: ./src/core/VaultManagerV2.sol

222:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

258:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

277:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222-L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258-L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277-L277), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

58:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue
```
[58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58-L58), 


#### Recommendation


It is recommended not to initialize integer variables to `0` to save some Gas.


### Unused import
The identifier is imported but never used within the file.

```solidity
Path: ./src/core/VaultManagerV2.sol

12:import {ERC20}             from "@solmate/src/tokens/ERC20.sol";	// @audit-issue: ERC20 not used in the contract.
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

6:import {Dyad}                   from "./Dyad.sol";	// @audit-issue: Dyad not used in the contract.
```
[6](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L6-L6), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

9:import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";	// @audit-issue: BoundedKerosineVault not used in the contract.
```
[9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L9-L9), 


#### Recommendation

Regularly review your Solidity code to remove unused imports. This practice declutters the codebase, making it easier to understand and maintain. In addition, consider using tools or IDE features that can automatically detect and highlight unused imports for cleanup. Keeping imports limited to only what is necessary helps maintain a clear understanding of the contract's dependencies and reduces potential confusion for developers working on or reviewing the code.

### Excessive Authorization in Contract Functions
A contract where a high percentage of functions require authorization (e.g., restricted to the contract owner or specific roles) may indicate over-centralization or excessive control. This could limit the contract's flexibility, reduce trust among users, and potentially create bottleneck points that could be exploited or become failure points. While some level of control is necessary for administrative purposes, overly restrictive access can detract from the decentralized nature of blockchain applications and concentrate too much power in the hands of a few.

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `setUnboundedKerosineVault`
	List of functions that require authorization: `setUnboundedKerosineVault`
	List of functions that doesn't require authorization: None
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `remove`, `add`
	List of functions that require authorization: `remove`, `add`
	List of functions that doesn't require authorization: None
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `deposit`, `move`
	List of functions that require authorization: `deposit`, `move`
	List of functions that doesn't require authorization: None
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `withdraw`, `setDenominator`
	List of functions that require authorization: `withdraw`, `setDenominator`
	List of functions that doesn't require authorization: None
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Make contract more decentralized.

### `public` functions not called by the contract should be declared `external` instead
In Solidity, function visibility is an important aspect that determines how and where a function can be called from. Two commonly used visibilities are `public` and `external`. A `public` function can be called both from other functions inside the same contract and from outside transactions, while an `external` function can only be called from outside the contract.
A potential pitfall in smart contract development is the misuse of the `public` keyword for functions that are only meant to be accessed externally. When a function is not used internally within a contract and is only intended for external calls, it should be labeled as `external` rather than `public`. Using `public` unnecessarily can introduce potential vulnerabilities and also make the contract consume more gas than required. This is because `public` functions have to add additional code to handle both internal and external calls, while `external` functions can be more optimized since they only handle external calls.


```solidity
Path: ./src/core/Vault.kerosine.sol

36:  function deposit(	// @audit-issue

60:  function getUsdValue(	// @audit-issue
```
[36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L36), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L60), 


#### Recommendation

To optimize gas usage and improve code clarity, declare functions that are not called internally within the contract and are intended for external access as `external` rather than `public`. This ensures that these functions are only callable externally, reducing unnecessary gas consumption and potential security risks.

### `if`-statement can be converted to a ternary
The code can be made more compact while also increasing readability by converting the following `if`-statements to ternaries (e.g. `foo += (x > y) ? a : b`)

```solidity
Path: ./src/core/VaultManagerV2.sol

261:        if (vaultLicenser.isLicensed(address(vault))) {	// @audit-issue
262:          usdValue = vault.getUsdValue(id);        
263:        }

280:        if (keroseneManager.isLicensed(address(vault))) {	// @audit-issue
281:          usdValue = vault.getUsdValue(id);        
282:        }
```
[261](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L261-L263), [280](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L280-L282), 


#### Recommendation

Consider using single line if statements as ternary.

### Custom error has no error details
Consider adding parameters to the error to indicate which user or values caused the failure

```solidity
Path: ./src/core/KerosineManager.sol

8:  error TooManyVaults();	// @audit-issue

9:  error VaultAlreadyAdded();	// @audit-issue

10:  error VaultNotFound();	// @audit-issue
```
[8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L10-L10), 


#### Recommendation

When defining custom errors, consider adding parameters or error details that provide information about the specific conditions or inputs that caused the error. Including error details can make debugging and troubleshooting easier by providing context on the cause of the failure.

### Constants in comparisons should appear on the left side
Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html)

```solidity
Path: ./src/core/VaultManagerV2.sol

237:      if (_dyad == 0) return type(uint).max;	// @audit-issue
```
[237](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L237-L237), 


#### Recommendation

To prevent typo bugs and improve code readability, it's advisable to place constants on the left side of comparisons. This coding practice helps catch accidental assignment (=) instead of comparison (==) and enhances code quality.

### Duplicated `require()`/`revert()` checks should be refactored to a modifier or function
In Solidity contracts, it's common to encounter duplicated `require()` or `revert()` statements across multiple functions. These statements are crucial for validating conditions and ensuring contract integrity. However, repeated checks can lead to code redundancy, making the contract larger and more difficult to maintain. This redundancy can be streamlined by encapsulating the repeated logic in a modifier or a dedicated function. By doing so, the code becomes more concise, easier to audit, and more gas-efficient. Furthermore, centralizing the validation logic in a single location makes the codebase more adaptable to changes and reduces the risk of inconsistencies or errors in future updates.

```solidity
Path: ./src/core/VaultManagerV2.sol

101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();	// @audit-issue: Same if statement in line(s): ['113']

152:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 	// @audit-issue: Same if statement in line(s): ['167']
```
[101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101-L101), [152](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L152-L152), 


#### Recommendation

Consolidate repeated `require()` or `revert()` checks in Solidity by creating a modifier or a separate function. Apply this modifier to all functions requiring the same validation, or call the function at the beginning of each relevant function. This refactoring enhances contract efficiency, maintainability, and consistency, while potentially reducing gas costs associated with deploying and executing redundant code.

### Duplicate import statements
Contracts often depend on libraries and other contracts to modularize code and reuse functionalities. However, redundant imports occur when a contract imports a library or another contract that is already imported by one of its dependencies. This redundancy does not impact the compiled bytecode but can clutter the codebase, making it harder to understand the direct dependencies of each contract. Simplifying imports by removing these redundancies enhances code readability and maintainability.

```solidity
Path: ./src/core/VaultManagerV2.sol

6:import {Licenser}        from "./Licenser.sol";	// @audit-issue: Same library is also imported on: `['Dyad']`, at lines: `[5]`

8:import {IVaultManager}   from "../interfaces/IVaultManager.sol";	// @audit-issue: Same library is also imported on: `['Vault']`, at lines: `[4]`

11:import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";	// @audit-issue: Same library is also imported on: `['Vault']`, at lines: `[11]`

12:import {ERC20}             from "@solmate/src/tokens/ERC20.sol";	// @audit-issue: Same library is also imported on: `['Dyad', 'Vault']`, at lines: `[6, 12]`

13:import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";	// @audit-issue: Same library is also imported on: `['DNft', 'Vault']`, at lines: `[5, 10]`
```
[6](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L6-L6), [8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L8-L8), [11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L11-L11), [12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L13-L13), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

5:import {IVaultManager}          from "../interfaces/IVaultManager.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault']`, at lines: `[4]`

7:import {KerosineManager}        from "./KerosineManager.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault']`, at lines: `[5]`

10:import {ERC20} from "@solmate/src/tokens/ERC20.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault', 'Dyad']`, at lines: `[9, 6]`
```
[5](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L5-L5), [7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L7-L7), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L10-L10), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

5:import {IVaultManager}        from "../interfaces/IVaultManager.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault', 'Vault']`, at lines: `[4, 4]`

8:import {KerosineManager}      from "./KerosineManager.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault']`, at lines: `[5]`

12:import {ERC20}           from "@solmate/src/tokens/ERC20.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault', 'Vault', 'Dyad']`, at lines: `[9, 12, 6]`

13:import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";	// @audit-issue: Same library is also imported on: `['KerosineVault', 'Vault']`, at lines: `[8, 10]`
```
[5](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L5-L5), [8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L8-L8), [12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L13-L13), 


#### Recommendation

Review your Solidity contracts and eliminate duplicate import statements. Ensure each file is imported only once where it's needed. If you find the same import statement across multiple files, consider whether you can restructure your code to centralize common logic or dependencies, potentially through base contracts or libraries. Regularly conduct code audits or utilize linters and other static analysis tools to identify and resolve duplicate imports, thereby enhancing the clarity, structure, and security of your Solidity codebase.

### Unnecessary Use of `=` in Solidity Version Specification
In Solidity, the `pragma` statement specifies the compiler version required for the contract. The Solidity documentation and common practice show that using `pragma solidity ^version;` or `pragma solidity version;` is the standard way to declare the compiler version, where `version` represents a specific version number like `0.8.24`. The addition of an equals sign (`=`) as in `pragma solidity =0.8.24;` is redundant because the Solidity compiler interprets version specifications without the `=` sign in the same way. The equals sign does not alter the meaning or functionality of the version pragma but could lead to confusion or inconsistency in code style.

```solidity
Path: ./src/staking/KerosineDenominator.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2-L2), 


```solidity
Path: ./src/core/VaultManagerV2.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2-L2), 


```solidity
Path: ./src/core/KerosineManager.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2-L2), 


#### Recommendation

Review your Solidity contracts and standardize the version pragma statement by omitting the unnecessary `=` sign. Use `pragma solidity 0.8.24;` instead of `pragma solidity =0.8.24;` to specify the compiler version. This change aligns your contracts with common Solidity practices and enhances code readability and consistency. Consider adopting a linter or formatter tool that enforces standard Solidity coding conventions, including the correct format for version pragmas, to maintain uniformity across your project's codebase.

### Enforce Explicit Bit Size for `uint` and `int` Variables
Adopt best practices by explicitly defining `uint256` and `int256`, instead of using `uint` and `int` without specified bit sizes.

```solidity
Path: ./src/staking/KerosineDenominator.sol

17:  function denominator() external view returns (uint) {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17-L17), 


```solidity
Path: ./src/core/VaultManagerV2.sol

22:  uint public constant MAX_VAULTS          = 5;	// @audit-issue

23:  uint public constant MAX_VAULTS_KEROSENE = 5;	// @audit-issue

25:  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%	// @audit-issue

26:  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%	// @audit-issue

34:  mapping (uint => EnumerableSet.AddressSet) internal vaults; 	// @audit-issue

35:  mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 	// @audit-issue

37:  mapping (uint => uint) public idToBlockOfLastDeposit;	// @audit-issue

39:  modifier isDNftOwner(uint id) {	// @audit-issue

42:  modifier isValidDNft(uint id) {	// @audit-issue

68:      uint    id,	// @audit-issue

81:      uint    id,	// @audit-issue

95:      uint    id,	// @audit-issue

107:      uint    id,	// @audit-issue

120:    uint    id,	// @audit-issue

122:    uint    amount	// @audit-issue

135:    uint    id,	// @audit-issue

137:    uint    amount,	// @audit-issue

144:    uint dyadMinted = dyad.mintedDyad(address(this), id);	// @audit-issue

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue

157:    uint    id,	// @audit-issue

158:    uint    amount,	// @audit-issue

164:    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;	// @audit-issue

173:    uint id,	// @audit-issue

174:    uint amount	// @audit-issue

185:    uint    id,	// @audit-issue

187:    uint    amount,	// @audit-issue

192:    returns (uint) { 	// @audit-issue

195:      uint asset = amount 	// @audit-issue

206:    uint id,	// @audit-issue

207:    uint to	// @audit-issue

213:      uint cr = collatRatio(id);	// @audit-issue

217:      uint cappedCr               = cr < 1e18 ? 1e18 : cr;	// @audit-issue

218:      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);	// @audit-issue

219:      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);	// @audit-issue

221:      uint numberOfVaults = vaults[id].length();	// @audit-issue

224:          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);	// @audit-issue

222:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

231:    uint id	// @audit-issue

235:    returns (uint) {	// @audit-issue

236:      uint _dyad = dyad.mintedDyad(address(this), id);	// @audit-issue

242:    uint id	// @audit-issue

246:    returns (uint) {	// @audit-issue

251:    uint id	// @audit-issue

255:    returns (uint) {	// @audit-issue

256:      uint totalUsdValue;	// @audit-issue

257:      uint numberOfVaults = vaults[id].length(); 	// @audit-issue

260:        uint usdValue;	// @audit-issue

258:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

270:    uint id	// @audit-issue

274:    returns (uint) {	// @audit-issue

275:      uint totalUsdValue;	// @audit-issue

276:      uint numberOfVaults = vaultsKerosene[id].length(); 	// @audit-issue

279:        uint usdValue;	// @audit-issue

277:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

291:    uint id	// @audit-issue

300:    uint    id,	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26-L26), [34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L34-L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L35-L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L37-L37), [39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42-L42), [68](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L68-L68), [81](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L81-L81), [95](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L95-L95), [107](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L107-L107), [120](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L120-L120), [122](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L122-L122), [135](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L135-L135), [137](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L137-L137), [144](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L144-L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L146), [157](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L157-L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L158-L158), [164](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L164-L164), [173](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L173-L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L174-L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L185-L185), [187](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L187-L187), [192](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L192-L192), [195](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L195-L195), [206](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L206-L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L207-L207), [213](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L213-L213), [217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217-L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L218-L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L219-L219), [221](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L221-L221), [224](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L224-L224), [222](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L222-L222), [231](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L231-L231), [235](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L235-L235), [236](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L236-L236), [242](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L242-L242), [246](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L246-L246), [251](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L251-L251), [255](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L255-L255), [256](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L256-L256), [257](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L257-L257), [260](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L260-L260), [258](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L258-L258), [270](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L270-L270), [274](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L274-L274), [275](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L275-L275), [276](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L276-L276), [279](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L279-L279), [277](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L277-L277), [291](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L291-L291), [300](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L300-L300), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

33:    uint    id,	// @audit-issue

35:    uint    amount	// @audit-issue

48:    returns (uint) {	// @audit-issue
```
[33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L33-L33), [35](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L35-L35), [48](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L48-L48), 


```solidity
Path: ./src/core/KerosineManager.sol

14:  uint public constant MAX_VAULTS = 10;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14-L14), 


```solidity
Path: ./src/core/Vault.kerosine.sol

19:  mapping(uint => uint) public id2asset;	// @audit-issue

37:    uint id,	// @audit-issue

38:    uint amount	// @audit-issue

48:    uint from,	// @audit-issue

49:    uint to,	// @audit-issue

50:    uint amount	// @audit-issue

61:    uint id	// @audit-issue

65:    returns (uint) {	// @audit-issue

73:    returns (uint); 	// @audit-issue
```
[19](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L19-L19), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L37-L37), [38](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L38-L38), [48](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L48-L48), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L49-L49), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L50-L50), [61](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L61-L61), [65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L65-L65), [73](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L73-L73), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

31:    uint    id,	// @audit-issue

33:    uint    amount	// @audit-issue

54:    returns (uint) {	// @audit-issue

55:      uint tvl;	// @audit-issue

57:      uint numberOfVaults = vaults.length;	// @audit-issue

58:      for (uint i = 0; i < numberOfVaults; i++) {	// @audit-issue

65:      uint numerator   = tvl - dyad.totalSupply();	// @audit-issue

66:      uint denominator = kerosineDenominator.denominator();	// @audit-issue
```
[31](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L31-L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L33-L33), [54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L54-L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L55-L55), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L57-L57), [58](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L58-L58), [65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L66-L66), 


#### Recommendation

Always specify the bit size when declaring `uint` and `int` variables in Solidity. Use `uint256` or `int256` instead of the generic `uint` and `int`. This explicit declaration enhances code readability and clarity, particularly in contracts that utilize various integer sizes. Adhering to this best practice helps in maintaining a clear and unambiguous codebase, making the code more accessible and understandable to developers and auditors alike.

### Dependence on external protocols
External protocols should be monitored as such dependencies may introduce vulnerabilities if a vulnerability is found /introduced in the external protocol

```solidity
Path: ./src/core/VaultManagerV2.sol

11:import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";	// @audit-issue

12:import {ERC20}             from "@solmate/src/tokens/ERC20.sol";	// @audit-issue

13:import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";	// @audit-issue

14:import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";	// @audit-issue

15:import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";	// @audit-issue
```
[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L11-L11), [12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L13-L13), [14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L14-L14), [15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L15-L15), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

10:import {ERC20} from "@solmate/src/tokens/ERC20.sol";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L10-L10), 


```solidity
Path: ./src/core/KerosineManager.sol

4:import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";	// @audit-issue

5:import {Owned}         from "@solmate/src/auth/Owned.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L4-L4), [5](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L5-L5), 


```solidity
Path: ./src/core/Vault.kerosine.sol

8:import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";	// @audit-issue

9:import {ERC20}           from "@solmate/src/tokens/ERC20.sol";	// @audit-issue

10:import {Owned}           from "@solmate/src/auth/Owned.sol";	// @audit-issue
```
[8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L10-L10), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

12:import {ERC20}           from "@solmate/src/tokens/ERC20.sol";	// @audit-issue

13:import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L12-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L13-L13), 


#### Recommendation

Regularly monitor and review the external protocols your Solidity contracts depend on for any updates or identified vulnerabilities. Consider implementing fallback mechanisms or contingency plans in your contracts to handle potential failures or compromises in these external protocols. Additionally, thoroughly audit and test the integration points with external protocols to ensure they adhere to your contract's security standards. Where possible, design your contract architecture to minimize reliance on external protocols or allow for upgradability in response to changes in these dependencies. Stay informed about developments in the protocols you depend on and actively participate in their community for early awareness of potential issues.

### Incorrect withdraw declaration
In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for `withdraw` should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.

```solidity
Path: ./src/core/VaultManagerV2.sol

134:  function withdraw(	// @audit-issue
```
[134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134-L134), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

32:  function withdraw(	// @audit-issue
```
[32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L32), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

30:  function withdraw(	// @audit-issue
```
[30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L30), 


#### Recommendation

Review the function declarations in your Solidity contracts, particularly for critical operations like `withdraw`, to ensure that they correctly specify return types. If a function is intended to indicate success or failure, it should explicitly declare a `bool` return type in its signature. For example, modify the `withdraw` function declaration from:
```solidity
function withdraw(uint256 amount) public {
    // Implementation
}

// to

function withdraw(uint256 amount) public returns (bool) {
    // Implementation
    return true; // Indicate success
}
```


### Bug in Deduplication of Verbatim Blocks
The current Solidity version has the [Bug in Deduplication of Verbatim Blocks](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/) issue.

```solidity
Path: ./src/staking/KerosineDenominator.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L2-L2), 


```solidity
Path: ./src/core/VaultManagerV2.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L2-L2), 


```solidity
Path: ./src/core/KerosineManager.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L2-L2), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

2:pragma solidity =0.8.17;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L2-L2), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/).

### Style Guide: Surround top level declarations in Solidity source with two blank lines.
1- Surround top level declarations in Solidity source with two blank lines.
2- Within a contract surround function declarations with a single blank line.


```solidity
Path: ./src/core/VaultManagerV2.sol

41:  }	// @audit-issue: There should be single blank line between function declarations.
42:  modifier isValidDNft(uint id) {

44:  }	// @audit-issue: There should be single blank line between function declarations.
45:  modifier isLicensed(address vault) {

64:  }
65:
66:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
67:  function add(

91:  }
92:
93:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
94:  function remove(

116:  }
117:
118:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
119:  function deposit(

131:  }
132:
133:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
134:  function withdraw(

153:  }
154:
155:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
156:  function mintDyad(

169:  }
170:
171:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
172:  function burnDyad(

181:  }
182:
183:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
184:  function redeemDyad(

202:  }
203:
204:  /// @inheritdoc IVaultManager	// @audit-issue: There should be single blank line between function declarations.
205:  function liquidate(

286:  }
287:
288:  // ----------------- MISC ----------------- //
289:	// @audit-issue: There should be single blank line between function declarations.
290:  function getVaults(
```
[41](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L41-L42), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L44-L45), [66](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L64-L67), [93](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L91-L94), [118](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L116-L119), [133](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L131-L134), [155](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L153-L156), [171](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L169-L172), [183](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L181-L184), [204](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L202-L205), [289](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L286-L290), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/latest/style-guide.html#blank-lines).

### Immutable redefined elsewhere
Consider defining in only one contract so that values cannot become out of sync when only one location is updated.

```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

18:  Dyad                 public immutable dyad;	// @audit-issue seen in: ./src/core/VaultManagerV2.sol
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L18-L18), 


#### Recommendation

To avoid immutable values being redefined in multiple locations, consider defining immutables in a single contract.

### Contract should expose an `interface`
All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.


```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Consider defining an `interface` that includes all `external`/`public` functions of the contract. Exposing a well-defined interface helps ensure that the entire API is extracted and provides a clear and standardized way for other contracts or users to interact with your contract.

### Consider using named returns
Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

```solidity
Path: ./src/staking/KerosineDenominator.sol

17:  function denominator() external view returns (uint) {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17-L17), 


```solidity
Path: ./src/core/VaultManagerV2.sol

184:  function redeemDyad(
185:    uint    id,
186:    address vault,
187:    uint    amount,
188:    address to
189:  )
190:    external 
191:      isDNftOwner(id)
192:    returns (uint) { 	// @audit-issue

230:  function collatRatio(
231:    uint id
232:  )
233:    public 
234:    view
235:    returns (uint) {	// @audit-issue

241:  function getTotalUsdValue(
242:    uint id
243:  ) 
244:    public 
245:    view
246:    returns (uint) {	// @audit-issue

250:  function getNonKeroseneValue(
251:    uint id
252:  ) 
253:    public 
254:    view
255:    returns (uint) {	// @audit-issue

269:  function getKeroseneValue(
270:    uint id
271:  ) 
272:    public 
273:    view
274:    returns (uint) {	// @audit-issue

290:  function getVaults(
291:    uint id
292:  ) 
293:    external 
294:    view 
295:    returns (address[] memory) {	// @audit-issue

299:  function hasVault(
300:    uint    id,
301:    address vault
302:  ) 
303:    external 
304:    view 
305:    returns (bool) {	// @audit-issue
```
[192](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184-L192), [235](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230-L235), [246](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241-L246), [255](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250-L255), [274](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269-L274), [295](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290-L295), [305](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299-L305), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

44:  function assetPrice() 
45:    public 
46:    view 
47:    override
48:    returns (uint) {	// @audit-issue
```
[48](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L48), 


```solidity
Path: ./src/core/KerosineManager.sol

37:  function getVaults() 
38:    external 
39:    view 
40:    returns (address[] memory) {	// @audit-issue

44:  function isLicensed(
45:    address vault
46:  ) 
47:    external 
48:    view 
49:    returns (bool) {	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37-L40), [49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44-L49), 


```solidity
Path: ./src/core/Vault.kerosine.sol

60:  function getUsdValue(
61:    uint id
62:  )
63:    public
64:    view 
65:    returns (uint) {	// @audit-issue

69:  function assetPrice() 
70:    public 
71:    view 
72:    virtual
73:    returns (uint); 	// @audit-issue
```
[65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L65), [73](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69-L73), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

50:  function assetPrice() 
51:    public 
52:    view 
53:    override
54:    returns (uint) {	// @audit-issue
```
[54](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L54), 


#### Recommendation

Adopt named returns in your Solidity functions, especially in cases where functions contain a single return statement. This approach enhances code readability and documentation by making the return values clear and explicit. When defining your function, specify the return types with names, and manipulate these named variables directly within your function logic. Additionally, leverage named returns to streamline your NatSpec documentation, providing clear descriptions for each return variable. Evaluate your current contracts for opportunities to refactor functions to use named returns, prioritizing those with simple return patterns for immediate benefits in gas efficiency and code clarity.

### Inefficient Array Usage
Use mappings instead of arrays for managing lists of data in order to conserve gas. Mappings are less expensive and more efficient for accessing any value without having to iterate through an array.

```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

56:      address[] memory vaults = kerosineManager.getVaults();	// @audit-issue
```
[56](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L56-L56), 


#### Recommendation

In scenarios where data access efficiency is critical, prefer using mappings over arrays in Solidity contracts. Mappings offer more efficient and gas-effective data retrieval and updates, especially when dealing with large or frequently accessed datasets. Ensure to structure your data and choose keys thoughtfully to maximize the efficiency gains offered by mappings. While arrays might be suitable for ordered data or when the entire dataset needs to be iterated, for most other use cases, mappings are likely to be the more gas-efficient choice.

### Complex math should be split into multiple steps
Consider splitting long arithmetic calculations (more than 4 operations) into multiple steps to improve the code readability.

```solidity
Path: ./src/core/VaultManagerV2.sol

146:    uint value = amount * _vault.assetPrice() 	// @audit-issue
147:                  * 1e18 
148:                  / 10**_vault.oracle().decimals() 
149:                  / 10**_vault.asset().decimals();

195:      uint asset = amount 	// @audit-issue
196:                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                    / _vault.assetPrice() 
198:                    / 1e18;
```
[146](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L146-L149), [195](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L195-L198), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

60:        tvl += vault.asset().balanceOf(address(vault)) 	// @audit-issue
61:                * vault.assetPrice() * 1e18
62:                / (10**vault.asset().decimals()) 
63:                / (10**vault.oracle().decimals());
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L60-L63), 


#### Recommendation

To enhance code readability and maintainability, it's advisable to break down complex arithmetic calculations into multiple steps. This not only makes the code more understandable but also helps in debugging and verifying the correctness of calculations.

### Unnecessary Use of override Keyword
In Solidity version 0.8.8 and later, the use of the override keyword becomes superfluous when a function is overriding solely from an interface and the function isn't present in multiple base contracts. Previously, the override keyword was required as an explicit indication to the compiler. However, this is no longer the case, and the extraneous use of the keyword can make the code less clean and more verbose.
Solidity documentation on [Function Overriding](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding).


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

44:  function assetPrice() 	// @audit-issue
45:    public 
46:    view 
47:    override
48:    returns (uint) {
```
[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L48), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

50:  function assetPrice() 	// @audit-issue
51:    public 
52:    view 
53:    override
54:    returns (uint) {
```
[50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L54), 


#### Recommendation

In Solidity versions 0.8.8 and later, the `override` keyword is no longer required for functions that are solely overriding from an interface and not present in multiple base contracts. Removing the unnecessary `override` keyword can make the code cleaner and less verbose.

### Use a single file for all system-wide constants
System-wide constants should be declared in a single file for better maintainability and readability. This contract seems to contain constants which could potentially be system-wide and could be better managed if they were centralized in a single location.

```solidity
Path: ./src/core/VaultManagerV2.sol

22:  uint public constant MAX_VAULTS          = 5;	// @audit-issue

23:  uint public constant MAX_VAULTS_KEROSENE = 5;	// @audit-issue

25:  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%	// @audit-issue

26:  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L26-L26), 


```solidity
Path: ./src/core/KerosineManager.sol

14:  uint public constant MAX_VAULTS = 10;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L14-L14), 


#### Recommendation

Consider centralizing system-wide constants in a single file for better maintainability and readability. This practice makes it easier to manage and update constants across the contract and promotes consistency in your codebase.

### Include sender information in events
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

```solidity
Path: ./src/core/VaultManagerV2.sol

77:    emit Added(id, vault);	// @audit-issue

90:    emit Added(id, vault);	// @audit-issue

103:    emit Removed(id, vault);	// @audit-issue

115:    emit Removed(id, vault);	// @audit-issue

168:    emit MintDyad(id, amount, to);	// @audit-issue

200:      emit RedeemDyad(id, vault, amount, to);	// @audit-issue
```
[77](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L77-L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L90-L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L103-L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L115-L115), [168](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L168-L168), [200](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L200-L200), 


```solidity
Path: ./src/core/Vault.kerosine.sol

44:    emit Deposit(id, amount);	// @audit-issue

57:    emit Move(from, to, amount);	// @audit-issue
```
[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L44-L44), [57](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L57-L57), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

40:    emit Withdraw(id, to, amount);	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L40-L40), 


#### Recommendation

To improve the usability and analysis of your smart contract events, consider including the `msg.sender` address as part of the event data. This enables easier filtering and identification of the sender's actions within your contract, providing valuable insights for users and external tools.

### Avoid external calls in modifiers
It is unusual to have external calls in modifiers, and doing so will make reviewers more likely to miss important external interactions. Consider moving the external call to an internal function, and calling that function from the modifier.

```solidity
Path: ./src/core/VaultManagerV2.sol

40:    if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;	// @audit-issue

43:    if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;	// @audit-issue

46:    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L46-L46), 


#### Recommendation

Refrain from incorporating external calls directly within modifiers. Instead, encapsulate the external call within an internal function and invoke this function from within the body of the functions that use the modifier. This approach enhances code readability and security, making it easier for reviewers and auditors to track external interactions. Additionally, it centralizes external calls, simplifying the management and review of these potentially risky operations. Always ensure external calls are handled with care, implementing checks, balances, and reentrancy guards as necessary to protect your contract from malicious actors and unintended consequences.

### Control structures do not follow the Solidity Style Guide
Refer to the [Solidity style guide - Control Structures](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#control-structures).

```solidity
Path: ./src/core/VaultManagerV2.sol

59:  function setKeroseneManager(KerosineManager _keroseneManager) 	// @audit-issue

67:  function add(
68:      uint    id,
69:      address vault
70:  ) 	// @audit-issue

80:  function addKerosene(
81:      uint    id,
82:      address vault
83:  ) 	// @audit-issue

94:  function remove(
95:      uint    id,
96:      address vault
97:  ) 	// @audit-issue

106:  function removeKerosene(
107:      uint    id,
108:      address vault
109:  ) 	// @audit-issue

119:  function deposit(
120:    uint    id,
121:    address vault,
122:    uint    amount
123:  ) 	// @audit-issue

134:  function withdraw(
135:    uint    id,
136:    address vault,
137:    uint    amount,
138:    address to
139:  ) 	// @audit-issue

156:  function mintDyad(
157:    uint    id,
158:    uint    amount,
159:    address to
160:  )	// @audit-issue

172:  function burnDyad(
173:    uint id,
174:    uint amount
175:  ) 	// @audit-issue

205:  function liquidate(
206:    uint id,
207:    uint to
208:  ) 	// @audit-issue
```
[59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59-L59), [70](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67-L70), [83](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80-L83), [97](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94-L97), [109](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106-L109), [123](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119-L123), [139](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134-L139), [160](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156-L160), [175](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172-L175), [208](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205-L208), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

23:  function setUnboundedKerosineVault(
24:    UnboundedKerosineVault _unboundedKerosineVault
25:  )	// @audit-issue

32:  function withdraw(
33:    uint    id,
34:    address to,
35:    uint    amount
36:  ) 	// @audit-issue
```
[25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23-L25), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L36), 


```solidity
Path: ./src/core/KerosineManager.sol

18:  function add(
19:    address vault
20:  ) 	// @audit-issue

28:  function remove(
29:    address vault
30:  ) 	// @audit-issue
```
[20](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18-L20), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28-L30), 


```solidity
Path: ./src/core/Vault.kerosine.sol

36:  function deposit(
37:    uint id,
38:    uint amount
39:  )	// @audit-issue

47:  function move(
48:    uint from,
49:    uint to,
50:    uint amount
51:  )	// @audit-issue
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L39), [51](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47-L51), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

30:  function withdraw(
31:    uint    id,
32:    address to,
33:    uint    amount
34:  ) 	// @audit-issue

43:  function setDenominator(KerosineDenominator _kerosineDenominator) 	// @audit-issue
```
[34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L34), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43-L43), 


#### Recommendation

Adhere to the Solidity style guide regarding control structures by avoiding the definition of multiple functions with identical names in a contract. Unique and descriptive function names improve code clarity and prevent potential confusion or errors. Consult [Solidity style guide - Control Structures](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#control-structures) for best practices.

### Consider making contracts `Upgradeable`
This allows for bugs to be fixed in production, at the expense of significantly increasing centralization.

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Assess the need for upgradeability in your Solidity contracts based on the project's requirements and lifecycle. If chosen, implement a well-known proxy pattern ensuring rigorous security and governance mechanisms are in place. Be aware of the increased centralization and plan accordingly to mitigate potential risks, such as through decentralized governance models or multi-sig control for upgrade decisions.

### Variable names for `immutable`s should use CONSTANT_CASE
For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)

```solidity
Path: ./src/core/VaultManagerV2.sol

28:  DNft     public immutable dNft;	// @audit-issue name should be: D_NFT

29:  Dyad     public immutable dyad;	// @audit-issue name should be: DYAD

30:  Licenser public immutable vaultLicenser;	// @audit-issue name should be: VAULT_LICENSER
```
[28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L28-L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L29-L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L30-L30), 


```solidity
Path: ./src/core/Vault.kerosine.sol

15:  IVaultManager   public immutable vaultManager;	// @audit-issue name should be: VAULT_MANAGER

16:  ERC20           public immutable asset;	// @audit-issue name should be: ASSET

17:  KerosineManager public immutable kerosineManager;	// @audit-issue name should be: KEROSINE_MANAGER
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L15-L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L16-L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

18:  Dyad                 public immutable dyad;	// @audit-issue name should be: DYAD
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L18-L18), 


#### Recommendation

When naming `immutable` variables, follow the CONSTANT_CASE convention, which means using all capital letters with underscores to separate words. This naming convention improves code readability and aligns with best practices for naming constants.

### Revert statements within external and public functions can be used to perform DOS attacks
In Solidity, `revert` statements are used to undo changes and throw an exception when certain conditions are not met. However, in public and external functions, improper use of `revert` can be exploited for Denial of Service (DoS) attacks. An attacker can intentionally trigger these `revert' conditions, causing legitimate transactions to consistently fail. For example, if a function relies on specific conditions from user input or contract state, an attacker could manipulate these to continually force `revert`s, blocking the function's execution. Therefore, it's crucial to design contract logic to handle exceptions properly and avoid scenarios where `revert` can be predictably triggered by malicious actors. This includes careful input validation and considering alternative design patterns that are less susceptible to such abuses.

```solidity
Path: ./src/core/VaultManagerV2.sol

74:    if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();	// @audit-issue

75:    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();	// @audit-issue

76:    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();	// @audit-issue

87:    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();	// @audit-issue

88:    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();	// @audit-issue

89:    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();	// @audit-issue

101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();	// @audit-issue

102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();	// @audit-issue

113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();	// @audit-issue

114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();	// @audit-issue

143:    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();	// @audit-issue

150:    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();	// @audit-issue

152:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 	// @audit-issue

165:    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();	// @audit-issue

167:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 	// @audit-issue

214:      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();	// @audit-issue
```
[74](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L114-L114), [143](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L143-L143), [150](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L214-L214), 


#### Recommendation

Design your Solidity contract's public and external functions with care to mitigate the risk of DoS attacks via `revert` statements. Implement robust input validation to ensure inputs are within expected bounds and conditions. Consider alternative logic or design patterns that reduce the reliance on `revert` for critical operations, particularly those that can be influenced externally. Evaluate the use of modifiers, try-catch blocks, or state checks that allow for safer handling of conditions and exceptions. Ensure that your contract's critical functionality remains accessible and resilient against potential abuse of `revert` behavior by malicious actors.

### Consider adding emergency-stop functionality
In the event of a security breach or any unforeseen emergency, swiftly suspending all protocol operations becomes crucial. Having a mechanism in place to halt all functions collectively, instead of pausing individual contracts separately, substantially enhances the efficiency of mitigating ongoing attacks or vulnerabilities. This not only quickens the response time to potential threats but also reduces operational stress during these critical periods. Therefore, consider integrating a 'circuit breaker' or 'emergency stop' function into the smart contract system architecture. Such a feature would provide the capability to suspend the entire protocol instantly, which could prove invaluable during a time-sensitive crisis management situation.

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Implement an emergency-stop feature in your Solidity contract system to enhance security and crisis response capabilities. This can be achieved through a 'circuit breaker' pattern, where a central switch or set of conditions can instantly suspend critical operations across the contract ecosystem. Ensure that this mechanism is accessible to authorized parties only, such as contract administrators or a decentralized governance system. Design the emergency-stop functionality to be transparent and auditable, with clear conditions and processes for activation and deactivation. Regularly test and audit this feature to ensure its reliability and effectiveness in potential emergency situations.

### For extended 'using-for' usage, use the latest pragma version
Solidity versions of 0.8.13 or above can make use of enhanced using-for notation within contracts.

```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Update your Solidity contracts to use the latest pragma version, ideally 0.8.13 or higher, to leverage the enhanced 'using-for' notation. This upgrade will enable you to apply library functions to user-defined types more effectively, enhancing the functionality and readability of your contracts. Make sure to thoroughly test your contracts after upgrading to ensure compatibility and to take full advantage of the latest Solidity features and improvements. Regularly keep your contracts updated with the latest Solidity versions to stay aligned with the evolving capabilities and best practices of the language.

### Consider only defining one library/interface/contract per sol file
Combining multiple libraries, interfaces, or contracts in a single .sol file can lead to clutter, reduced readability, and versioning issues. Resolution: Adopt the best practice of defining only one library, interface, or contract per Solidity file. This modular approach enhances clarity, simplifies unit testing, and streamlines code review. Furthermore, segregating components makes version management easier, as updates to one component won't necessitate changes to a file housing multiple unrelated components. Structured file management can further assist in avoiding naming collisions and ensure smoother integration into larger systems or DApps.

```solidity
Path: ./src/staking/KerosineDenominator.sol

4:import {Parameters} from "../params/Parameters.sol";	// @audit-issue
5:import {Kerosine} from "../staking/Kerosine.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L4-L5), 


```solidity
Path: ./src/core/VaultManagerV2.sol

4:import {DNft}            from "./DNft.sol";	// @audit-issue
5:import {Dyad}            from "./Dyad.sol";
6:import {Licenser}        from "./Licenser.sol";
7:import {Vault}           from "./Vault.sol";
8:import {IVaultManager}   from "../interfaces/IVaultManager.sol";
9:import {KerosineManager} from "../../src/core/KerosineManager.sol";
10:
11:import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
12:import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
13:import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
14:import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
15:import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L4-L15), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

4:import {KerosineVault}          from "./Vault.kerosine.sol";	// @audit-issue
5:import {IVaultManager}          from "../interfaces/IVaultManager.sol";
6:import {Dyad}                   from "./Dyad.sol";
7:import {KerosineManager}        from "./KerosineManager.sol";
8:import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";
9:
10:import {ERC20} from "@solmate/src/tokens/ERC20.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L4-L10), 


```solidity
Path: ./src/core/KerosineManager.sol

4:import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";	// @audit-issue
5:import {Owned}         from "@solmate/src/auth/Owned.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L4-L5), 


```solidity
Path: ./src/core/Vault.kerosine.sol

4:import {IVaultManager}   from "../interfaces/IVaultManager.sol";	// @audit-issue
5:import {KerosineManager} from "./KerosineManager.sol";
6:import {IVault}          from "../interfaces/IVault.sol";
7:
8:import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
9:import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
10:import {Owned}           from "@solmate/src/auth/Owned.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L4-L10), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

4:import {KerosineVault}        from "./Vault.kerosine.sol";	// @audit-issue
5:import {IVaultManager}        from "../interfaces/IVaultManager.sol";
6:import {Vault}                from "./Vault.sol";
7:import {Dyad}                 from "./Dyad.sol";
8:import {KerosineManager}      from "./KerosineManager.sol";
9:import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
10:import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
11:
12:import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
13:import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
```
[4](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L4-L13), 


#### Recommendation

Adopt a modular file structure in your Solidity projects by defining only one library, interface, or contract per file. This approach significantly enhances the clarity and readability of your code, making it easier to manage, test, and review. It also simplifies version control, as updates to individual components are isolated to their respective files, reducing the risk of unintended side effects. Organize your project directory to reflect this structure, with a clear naming convention that matches file names to their contained contracts, libraries, or interfaces. This organization not only prevents naming collisions but also facilitates smoother integration into larger systems or decentralized applications (DApps).

### Reduce deployment costs by tweaking contracts' metadata
When solidity generates the bytecode for the smart contract to be deployed, it appends metadata about the compilation at the end of the bytecode.
By default, the solidity compiler appends metadata at the end of the “actual” initcode, which gets stored to the blockchain when the constructor finishes executing.
Consider tweaking the metadata to avoid this unnecessary allocation. A full guide can be found [here](https://www.rareskills.io/post/solidity-metadata).
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

See [this](https://www.rareskills.io/post/solidity-metadata) link, at its bottom, for full details

### All verbatim blocks are considered identical by deduplicator and can incorrectly be unified
The Solidity Team reported a bug on October 24, 2023, affecting Yul code using the verbatim builtin, specifically in the Block Deduplicator optimizer step. This bug, present since Solidity version 0.8.5, caused incorrect deduplication of verbatim assembly items surrounded by identical opcodes, considering them identical regardless of their data. The bug was confined to pure Yul compilation with optimization enabled and was unlikely to be exploited as an attack vector. The conditions triggering the bug were very specific, and its occurrence was deemed to have a low likelihood. The bug was rated with an overall low score due to these factors.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Review and assess any Solidity contracts, especially those involving Yul code, that may be impacted by this deduplication bug. If your contracts rely on the Block Deduplicator optimizer and use verbatim blocks in a way that could be affected by this issue, consider updating your Solidity version to one where this bug is fixed, or adjust your contract to avoid this specific scenario. Stay informed about updates from the Solidity Team regarding this and similar issues, and regularly update your Solidity compiler to the latest version to benefit from bug fixes and optimizations. Given the specific and limited nature of this bug, its impact may be minimal, but caution is advised for contracts with complex assembly code or those heavily reliant on optimizer behaviors.

### Consider adding formal verification proofs
Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Consider integrating formal verification into your Solidity contract development process. This can be done by defining formal specifications and properties that your contract should adhere to and using mathematical methods to verify these aspects. Tools and platforms like Certora Prover, Scribble, or OpenZeppelin's test environment can assist in this process. Formal verification should complement traditional testing and auditing methods, offering an additional layer of security assurance. Keep in mind that formal verification requires a thorough understanding of mathematical logic and contract specifications, so it may necessitate additional resources or expertise. Nevertheless, the investment in formal verification can significantly enhance the trustworthiness and robustness of your smart contracts.

### Contracts should have full test coverage
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Consider writing test cases.

### Large or complicated code bases should implement invariant tests
This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts. Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Consider writing invariant test cases.

### Consider adding formal verification proofs
Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L1), 


#### Recommendation

Consider using formal verification.

### NatSpec: Whitespace in Expressions
See the [Whitespace in Expressions](https://docs.soliditylang.org/en/latest/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide.


```solidity
Path: ./src/core/VaultManagerV2.sol

217:      uint cappedCr               = cr < 1e18 ? 1e18 : cr;	// @audit-issue: Variable declaration should be like `uint256 x = 3`

219:      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);	// @audit-issue: Variable declaration should be like `uint256 x = 3`

223:          Vault vault      = Vault(vaults[id].at(i));	// @audit-issue: Variable declaration should be like `uint256 x = 3`
```
[217](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L217-L217), [219](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L219-L219), [223](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L223-L223), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

65:      uint numerator   = tvl - dyad.totalSupply();	// @audit-issue: Variable declaration should be like `uint256 x = 3`
```
[65](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L65-L65), 


#### Recommendation

Review and align your Solidity code with the whitespace guidelines provided in the Solidity Style Guide, particularly for expressions. Ensure consistent spacing around operators and commas, and adopt a uniform style for indentation and line breaks in complex expressions. This alignment not only enhances the readability of your code but also promotes a standardized coding style that aligns with community best practices. Utilize linters or automated code formatting tools, where possible, to enforce these whitespace guidelines consistently across your codebase.

### NatSpec: Body of `if` statement should be placed on a new line
According to the [Solidity style guide](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures), `if` statements whose body contains a single line should look like this: solidity `if (x < 10)     x += 1; `

```solidity
Path: ./src/core/VaultManagerV2.sol

40:    if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;	// @audit-issue

43:    if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;	// @audit-issue

46:    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;	// @audit-issue

74:    if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();	// @audit-issue

75:    if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();	// @audit-issue

76:    if (!vaults[id].add(vault))            revert VaultAlreadyAdded();	// @audit-issue

87:    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();	// @audit-issue

88:    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();	// @audit-issue

89:    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();	// @audit-issue

101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();	// @audit-issue

102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();	// @audit-issue

113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();	// @audit-issue

114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();	// @audit-issue

143:    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();	// @audit-issue

150:    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();	// @audit-issue

152:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 	// @audit-issue

165:    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();	// @audit-issue

167:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 	// @audit-issue

214:      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();	// @audit-issue

237:      if (_dyad == 0) return type(uint).max;	// @audit-issue
```
[40](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L40-L40), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L43-L43), [46](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L46-L46), [74](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L74-L74), [75](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L75-L75), [76](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L76-L76), [87](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L87-L87), [88](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L88-L88), [89](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L89-L89), [101](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L101-L101), [102](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L102-L102), [113](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L113-L113), [114](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L114-L114), [143](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L143-L143), [150](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L167-L167), [214](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L214-L214), [237](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L237-L237), 


```solidity
Path: ./src/core/KerosineManager.sol

24:    if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();	// @audit-issue

25:    if (!vaults.add(vault))            revert VaultAlreadyAdded();	// @audit-issue

34:    if (!vaults.remove(vault)) revert VaultNotFound();	// @audit-issue
```
[24](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L24-L24), [25](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L25-L25), [34](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L34-L34), 


```solidity
Path: ./src/core/Vault.kerosine.sol

22:    if (msg.sender != address(vaultManager)) revert NotVaultManager();	// @audit-issue
```
[22](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L22-L22), 


#### Recommendation

Adhere to the Solidity style guide by formatting single-line `if` statements with the body on the same line as the condition. For example, use `if (x < 10) x += 1;` for concise and clear code. This style of formatting enhances readability and maintains consistency with Solidity's recommended best practices. It's particularly effective for simple and short conditional operations within the contract's code.

### Invalid NatSpec comment style
NatSpec must begin with `///`, or use the `/** ... */` syntax. The compiler doesn't count `//` or `/* ... */` as NatSpec

```solidity
Path: ./src/staking/KerosineDenominator.sol

18:    // @dev: We subtract all the Kerosene in the multi-sig.	// @audit-issue
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L18-L18), 


#### Recommendation

Ensure that all NatSpec comments in your Solidity contracts adhere to the correct syntax: use `///` for single-line comments and `/** ... */` for multi-line comments. Review and update your existing comments to align with these guidelines. Avoid using regular comment syntax `//` or `/* ... */` for NatSpec documentation, as these will not be recognized by the compiler for generating automated documentation. Correctly formatted NatSpec comments improve the readability of your code and are essential for generating clear and useful documentation for users and developers interacting with your contract interfaces.

### NatSpec: Contract declarations should have `@author` tag
In the world of decentralized code, giving credit is key. NatSpec's `@author` tag acknowledges the minds behind the code. It appears this Solidity contract omits the `@author` directive in its NatSpec annotations. Properly attributing code to its contributors not only recognizes effort but also aids in establishing trust and credibility. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue missing `@author` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue missing `@author` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue missing `@author` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue missing `@author` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue missing `@author` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue missing `@author` tag
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@dev` tag
NatSpec comments are a critical part of Solidity's documentation system, designed to help developers and others understand the behavior and purpose of a contract. The `@dev` tag, in particular, provides context and insight into the contract's development considerations. A missing `@dev` comment can lead to misunderstandings about the contract, making it harder for others to contribute to or use the contract effectively. Therefore, it's highly recommended to include `@dev` comments in the documentation to enhance code readability and maintainability. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue missing `@dev` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue missing `@dev` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue missing `@dev` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue missing `@dev` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue missing `@dev` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue missing `@dev` tag
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@notice` tag
The `@notice` is used to explain to users what the contract does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue missing `@notice` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue missing `@notice` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue missing `@notice` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue missing `@notice` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue missing `@notice` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue missing `@notice` tag
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@title` tag
The `@title` is used to explain to users what the contract does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

```solidity
Path: ./src/staking/KerosineDenominator.sol

7:contract KerosineDenominator is Parameters {	// @audit-issue missing `@title` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L7-L7), 


```solidity
Path: ./src/core/VaultManagerV2.sol

17:contract VaultManagerV2 is IVaultManager, Initializable {	// @audit-issue missing `@title` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L17-L17), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

12:contract BoundedKerosineVault is KerosineVault {	// @audit-issue missing `@title` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L12-L12), 


```solidity
Path: ./src/core/KerosineManager.sol

7:contract KerosineManager is Owned(msg.sender) {	// @audit-issue missing `@title` tag
```
[7](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L7-L7), 


```solidity
Path: ./src/core/Vault.kerosine.sol

12:abstract contract KerosineVault is IVault, Owned(msg.sender) {	// @audit-issue missing `@title` tag
```
[12](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L12-L12), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

15:contract UnboundedKerosineVault is KerosineVault {	// @audit-issue missing `@title` tag
```
[15](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L15-L15), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Use `@inheritdoc` for overriden functions.
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

44:  function assetPrice() 	// @audit-issue missing `@inheritdoc` tag
```
[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L44), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

50:  function assetPrice() 	// @audit-issue missing `@inheritdoc` tag
```
[50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L50), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function `@return` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including `@return` tag will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/staking/KerosineDenominator.sol

17:  function denominator() external view returns (uint) {	// @audit-issue missing `@return` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17-L17), 


```solidity
Path: ./src/core/VaultManagerV2.sol

184:  function redeemDyad(	// @audit-issue missing `@return` tag

230:  function collatRatio(	// @audit-issue missing `@return` tag

241:  function getTotalUsdValue(	// @audit-issue missing `@return` tag

250:  function getNonKeroseneValue(	// @audit-issue missing `@return` tag

269:  function getKeroseneValue(	// @audit-issue missing `@return` tag

290:  function getVaults(	// @audit-issue missing `@return` tag

299:  function hasVault(	// @audit-issue missing `@return` tag
```
[184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184-L184), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230-L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241-L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250-L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269-L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290-L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299-L299), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

44:  function assetPrice() 	// @audit-issue missing `@return` tag
```
[44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L44), 


```solidity
Path: ./src/core/KerosineManager.sol

37:  function getVaults() 	// @audit-issue missing `@return` tag

44:  function isLicensed(	// @audit-issue missing `@return` tag
```
[37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37-L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44-L44), 


```solidity
Path: ./src/core/Vault.kerosine.sol

60:  function getUsdValue(	// @audit-issue missing `@return` tag

69:  function assetPrice() 	// @audit-issue missing `@return` tag
```
[60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69-L69), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

50:  function assetPrice() 	// @audit-issue missing `@return` tag
```
[50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L50), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function declarations should have `@notice` tag
The `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a function does. It appears that this contract's function declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a function's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/staking/KerosineDenominator.sol

11:  constructor(	// @audit-issue missing `@notice` tag

17:  function denominator() external view returns (uint) {	// @audit-issue missing `@notice` tag
```
[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11-L11), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17-L17), 


```solidity
Path: ./src/core/VaultManagerV2.sol

49:  constructor(	// @audit-issue missing `@notice` tag

59:  function setKeroseneManager(KerosineManager _keroseneManager) 	// @audit-issue missing `@notice` tag

67:  function add(	// @audit-issue missing `@notice` tag

80:  function addKerosene(	// @audit-issue missing `@notice` tag

94:  function remove(	// @audit-issue missing `@notice` tag

106:  function removeKerosene(	// @audit-issue missing `@notice` tag

119:  function deposit(	// @audit-issue missing `@notice` tag

134:  function withdraw(	// @audit-issue missing `@notice` tag

156:  function mintDyad(	// @audit-issue missing `@notice` tag

172:  function burnDyad(	// @audit-issue missing `@notice` tag

184:  function redeemDyad(	// @audit-issue missing `@notice` tag

205:  function liquidate(	// @audit-issue missing `@notice` tag

230:  function collatRatio(	// @audit-issue missing `@notice` tag

241:  function getTotalUsdValue(	// @audit-issue missing `@notice` tag

250:  function getNonKeroseneValue(	// @audit-issue missing `@notice` tag

269:  function getKeroseneValue(	// @audit-issue missing `@notice` tag

290:  function getVaults(	// @audit-issue missing `@notice` tag

299:  function hasVault(	// @audit-issue missing `@notice` tag
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49-L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59-L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67-L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80-L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94-L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106-L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119-L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134-L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156-L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172-L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184-L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205-L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230-L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241-L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250-L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269-L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290-L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299-L299), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

17:  constructor(	// @audit-issue missing `@notice` tag

23:  function setUnboundedKerosineVault(	// @audit-issue missing `@notice` tag

32:  function withdraw(	// @audit-issue missing `@notice` tag

44:  function assetPrice() 	// @audit-issue missing `@notice` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17-L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23-L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L44), 


```solidity
Path: ./src/core/KerosineManager.sol

18:  function add(	// @audit-issue missing `@notice` tag

28:  function remove(	// @audit-issue missing `@notice` tag

37:  function getVaults() 	// @audit-issue missing `@notice` tag

44:  function isLicensed(	// @audit-issue missing `@notice` tag
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18-L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28-L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37-L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44-L44), 


```solidity
Path: ./src/core/Vault.kerosine.sol

26:  constructor(	// @audit-issue missing `@notice` tag

36:  function deposit(	// @audit-issue missing `@notice` tag

47:  function move(	// @audit-issue missing `@notice` tag

60:  function getUsdValue(	// @audit-issue missing `@notice` tag

69:  function assetPrice() 	// @audit-issue missing `@notice` tag
```
[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26-L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47-L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69-L69), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

21:  constructor(	// @audit-issue missing `@notice` tag

30:  function withdraw(	// @audit-issue missing `@notice` tag

43:  function setDenominator(KerosineDenominator _kerosineDenominator) 	// @audit-issue missing `@notice` tag

50:  function assetPrice() 	// @audit-issue missing `@notice` tag
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21-L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43-L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L50), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function declarations should have `@dev` tag
Some functions have an incomplete NatSpec: add a `@dev` notation to describe the function to improve the code documentation.

```solidity
Path: ./src/staking/KerosineDenominator.sol

11:  constructor(	// @audit-issue missing `@dev` tag

17:  function denominator() external view returns (uint) {	// @audit-issue missing `@dev` tag
```
[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11-L11), [17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L17-L17), 


```solidity
Path: ./src/core/VaultManagerV2.sol

49:  constructor(	// @audit-issue missing `@dev` tag

59:  function setKeroseneManager(KerosineManager _keroseneManager) 	// @audit-issue missing `@dev` tag

67:  function add(	// @audit-issue missing `@dev` tag

80:  function addKerosene(	// @audit-issue missing `@dev` tag

94:  function remove(	// @audit-issue missing `@dev` tag

106:  function removeKerosene(	// @audit-issue missing `@dev` tag

119:  function deposit(	// @audit-issue missing `@dev` tag

134:  function withdraw(	// @audit-issue missing `@dev` tag

156:  function mintDyad(	// @audit-issue missing `@dev` tag

172:  function burnDyad(	// @audit-issue missing `@dev` tag

184:  function redeemDyad(	// @audit-issue missing `@dev` tag

205:  function liquidate(	// @audit-issue missing `@dev` tag

230:  function collatRatio(	// @audit-issue missing `@dev` tag

241:  function getTotalUsdValue(	// @audit-issue missing `@dev` tag

250:  function getNonKeroseneValue(	// @audit-issue missing `@dev` tag

269:  function getKeroseneValue(	// @audit-issue missing `@dev` tag

290:  function getVaults(	// @audit-issue missing `@dev` tag

299:  function hasVault(	// @audit-issue missing `@dev` tag
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49-L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59-L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67-L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80-L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94-L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106-L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119-L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134-L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156-L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172-L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184-L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205-L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230-L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241-L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250-L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269-L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290-L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299-L299), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

17:  constructor(	// @audit-issue missing `@dev` tag

23:  function setUnboundedKerosineVault(	// @audit-issue missing `@dev` tag

32:  function withdraw(	// @audit-issue missing `@dev` tag

44:  function assetPrice() 	// @audit-issue missing `@dev` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17-L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23-L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L44-L44), 


```solidity
Path: ./src/core/KerosineManager.sol

18:  function add(	// @audit-issue missing `@dev` tag

28:  function remove(	// @audit-issue missing `@dev` tag

37:  function getVaults() 	// @audit-issue missing `@dev` tag

44:  function isLicensed(	// @audit-issue missing `@dev` tag
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18-L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28-L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L37-L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44-L44), 


```solidity
Path: ./src/core/Vault.kerosine.sol

26:  constructor(	// @audit-issue missing `@dev` tag

36:  function deposit(	// @audit-issue missing `@dev` tag

47:  function move(	// @audit-issue missing `@dev` tag

60:  function getUsdValue(	// @audit-issue missing `@dev` tag

69:  function assetPrice() 	// @audit-issue missing `@dev` tag
```
[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26-L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47-L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L69-L69), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

21:  constructor(	// @audit-issue missing `@dev` tag

30:  function withdraw(	// @audit-issue missing `@dev` tag

43:  function setDenominator(KerosineDenominator _kerosineDenominator) 	// @audit-issue missing `@dev` tag

50:  function assetPrice() 	// @audit-issue missing `@dev` tag
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21-L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43-L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L50-L50), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function/Constructor `@param` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/staking/KerosineDenominator.sol

11:  constructor(	// @audit-issue missing `@param` tag
```
[11](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/staking/KerosineDenominator.sol#L11-L11), 


```solidity
Path: ./src/core/VaultManagerV2.sol

49:  constructor(	// @audit-issue missing `@param` tag

59:  function setKeroseneManager(KerosineManager _keroseneManager) 	// @audit-issue missing `@param` tag

67:  function add(	// @audit-issue missing `@param` tag

80:  function addKerosene(	// @audit-issue missing `@param` tag

94:  function remove(	// @audit-issue missing `@param` tag

106:  function removeKerosene(	// @audit-issue missing `@param` tag

119:  function deposit(	// @audit-issue missing `@param` tag

134:  function withdraw(	// @audit-issue missing `@param` tag

156:  function mintDyad(	// @audit-issue missing `@param` tag

172:  function burnDyad(	// @audit-issue missing `@param` tag

184:  function redeemDyad(	// @audit-issue missing `@param` tag

205:  function liquidate(	// @audit-issue missing `@param` tag

230:  function collatRatio(	// @audit-issue missing `@param` tag

241:  function getTotalUsdValue(	// @audit-issue missing `@param` tag

250:  function getNonKeroseneValue(	// @audit-issue missing `@param` tag

269:  function getKeroseneValue(	// @audit-issue missing `@param` tag

290:  function getVaults(	// @audit-issue missing `@param` tag

299:  function hasVault(	// @audit-issue missing `@param` tag
```
[49](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L49-L49), [59](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L59-L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L67-L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L80-L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L94-L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L106-L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L119-L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L134-L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L156-L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L172-L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L184-L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L205-L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L230-L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L241-L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L250-L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L269-L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L290-L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L299-L299), 


```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

17:  constructor(	// @audit-issue missing `@param` tag

23:  function setUnboundedKerosineVault(	// @audit-issue missing `@param` tag

32:  function withdraw(	// @audit-issue missing `@param` tag
```
[17](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L17-L17), [23](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L23-L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L32-L32), 


```solidity
Path: ./src/core/KerosineManager.sol

18:  function add(	// @audit-issue missing `@param` tag

28:  function remove(	// @audit-issue missing `@param` tag

44:  function isLicensed(	// @audit-issue missing `@param` tag
```
[18](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L18-L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L28-L28), [44](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L44-L44), 


```solidity
Path: ./src/core/Vault.kerosine.sol

26:  constructor(	// @audit-issue missing `@param` tag

36:  function deposit(	// @audit-issue missing `@param` tag

47:  function move(	// @audit-issue missing `@param` tag

60:  function getUsdValue(	// @audit-issue missing `@param` tag
```
[26](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L26-L26), [36](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L36-L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L47-L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L60-L60), 


```solidity
Path: ./src/core/Vault.kerosine.unbounded.sol

21:  constructor(	// @audit-issue missing `@param` tag

30:  function withdraw(	// @audit-issue missing `@param` tag

43:  function setDenominator(KerosineDenominator _kerosineDenominator) 	// @audit-issue missing `@param` tag
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L21-L21), [30](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L30-L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.unbounded.sol#L43-L43), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifier declarations should have `@notice` tag
In Solidity, the `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a modifier does. It appears that this contract's modifier declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a modifier's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/core/VaultManagerV2.sol

39:  modifier isDNftOwner(uint id) {	// @audit-issue missing `@notice` tag

42:  modifier isValidDNft(uint id) {	// @audit-issue missing `@notice` tag

45:  modifier isLicensed(address vault) {	// @audit-issue missing `@notice` tag
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42-L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45-L45), 


```solidity
Path: ./src/core/Vault.kerosine.sol

21:  modifier onlyVaultManager() {	// @audit-issue missing `@notice` tag
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21-L21), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifier declarations should have `@dev` tag
Some modifiers have an incomplete NatSpec: add a `@dev` notation to describe the modifier to improve the code documentation.

```solidity
Path: ./src/core/VaultManagerV2.sol

39:  modifier isDNftOwner(uint id) {	// @audit-issue missing `@dev` tag

42:  modifier isValidDNft(uint id) {	// @audit-issue missing `@dev` tag

45:  modifier isLicensed(address vault) {	// @audit-issue missing `@dev` tag
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42-L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45-L45), 


```solidity
Path: ./src/core/Vault.kerosine.sol

21:  modifier onlyVaultManager() {	// @audit-issue missing `@dev` tag
```
[21](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.sol#L21-L21), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifiers `@param` tag is missing
Function modifiers should include NatSpec comments with @param tags describing each input parameter. This promotes better code readability and documentation. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/core/VaultManagerV2.sol

39:  modifier isDNftOwner(uint id) {	// @audit-issue missing `@param` tag

42:  modifier isValidDNft(uint id) {	// @audit-issue missing `@param` tag

45:  modifier isLicensed(address vault) {	// @audit-issue missing `@param` tag
```
[39](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L39-L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L42-L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/VaultManagerV2.sol#L45-L45), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error declarations should have `@notice` tag
The `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a error does. It appears that this contract's modifier declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a error's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

13:  error NotWithdrawable(uint id, address to, uint amount);	// @audit-issue missing `@notice` tag
```
[13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L13-L13), 


```solidity
Path: ./src/core/KerosineManager.sol

8:  error TooManyVaults();	// @audit-issue missing `@notice` tag

9:  error VaultAlreadyAdded();	// @audit-issue missing `@notice` tag

10:  error VaultNotFound();	// @audit-issue missing `@notice` tag
```
[8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L10-L10), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error declarations should have `@dev` tag
Some errors have an incomplete NatSpec: add a `@dev` notation to describe the error to improve the code documentation.

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

13:  error NotWithdrawable(uint id, address to, uint amount);	// @audit-issue missing `@dev` tag
```
[13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L13-L13), 


```solidity
Path: ./src/core/KerosineManager.sol

8:  error TooManyVaults();	// @audit-issue missing `@dev` tag

9:  error VaultAlreadyAdded();	// @audit-issue missing `@dev` tag

10:  error VaultNotFound();	// @audit-issue missing `@dev` tag
```
[8](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L8-L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L9-L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/KerosineManager.sol#L10-L10), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error `@param` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of error arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/core/Vault.kerosine.bounded.sol

13:  error NotWithdrawable(uint id, address to, uint amount);	// @audit-issue missing `@param` tag
```
[13](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/./src/core/Vault.kerosine.bounded.sol#L13-L13), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).