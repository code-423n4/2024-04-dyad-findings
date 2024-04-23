## LightChaser-V3

### Generated for: Code4rena : Dyad

### Generated on: 2024-04-23

## Total findings: 51

### Total Medium findings: 2

### Total Low findings: 14

### Total Gas findings: 13

### Total NonCritical findings: 22

#### Note
Care has been taken to ensure findings already existant in the 4nalyzer report are non existant in this report unless instances not captured by 4nalyzer were found.

# Summary for Medium findings

| Number | Details | Instances |
|----------|----------|----------|
| [Medium-1] | Privileged functions can create points of failure | 2 |
| [Medium-2] | Withdraw on tokens which are payable but have no withdraw functionality | 1 |
# Summary for Low findings

| Number | Details | Instances |
|----------|----------|----------|
| [Low-1] | Incorrect comparison against a max value  | 3 |
| [Low-2] | Upgradable contracts should have a __gap variable | 1 |
| [Low-3] | Use _disableInitializers() to ensure initialization occurs once | 1 |
| [Low-4] | Loss of precision | 2 |
| [Low-5] | Critical functions should be a two step procedure | 2 |
| [Low-6] | Constant decimal values | 5 |
| [Low-7] | Revert on Transfer to the Zero Address | 1 |
| [Low-8] | Incorrect withdraw declaration | 3 |
| [Low-9] | Create methods are suspicious of the reorg attack | 1 |
| [Low-10] | Non constant/immutable state variables are missing a setter post deployment | 1 |
| [Low-11] | Constructors missing validation | 3 |
| [Low-12] | In production vm.log and it's counterparts should not be used | 2 |
| [Low-13] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 2 |
| [Low-14] | Loss of precision | 2 |
# Summary for NonCritical findings

| Number | Details | Instances |
|----------|----------|----------|
| [NonCritical-1] | Critical functions should have a timelock | 2 |
| [NonCritical-2] | SafeTransferLib does not ensure that the token contract exists | 2 |
| [NonCritical-3] | In functions which accept an address as a parameter, there should be a zero address check to prevent bugs | 14 |
| [NonCritical-4] | Avoid updating storage when the value hasn't changed | 2 |
| [NonCritical-5] | Old Solidity version | 1 |
| [NonCritical-6] | Contracts should have all public/external functions exposed by interfaces | 30 |
| [NonCritical-7] | Emits without msg.sender parameter | 1 |
| [NonCritical-8] | Remove forge-std import | 1 |
| [NonCritical-9] | Unused import | 1 |
| [NonCritical-10] | Events may be emitted out of order due to code not follow the best practice of check-effects-interaction | 3 |
| [NonCritical-11] | Don't only depend on Solidity's arithmetic ordering. | 1 |
| [NonCritical-12] | Contracts with only unimplemented functions can be labeled as abstract | 1 |
| [NonCritical-13] | A event should be emitted if a non immutable state variable is set in a constructor | 3 |
| [NonCritical-14] | There should not be more than one space before assignment | 12 |
| [NonCritical-15] | Mappings should not have a space before the parenthesis. | 3 |
| [NonCritical-16] | Avoid declaring variables with the names of defined functions within the project | 1 |
| [NonCritical-17] | Errors should have parameters | 6 |
| [NonCritical-18] | NatSpec: @notice tags missing from contract/abstract/library/interface/function/modifier/constructor/receive/fallback | 8 |
| [NonCritical-19] | Natspec @author is missing from contract/interface/library | 7 |
| [NonCritical-20] | Natspec @title is missing from contract/interface/library | 7 |
| [NonCritical-21] | NatSpec: @dev tags missing from contract/abstract/library/interface/function/modifier/constructor/receive/fallback | 8 |
| [NonCritical-22] | Incorrect NatSpec Syntax | 1 |
# Summary for Gas findings

| Number | Details | Instances | Gas |
|----------|----------|----------|----------|
| [Gas-1] | Using named returns for pure and view functions is cheaper than using regular returns | 12 | 3744 |
| [Gas-2] | Public functions not used internally can be marked as external to save gas | 1 | 0.0 |
| [Gas-3] | Use assembly to emit events | 9 | 3078 |
| [Gas-4] | Counting down in for statements is more gas efficient | 8 | 0.0 |
| [Gas-5] | Use assembly to validate msg.sender | 1 | 0.0 |
| [Gas-6] | Unnecessary casting as variable is already of the same type | 1 | 22 |
| [Gas-7] | Simple checks for zero uint can be done using assembly to save gas | 1 | 18 |
| [Gas-8] | Solidity versions 0.8.19 and above are more gas efficient | 1 | 1000 |
| [Gas-9] | Constructors can be marked as payable to save deployment gas | 5 | 0.0 |
| [Gas-10] | Use OZ Array.unsafeAccess() to avoid repeated array length checks | 1 | 52500 |
| [Gas-11] | Consider pre-calculating the address of address(this) to save gas | 4 | 0.0 |
| [Gas-12] | Public functions not called internally | 1 | 0.0 |
| [Gas-13] | Use constants instead of type(uint<n>).max | 1 | 0.0 |
## [Medium-1] Privileged functions can create points of failure

### Resolution 
Ensure such accounts are protected and consider implementing multi sig to prevent a single point of failure

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[47](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L47-L53)']
```solidity
47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager // <= FOUND
54:   
```
['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L36)']
```solidity
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager // <= FOUND
37:   
```


</details>

## [Medium-2] Withdraw on tokens which are payable but have no withdraw functionality

### Resolution 
Executing a `.withdraw` function on an externally determined contract can be risky. Even if the target contract is payable, it might not implement a withdraw function or might implement it differently than expected. If the contract doesn't have a withdraw function, a function call will lead to a transaction failure. Moreover, if the external contract has malevolent code in its `.withdraw` function, it could exploit your contract in unexpected ways. To mitigate this risk, ensure you interact only with trusted contracts, ideally those adhering to standard interfaces like ERC20's `transfer`. Avoid arbitrary calls to `.withdraw` without a clear understanding of the target contract's functionality.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[134](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L134-L134)']
```solidity
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
151:     _vault.withdraw(id, to, amount);
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
153:   }
```


</details>

## [Low-1] Incorrect comparison against a max value 

### Resolution 
Comparing a value using `>= MAX_VALUE` is conceptually incorrect when `MAX_VALUE` is defined as the upper limit that a variable can take. According to the definition of a maximum value, the condition should only revert if the variable is greater than `MAX_VALUE`, not equal to it. Using `>=` can introduce unintended behavior, as the condition will trigger a revert even when the variable reaches its legitimate upper bound. This can lead to bugs and vulnerabilities, as well as hamper the contract's intended functionality. The resolution is to strictly use `>` when making comparisons against a defined `MAX_VALUE` to align with its conceptual definition and to prevent unintended reverts or vulnerabilities.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[74](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L74-L74)']
```solidity
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults(); // <= FOUND
```
['[87](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L87-L87)']
```solidity
87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults(); // <= FOUND
```
['[24](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L24-L24)']
```solidity
24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults(); // <= FOUND
```


</details>

## [Low-2] Upgradable contracts should have a __gap variable

### Resolution 
This is to ensure the team can add new state variables without compromising compatability.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable 
```


</details>

## [Low-3] Use _disableInitializers() to ensure initialization occurs once

### Resolution 
`disableInitializers()` should be used in upgradeable contracts to ensure the initializer functions can't be called more than once. In upgradeable contracts, initializer functions set initial state and values, but if they can be invoked multiple times, it could lead to unexpected behavior or vulnerabilities. By calling `disableInitializers()` after the initial setup, you essentially lock the initializer functions, ensuring they can only be called once during the contract's lifecycle. This prevents repeated initializations, helping to maintain the integrity and security of the contract, and providing a safeguard against potential manipulation or misuse of the initialization functions.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable  // <= FOUND
```


</details>

## [Low-4] Loss of precision

