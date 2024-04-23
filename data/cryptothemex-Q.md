## Summary

| |Issue|Instances| Gas Savings
|-|:-|:-:|:-:|
| [[L-01](#l-01)] | `addresses` shouldn't be hard-coded | 2| 0|
| [[L-02](#l-02)] | Function calls within loops | 3| 0|
| [[L-03](#l-03)] | Loops in external functions should be avoided due to high gas costs and possible DOS | 1| 0|
| [[L-04](#l-04)] | External calls in `modifier` | 2| 0|
| [[L-05](#l-05)] | Missing `require` check while setting min/ max values | 1| 0|
| [[L-06](#l-06)] | Upgradable contracts not taken into account when making wrapped calls | 2| 0|
| [[L-07](#l-07)] | Dangerous strict equalities | 1| 0|
| [[L-08](#l-08)] | Reentrancy vulnerabilities (events) | 4| 0|
| [[L-09](#l-09)] | Uninitialized local variables | 2| 0|
| [[N-01](#n-01)] | Consider emitting an event at the end of the constructor | 5| 0|
| [[N-02](#n-02)] | Events are missing sender information | 9| 0|
| [[N-03](#n-03)] | Validate user inputs | 8| 0|
| [[N-04](#n-04)] | Conformance to Solidity naming conventions | 3| 0|
| [[N-05](#n-05)] | Unused state variable | 2| 0|
| [[N-06](#n-06)] | Constant decimal values | 8| 0|
| [[N-07](#n-07)] | Constants in comparisons should appear on the left side | 4| 0|
| [[N-08](#n-08)] | Consider using descriptive `constant`s when passing zero as a function argument | 1| 0|
| [[N-09](#n-09)] | Use of `override` is unnecessary | 2| 0|
| [[N-10](#n-10)] | Consider using a `struct` rather than having many function input parameters | 7| 0|
| [[N-11](#n-11)] | uint/int variables should have the bit size defined explicitly | 59| 0|
| [[N-12](#n-12)] | Consider using named function arguments | 6| 0|
| [[N-13](#n-13)] | Consider using named returns | 12| 0|
| [[N-14](#n-14)] | Use scratch space when building emitted events with two data arguments | 5| 75|
| [[N-15](#n-15)] | Use `do`-`while` loop | 4| 0|

### Low Risk Issues

### [L-01]<a name="l-01"></a> `addresses` shouldn't be hard-coded

Hardcoded addresses prevent the contract from upgradation, work on different chains and may brick the system.It is often better to declare `address`es as `immutable`, and assign them via constructor arguments. This allows the code to remain the same across deployments on different networks, and avoids recompilation when addresses need to change.

*There are 2 instance(s) of this issue:*

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator (src/staking/KerosineDenominator.sol#7-23) has hardcoded addresse(s) 
	- Parameters.GOERLI_OWNER (src/params/Parameters.sol#7)
	- Parameters.GOERLI_DNFT (src/params/Parameters.sol#8)
	- Parameters.GOERLI_WETH (src/params/Parameters.sol#9)
	- Parameters.GOERLI_WETH_ORACLE (src/params/Parameters.sol#10)
	- Parameters.GOERLI_FEE_RECIPIENT (src/params/Parameters.sol#12)
	- Parameters.GOERLI_VAULT_MANAGER (src/params/Parameters.sol#13)
	- Parameters.GOERLI_CHAINLINK_STETH (src/params/Parameters.sol#16)
	- Parameters.GOERLI_WSTETH (src/params/Parameters.sol#17)
	- Parameters.GOERLI_DYAD (src/params/Parameters.sol#18)
	- Parameters.GOERLI_WETH_DYAD_UNI (src/params/Parameters.sol#19)
	- Parameters.MAINNET_OWNER (src/params/Parameters.sol#22)
	- Parameters.MAINNET_DNFT (src/params/Parameters.sol#23)
	- Parameters.MAINNET_WETH (src/params/Parameters.sol#24)
	- Parameters.MAINNET_WETH_ORACLE (src/params/Parameters.sol#25)
	- Parameters.MAINNET_FEE_RECIPIENT (src/params/Parameters.sol#27)
	- Parameters.MAINNET_VAULT_MANAGER (src/params/Parameters.sol#28)
	- Parameters.MAINNET_CHAINLINK_STETH (src/params/Parameters.sol#29)
	- Parameters.MAINNET_WSTETH (src/params/Parameters.sol#30)
	- Parameters.MAINNET_DYAD (src/params/Parameters.sol#31)
	- Parameters.MAINNET_WETH_DYAD_UNI (src/params/Parameters.sol#32)
	- Parameters.MAINNET_KEROSENE (src/params/Parameters.sol#33)
	- Parameters.MAINNET_STAKING (src/params/Parameters.sol#34)
	- Parameters.MAINNET_WETH_VAULT (src/params/Parameters.sol#35)
	- Parameters.MAINNET_WSTETH_VAULT (src/params/Parameters.sol#36)
	- Parameters.MAINNET_VAULT_MANAGER_LICENSER (src/params/Parameters.sol#37)
	- Parameters.SEPOLIA_OWNER (src/params/Parameters.sol#40)
	- Parameters.SEPOLIA_WETH (src/params/Parameters.sol#42)
	- Parameters.SEPOLIA_WETH_ORACLE (src/params/Parameters.sol#43)
	- Parameters.SEPOLIA_FEE_RECIPIENT (src/params/Parameters.sol#45)
	- Parameters.SEPOLIA_CHAINLINK_STETH (src/params/Parameters.sol#49)
	- Parameters.SEPOLIA_WSTETH (src/params/Parameters.sol#50)
	- Parameters.SEPOLIA_WETH_DYAD_UNI (src/params/Parameters.sol#52)

/// @audit ****************** Affected Code *******************
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

*GitHub* : [7-23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L23)

```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit ******************* Issue Detail *******************
DeployV2 (script/deploy/Deploy.V2.s.sol#35-114) has hardcoded addresse(s) 
	- CommonBase.CONSOLE (lib/forge-std/src/Base.sol#11)
	- CommonBase.DEFAULT_TEST_CONTRACT (lib/forge-std/src/Base.sol#15)
	- ScriptBase.CREATE2_FACTORY (lib/forge-std/src/Base.sol#28)
	- Parameters.GOERLI_OWNER (src/params/Parameters.sol#7)
	- Parameters.GOERLI_DNFT (src/params/Parameters.sol#8)
	- Parameters.GOERLI_WETH (src/params/Parameters.sol#9)
	- Parameters.GOERLI_WETH_ORACLE (src/params/Parameters.sol#10)
	- Parameters.GOERLI_FEE_RECIPIENT (src/params/Parameters.sol#12)
	- Parameters.GOERLI_VAULT_MANAGER (src/params/Parameters.sol#13)
	- Parameters.GOERLI_CHAINLINK_STETH (src/params/Parameters.sol#16)
	- Parameters.GOERLI_WSTETH (src/params/Parameters.sol#17)
	- Parameters.GOERLI_DYAD (src/params/Parameters.sol#18)
	- Parameters.GOERLI_WETH_DYAD_UNI (src/params/Parameters.sol#19)
	- Parameters.MAINNET_OWNER (src/params/Parameters.sol#22)
	- Parameters.MAINNET_DNFT (src/params/Parameters.sol#23)
	- Parameters.MAINNET_WETH (src/params/Parameters.sol#24)
	- Parameters.MAINNET_WETH_ORACLE (src/params/Parameters.sol#25)
	- Parameters.MAINNET_FEE_RECIPIENT (src/params/Parameters.sol#27)
	- Parameters.MAINNET_VAULT_MANAGER (src/params/Parameters.sol#28)
	- Parameters.MAINNET_CHAINLINK_STETH (src/params/Parameters.sol#29)
	- Parameters.MAINNET_WSTETH (src/params/Parameters.sol#30)
	- Parameters.MAINNET_DYAD (src/params/Parameters.sol#31)
	- Parameters.MAINNET_WETH_DYAD_UNI (src/params/Parameters.sol#32)
	- Parameters.MAINNET_KEROSENE (src/params/Parameters.sol#33)
	- Parameters.MAINNET_STAKING (src/params/Parameters.sol#34)
	- Parameters.MAINNET_WETH_VAULT (src/params/Parameters.sol#35)
	- Parameters.MAINNET_WSTETH_VAULT (src/params/Parameters.sol#36)
	- Parameters.MAINNET_VAULT_MANAGER_LICENSER (src/params/Parameters.sol#37)
	- Parameters.SEPOLIA_OWNER (src/params/Parameters.sol#40)
	- Parameters.SEPOLIA_WETH (src/params/Parameters.sol#42)
	- Parameters.SEPOLIA_WETH_ORACLE (src/params/Parameters.sol#43)
	- Parameters.SEPOLIA_FEE_RECIPIENT (src/params/Parameters.sol#45)
	- Parameters.SEPOLIA_CHAINLINK_STETH (src/params/Parameters.sol#49)
	- Parameters.SEPOLIA_WSTETH (src/params/Parameters.sol#50)
	- Parameters.SEPOLIA_WETH_DYAD_UNI (src/params/Parameters.sol#52)

/// @audit ****************** Affected Code *******************

```

*GitHub* : [35-114](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35-L114)

### [L-02]<a name="l-02"></a> Function calls within loops

Making function calls within loops in Solidity can lead to inefficient gas usage, potential bottlenecks, and increased vulnerability to attacks. Each function call or external call consumes gas, and when executed within a loop, the gas cost multiplies, potentially causing the transaction to run out of gas or exceed block gas limits. This can result in transaction failure or unpredictable behavior.

*There are 3 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228) has function calls inside a loop: 
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#223)
	- collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare) (src/core/VaultManagerV2.sol#224)

/// @audit ************** Possible Issue Line(s) **************
	L#223,  L#224,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [205-228](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.getKeroseneValue(uint256) (src/core/VaultManagerV2.sol#269-286) has function calls inside a loop: 
	- vault = Vault(vaultsKerosene[id].at(i)) (src/core/VaultManagerV2.sol#278)

/// @audit ************** Possible Issue Line(s) **************
	L#278,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [269-286](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269-L286)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.getNonKeroseneValue(uint256) (src/core/VaultManagerV2.sol#250-267) has function calls inside a loop: 
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#259)

/// @audit ************** Possible Issue Line(s) **************
	L#259,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [250-267](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250-L267)

### [L-03]<a name="l-03"></a> Loops in external functions should be avoided due to high gas costs and possible DOS

In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. For example, Nested loops can become exceptionally gas expensive and should be used sparingly.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228) is external function and has a loop.

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [205-228](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228)

### [L-04]<a name="l-04"></a> External calls in `modifier`

External calls within modifiers can introduce unintended reentrancy risks and obscure the flow of a contract's logic. Modifiers are designed to perform checks before executing function logic, and using external calls can make the flow unpredictable due to the potential for state changes or reentrancy by the called contract. Such ambiguity makes code harder to audit and understand. To ensure clarity and security, avoid external calls in modifiers. Instead, place them in the function body, where their execution order and effects are more explicit. This practice enhances contract readability, aids auditors, and minimizes unexpected behaviors.

*There are 2 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.isValidDNft(uint256) (src/core/VaultManagerV2.sol#42-44) has external calls:-
	- dNft.ownerOf(id) == address(0) (src/core/VaultManagerV2.sol#43)

/// @audit ************** Possible Issue Line(s) **************
	L#43,  

/// @audit ****************** Affected Code *******************
  42:   modifier isValidDNft(uint id) {
  43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
  44:   }

```

*GitHub* : [42-44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42-L44)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.isDNftOwner(uint256) (src/core/VaultManagerV2.sol#39-41) has external calls:-
	- dNft.ownerOf(id) != msg.sender (src/core/VaultManagerV2.sol#40)

/// @audit ************** Possible Issue Line(s) **************
	L#40,  

/// @audit ****************** Affected Code *******************
  39:   modifier isDNftOwner(uint id) {
  40:     if (dNft.ownerOf(id) != msg.sender)   revert NotOwner();    _;
  41:   }

```

*GitHub* : [39-41](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39-L41)

### [L-05]<a name="l-05"></a> Missing `require` check while setting min/ max values

When settings min/max values, ensure there are `require` checks in place to prevent incorrect values from being set.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.setDenominator(KerosineDenominator) (src/core/Vault.kerosine.unbounded.sol#43-48) updates min/ max, but should have a `require` to prevent incorrect values from being set.

/// @audit ****************** Affected Code *******************
  43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
  44:     external 
  45:       onlyOwner
  46:   {
  47:     kerosineDenominator = _kerosineDenominator;
  48:   }

```

*GitHub* : [43-48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48)

### [L-06]<a name="l-06"></a> Upgradable contracts not taken into account when making wrapped calls

When wrapping a token address with interfaces like IERC20 for external calls, especially in the context of upgradable contracts, it's essential to account for the potential changes these tokens might undergo. Upgrades can modify a token's behavior or interface, which could introduce compatibility issues or vulnerabilities in the interacting protocol. **Recom:** To manage this risk, integrate an allowlist system in your protocol. This system would monitor for upgrades in token contracts. Upon detecting an upgrade, the corresponding token contract would be automatically removed from the allowlist, suspending its interaction with your protocol. The contract can only be re-added to the allowlist after a thorough review to confirm its continued compatibility and safety post-upgrade. This approach helps maintain a secure and adaptable protocol, ensuring it only interacts with verified, stable versions of external contracts. Regular audits and ongoing monitoring of these external contracts are vital for maintaining the integrity and security of the protocol.

*There are 2 instance(s) of this issue:*

```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit ******************* Issue Detail *******************
DeployV2.run() (script/deploy/Deploy.V2.s.sol#36-113) casts address to ERC20
	- ethVault = new Vault(vaultManager,ERC20(MAINNET_WETH),IAggregatorV3(MAINNET_WETH_ORACLE)) (script/deploy/Deploy.V2.s.sol#49-53) casts (address) to (ERC20).

/// @audit ************** Possible Issue Line(s) **************
	L#49-53,  

/// @audit ****************** Affected Code *******************
  49:     Vault ethVault = new Vault(
  50:       vaultManager,
  51:       ERC20        (MAINNET_WETH),
  52:       IAggregatorV3(MAINNET_WETH_ORACLE)
  53:     );

```

*GitHub* : [36-113](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36-L113)

```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit ******************* Issue Detail *******************
DeployV2.run() (script/deploy/Deploy.V2.s.sol#36-113) casts address to ERC20
	- ethVault = new Vault(vaultManager,ERC20(MAINNET_WETH),IAggregatorV3(MAINNET_WETH_ORACLE)) (script/deploy/Deploy.V2.s.sol#49-53) casts (address) to (ERC20).
	- wstEth = new VaultWstEth(vaultManager,ERC20(MAINNET_WSTETH),IAggregatorV3(MAINNET_CHAINLINK_STETH)) (script/deploy/Deploy.V2.s.sol#56-60) casts (address) to (ERC20).

/// @audit ************** Possible Issue Line(s) **************
	L#49-53,  L#56-60,  

/// @audit ****************** Affected Code *******************
  49:     Vault ethVault = new Vault(
  50:       vaultManager,
  51:       ERC20        (MAINNET_WETH),
  52:       IAggregatorV3(MAINNET_WETH_ORACLE)
  53:     );
  56:     VaultWstEth wstEth = new VaultWstEth(
  57:       vaultManager, 
  58:       ERC20        (MAINNET_WSTETH), 
  59:       IAggregatorV3(MAINNET_CHAINLINK_STETH)
  60:     );

```

*GitHub* : [36-113](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L36-L113)

### [L-07]<a name="l-07"></a> Dangerous strict equalities

Use of strict equalities that can be easily manipulated by an attacker.  **Recom:** Don't use strict equality and try using `>=` or `<=` to cover broader edge cases.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.withdraw(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#134-153) uses a dangerous strict equality:
	- idToBlockOfLastDeposit[id] == block.number (src/core/VaultManagerV2.sol#143)

/// @audit ************** Possible Issue Line(s) **************
	L#143,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [134-153](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L153)

### [L-08]<a name="l-08"></a> Reentrancy vulnerabilities (events)

Possible Reentrancy vulnerabilities leading to out-of-order Events.  **Recom:**  Ensure that events follow the best practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), and are emitted before external calls.

*There are 4 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
Reentrancy (events) in VaultManagerV2.mintDyad(uint256,uint256,address) (src/core/VaultManagerV2.sol#156-169):
	External calls:
	- dyad.mint(id,to,amount) (src/core/VaultManagerV2.sol#166)
	Event emitted after the call(s):
	- MintDyad(id,amount,to) (src/core/VaultManagerV2.sol#168)

/// @audit ************** Possible Issue Line(s) **************
	L#166,  L#168,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [156-169](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
Reentrancy (events) in VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228):
	External calls:
	- dyad.burn(id,msg.sender,dyad.mintedDyad(address(this),id)) (src/core/VaultManagerV2.sol#215)
	- vault.move(id,to,collateral) (src/core/VaultManagerV2.sol#225)
	Event emitted after the call(s):
	- Liquidate(id,msg.sender,to) (src/core/VaultManagerV2.sol#227)

/// @audit ************** Possible Issue Line(s) **************
	L#215,  L#225,  L#227,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [205-228](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
Reentrancy (events) in VaultManagerV2.burnDyad(uint256,uint256) (src/core/VaultManagerV2.sol#172-181):
	External calls:
	- dyad.burn(id,msg.sender,amount) (src/core/VaultManagerV2.sol#179)
	Event emitted after the call(s):
	- BurnDyad(id,amount,msg.sender) (src/core/VaultManagerV2.sol#180)

/// @audit ************** Possible Issue Line(s) **************
	L#179,  L#180,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [172-181](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L172-L181)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
Reentrancy (events) in VaultManagerV2.redeemDyad(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#184-202):
	External calls:
	- dyad.burn(id,msg.sender,amount) (src/core/VaultManagerV2.sol#193)
	- withdraw(id,vault,asset,to) (src/core/VaultManagerV2.sol#199)
		- _vault.withdraw(id,to,amount) (src/core/VaultManagerV2.sol#151)
	Event emitted after the call(s):
	- RedeemDyad(id,vault,amount,to) (src/core/VaultManagerV2.sol#200)

/// @audit ************** Possible Issue Line(s) **************
	L#193,  L#199,  L#151,  L#200,  

/// @audit ****************** Affected Code *******************
 151:     _vault.withdraw(id, to, amount);
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

*GitHub* : [184-202](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L202)

### [L-09]<a name="l-09"></a> Uninitialized local variables

Local variables without initialization may use default value and result in a wrong computation.  **Recom:** Initialize all the variables before use. If a variable is meant to be initialized to zero, explicitly set it to zero to improve code readability.

*There are 2 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.getNonKeroseneValue(uint256).usdValue (src/core/VaultManagerV2.sol#260) is a local variable never initialized

/// @audit ************** Possible Issue Line(s) **************
	L#260,  

/// @audit ****************** Affected Code *******************
 260:         uint usdValue;

```

*GitHub* : [260-260](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L260-L260)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.getKeroseneValue(uint256).usdValue (src/core/VaultManagerV2.sol#279) is a local variable never initialized

/// @audit ************** Possible Issue Line(s) **************
	L#279,  

/// @audit ****************** Affected Code *******************
 279:         uint usdValue;

```

*GitHub* : [279-279](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L279-L279)

### NonCritical Risk Issues

### [N-01]<a name="n-01"></a> Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed

*There are 5 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager) (src/core/Vault.kerosine.unbounded.sol#21-28) may emit `event` at the end of `constructor`

/// @audit ****************** Affected Code *******************
  21:   constructor(
  22:       IVaultManager   _vaultManager,
  23:       ERC20           _asset, 
  24:       Dyad            _dyad, 
  25:       KerosineManager _kerosineManager
  26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
  27:       dyad = _dyad;
  28:   }

```

*GitHub* : [21-28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L28)

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.sol#26-34) may emit `event` at the end of `constructor`

/// @audit ****************** Affected Code *******************
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

*GitHub* : [26-34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L34)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.constructor(DNft,Dyad,Licenser) (src/core/VaultManagerV2.sol#49-57) may emit `event` at the end of `constructor`

/// @audit ****************** Affected Code *******************
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

*GitHub* : [49-57](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L57)

```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.bounded.sol#17-21) may emit `event` at the end of `constructor`

/// @audit ****************** Affected Code *******************
  17:   constructor(
  18:     IVaultManager   _vaultManager,
  19:     ERC20           _asset, 
  20:     KerosineManager _kerosineManager
  21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```

*GitHub* : [17-21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator.constructor(Kerosine) (src/staking/KerosineDenominator.sol#11-15) may emit `event` at the end of `constructor`

/// @audit ****************** Affected Code *******************
  11:   constructor(
  12:     Kerosine _kerosine
  13:   ) {
  14:     kerosine = _kerosine;
  15:   }

```

*GitHub* : [11-15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L15)

### [N-02]<a name="n-02"></a> Events are missing sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

*There are 9 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.add(uint256,address) (src/core/VaultManagerV2.sol#67-78) may emit `msg.sender` in :-
	- Added(id,vault) (src/core/VaultManagerV2.sol#77)

/// @audit ************** Possible Issue Line(s) **************
	L#77,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [67-78](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67-L78)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.remove(uint256,address) (src/core/VaultManagerV2.sol#94-104) may emit `msg.sender` in :-
	- Removed(id,vault) (src/core/VaultManagerV2.sol#103)

/// @audit ************** Possible Issue Line(s) **************
	L#103,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [94-104](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94-L104)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.withdraw(uint256,address,uint256) (src/core/Vault.kerosine.unbounded.sol#30-41) may emit `msg.sender` in :-
	- Withdraw(id,to,amount) (src/core/Vault.kerosine.unbounded.sol#40)

/// @audit ************** Possible Issue Line(s) **************
	L#40,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [30-41](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L41)

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.deposit(uint256,uint256) (src/core/Vault.kerosine.sol#36-45) may emit `msg.sender` in :-
	- Deposit(id,amount) (src/core/Vault.kerosine.sol#44)

/// @audit ************** Possible Issue Line(s) **************
	L#44,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [36-45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36-L45)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.redeemDyad(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#184-202) may emit `msg.sender` in :-
	- RedeemDyad(id,vault,amount,to) (src/core/VaultManagerV2.sol#200)

/// @audit ************** Possible Issue Line(s) **************
	L#200,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [184-202](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L202)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.addKerosene(uint256,address) (src/core/VaultManagerV2.sol#80-91) may emit `msg.sender` in :-
	- Added(id,vault) (src/core/VaultManagerV2.sol#90)

/// @audit ************** Possible Issue Line(s) **************
	L#90,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [80-91](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L91)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.removeKerosene(uint256,address) (src/core/VaultManagerV2.sol#106-116) may emit `msg.sender` in :-
	- Removed(id,vault) (src/core/VaultManagerV2.sol#115)

/// @audit ************** Possible Issue Line(s) **************
	L#115,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [106-116](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L116)

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.move(uint256,uint256,uint256) (src/core/Vault.kerosine.sol#47-58) may emit `msg.sender` in :-
	- Move(from,to,amount) (src/core/Vault.kerosine.sol#57)

/// @audit ************** Possible Issue Line(s) **************
	L#57,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [47-58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47-L58)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.mintDyad(uint256,uint256,address) (src/core/VaultManagerV2.sol#156-169) may emit `msg.sender` in :-
	- MintDyad(id,amount,to) (src/core/VaultManagerV2.sol#168)

/// @audit ************** Possible Issue Line(s) **************
	L#168,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [156-169](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169)

### [N-03]<a name="n-03"></a> Validate user inputs

There are no validations done on the arguments below. Consider that the Solidity [documentation](https://docs.soliditylang.org/en/latest/control-structures.html#panic-via-assert-and-error-via-require) states that `Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix`. This means that there should be explicit checks for expected ranges of inputs. Underflows/overflows result in panics should not be used as range checks, and allowing funds to be sent to  `0x0`, which is the default value of address variables and has many gotchas, should be avoided.

*There are 8 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.mintDyad(uint256,uint256,address) (src/core/VaultManagerV2.sol#156-169) does not validate following parameters:- 
	- VaultManagerV2.mintDyad(uint256,uint256,address).id (src/core/VaultManagerV2.sol#157)

/// @audit ************** Possible Issue Line(s) **************
	L#157,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [156-169](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.addKerosene(uint256,address) (src/core/VaultManagerV2.sol#80-91) does not validate following parameters:- 
	- VaultManagerV2.addKerosene(uint256,address).id (src/core/VaultManagerV2.sol#81)
	- VaultManagerV2.addKerosene(uint256,address).vault (src/core/VaultManagerV2.sol#82)

/// @audit ************** Possible Issue Line(s) **************
	L#81,  L#82,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [80-91](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80-L91)

```solidity
File: src/core/KerosineManager.sol

/// @audit ******************* Issue Detail *******************
KerosineManager.add(address) (src/core/KerosineManager.sol#18-26) does not validate following parameters:- 
	- KerosineManager.add(address).vault (src/core/KerosineManager.sol#19)

/// @audit ************** Possible Issue Line(s) **************
	L#19,  

/// @audit ****************** Affected Code *******************
  18:   function add(
  19:     address vault
  20:   ) 
  21:     external 
  22:       onlyOwner
  23:   {
  24:     if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
  25:     if (!vaults.add(vault))            revert VaultAlreadyAdded();
  26:   }

```

*GitHub* : [18-26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18-L26)

```solidity
File: src/core/KerosineManager.sol

/// @audit ******************* Issue Detail *******************
KerosineManager.remove(address) (src/core/KerosineManager.sol#28-35) does not validate following parameters:- 
	- KerosineManager.remove(address).vault (src/core/KerosineManager.sol#29)

/// @audit ************** Possible Issue Line(s) **************
	L#29,  

/// @audit ****************** Affected Code *******************
  28:   function remove(
  29:     address vault
  30:   ) 
  31:     external 
  32:       onlyOwner
  33:   {
  34:     if (!vaults.remove(vault)) revert VaultNotFound();
  35:   }

```

*GitHub* : [28-35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28-L35)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.remove(uint256,address) (src/core/VaultManagerV2.sol#94-104) does not validate following parameters:- 
	- VaultManagerV2.remove(uint256,address).id (src/core/VaultManagerV2.sol#95)
	- VaultManagerV2.remove(uint256,address).vault (src/core/VaultManagerV2.sol#96)

/// @audit ************** Possible Issue Line(s) **************
	L#95,  L#96,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [94-104](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94-L104)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.add(uint256,address) (src/core/VaultManagerV2.sol#67-78) does not validate following parameters:- 
	- VaultManagerV2.add(uint256,address).id (src/core/VaultManagerV2.sol#68)
	- VaultManagerV2.add(uint256,address).vault (src/core/VaultManagerV2.sol#69)

/// @audit ************** Possible Issue Line(s) **************
	L#68,  L#69,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [67-78](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67-L78)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.withdraw(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#134-153) does not validate following parameters:- 
	- VaultManagerV2.withdraw(uint256,address,uint256,address).id (src/core/VaultManagerV2.sol#135)

/// @audit ************** Possible Issue Line(s) **************
	L#135,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [134-153](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L153)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.removeKerosene(uint256,address) (src/core/VaultManagerV2.sol#106-116) does not validate following parameters:- 
	- VaultManagerV2.removeKerosene(uint256,address).id (src/core/VaultManagerV2.sol#107)
	- VaultManagerV2.removeKerosene(uint256,address).vault (src/core/VaultManagerV2.sol#108)

/// @audit ************** Possible Issue Line(s) **************
	L#107,  L#108,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [106-116](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106-L116)

### [N-04]<a name="n-04"></a> Conformance to Solidity naming conventions

Solidity defines a [naming convention](https://solidity.readthedocs.io/en/v0.4.25/style-guide.html#naming-conventions) that should be followed.  **Recom:** Follow the Solidity [naming convention](https://solidity.readthedocs.io/en/v0.4.25/style-guide.html#naming-conventions).

*There are 3 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
Parameter BoundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault)._unboundedKerosineVault (src/core/Vault.kerosine.bounded.sol#24) is not in mixedCase

/// @audit ************** Possible Issue Line(s) **************
	L#24,  

/// @audit ****************** Affected Code *******************
  24:     UnboundedKerosineVault _unboundedKerosineVault

```

*GitHub* : [24-24](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L24-L24)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
Parameter VaultManagerV2.setKeroseneManager(KerosineManager)._keroseneManager (src/core/VaultManagerV2.sol#59) is not in mixedCase

/// @audit ************** Possible Issue Line(s) **************
	L#59,  

/// @audit ****************** Affected Code *******************
  59:   function setKeroseneManager(KerosineManager _keroseneManager) 

```

*GitHub* : [59-59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L59)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
Parameter UnboundedKerosineVault.setDenominator(KerosineDenominator)._kerosineDenominator (src/core/Vault.kerosine.unbounded.sol#43) is not in mixedCase

/// @audit ************** Possible Issue Line(s) **************
	L#43,  

/// @audit ****************** Affected Code *******************
  43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

```

*GitHub* : [43-43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L43)

### [N-05]<a name="n-05"></a> Unused state variable

Unused state variable.  **Recom:** Remove unused state variables.

*There are 2 instance(s) of this issue:*

```solidity
File: script/deploy/Deploy.V2.s.sol

/// @audit ******************* Issue Detail *******************
DeployV2 (script/deploy/Deploy.V2.s.sol#35-114) has following non-used variables 
	- Parameters.SEPOLIA_WETH_ORACLE (src/params/Parameters.sol#43)

/// @audit ****************** Affected Code *******************

```

*GitHub* : [35-114](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L35-L114)

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator (src/staking/KerosineDenominator.sol#7-23) has following non-used variables 
	- Parameters.MAINNET_KEROSENE (src/params/Parameters.sol#33)

/// @audit ****************** Affected Code *******************
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

*GitHub* : [7-23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7-L23)

### [N-06]<a name="n-06"></a> Constant decimal values

The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations. Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts. This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under/overflows that could jeopardize contract integrity and user funds.

*There are 8 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;

```



*GitHub* : [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L66-L66)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

67:       return numerator * 1e8 / denominator;

```



*GitHub* : [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67-L67)

```solidity
File: src/core/VaultManagerV2.sol

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

198:                     / 1e18;

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

```


*GitHub* : [25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26-L26), [198](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L198-L198), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217-L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L218-L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L219-L219)

### [N-07]<a name="n-07"></a> Constants in comparisons should appear on the left side

Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html) where the first '!', '>', '<', or '=' at the beginning of the operator is missing.

*There are 4 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

237:       if (_dyad == 0) return type(uint).max;

```


*GitHub* : [101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101-L101), [113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113-L113), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217-L217), [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237-L237)

### [N-08]<a name="n-08"></a> Consider using descriptive `constant`s when passing zero as a function argument

Passing zero as a function argument can sometimes result in a security issue (e.g. passing zero as the slippage parameter). Consider using a `constant` variable with a descriptive name, so it's clear that the argument is intentionally being used, and for the right reasons.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

```


*GitHub* : [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L43-L43)

### [N-09]<a name="n-09"></a> Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are 2 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice() 
        public 
        view 
        override

```



*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L47)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice() 
        public 
        view 
        override

```


*GitHub* : [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L53)

### [N-10]<a name="n-10"></a> Consider using a `struct` rather than having many function input parameters

Often times, a subset of the parameters would be more clear if they were passed as a struct.

*There are 7 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.bounded.sol

32:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 

```



*GitHub* : [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32-L36)

```solidity
File: src/core/Vault.kerosine.sol

47:   function move(
        uint from,
        uint to,
        uint amount
      )

```



*GitHub* : [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47-L51)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(
        uint    id,
        address to,
        uint    amount
      ) 

```



*GitHub* : [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30-L34)

```solidity
File: src/core/VaultManagerV2.sol

119:   function deposit(
         uint    id,
         address vault,
         uint    amount
       ) 

134:   function withdraw(
         uint    id,
         address vault,
         uint    amount,
         address to
       ) 

156:   function mintDyad(
         uint    id,
         uint    amount,
         address to
       )

184:   function redeemDyad(
         uint    id,
         address vault,
         uint    amount,
         address to
       )

```


*GitHub* : [119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L123), [134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134-L139), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L160), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184-L189)

### [N-11]<a name="n-11"></a> uint/int variables should have the bit size defined explicitly

Instead of using uint to declare uint258, explicitly define uint258 to ensure there is no confusion.

*There are 59 instance(s) of this issue:*

```solidity
File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```



*GitHub* : [14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14-L14)

```solidity
File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

33:     uint    id,

35:     uint    amount

```



*GitHub* : [13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13-L13), [33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L33-L33), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L35-L35)

```solidity
File: src/core/Vault.kerosine.sol

37:     uint id,

38:     uint amount

48:     uint from,

49:     uint to,

50:     uint amount

61:     uint id

```



*GitHub* : [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L37-L37), [38](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L38-L38), [48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L48-L48), [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L49-L49), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L50-L50), [61](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L61-L61)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

31:     uint    id,

33:     uint    amount

55:       uint tvl;

57:       uint numberOfVaults = vaults.length;

65:       uint numerator   = tvl - dyad.totalSupply();

66:       uint denominator = kerosineDenominator.denominator();

```



*GitHub* : [31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L31-L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L33-L33), [55](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L55-L55), [57](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L57-L57), [65](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L65-L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L66-L66)

```solidity
File: src/core/VaultManagerV2.sol

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

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

195:       uint asset = amount 

206:     uint id,

207:     uint to

213:       uint cr = collatRatio(id);

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

221:       uint numberOfVaults = vaults[id].length();

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

231:     uint id

236:       uint _dyad = dyad.mintedDyad(address(this), id);

242:     uint id

251:     uint id

256:       uint totalUsdValue;

257:       uint numberOfVaults = vaults[id].length(); 

260:         uint usdValue;

270:     uint id

275:       uint totalUsdValue;

276:       uint numberOfVaults = vaultsKerosene[id].length(); 

279:         uint usdValue;

291:     uint id

300:     uint    id,

```


*GitHub* : [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22-L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23-L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25-L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26-L26), [68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L68-L68), [81](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L81-L81), [95](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L95-L95), [107](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L107-L107), [120](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L120-L120), [122](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L122-L122), [135](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L135-L135), [137](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L137-L137), [144](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L144-L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L146), [157](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L157-L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L158-L158), [164](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L164-L164), [173](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L173-L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L174-L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L185-L185), [187](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L187-L187), [195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L195), [206](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L206-L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L207-L207), [213](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L213-L213), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217-L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L218-L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L219-L219), [221](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L221-L221), [224](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L224-L224), [231](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L231-L231), [236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236-L236), [242](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L242-L242), [251](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L251-L251), [256](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L256-L256), [257](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L257-L257), [260](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L260-L260), [270](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L270-L270), [275](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L275-L275), [276](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L276-L276), [279](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L279-L279), [291](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L291-L291), [300](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L300-L300)

### [N-12]<a name="n-12"></a> Consider using named function arguments

When calling functions in external contracts with multiple arguments, consider using [named](https://docs.soliditylang.org/en/latest/control-structures.html#function-calls-with-named-parameters) function parameters, rather than positional ones.

*There are 6 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

151:     _vault.withdraw(id, to, amount);

166:     dyad.mint(id, to, amount);

179:     dyad.burn(id, msg.sender, amount);

193:       dyad.burn(id, msg.sender, amount);

215:       dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

225:           vault.move(id, to, collateral);

```


*GitHub* : [151](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L151-L151), [166](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L166-L166), [179](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L179-L179), [193](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L193-L193), [215](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L215-L215), [225](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L225-L225)

### [N-13]<a name="n-13"></a> Consider using named returns

Using named returns in Solidity functions enhances code readability and clarity. By explicitly naming return variables in the function signature, developers can document what each return value represents, making the code easier to understand and maintain. This practice can also slightly optimize gas usage by avoiding extra variable declarations.

*There are 12 instance(s) of this issue:*

```solidity
File: src/core/KerosineManager.sol

49:     returns (bool) {

```



*GitHub* : [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L49-L49)

```solidity
File: src/core/Vault.kerosine.bounded.sol

48:     returns (uint) {

```



*GitHub* : [48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L48-L48)

```solidity
File: src/core/Vault.kerosine.sol

65:     returns (uint) {

73:     returns (uint); 

```



*GitHub* : [65](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L65-L65), [73](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L73-L73)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

54:     returns (uint) {

```



*GitHub* : [54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L54-L54)

```solidity
File: src/core/VaultManagerV2.sol

192:     returns (uint) { 

235:     returns (uint) {

246:     returns (uint) {

255:     returns (uint) {

274:     returns (uint) {

305:     returns (bool) {

```



*GitHub* : [192](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L192-L192), [235](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L235-L235), [246](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L246-L246), [255](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L255-L255), [274](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L274-L274), [305](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L305-L305)

```solidity
File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17-L17)

### [N-14]<a name="n-14"></a> Use scratch space when building emitted events with two data arguments

Using the [scratch space](https://gist.github.com/IllIllI000/87c4f03139fa03780fa548b8e4b02b5b) for more than one, but at most two words worth of data (non-indexed arguments) will save gas over needing Solidity's abi memory expansion used for emitting normally.

*There are 5 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.sol

44:     emit Deposit(id, amount);

```



*GitHub* : [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L44-L44)

```solidity
File: src/core/VaultManagerV2.sol

77:     emit Added(id, vault);

90:     emit Added(id, vault);

103:     emit Removed(id, vault);

115:     emit Removed(id, vault);

```


*GitHub* : [77](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L77-L77), [90](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L90-L90), [103](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L103-L103), [115](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L115-L115)

### [N-15]<a name="n-15"></a> Use `do`-`while` loop

`do`-`while` is cheaper than `for`-loops when the initial check can be skipped. 

`for (uint256 i; i < len; ++i){ ... }` -> `do { ...; ++i } while (i < len);`

*There are 4 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```



*GitHub* : [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58-L58)

```solidity
File: src/core/VaultManagerV2.sol

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```


*GitHub* : [222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222-L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258-L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277-L277)