### Resolution 
Dividing by large numbers in Solidity can cause a loss of precision due to the language's inherent integer division behavior. Solidity does not support floating-point arithmetic, and as a result, division between integers yields an integer result, truncating any fractional part. When dividing by a large number, the resulting value may become significantly smaller, leading to a loss of precision, as the fractional part is discarded.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L197)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount);
194:       Vault _vault = Vault(vault);
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice()  // <= FOUND
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to);
201:       return asset;
202:   }
```
['[50](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L50-L63)']
```solidity
50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
55:       uint tvl;
56:       address[] memory vaults = kerosineManager.getVaults();
57:       uint numberOfVaults = vaults.length;
58:       for (uint i = 0; i < numberOfVaults; i++) {
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals())  // <= FOUND
63:                 / (10**vault.oracle().decimals()); // <= FOUND
64:       }
65:       uint numerator   = tvl - dyad.totalSupply();
66:       uint denominator = kerosineDenominator.denominator();
67:       return numerator * 1e8 / denominator; // <= FOUND
68:   }
```


</details>

## [Low-5] Critical functions should be a two step procedure

### Resolution 
Critical functions in Solidity contracts should follow a two-step procedure to enhance security, minimize human error, and ensure proper access control. By dividing sensitive operations into distinct phases, such as initiation and confirmation, developers can introduce a safeguard against unintended actions or unauthorized access.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[23](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L23-L23)']
```solidity
23:   function setUnboundedKerosineVault( // <= FOUND
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   
```
['[43](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L43-L43)']
```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator)  // <= FOUND
44:     external 
45:       onlyOwner
46:   
```


</details>

## [Low-6] Constant decimal values

### Resolution 
The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.

Resolution: Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts. This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under/overflows that could jeopardize contract integrity and user funds.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[217](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L217-L217)']
```solidity
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr; // <= FOUND
```
['[218](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L218-L218)']
```solidity
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD); // <= FOUND
```
['[219](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L219-L219)']
```solidity
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr); // <= FOUND
```
['[66](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L66-L66)']
```solidity
66:       return id2asset[id] * assetPrice() / 1e8; // <= FOUND
```
['[67](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L67-L67)']
```solidity
67:       return numerator * 1e8 / denominator; // <= FOUND
```


</details>

## [Low-7] Revert on Transfer to the Zero Address

### Resolution 
Many ERC-20 and ERC-721 token contracts implement a safeguard that reverts transactions which attempt to transfer tokens to the zero address. This is because such transfers are often the result of programming errors. The OpenZeppelin library, a popular choice for implementing these standards, includes this safeguard. For token contract developers who want to avoid unintentional transfers to the zero address, it's good practice to include a condition that reverts the transaction if the recipient's address is the zero address. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L40)']
```solidity
30:   function withdraw(
31:     uint    id, // <= FOUND
32:     address to, // <= FOUND
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {
38:     id2asset[id] -= amount;
39:     asset.safeTransfer(to, amount);  // <= FOUND
40:     emit Withdraw(id, to, amount); // <= FOUND
41:   }
```


</details>

## [Low-8] Incorrect withdraw declaration

### Resolution 
In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for `withdraw` should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L32-L32)']
```solidity
32:   function withdraw( // <= FOUND
33:     uint    id,
34:     address vault,
35:     uint    amount,
36:     address to
37:   ) 
38:     public
39:       isDNftOwner(id)
40:   
```
['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L32-L32)']
```solidity
32:   function withdraw( // <= FOUND
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:     view
39:       onlyVaultManager
40:   
```
['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L32-L32)']
```solidity
32:   function withdraw( // <= FOUND
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:       onlyVaultManager
39:   
```


</details>

## [Low-9] Create methods are suspicious of the reorg attack

### Resolution 
"Create" methods, which deploy contracts via " = new <contract>", are at risk from re-org attacks since the derived contract address is solely based on the Factory's nonce. Re-orgs, chain reorganizations, can occur across all EVM chains. The vulnerability amplifies when deploying contracts on EVM-compatible L2 solutions like Arbitrum and Polygon, which are notably susceptible to re-org attacks. Ethereum, a primary deployment target, has already experienced re-org events.

To bolster security against re-org threats, developers are advised to use the `create2` method for contract deployments instead of the basic `create`. By using `create2` with a salt that includes `msg.sender`, the contract's address derivation becomes more predictable and less prone to unexpected changes due to re-orgs. This strategy not only provides a more consistent deployment pattern but also minimizes risks associated with potential blockchain reorganizations.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[36](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L36-L71)']
```solidity
36:   function run() public returns (Contracts memory) {
37:     vm.startBroadcast();  
38: 
39:     Licenser vaultLicenser = new Licenser();
40: 
42:     VaultManagerV2 vaultManager = new VaultManagerV2( // <= FOUND
43:       DNft(MAINNET_DNFT),
44:       Dyad(MAINNET_DYAD),
45:       vaultLicenser
46:     );
47: 
49:     Vault ethVault = new Vault(
50:       vaultManager,
51:       ERC20        (MAINNET_WETH),
52:       IAggregatorV3(MAINNET_WETH_ORACLE)
53:     );
54: 
56:     VaultWstEth wstEth = new VaultWstEth(
57:       vaultManager, 
58:       ERC20        (MAINNET_WSTETH), 
59:       IAggregatorV3(MAINNET_CHAINLINK_STETH)
60:     );
61: 
62:     KerosineManager kerosineManager = new KerosineManager(); // <= FOUND
63: 
64:     kerosineManager.add(address(ethVault));
65:     kerosineManager.add(address(wstEth));
66: 
67:     vaultManager.setKeroseneManager(kerosineManager);
68: 
69:     kerosineManager.transferOwnership(MAINNET_OWNER);
70: 
71:     UnboundedKerosineVault unboundedKerosineVault = new UnboundedKerosineVault( // <= FOUND
72:       vaultManager,
73:       Kerosine(MAINNET_KEROSENE), 
74:       Dyad    (MAINNET_DYAD),
75:       kerosineManager
76:     );
77: 
78:     BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault( // <= FOUND
79:       vaultManager,
80:       Kerosine(MAINNET_KEROSENE), 
81:       kerosineManager
82:     );
83: 
84:     KerosineDenominator kerosineDenominator       = new KerosineDenominator( // <= FOUND
85:       Kerosine(MAINNET_KEROSENE)
86:     );
87: 
88:     unboundedKerosineVault.setDenominator(kerosineDenominator);
89: 
90:     unboundedKerosineVault.transferOwnership(MAINNET_OWNER);
91:     boundedKerosineVault.  transferOwnership(MAINNET_OWNER);
92: 
93:     vaultLicenser.add(address(ethVault));
94:     vaultLicenser.add(address(wstEth));
95:     vaultLicenser.add(address(unboundedKerosineVault));
96:     
98:     vaultLicenser.transferOwnership(MAINNET_OWNER);
99: 
100:     vm.stopBroadcast();  
101: 
102:     return Contracts(
103:       Kerosine(MAINNET_KEROSENE),
104:       vaultLicenser,
105:       vaultManager,
106:       ethVault,
107:       wstEth,
108:       kerosineManager,
109:       unboundedKerosineVault,
110:       boundedKerosineVault,
111:       kerosineDenominator
112:     );
113:   }
```


</details>

## [Low-10] Non constant/immutable state variables are missing a setter post deployment

### Resolution 
Non-constant or non-immutable state variables lacking a setter function can create inflexibility in contract operations. If there's no way to update these variables post-deployment, the contract might not adapt to changing conditions or requirements, which can be a significant drawback, especially in upgradable or long-lived contracts. To resolve this, implement setter functions guarded by appropriate access controls, like `onlyOwner` or similar modifiers, so that these variables can be updated as required while maintaining security. This enables smoother contract maintenance and feature upgrades.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[9](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L9-L9)']
```solidity
9:   Kerosine public kerosine;
```


</details>

## [Low-11] Constructors missing validation

### Resolution 
In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[11](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L11-L11)']
```solidity
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }
```
['[49](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L49-L49)']
```solidity
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
['[26](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L26-L26)']
```solidity
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


</details>

## [Low-12] In production vm.log and it's counterparts should not be used

### Resolution 
vm calls are meant to be used within testing environments and can have unforeseen consequences when used in production code

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[37](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L37-L37)']
```solidity
37:     vm.startBroadcast();   // <= FOUND
```
['[100](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L100-L100)']
```solidity
100:     vm.stopBroadcast();   // <= FOUND
```


</details>

## [Low-13] Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

### Resolution 
While adherence to the check-effects-interaction pattern is commendable, the absence of a reentrancy guard in functions, especially where transfer hooks might be present, can expose the protocol users to risks of read-only reentrancies. Such reentrancy vulnerabilities can be exploited to execute malicious actions even without altering the contract state. Without a reentrancy guard, the only potential mitigation would be to blocklist the entire protocol - an extreme and disruptive measure. Therefore, incorporating a reentrancy guard into these functions is vital to bolster security, as it helps protect against both traditional reentrancy attacks and read-only reentrancies, ensuring robust and safe protocol operations.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L30)']
```solidity
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
['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L39)']
```solidity
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   {
38:     id2asset[id] -= amount;
39:     asset.safeTransfer(to, amount);  // <= FOUND
40:     emit Withdraw(id, to, amount);
41:   }
```


</details>

## [Low-14] Loss of precision

### Resolution 
Dividing by large numbers in Solidity can cause a loss of precision due to the language's inherent integer division behavior. Solidity does not support floating-point arithmetic, and as a result, division between integers yields an integer result, truncating any fractional part. When dividing by a large number, the resulting value may become significantly smaller, leading to a loss of precision, as the fractional part is discarded.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L197)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount);
194:       Vault _vault = Vault(vault);
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice()  // <= FOUND
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to);
201:       return asset;
202:   }
```
['[50](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L50-L63)']
```solidity
50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
55:       uint tvl;
56:       address[] memory vaults = kerosineManager.getVaults();
57:       uint numberOfVaults = vaults.length;
58:       for (uint i = 0; i < numberOfVaults; i++) {
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals())  // <= FOUND
63:                 / (10**vault.oracle().decimals()); // <= FOUND
64:       }
65:       uint numerator   = tvl - dyad.totalSupply();
66:       uint denominator = kerosineDenominator.denominator();
67:       return numerator * 1e8 / denominator; // <= FOUND
68:   }
```


</details>

## [NonCritical-1] Critical functions should have a timelock

### Resolution 
Critical functions, especially those affecting protocol parameters or user funds, are potential points of failure or exploitation. To mitigate risks, incorporating a timelock on such functions can be beneficial. A timelock requires a waiting period between the time an action is initiated and when it's executed, giving stakeholders time to react, potentially vetoing malicious or erroneous changes. To implement, integrate a smart contract like OpenZeppelin's `TimelockController` or build a custom mechanism. This ensures governance decisions or administrative changes are transparent and allows for community or multi-signature interventions, enhancing protocol security and trustworthiness.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[23](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L23-L23)']
```solidity
23:   function setUnboundedKerosineVault( // <= FOUND
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   
```
['[43](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L43-L43)']
```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator)  // <= FOUND
44:     external 
45:       onlyOwner
46:   
```


</details>

## [NonCritical-2] SafeTransferLib does not ensure that the token contract exists

### Resolution 
SafeTransferLib as similarly named function as OpenZepelins SafeERC20 module however it's functions such as safeTransferFrom don't check if the contract exists which can result in silent failures when performing such operations. As such it is recommended to perform a contract existence check beforehand. 

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[13](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L13-L13)']
```solidity
13: import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol"; // <= FOUND
```
['[8](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L8-L8)']
```solidity
8: import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol"; // <= FOUND
```


</details>

## [NonCritical-3] In functions which accept an address as a parameter, there should be a zero address check to prevent bugs

### Resolution 
In smart contract development, especially with Solidity, it's crucial to validate inputs to functions. When a function accepts an Ethereum address as a parameter, implementing a zero address check (i.e., ensuring the address is not `0x0`) is a best practice to prevent potential bugs and vulnerabilities. The zero address (`0x0`) is a default value and generally indicates an uninitialized or invalid state. Passing the zero address to certain functions can lead to unintended behaviors, like funds getting locked permanently or transactions failing silently. By checking for and rejecting the zero address, developers can ensure that the function operates as intended and interacts only with valid Ethereum addresses. This check enhances the contract's robustness and security.

Num of instances: 14

### Findings 


<details><summary>Click to show findings</summary>

['[67](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L67-L67)']
```solidity
67:   function add(
68:       uint    id,
69:       address vault
70:   ) 
71:     external
72:       isDNftOwner(id)
73:   
```
['[80](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L80-L80)']
```solidity
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   ) 
84:     external
85:       isDNftOwner(id)
86:   
```
['[94](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L94-L94)']
```solidity
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 
98:     external
99:       isDNftOwner(id)
100:   
```
['[106](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L106-L106)']
```solidity
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 
110:     external
111:       isDNftOwner(id)
112:   
```
['[119](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L119-L119)']
```solidity
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   
```
['[134](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L134-L134)']
```solidity
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   
```
['[156](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L156-L156)']
```solidity
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   
```
['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L184)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) 
```
['[299](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L299-L299)']
```solidity
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   ) 
303:     external 
304:     view 
305:     returns (bool) 
```
['[18](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L18-L18)']
```solidity
18:   function add(
19:     address vault
20:   ) 
21:     external 
22:       onlyOwner
23:   
```
['[28](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L28-L28)']
```solidity
28:   function remove(
29:     address vault
30:   ) 
31:     external 
32:       onlyOwner
33:   
```
['[44](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L44-L44)']
```solidity
44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) 
```
['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L32-L32)']
```solidity
32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:     view
39:       onlyVaultManager
40:   
```
['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L30)']
```solidity
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   
```


</details>

## [NonCritical-4] Avoid updating storage when the value hasn't changed

### Resolution 
In Solidity, manipulating contract storage comes with significant gas costs. One can optimize gas usage by preventing unnecessary storage updates when the new value is the same as the existing one. If an existing value is the same as the new one, not reassigning it to the storage could potentially save substantial amounts of gas, notably 2900 gas for a 'Gsreset'. This saving may come at the expense of a cold storage load operation ('Gcoldsload'), which costs 2100 gas, or a warm storage access operation ('Gwarmaccess'), which costs 100 gas. Therefore, the gas efficiency of your contract can be significantly improved by adding a check that compares the new value with the current one before any storage update operation. If the values are the same, you can bypass the storage operation, thereby saving gas.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[23](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L23-L23)']
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
['[43](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L43-L43)']
```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }
```


</details>

## [NonCritical-5] Old Solidity version

### Resolution 
Using outdated Solidity versions can lead to security risks and inefficiencies. It's recommended to adopt newer versions, ideally the latest, which as of now is 0.8.24. This ensures access to the latest bug fixes, features, and optimizations, particularly crucial for Layer 2 deployments. Regular updates to versions like 0.8.19 or later, up to 0.8.24, enhance contract security and performance.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L2-L2)']
```solidity
2: pragma solidity =0.8.17;
```


</details>

## [NonCritical-6] Contracts should have all public/external functions exposed by interfaces

### Resolution 
Contracts should expose all public and external functions through interfaces. This practice ensures a clear and consistent definition of how the contract can be interacted with, promoting better transparency and integration.

Num of instances: 30

### Findings 


<details><summary>Click to show findings</summary>

['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L17-L17)']
```solidity
17:   function denominator() external view returns (uint) 
```
['[59](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L59-L59)']
```solidity
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     
```
['[67](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L67-L67)']
```solidity
67:   function add(
68:       uint    id,
69:       address vault
70:   ) 
71:     external
72:       isDNftOwner(id)
73:   
```
['[80](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L80-L80)']
```solidity
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   ) 
84:     external
85:       isDNftOwner(id)
86:   
```
['[94](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L94-L94)']
```solidity
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 
98:     external
99:       isDNftOwner(id)
100:   
```
['[106](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L106-L106)']
```solidity
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 
110:     external
111:       isDNftOwner(id)
112:   
```
['[119](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L119-L119)']
```solidity
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   
```
['[156](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L156-L156)']
```solidity
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   
```
['[172](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L172-L172)']
```solidity
172:   function burnDyad(
173:     uint id,
174:     uint amount
175:   ) 
176:     external 
177:       isValidDNft(id)
178:   
```
['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L184)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) 
```
['[205](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L205-L205)']
```solidity
205:   function liquidate(
206:     uint id,
207:     uint to
208:   ) 
209:     external 
210:       isValidDNft(id)
211:       isValidDNft(to)
212:     
```
['[290](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L290-L290)']
```solidity
290:   function getVaults(
291:     uint id
292:   ) 
293:     external 
294:     view 
295:     returns (address[] memory) 
```
['[299](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L299-L299)']
```solidity
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   ) 
303:     external 
304:     view 
305:     returns (bool) 
```
['[47](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L47-L47)']
```solidity
47:   function move(
48:     uint from,
49:     uint to,
50:     uint amount
51:   )
52:     external
53:       onlyVaultManager
54:   
```
['[18](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L18-L18)']
```solidity
18:   function add(
19:     address vault
20:   ) 
21:     external 
22:       onlyOwner
23:   
```
['[28](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L28-L28)']
```solidity
28:   function remove(
29:     address vault
30:   ) 
31:     external 
32:       onlyOwner
33:   
```
['[37](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L37-L37)']
```solidity
37:   function getVaults() 
38:     external 
39:     view 
40:     returns (address[] memory) 
```
['[44](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L44-L44)']
```solidity
44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) 
```
['[23](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L23-L23)']
```solidity
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   
```
['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L32-L32)']
```solidity
32:   function withdraw(
33:     uint    id,
34:     address to,
35:     uint    amount
36:   ) 
37:     external 
38:     view
39:       onlyVaultManager
40:   
```
['[30](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L30-L30)']
```solidity
30:   function withdraw(
31:     uint    id,
32:     address to,
33:     uint    amount
34:   ) 
35:     external 
36:       onlyVaultManager
37:   
```
['[43](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L43-L43)']
```solidity
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   
```
['[134](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L134-L134)']
```solidity
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   
```
['[230](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L230-L230)']
```solidity
230:   function collatRatio(
231:     uint id
232:   )
233:     public 
234:     view
235:     returns (uint) 
```
['[241](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L241-L241)']
```solidity
241:   function getTotalUsdValue(
242:     uint id
243:   ) 
244:     public 
245:     view
246:     returns (uint) 
```
['[250](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L250-L250)']
```solidity
250:   function getNonKeroseneValue(
251:     uint id
252:   ) 
253:     public 
254:     view
255:     returns (uint) 
```
['[269](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L269-L269)']
```solidity
269:   function getKeroseneValue(
270:     uint id
271:   ) 
272:     public 
273:     view
274:     returns (uint) 
```
['[36](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L36-L36)']
```solidity
36:   function deposit(
37:     uint id,
38:     uint amount
39:   )
40:     public 
41:       onlyVaultManager
42:   
```
['[60](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L60-L60)']
```solidity
60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view 
65:     returns (uint) 
```
['[36](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L36-L36)']
```solidity
36:   function run() public returns (Contracts memory) 
```


</details>

## [NonCritical-7] Emits without msg.sender parameter

### Resolution 
In Solidity, when `msg.sender` plays a crucial role in a function's logic, it's important for transparency and auditability that any events emitted by this function include `msg.sender` as a parameter. This practice enhances the traceability and accountability of transactions, allowing users and external observers to easily track who initiated a particular action. Including `msg.sender` in event logs helps in creating a clear and verifiable record of interactions with the contract, thereby increasing user trust and facilitating easier debugging and analysis of contract behavior. It's a key aspect of writing clear, transparent, and user-friendly smart contracts.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L200)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount); // <= FOUND
194:       Vault _vault = Vault(vault);
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to); // <= FOUND
201:       return asset;
202:   }
```


</details>

## [NonCritical-8] Remove forge-std import

### Resolution 
Logging and debugging libraries such as forge-std are crucial tools during the development phase of a smart contract, as they provide critical insights into the execution of the contract. However, it's essential to remove or disable these libraries in the production version of your contract. Leaving such libraries active in the final version can lead to unnecessary gas costs, as logging operations consume gas, and it can potentially expose sensitive internal state information.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[4](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L4-L4)']
```solidity
4: import "forge-std/Script.sol"; // <= FOUND
```


</details>

## [NonCritical-9] Unused import

### Resolution 
If these serve no purpose, they should be safely removed

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[13](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L13-L13)']
```solidity
13: import {IWETH}                  from "../../src/interfaces/IWETH.sol"; // <= FOUND
```


</details>

## [NonCritical-10] Events may be emitted out of order due to code not follow the best practice of check-effects-interaction

### Resolution 
The "check-effects-interaction" pattern also impacts event ordering. When a contract doesn't adhere to this pattern, events might be emitted in a sequence that doesn't reflect the actual logical flow of operations. This can cause confusion during event tracking, potentially leading to erroneous off-chain interpretations. To rectify this, always ensure that checks are performed first, state modifications come next, and interactions with external contracts or addresses are done last. This will ensure events are emitted in a logical, consistent manner, providing a clear and accurate chronological record of on-chain actions for off-chain systems and observers.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[184](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L184-L184)']
```solidity
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount);
194:       Vault _vault = Vault(vault);
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to);
201:       return asset;
202:   }
```
['[94](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L94-L94)']
```solidity
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 
98:     external
99:       isDNftOwner(id)
100:   {
101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();
103:     emit Removed(id, vault);
104:   }
```
['[106](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L106-L106)']
```solidity
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 
110:     external
111:       isDNftOwner(id)
112:   {
113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
114:     if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
115:     emit Removed(id, vault);
116:   }
```


</details>

## [NonCritical-11] Don't only depend on Solidity's arithmetic ordering.

### Resolution 
Relying on Solidity's default arithmetic operator precedence can lead to misunderstood or overlooked nuances in code execution. Misinterpretation risks can be significant, especially when different developers or auditors review the code. To ensure clarity and minimize potential errors, it's recommended to use parentheses. These not only override the default precedence when needed but also emphasize the intended order of operations. By deliberately showing the intended calculation sequence using parentheses, developers make the code's logic explicit, reducing the risk of unintended behaviors and making the codebase more maintainable and understandable for all stakeholders.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[67](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L67-L67)']
```solidity
67:       return numerator * 1e8 / denominator; // <= FOUND
```


</details>

## [NonCritical-12] Contracts with only unimplemented functions can be labeled as abstract

### Resolution 
In Solidity, a contract that's not meant to be deployed on its own but is intended to be inherited by other contracts should be marked `abstract`. This ensures that developers recognize the contract's incomplete or intended-to-be-extended nature. If a contract has unimplemented functions or is designed with the intention that another contract should extend its functionality, it should be explicitly labeled as `abstract`. This helps prevent inadvertent deployments and clearly communicates the contract's purpose to other developers. Resolution: Review the contract, and if it's not supposed to function standalone, mark it as `abstract` to make the intention clear.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L7-L7)']
```solidity
7: contract KerosineManager is Owned(msg.sender) 
```


</details>

## [NonCritical-13] A event should be emitted if a non immutable state variable is set in a constructor

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[11](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L11-L14)']
```solidity
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine; // <= FOUND
15:   }
```
['[49](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L49-L55)']
```solidity
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
54:     dNft          = _dNft; // <= FOUND
55:     dyad          = _dyad; // <= FOUND
56:     vaultLicenser = _licenser;
57:   }
```
['[26](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L26-L32)']
```solidity
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
31:     vaultManager    = _vaultManager; // <= FOUND
32:     asset           = _asset; // <= FOUND
33:     kerosineManager = _kerosineManager;
34:   }
```


</details>

## [NonCritical-14] There should not be more than one space before assignment

### Resolution 
At times, devs may add multiple spaces before an assignment of a variable to be inline with future assignments in lines above/below, in solidity this practise should not be followed as it's against the official style guide.

Num of instances: 12

### Findings 


<details><summary>Click to show findings</summary>

['[22](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L22-L22)']
```solidity
22:   uint public constant MAX_VAULTS          = 5; // <= FOUND
```
['[26](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L26-L26)']
```solidity
26:   uint public constant LIQUIDATION_REWARD        = 0.2e18;  // <= FOUND
```
['[54](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L54-L54)']
```solidity
54:     dNft          = _dNft; // <= FOUND
```
['[55](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L55-L55)']
```solidity
55:     dyad          = _dyad; // <= FOUND
```
['[217](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L217-L217)']
```solidity
217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr; // <= FOUND
```
['[219](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L219-L219)']
```solidity
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr); // <= FOUND
```
['[223](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L223-L223)']
```solidity
223:           Vault vault      = Vault(vaults[id].at(i)); // <= FOUND
```
['[31](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L31-L31)']
```solidity
31:     vaultManager    = _vaultManager; // <= FOUND
```
['[32](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L32-L32)']
```solidity
32:     asset           = _asset; // <= FOUND
```
['[65](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L65-L65)']
```solidity
65:       uint numerator   = tvl - dyad.totalSupply(); // <= FOUND
```
['[78](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L78-L78)']
```solidity
78:     BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault( // <= FOUND
79:       vaultManager,
80:       Kerosine(MAINNET_KEROSENE), 
81:       kerosineManager
82:     );
```
['[84](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L84-L84)']
```solidity
84:     KerosineDenominator kerosineDenominator       = new KerosineDenominator( // <= FOUND
85:       Kerosine(MAINNET_KEROSENE)
86:     );
```


</details>

## [NonCritical-15] Mappings should not have a space before the parenthesis.

### Resolution 
Yes: mapping( 
 No: mapping (

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[34](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L34-L34)']
```solidity
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults;  // <= FOUND
```
['[35](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L35-L35)']
```solidity
35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;  // <= FOUND
```
['[37](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L37-L37)']
```solidity
37:   mapping (uint => uint) public idToBlockOfLastDeposit; // <= FOUND
```


</details>

## [NonCritical-16] Avoid declaring variables with the names of defined functions within the project

### Resolution 
Having such variables can create confusion in both developers and in users of the project. Consider renaming these variables to improve code clarity.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[66](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L66-L66)']
```solidity
66:       uint denominator = kerosineDenominator.denominator(); // <= FOUND
```


</details>

## [NonCritical-17] Errors should have parameters

### Resolution 
In Solidity, custom errors with parameters offer a gas-efficient way to convey detailed information about issues encountered during contract execution. Unlike revert messages, which are strings consuming more gas, custom errors defined with parameters allow developers to specify types and details of errors succinctly. This method enhances debugging, provides clearer insights into contract failures, and improves the developer's and end-user's understanding of what went wrong, all while optimizing for gas usage and maintaining contract efficiency.

Num of instances: 6

### Findings 


<details><summary>Click to show findings</summary>

['[8](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L8-L8)']
```solidity
8:   error TooManyVaults(); // <= FOUND
```
['[9](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L9-L9)']
```solidity
9:   error VaultAlreadyAdded(); // <= FOUND
```
['[10](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L10-L10)']
```solidity
10:   error VaultNotFound(); // <= FOUND
```
['[8](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L8-L8)']
```solidity
8: error TooManyVaults(); // <= FOUND
```
['[9](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L9-L9)']
```solidity
9: error VaultAlreadyAdded(); // <= FOUND
```
['[10](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L10-L10)']
```solidity
10: error VaultNotFound(); // <= FOUND
```


</details>

## [NonCritical-18] NatSpec: @notice tags missing from contract/abstract/library/interface/function/modifier/constructor/receive/fallback

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L7-L7)']
```solidity
7: contract KerosineDenominator is Parameters 
```
['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable 
```
['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L7-L7)']
```solidity
7: contract KerosineManager is Owned(msg.sender) 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L12-L12)']
```solidity
12: contract BoundedKerosineVault is KerosineVault 
```
['[15](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L15-L15)']
```solidity
15: contract UnboundedKerosineVault is KerosineVault 
```
['[35](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L35-L35)']
```solidity
35: contract DeployV2 is Script, Parameters 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) 
```


</details>

## [NonCritical-19] Natspec @author is missing from contract/interface/library

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L7-L7)']
```solidity
7: contract KerosineDenominator is Parameters {
8: 
9:   Kerosine public kerosine;
10: 
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }
16: 
17:   function denominator() external view returns (uint) {
18:     // @dev: We subtract all the Kerosene in the multi-sig.
19:     //       We are aware that this is not a great solution. That is
20:     //       why we can switch out Denominator contracts.
21:     return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
22:   } 
23: }
```
['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable {
18:   using EnumerableSet     for EnumerableSet.AddressSet;
19:   using FixedPointMathLib for uint;
20:   using SafeTransferLib   for ERC20;
21: 
22:   uint public constant MAX_VAULTS          = 5;
23:   uint public constant MAX_VAULTS_KEROSENE = 5;
24: 
25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%
26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
27: 
28:   DNft     public immutable dNft;
29:   Dyad     public immutable dyad;
30:   Licenser public immutable vaultLicenser;
31: 
32:   KerosineManager public keroseneManager;
33: 
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 
35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 
36: 
37:   mapping (uint => uint) public idToBlockOfLastDeposit;
38: 
39:   modifier isDNftOwner(uint id) {
40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
41:   }
42:   modifier isValidDNft(uint id) {
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44:   }
45:   modifier isLicensed(address vault) {
46:     if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47:   }
48: 
49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
54:     dNft          = _dNft;
55:     dyad          = _dyad;
56:     vaultLicenser = _licenser;
57:   }
58: 
59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }
65: 
66:   /// @inheritdoc IVaultManager
67:   function add(
68:       uint    id,
69:       address vault
70:   ) 
71:     external
72:       isDNftOwner(id)
73:   {
74:     if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
75:     if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
76:     if (!vaults[id].add(vault))            revert VaultAlreadyAdded();
77:     emit Added(id, vault);
78:   }
79: 
80:   function addKerosene(
81:       uint    id,
82:       address vault
83:   ) 
84:     external
85:       isDNftOwner(id)
86:   {
87:     if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
88:     if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
89:     if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
90:     emit Added(id, vault);
91:   }
92: 
93:   /// @inheritdoc IVaultManager
94:   function remove(
95:       uint    id,
96:       address vault
97:   ) 
98:     external
99:       isDNftOwner(id)
100:   {
101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
102:     if (!vaults[id].remove(vault))     revert VaultNotAdded();
103:     emit Removed(id, vault);
104:   }
105: 
106:   function removeKerosene(
107:       uint    id,
108:       address vault
109:   ) 
110:     external
111:       isDNftOwner(id)
112:   {
113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
114:     if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
115:     emit Removed(id, vault);
116:   }
117: 
118:   /// @inheritdoc IVaultManager
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   {
127:     idToBlockOfLastDeposit[id] = block.number;
128:     Vault _vault = Vault(vault);
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
130:     _vault.deposit(id, amount);
131:   }
132: 
133:   /// @inheritdoc IVaultManager
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
151:     _vault.withdraw(id, to, amount);
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
153:   }
154: 
155:   /// @inheritdoc IVaultManager
156:   function mintDyad(
157:     uint    id,
158:     uint    amount,
159:     address to
160:   )
161:     external 
162:       isDNftOwner(id)
163:   {
164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
166:     dyad.mint(id, to, amount);
167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
168:     emit MintDyad(id, amount, to);
169:   }
170: 
171:   /// @inheritdoc IVaultManager
172:   function burnDyad(
173:     uint id,
174:     uint amount
175:   ) 
176:     external 
177:       isValidDNft(id)
178:   {
179:     dyad.burn(id, msg.sender, amount);
180:     emit BurnDyad(id, amount, msg.sender);
181:   }
182: 
183:   /// @inheritdoc IVaultManager
184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount);
194:       Vault _vault = Vault(vault);
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to);
201:       return asset;
202:   }
203: 
204:   /// @inheritdoc IVaultManager
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
223:           Vault vault      = Vault(vaults[id].at(i));
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225:           vault.move(id, to, collateral);
226:       }
227:       emit Liquidate(id, msg.sender, to);
228:   }
229: 
230:   function collatRatio(
231:     uint id
232:   )
233:     public 
234:     view
235:     returns (uint) {
236:       uint _dyad = dyad.mintedDyad(address(this), id);
237:       if (_dyad == 0) return type(uint).max;
238:       return getTotalUsdValue(id).divWadDown(_dyad);
239:   }
240: 
241:   function getTotalUsdValue(
242:     uint id
243:   ) 
244:     public 
245:     view
246:     returns (uint) {
247:       return getNonKeroseneValue(id) + getKeroseneValue(id);
248:   }
249: 
250:   function getNonKeroseneValue(
251:     uint id
252:   ) 
253:     public 
254:     view
255:     returns (uint) {
256:       uint totalUsdValue;
257:       uint numberOfVaults = vaults[id].length(); 
258:       for (uint i = 0; i < numberOfVaults; i++) {
259:         Vault vault = Vault(vaults[id].at(i));
260:         uint usdValue;
261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }
264:         totalUsdValue += usdValue;
265:       }
266:       return totalUsdValue;
267:   }
268: 
269:   function getKeroseneValue(
270:     uint id
271:   ) 
272:     public 
273:     view
274:     returns (uint) {
275:       uint totalUsdValue;
276:       uint numberOfVaults = vaultsKerosene[id].length(); 
277:       for (uint i = 0; i < numberOfVaults; i++) {
278:         Vault vault = Vault(vaultsKerosene[id].at(i));
279:         uint usdValue;
280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }
283:         totalUsdValue += usdValue;
284:       }
285:       return totalUsdValue;
286:   }
287: 
288:   // ----------------- MISC ----------------- //
289: 
290:   function getVaults(
291:     uint id
292:   ) 
293:     external 
294:     view 
295:     returns (address[] memory) {
296:       return vaults[id].values();
297:   }
298: 
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   ) 
303:     external 
304:     view 
305:     returns (bool) {
306:       return vaults[id].contains(vault);
307:   }
308: }
```
['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L7-L7)']
```solidity
7: contract KerosineManager is Owned(msg.sender) {
8:   error TooManyVaults();
9:   error VaultAlreadyAdded();
10:   error VaultNotFound();
11: 
12:   using EnumerableSet for EnumerableSet.AddressSet;
13: 
14:   uint public constant MAX_VAULTS = 10;
15: 
16:   EnumerableSet.AddressSet private vaults;
17: 
18:   function add(
19:     address vault
20:   ) 
21:     external 
22:       onlyOwner
23:   {
24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
25:     if (!vaults.add(vault))            revert VaultAlreadyAdded();
26:   }
27: 
28:   function remove(
29:     address vault
30:   ) 
31:     external 
32:       onlyOwner
33:   {
34:     if (!vaults.remove(vault)) revert VaultNotFound();
35:   }
36: 
37:   function getVaults() 
38:     external 
39:     view 
40:     returns (address[] memory) {
41:       return vaults.values();
42:   }
43: 
44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) {
50:       return vaults.contains(vault);
51:   }
52: }
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L12-L12)']
```solidity
12: contract BoundedKerosineVault is KerosineVault {
13:   error NotWithdrawable(uint id, address to, uint amount);
14: 
15:   UnboundedKerosineVault public unboundedKerosineVault;
16: 
17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
22: 
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }
31: 
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
43: 
44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {
49:       return unboundedKerosineVault.assetPrice() * 2;
50:   }
51: }
```
['[15](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L15-L15)']
```solidity
15: contract UnboundedKerosineVault is KerosineVault {
16:   using SafeTransferLib for ERC20;
17: 
18:   Dyad                 public immutable dyad;
19:   KerosineDenominator  public kerosineDenominator;
20: 
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27:       dyad = _dyad;
28:   }
29: 
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
42: 
43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }
49: 
50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
55:       uint tvl;
56:       address[] memory vaults = kerosineManager.getVaults();
57:       uint numberOfVaults = vaults.length;
58:       for (uint i = 0; i < numberOfVaults; i++) {
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
64:       }
65:       uint numerator   = tvl - dyad.totalSupply();
66:       uint denominator = kerosineDenominator.denominator();
67:       return numerator * 1e8 / denominator;
68:   }
69: }
```
['[35](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L35-L35)']
```solidity
35: contract DeployV2 is Script, Parameters {
36:   function run() public returns (Contracts memory) {
37:     vm.startBroadcast();  // ----------------------
38: 
39:     Licenser vaultLicenser = new Licenser();
40: 
41:     // Vault Manager needs to be licensed through the Vault Manager Licenser
42:     VaultManagerV2 vaultManager = new VaultManagerV2(
43:       DNft(MAINNET_DNFT),
44:       Dyad(MAINNET_DYAD),
45:       vaultLicenser
46:     );
47: 
48:     // weth vault
49:     Vault ethVault = new Vault(
50:       vaultManager,
51:       ERC20        (MAINNET_WETH),
52:       IAggregatorV3(MAINNET_WETH_ORACLE)
53:     );
54: 
55:     // wsteth vault
56:     VaultWstEth wstEth = new VaultWstEth(
57:       vaultManager, 
58:       ERC20        (MAINNET_WSTETH), 
59:       IAggregatorV3(MAINNET_CHAINLINK_STETH)
60:     );
61: 
62:     KerosineManager kerosineManager = new KerosineManager();
63: 
64:     kerosineManager.add(address(ethVault));
65:     kerosineManager.add(address(wstEth));
66: 
67:     vaultManager.setKeroseneManager(kerosineManager);
68: 
69:     kerosineManager.transferOwnership(MAINNET_OWNER);
70: 
71:     UnboundedKerosineVault unboundedKerosineVault = new UnboundedKerosineVault(
72:       vaultManager,
73:       Kerosine(MAINNET_KEROSENE), 
74:       Dyad    (MAINNET_DYAD),
75:       kerosineManager
76:     );
77: 
78:     BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault(
79:       vaultManager,
80:       Kerosine(MAINNET_KEROSENE), 
81:       kerosineManager
82:     );
83: 
84:     KerosineDenominator kerosineDenominator       = new KerosineDenominator(
85:       Kerosine(MAINNET_KEROSENE)
86:     );
87: 
88:     unboundedKerosineVault.setDenominator(kerosineDenominator);
89: 
90:     unboundedKerosineVault.transferOwnership(MAINNET_OWNER);
91:     boundedKerosineVault.  transferOwnership(MAINNET_OWNER);
92: 
93:     vaultLicenser.add(address(ethVault));
94:     vaultLicenser.add(address(wstEth));
95:     vaultLicenser.add(address(unboundedKerosineVault));
96:     // vaultLicenser.add(address(boundedKerosineVault)):
97: 
98:     vaultLicenser.transferOwnership(MAINNET_OWNER);
99: 
100:     vm.stopBroadcast();  // ----------------------------
101: 
102:     return Contracts(
103:       Kerosine(MAINNET_KEROSENE),
104:       vaultLicenser,
105:       vaultManager,
106:       ethVault,
107:       wstEth,
108:       kerosineManager,
109:       unboundedKerosineVault,
110:       boundedKerosineVault,
111:       kerosineDenominator
112:     );
113:   }
114: }
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) {
13:   using SafeTransferLib for ERC20;
14: 
15:   IVaultManager   public immutable vaultManager;
16:   ERC20           public immutable asset;
17:   KerosineManager public immutable kerosineManager;
18: 
19:   mapping(uint => uint) public id2asset;
20: 
21:   modifier onlyVaultManager() {
22:     if (msg.sender != address(vaultManager)) revert NotVaultManager();
23:     _;
24:   }
25: 
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
31:     vaultManager    = _vaultManager;
32:     asset           = _asset;
33:     kerosineManager = _kerosineManager;
34:   }
35: 
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
46: 
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
59: 
60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view 
65:     returns (uint) {
66:       return id2asset[id] * assetPrice() / 1e8;
67:   }
68: 
69:   function assetPrice() 
70:     public 
71:     view 
72:     virtual
73:     returns (uint); 
74: }
```


</details>

## [NonCritical-20] Natspec @title is missing from contract/interface/library

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L7-L7)']
```solidity
7: contract KerosineDenominator is Parameters 
```
['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable 
```
['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L7-L7)']
```solidity
7: contract KerosineManager is Owned(msg.sender) 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L12-L12)']
```solidity
12: contract BoundedKerosineVault is KerosineVault 
```
['[15](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L15-L15)']
```solidity
15: contract UnboundedKerosineVault is KerosineVault 
```
['[35](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L35-L35)']
```solidity
35: contract DeployV2 is Script, Parameters 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) 
```


</details>

## [NonCritical-21] NatSpec: @dev tags missing from contract/abstract/library/interface/function/modifier/constructor/receive/fallback

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L7-L7)']
```solidity
7: contract KerosineDenominator is Parameters 
```
['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L17-L17)']
```solidity
17: contract VaultManagerV2 is IVaultManager, Initializable 
```
['[7](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L7-L7)']
```solidity
7: contract KerosineManager is Owned(msg.sender) 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L12-L12)']
```solidity
12: contract BoundedKerosineVault is KerosineVault 
```
['[15](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L15-L15)']
```solidity
15: contract UnboundedKerosineVault is KerosineVault 
```
['[35](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L35-L35)']
```solidity
35: contract DeployV2 is Script, Parameters 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) 
```
['[12](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L12-L12)']
```solidity
12: abstract contract KerosineVault is IVault, Owned(msg.sender) 
```


</details>

## [NonCritical-22] Incorrect NatSpec Syntax

### Resolution 
In Solidity, just like in most other programming languages, regular comments serve to make code more understandable for developers. These are usually denoted by `//` for single line comments, or `/* ... */` for multi-line comments, and are ignored by the compiler.

On the other hand, NatSpec comments in Solidity, denoted by `///` for single-line comments, or `/** ... */` for multi-line comments, serve a different purpose. Besides aiding developer comprehension, they also form a part of the contract's interface, as they can be parsed and used by tools such as automated documentation generators or IDEs to provide users with details about the contract's functions, parameters and behavior. NatSpec comments can also be retrieved via JSON interfaces, and as such, they're included in the contract's ABI. 

Thus, using `///` and `/** ... */` appropriately ensures not only proper documentation for developers, but also helps create a richer and more informative interface for users and external tools interacting with your contract.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[18](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L18-L18)']
```solidity
18: // @dev: We subtract all the Kerosene in the multi-sig. // <= FOUND
```


</details>

## [Gas-1] Using named returns for pure and view functions is cheaper than using regular returns

Num of instances: 12

### Findings 


<details><summary>Click to show findings</summary>

['[17](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L17-L21)']
```solidity
17:   function denominator() external view returns (uint) {
18:     
21:     return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER); // <= FOUND
22:   }
```
['[230](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L230-L238)']
```solidity
230:   function collatRatio(
231:     uint id
232:   )
233:     public 
234:     view
235:     returns (uint) {
236:       uint _dyad = dyad.mintedDyad(address(this), id);
237:       if (_dyad == 0) return type(uint).max; // <= FOUND
238:       return getTotalUsdValue(id).divWadDown(_dyad); // <= FOUND
239:   }
```
['[241](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L241-L247)']
```solidity
241:   function getTotalUsdValue(
242:     uint id
243:   ) 
244:     public 
245:     view
246:     returns (uint) {
247:       return getNonKeroseneValue(id) + getKeroseneValue(id); // <= FOUND
248:   }
```
['[250](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L250-L266)']
```solidity
250:   function getNonKeroseneValue(
251:     uint id
252:   ) 
253:     public 
254:     view
255:     returns (uint) {
256:       uint totalUsdValue;
257:       uint numberOfVaults = vaults[id].length(); 
258:       for (uint i = 0; i < numberOfVaults; i++) {
259:         Vault vault = Vault(vaults[id].at(i));
260:         uint usdValue;
261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }
264:         totalUsdValue += usdValue;
265:       }
266:       return totalUsdValue; // <= FOUND
267:   }
```
['[269](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L269-L285)']
```solidity
269:   function getKeroseneValue(
270:     uint id
271:   ) 
272:     public 
273:     view
274:     returns (uint) {
275:       uint totalUsdValue;
276:       uint numberOfVaults = vaultsKerosene[id].length(); 
277:       for (uint i = 0; i < numberOfVaults; i++) {
278:         Vault vault = Vault(vaultsKerosene[id].at(i));
279:         uint usdValue;
280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }
283:         totalUsdValue += usdValue;
284:       }
285:       return totalUsdValue; // <= FOUND
286:   }
```
['[290](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L290-L296)']
```solidity
290:   function getVaults(
291:     uint id
292:   ) 
293:     external 
294:     view 
295:     returns (address[] memory) {
296:       return vaults[id].values(); // <= FOUND
297:   }
```
['[299](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L299-L306)']
```solidity
299:   function hasVault(
300:     uint    id,
301:     address vault
302:   ) 
303:     external 
304:     view 
305:     returns (bool) {
306:       return vaults[id].contains(vault); // <= FOUND
307:   }
```
['[60](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L60-L66)']
```solidity
60:   function getUsdValue(
61:     uint id
62:   )
63:     public
64:     view 
65:     returns (uint) {
66:       return id2asset[id] * assetPrice() / 1e8; // <= FOUND
67:   }
```
['[37](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L37-L41)']
```solidity
37:   function getVaults() 
38:     external 
39:     view 
40:     returns (address[] memory) {
41:       return vaults.values(); // <= FOUND
42:   }
```
['[44](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/KerosineManager.sol#L44-L50)']
```solidity
44:   function isLicensed(
45:     address vault
46:   ) 
47:     external 
48:     view 
49:     returns (bool) {
50:       return vaults.contains(vault); // <= FOUND
51:   }
```
['[44](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.bounded.sol#L44-L49)']
```solidity
44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {
49:       return unboundedKerosineVault.assetPrice() * 2; // <= FOUND
50:   }
```
['[50](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L50-L67)']
```solidity
50:   function assetPrice() 
51:     public 
52:     view 
53:     override
54:     returns (uint) {
55:       uint tvl;
56:       address[] memory vaults = kerosineManager.getVaults();
57:       uint numberOfVaults = vaults.length;
58:       for (uint i = 0; i < numberOfVaults; i++) {
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
64:       }
65:       uint numerator   = tvl - dyad.totalSupply();
66:       uint denominator = kerosineDenominator.denominator();
67:       return numerator * 1e8 / denominator; // <= FOUND
68:   }
```


</details>

## [Gas-2] Public functions not used internally can be marked as external to save gas

### Resolution 
Public functions that aren't used internally in Solidity contracts should be made external to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for public functions. By using external visibility, developers can reduce gas consumption for external calls and ensure that the contract operates more cost-effectively for users. Moreover, setting the appropriate visibility level for functions also enhances code readability and maintainability, promoting a more secure and well-structured contract design.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[36](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L36-L36)']
```solidity
36:   function run() public returns (Contracts memory) 
```


</details>

## [Gas-3] Use assembly to emit events

### Resolution 
With the use of inline assembly in Solidity, we can take advantage of low-level features like scratch space and the free memory pointer, offering more gas-efficient ways of emitting events. The scratch space is a certain area of memory where we can temporarily store data, and the free memory pointer indicates the next available memory slot. Using these, we can efficiently assemble event data without incurring additional memory expansion costs. However, safety is paramount: to avoid overwriting or leakage, we must cache the free memory pointer before use and restore it afterward, ensuring that it points to the correct memory location post-operation.

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[77](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L77-L77)']
```solidity
77:     emit Added(id, vault); // <= FOUND
```
['[103](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L103-L103)']
```solidity
103:     emit Removed(id, vault); // <= FOUND
```
['[168](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L168-L168)']
```solidity
168:     emit MintDyad(id, amount, to); // <= FOUND
```
['[180](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L180-L180)']
```solidity
180:     emit BurnDyad(id, amount, msg.sender); // <= FOUND
```
['[200](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L200-L200)']
```solidity
200:       emit RedeemDyad(id, vault, amount, to); // <= FOUND
```
['[227](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L227-L227)']
```solidity
227:       emit Liquidate(id, msg.sender, to); // <= FOUND
```
['[44](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L44-L44)']
```solidity
44:     emit Deposit(id, amount); // <= FOUND
```
['[57](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L57-L57)']
```solidity
57:     emit Move(from, to, amount); // <= FOUND
```
['[40](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L40-L40)']
```solidity
40:     emit Withdraw(id, to, amount); // <= FOUND
```


</details>

## [Gas-4] Counting down in for statements is more gas efficient

### Resolution 
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[222](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L222-L222)']
```solidity
222:      for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
223:           Vault vault      = Vault(vaults[id].at(i));
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225:           vault.move(id, to, collateral);
226:       }
```
['[258](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L258-L258)']
```solidity
258:      for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
259:         Vault vault = Vault(vaults[id].at(i));
260:         uint usdValue;
261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }
264:         totalUsdValue += usdValue;
265:       }
```
['[277](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L277-L277)']
```solidity
277:      for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
278:         Vault vault = Vault(vaultsKerosene[id].at(i));
279:         uint usdValue;
280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }
283:         totalUsdValue += usdValue;
284:       }
```
['[58](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L58-L58)']
```solidity
58:      for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
64:       }
```
['[222](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L222-L222)']
```solidity
222:       for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
223:           Vault vault      = Vault(vaults[id].at(i));
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
225:           vault.move(id, to, collateral);
226:       }
```
['[258](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L258-L258)']
```solidity
258:       for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
259:         Vault vault = Vault(vaults[id].at(i));
260:         uint usdValue;
261:         if (vaultLicenser.isLicensed(address(vault))) {
262:           usdValue = vault.getUsdValue(id);        
263:         }
264:         totalUsdValue += usdValue;
265:       }
```
['[277](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L277-L277)']
```solidity
277:       for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
278:         Vault vault = Vault(vaultsKerosene[id].at(i));
279:         uint usdValue;
280:         if (keroseneManager.isLicensed(address(vault))) {
281:           usdValue = vault.getUsdValue(id);        
282:         }
283:         totalUsdValue += usdValue;
284:       }
```
['[58](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L58-L58)']
```solidity
58:       for (uint i = 0; i < numberOfVaults; i++) { // <= FOUND
59:         Vault vault = Vault(vaults[i]);
60:         tvl += vault.asset().balanceOf(address(vault)) 
61:                 * vault.assetPrice() * 1e18
62:                 / (10**vault.asset().decimals()) 
63:                 / (10**vault.oracle().decimals());
64:       }
```


</details>

## [Gas-5] Use assembly to validate msg.sender

### Resolution 
Utilizing assembly for validating `msg.sender` can potentially save gas as it allows for more direct and efficient access to Ethereum’s EVM opcodes, bypassing some of the overhead introduced by Solidity’s higher-level abstractions. However, this practice requires deep expertise in EVM, as incorrect implementation can introduce critical vulnerabilities. It is a trade-off between gas efficiency and code safety.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[22](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L22-L22)']
```solidity
22:     if (msg.sender != address(vaultManager)) revert NotVaultManager(); // <= FOUND
```


</details>

## [Gas-6] Unnecessary casting as variable is already of the same type

### Resolution 
Unnecessary casting of a variable to the same type is redundant and can contribute to gas inefficiency and code clutter. This situation commonly arises when developers, perhaps due to oversight or misunderstanding, explicitly cast a variable to its existing type. For example, casting a `uint256` variable to `uint256` again does not change its type or value but adds unnecessary operations to the code.

**Resolution**: Developers should scrutinize their code to identify and remove any unnecessary type casting. Utilizing linters or static analysis tools can aid in detecting such redundancies. Ensuring that the code is clean and efficient not only saves gas but also enhances readability and maintainability.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[119](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L119-L119)']
```solidity
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   {
127:     idToBlockOfLastDeposit[id] = block.number;
128:     Vault _vault = Vault(vault);
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
130:     _vault.deposit(id, amount);
131:   }
```


</details>

## [Gas-7] Simple checks for zero uint can be done using assembly to save gas

### Resolution 
Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations. 

**Resolution**: Implement inline assembly with Solidity's `assembly` block to perform zero checks. Ensure thorough testing and verification, as assembly lacks the safety checks of high-level Solidity, potentially introducing vulnerabilities if not used carefully.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[237](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L237-L237)']
```solidity
237:       if (_dyad == 0) return type(uint).max; // <= FOUND
```


</details>

## [Gas-8] Solidity versions 0.8.19 and above are more gas efficient

### Resolution 
Solidity version 0.8.19 introduced a array of gas optimizations which make contracts which use it more efficient. Provided compatability it may be beneficial to upgrade to this version

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L2-L2)']
```solidity
2: pragma solidity =0.8.17;
```


</details>

## [Gas-9] Constructors can be marked as payable to save deployment gas

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[11](https://github.com/code-423n4/2024-04-dyad/tree/main/src/staking/KerosineDenominator.sol#L11-L11)']
```solidity
11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }
```
['[49](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L49-L49)']
```solidity
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
['[26](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L26-L26)']
```solidity
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
['[26](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.sol#L26-L26)']
```solidity
26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager
30:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}
```
['[21](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L21-L21)']
```solidity
21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27:       dyad = _dyad;
28:   }
```


</details>

## [Gas-10] Use OZ Array.unsafeAccess() to avoid repeated array length checks

### Resolution 
The OpenZeppelin Array.unsafeAccess() method is a optimization strategy for Solidity, aimed at reducing gas costs by bypassing automatic length checks on storage array accesses. In Solidity, every access to an array element involves a hidden gas cost due to a length check, ensuring that accesses do not exceed the array bounds. However, if a developer has already verified the array's bounds earlier in the function or knows through logic that the access is safe, directly accessing the array elements without redundant length checks can save gas. This approach requires careful consideration to avoid out-of-bounds errors, as it trades off safety checks for efficiency.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[59](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/Vault.kerosine.unbounded.sol#L59-L59)']
```solidity
59:         Vault vault = Vault(vaults[i]); // <= FOUND
```


</details>

## [Gas-11] Consider pre-calculating the address of address(this) to save gas

### Resolution 
Consider saving the address(this) value within a constant using foundry's script.sol or solady's LibRlp.sol to save gas

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[144](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L144-L144)']
```solidity
144:     uint dyadMinted = dyad.mintedDyad(address(this), id); // <= FOUND
```
['[164](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L164-L164)']
```solidity
164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount; // <= FOUND
```
['[215](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L215-L215)']
```solidity
215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id)); // <= FOUND
```
['[236](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L236-L236)']
```solidity
236:       uint _dyad = dyad.mintedDyad(address(this), id); // <= FOUND
```


</details>

## [Gas-12] Public functions not called internally

### Resolution 
Public functions that aren't used internally in Solidity contracts should be made external to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for public functions. By using external visibility, developers can reduce gas consumption for external calls and ensure that the contract operates more cost-effectively for users. Moreover, setting the appropriate visibility level for functions also enhances code readability and maintainability, promoting a more secure and well-structured contract design.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[36](https://github.com/code-423n4/2024-04-dyad/tree/main/script/deploy/Deploy.V2.s.sol#L36-L36)']
```solidity
36:   function run() public returns (Contracts memory) 
```


</details>

## [Gas-13] Use constants instead of type(uint<n>).max

### Resolution 
In smart contract development, utilizing constants for known maximum or minimum values, rather than computing `type(uint<n>).max` or assuming `0` for `.min`, can significantly reduce gas costs. Constants require less runtime computation and storage, optimizing contract efficiency—a crucial strategy for developers aiming for cost-effective and performant code.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[237](https://github.com/code-423n4/2024-04-dyad/tree/main/src/core/VaultManagerV2.sol#L237-L237)']
```solidity
237:       if (_dyad == 0) return type(uint).max; // <= FOUND
```


</details>
