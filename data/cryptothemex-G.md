## Summary

| |Issue|Instances| Gas Savings
|-|:-|:-:|:-:|
| [[G-01](#g-01)] | Multiple accesses of a mapping/array should use a local variable cache | 5| 0|
| [[G-02](#g-02)] | Constructors can be marked `payable` | 5| 105|
| [[G-03](#g-03)] | Division which can not overflow | 4| 340|
| [[G-04](#g-04)] | Use assembly to emit events | 11| 418|
| [[G-05](#g-05)] | Emit event in setter function only if the state variable was changed | 2| 0|
| [[G-06](#g-06)] | Using Storage Instead of Memory for structs/arrays Saves Gas | 1| 4200|
| [[G-07](#g-07)] | Functions guaranteed to revert when called by normal users can be marked `payable` | 4| 0|
| [[G-08](#g-08)] | if variable is casted more than once, consider caching the result to save gas | 1| 0|
| [[G-09](#g-09)] | Inefficient Parameter Storage | 8| 400|
| [[G-10](#g-10)] | Avoid updating storage when the value hasn't changed | 3| 2400|
| [[G-11](#g-11)] | Solidity versions 0.8.19 and above are more gas efficient | 6| 0|
| [[G-12](#g-12)] | Use assembly to write address storage values | 1| 77|
| [[G-13](#g-13)] | State variable read in a loop | 3| 0|
| [[G-14](#g-14)] | Unnecessary casting as variable is already of the same type | 1| 0|
| [[G-15](#g-15)] | State variables that could be declared immutable | 1| 0|
| [[G-16](#g-16)] | checks for zero uint should be done using assembly to save gas | 1| 30|
| [[G-17](#g-17)] | `>=` costs less gas than `>` | 11| 33|
| [[G-18](#g-18)] | Counting down in for statements is more gas efficient | 4| 120|
| [[G-19](#g-19)] | Avoid transferring amounts of zero in order to save gas | 1| 100|

### Gas Risk Issues

### [G-01]<a name="g-01"></a> Multiple accesses of a mapping/array should use a local variable cache

The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's keccak256 hash (`Gkeccak256` - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

*There are 5 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.add(uint256,address) (src/core/VaultManagerV2.sol#67-78) should cache `vaults[id]` :-
	- vaults[id].length() >= MAX_VAULTS (src/core/VaultManagerV2.sol#74)
	- ! vaults[id].add(vault) (src/core/VaultManagerV2.sol#76)

/// @audit ************** Possible Issue Line(s) **************
	L#74,  L#76,  

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
VaultManagerV2.getNonKeroseneValue(uint256) (src/core/VaultManagerV2.sol#250-267) should cache `vaults[id]` :-
	- numberOfVaults = vaults[id].length() (src/core/VaultManagerV2.sol#257)
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#259)

/// @audit ************** Possible Issue Line(s) **************
	L#257,  L#259,  

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

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.addKerosene(uint256,address) (src/core/VaultManagerV2.sol#80-91) should cache `vaultsKerosene[id]` :-
	- vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE (src/core/VaultManagerV2.sol#87)
	- ! vaultsKerosene[id].add(vault) (src/core/VaultManagerV2.sol#89)

/// @audit ************** Possible Issue Line(s) **************
	L#87,  L#89,  

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
VaultManagerV2.getKeroseneValue(uint256) (src/core/VaultManagerV2.sol#269-286) should cache `vaultsKerosene[id]` :-
	- numberOfVaults = vaultsKerosene[id].length() (src/core/VaultManagerV2.sol#276)
	- vault = Vault(vaultsKerosene[id].at(i)) (src/core/VaultManagerV2.sol#278)

/// @audit ************** Possible Issue Line(s) **************
	L#276,  L#278,  

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
VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228) should cache `vaults[id]` :-
	- numberOfVaults = vaults[id].length() (src/core/VaultManagerV2.sol#221)
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#223)

/// @audit ************** Possible Issue Line(s) **************
	L#221,  L#223,  

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

### [G-02]<a name="g-02"></a> Constructors can be marked `payable`

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

*There are 5 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager) (src/core/Vault.kerosine.unbounded.sol#21-28) can be payable.

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
KerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.sol#26-34) can be payable.

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
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.bounded.sol#17-21) can be payable.

/// @audit ****************** Affected Code *******************
  17:   constructor(
  18:     IVaultManager   _vaultManager,
  19:     ERC20           _asset, 
  20:     KerosineManager _kerosineManager
  21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```

*GitHub* : [17-21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.constructor(DNft,Dyad,Licenser) (src/core/VaultManagerV2.sol#49-57) can be payable.

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
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator.constructor(Kerosine) (src/staking/KerosineDenominator.sol#11-15) can be payable.

/// @audit ****************** Affected Code *******************
  11:   constructor(
  12:     Kerosine _kerosine
  13:   ) {
  14:     kerosine = _kerosine;
  15:   }

```

*GitHub* : [11-15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L15)

### [G-03]<a name="g-03"></a> Division which can not overflow

Division operations on unsigned integers should be `unchecked` to save gas since they cannot overflow or underflow. Because unsigned integers cannot have negative values, execution of division operations outside `unchecked` blocks adds nothing but overhead. Saves about 85 gas.

*There are 4 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.getUsdValue(uint256) (src/core/Vault.kerosine.sol#60-67) perform division which can not overflow (can use unchecked) :-
	- id2asset[id] * assetPrice() / 1e8 (src/core/Vault.kerosine.sol#66)

/// @audit ************** Possible Issue Line(s) **************
	L#66,  

/// @audit ****************** Affected Code *******************
  60:   function getUsdValue(
  61:     uint id
  62:   )
  63:     public
  64:     view 
  65:     returns (uint) {
  66:       return id2asset[id] * assetPrice() / 1e8;
  67:   }

```

*GitHub* : [60-67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60-L67)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.redeemDyad(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#184-202) perform division which can not overflow (can use unchecked) :-
	- asset = amount * (10 ** (_vault.oracle().decimals() + _vault.asset().decimals())) / _vault.assetPrice() / 1e18 (src/core/VaultManagerV2.sol#195-198)

/// @audit ************** Possible Issue Line(s) **************
	L#195-198,  

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
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.assetPrice() (src/core/Vault.kerosine.unbounded.sol#50-68) perform division which can not overflow (can use unchecked) :-
	- tvl += vault.asset().balanceOf(address(vault)) * vault.assetPrice() * 1e18 / (10 ** vault.asset().decimals()) / (10 ** vault.oracle().decimals()) (src/core/Vault.kerosine.unbounded.sol#60-63)
	- numerator * 1e8 / denominator (src/core/Vault.kerosine.unbounded.sol#67)

/// @audit ************** Possible Issue Line(s) **************
	L#60-63,  L#67,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [50-68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L68)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.withdraw(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#134-153) perform division which can not overflow (can use unchecked) :-
	- value = amount * _vault.assetPrice() * 1e18 / 10 ** _vault.oracle().decimals() / 10 ** _vault.asset().decimals() (src/core/VaultManagerV2.sol#146-149)

/// @audit ************** Possible Issue Line(s) **************
	L#146-149,  

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

### [G-04]<a name="g-04"></a> Use assembly to emit events

With the use of inline assembly in Solidity, we can take advantage of low-level features like scratch space and the free memory pointer, offering more gas-efficient ways of emitting events. The scratch space is a certain area of memory where we can temporarily store data, and the free memory pointer indicates the next available memory slot. Using these, we can efficiently assemble event data without incurring additional memory expansion costs. However, safety is paramount: to avoid overwriting or leakage, we must cache the free memory pointer before use and restore it afterward, ensuring that it points to the correct memory location post-operation.

*There are 11 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.redeemDyad(uint256,address,uint256,address) (src/core/VaultManagerV2.sol#184-202) should emit event(s) using assembly :-
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
VaultManagerV2.addKerosene(uint256,address) (src/core/VaultManagerV2.sol#80-91) should emit event(s) using assembly :-
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
VaultManagerV2.mintDyad(uint256,uint256,address) (src/core/VaultManagerV2.sol#156-169) should emit event(s) using assembly :-
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

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228) should emit event(s) using assembly :-
	- Liquidate(id,msg.sender,to) (src/core/VaultManagerV2.sol#227)

/// @audit ************** Possible Issue Line(s) **************
	L#227,  

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
VaultManagerV2.burnDyad(uint256,uint256) (src/core/VaultManagerV2.sol#172-181) should emit event(s) using assembly :-
	- BurnDyad(id,amount,msg.sender) (src/core/VaultManagerV2.sol#180)

/// @audit ************** Possible Issue Line(s) **************
	L#180,  

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
VaultManagerV2.remove(uint256,address) (src/core/VaultManagerV2.sol#94-104) should emit event(s) using assembly :-
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
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.removeKerosene(uint256,address) (src/core/VaultManagerV2.sol#106-116) should emit event(s) using assembly :-
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
KerosineVault.deposit(uint256,uint256) (src/core/Vault.kerosine.sol#36-45) should emit event(s) using assembly :-
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
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.move(uint256,uint256,uint256) (src/core/Vault.kerosine.sol#47-58) should emit event(s) using assembly :-
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
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.withdraw(uint256,address,uint256) (src/core/Vault.kerosine.unbounded.sol#30-41) should emit event(s) using assembly :-
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
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.add(uint256,address) (src/core/VaultManagerV2.sol#67-78) should emit event(s) using assembly :-
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

### [G-05]<a name="g-05"></a> Emit event in setter function only if the state variable was changed

Emitting events in setter functions of smart contracts only when state variables change saves gas. This is because emitting events consumes gas, and unnecessary events, where no actual state change occurs, lead to wasteful consumption.

*There are 2 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.addKerosene(uint256,address) (src/core/VaultManagerV2.sol#80-91) should emit event only if state variable(s) changed :-
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
VaultManagerV2.add(uint256,address) (src/core/VaultManagerV2.sol#67-78) should emit event only if state variable(s) changed :-
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

### [G-06]<a name="g-06"></a> Using Storage Instead of Memory for structs/arrays Saves Gas

When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct / array to be read from storage. This incurs a Gcoldsload (2100 gas) for each field of the struct / array. If the fields are read from the new memory variable, they incur an additional MLOAD, which is more expensive than a simple stack read.

Instead of declaring the variable with the memory keyword, a more cost-effective approach is to declare the variable with the storage keyword. In this case, you can cache any fields that need to be re-read in stack variables. This approach significantly reduces gas costs, as you only incur the Gcoldsload for the fields actually read.

The only scenario where it makes sense to read the whole struct / array into a memory variable is if the full struct / array is being returned by the function or passed to a function that requires memory. Additionally, if the array / struct is being read from another memory array / struct, using a memory variable may be appropriate.

By carefully considering the storage and memory usage in your contract, you can optimize gas costs and improve the efficiency of your smart contract operations.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.assetPrice() (src/core/Vault.kerosine.unbounded.sol#50-68) should use storage instead of memory for :- 
	- vaults = kerosineManager.getVaults() (src/core/Vault.kerosine.unbounded.sol#56)

/// @audit ************** Possible Issue Line(s) **************
	L#56,  

/// @audit ****************** Affected Code *******************
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

```

*GitHub* : [50-68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50-L68)

### [G-07]<a name="g-07"></a> Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as `onlyOwner` is used, or a function checks `msg.sender` some other way, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are `CALLVALUE`(2),`DUP1`(3),`ISZERO`(3),`PUSH2`(3),`JUMPI`(10),`PUSH1`(3),`DUP1`(3),`REVERT`(0),`JUMPDEST`(1),`POP`(2), which costs an average of about **21 gas per call** to the function, in addition to the extra deployment cost

*There are 4 instance(s) of this issue:*

```solidity
File: src/core/KerosineManager.sol

/// @audit ******************* Issue Detail *******************
KerosineManager.add(address) (src/core/KerosineManager.sol#18-26) can be marked `payable`.

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
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault) (src/core/Vault.kerosine.bounded.sol#23-30) can be marked `payable`.

/// @audit ****************** Affected Code *******************
  23:   function setUnboundedKerosineVault(
  24:     UnboundedKerosineVault _unboundedKerosineVault
  25:   )
  26:     external
  27:     onlyOwner
  28:   {
  29:     unboundedKerosineVault = _unboundedKerosineVault;
  30:   }

```

*GitHub* : [23-30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30)

```solidity
File: src/core/KerosineManager.sol

/// @audit ******************* Issue Detail *******************
KerosineManager.remove(address) (src/core/KerosineManager.sol#28-35) can be marked `payable`.

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
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.setDenominator(KerosineDenominator) (src/core/Vault.kerosine.unbounded.sol#43-48) can be marked `payable`.

/// @audit ****************** Affected Code *******************
  43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
  44:     external 
  45:       onlyOwner
  46:   {
  47:     kerosineDenominator = _kerosineDenominator;
  48:   }

```

*GitHub* : [43-48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48)

### [G-08]<a name="g-08"></a> if variable is casted more than once, consider caching the result to save gas

Casting values multiple times in Solidity can be gas-inefficient. When a value undergoes repeated type conversions, the EVM must execute additional operations for each cast, consuming more gas than necessary. To optimize for gas efficiency, cache the result of the initial cast in a local variable and reuse it, rather than performing multiple casts. This not only conserves gas but also enhances code readability, reducing potential error points. For example, instead of repeatedly casting an `address` to `uint256`, cast once, store the result in a local variable, and reference that variable in subsequent operations.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.deposit(uint256,address,uint256) (src/core/VaultManagerV2.sol#119-131) casts (address vault) multiple time(s) :-
	- _vault = Vault(vault) (src/core/VaultManagerV2.sol#128)
	- _vault.asset().safeTransferFrom(msg.sender,address(vault),amount) (src/core/VaultManagerV2.sol#129)

/// @audit ************** Possible Issue Line(s) **************
	L#128,  L#129,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [119-131](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L131)

### [G-09]<a name="g-09"></a> Inefficient Parameter Storage

When passing function parameters, using the `calldata` area instead of `memory` can improve gas efficiency. `Calldata` is a read-only area where function arguments and external function calls' parameters are stored.

By using `calldata` for function parameters, you avoid unnecessary gas costs associated with copying data from calldata to `memory`. This is particularly beneficial when the parameter is read-only and is not modified during the function call.

*There are 8 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
KerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.sol#26-34) should use calldata instead of memory for :- 
	- KerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._vaultManager (src/core/Vault.kerosine.sol#27)
	- KerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._asset (src/core/Vault.kerosine.sol#28)
	- KerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._kerosineManager (src/core/Vault.kerosine.sol#29)

/// @audit ************** Possible Issue Line(s) **************
	L#27,  L#28,  L#29,  

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
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager) (src/core/Vault.kerosine.bounded.sol#17-21) should use calldata instead of memory for :- 
	- BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._vaultManager (src/core/Vault.kerosine.bounded.sol#18)
	- BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._asset (src/core/Vault.kerosine.bounded.sol#19)
	- BoundedKerosineVault.constructor(IVaultManager,ERC20,KerosineManager)._kerosineManager (src/core/Vault.kerosine.bounded.sol#20)

/// @audit ************** Possible Issue Line(s) **************
	L#18,  L#19,  L#20,  

/// @audit ****************** Affected Code *******************
  17:   constructor(
  18:     IVaultManager   _vaultManager,
  19:     ERC20           _asset, 
  20:     KerosineManager _kerosineManager
  21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```

*GitHub* : [17-21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.setDenominator(KerosineDenominator) (src/core/Vault.kerosine.unbounded.sol#43-48) should use calldata instead of memory for :- 
	- UnboundedKerosineVault.setDenominator(KerosineDenominator)._kerosineDenominator (src/core/Vault.kerosine.unbounded.sol#43)

/// @audit ************** Possible Issue Line(s) **************
	L#43,  

/// @audit ****************** Affected Code *******************
  43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
  44:     external 
  45:       onlyOwner
  46:   {
  47:     kerosineDenominator = _kerosineDenominator;
  48:   }

```

*GitHub* : [43-48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.setKeroseneManager(KerosineManager) (src/core/VaultManagerV2.sol#59-64) should use calldata instead of memory for :- 
	- VaultManagerV2.setKeroseneManager(KerosineManager)._keroseneManager (src/core/VaultManagerV2.sol#59)

/// @audit ************** Possible Issue Line(s) **************
	L#59,  

/// @audit ****************** Affected Code *******************
  59:   function setKeroseneManager(KerosineManager _keroseneManager) 
  60:     external
  61:       initializer 
  62:     {
  63:       keroseneManager = _keroseneManager;
  64:   }

```

*GitHub* : [59-64](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L64)

```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault) (src/core/Vault.kerosine.bounded.sol#23-30) should use calldata instead of memory for :- 
	- BoundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault)._unboundedKerosineVault (src/core/Vault.kerosine.bounded.sol#24)

/// @audit ************** Possible Issue Line(s) **************
	L#24,  

/// @audit ****************** Affected Code *******************
  23:   function setUnboundedKerosineVault(
  24:     UnboundedKerosineVault _unboundedKerosineVault
  25:   )
  26:     external
  27:     onlyOwner
  28:   {
  29:     unboundedKerosineVault = _unboundedKerosineVault;
  30:   }

```

*GitHub* : [23-30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.constructor(DNft,Dyad,Licenser) (src/core/VaultManagerV2.sol#49-57) should use calldata instead of memory for :- 
	- VaultManagerV2.constructor(DNft,Dyad,Licenser)._dNft (src/core/VaultManagerV2.sol#50)
	- VaultManagerV2.constructor(DNft,Dyad,Licenser)._dyad (src/core/VaultManagerV2.sol#51)
	- VaultManagerV2.constructor(DNft,Dyad,Licenser)._licenser (src/core/VaultManagerV2.sol#52)

/// @audit ************** Possible Issue Line(s) **************
	L#50,  L#51,  L#52,  

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
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator.constructor(Kerosine) (src/staking/KerosineDenominator.sol#11-15) should use calldata instead of memory for :- 
	- KerosineDenominator.constructor(Kerosine)._kerosine (src/staking/KerosineDenominator.sol#12)

/// @audit ************** Possible Issue Line(s) **************
	L#12,  

/// @audit ****************** Affected Code *******************
  11:   constructor(
  12:     Kerosine _kerosine
  13:   ) {
  14:     kerosine = _kerosine;
  15:   }

```

*GitHub* : [11-15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L15)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager) (src/core/Vault.kerosine.unbounded.sol#21-28) should use calldata instead of memory for :- 
	- UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager)._vaultManager (src/core/Vault.kerosine.unbounded.sol#22)
	- UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager)._asset (src/core/Vault.kerosine.unbounded.sol#23)
	- UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager)._dyad (src/core/Vault.kerosine.unbounded.sol#24)
	- UnboundedKerosineVault.constructor(IVaultManager,ERC20,Dyad,KerosineManager)._kerosineManager (src/core/Vault.kerosine.unbounded.sol#25)

/// @audit ************** Possible Issue Line(s) **************
	L#22,  L#23,  L#24,  L#25,  

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

### [G-10]<a name="g-10"></a> Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**)

*There are 3 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.setKeroseneManager(KerosineManager) (src/core/VaultManagerV2.sol#59-64) should only update if value changes.

/// @audit ****************** Affected Code *******************
  59:   function setKeroseneManager(KerosineManager _keroseneManager) 
  60:     external
  61:       initializer 
  62:     {
  63:       keroseneManager = _keroseneManager;
  64:   }

```

*GitHub* : [59-64](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L64)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
UnboundedKerosineVault.setDenominator(KerosineDenominator) (src/core/Vault.kerosine.unbounded.sol#43-48) should only update if value changes.

/// @audit ****************** Affected Code *******************
  43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
  44:     external 
  45:       onlyOwner
  46:   {
  47:     kerosineDenominator = _kerosineDenominator;
  48:   }

```

*GitHub* : [43-48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48)

```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
BoundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault) (src/core/Vault.kerosine.bounded.sol#23-30) should only update if value changes.

/// @audit ****************** Affected Code *******************
  23:   function setUnboundedKerosineVault(
  24:     UnboundedKerosineVault _unboundedKerosineVault
  25:   )
  26:     external
  27:     onlyOwner
  28:   {
  29:     unboundedKerosineVault = _unboundedKerosineVault;
  30:   }

```

*GitHub* : [23-30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30)

### [G-11]<a name="g-11"></a> Solidity versions 0.8.19 and above are more gas efficient

Solidity version 0.8.19 introduced a array of gas optimizations which make contracts which use it more efficient. Provided compatability it may be beneficial to upgrade to this version

*There are 6 instance(s) of this issue:*

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/staking/KerosineDenominator.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L2-L2)

```solidity
File: src/core/KerosineManager.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/core/KerosineManager.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L2-L2)

```solidity
File: src/core/Vault.kerosine.unbounded.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/core/Vault.kerosine.unbounded.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L2-L2)

```solidity
File: src/core/Vault.kerosine.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/core/Vault.kerosine.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L2-L2)

```solidity
File: src/core/Vault.kerosine.bounded.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/core/Vault.kerosine.bounded.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L2-L2)

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
=0.8.17 (src/core/VaultManagerV2.sol#2) version lesser than 0.8.19:

/// @audit ************** Possible Issue Line(s) **************
	L#2,  

/// @audit ****************** Affected Code *******************
   2: pragma solidity =0.8.17;

```

*GitHub* : [2-2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L2-L2)

### [G-12]<a name="g-12"></a> Use assembly to write address storage values

Using assembly to write address storage values can potentially save gas costs. This detector flags instances where address storage values are written without using assembly.

*There are 1 instance(s) of this issue:*

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator.slitherConstructorVariables() (src/staking/KerosineDenominator.sol#7-23) writes address state variable :- 
	- GOERLI_OWNER = 0xEd6715D2172BFd50C2DBF608615c2AB497904803 (src/params/Parameters.sol#7)
	- GOERLI_DNFT = 0x952E31dFeEB29F5398a36602E0E276F2b09B6651 (src/params/Parameters.sol#8)
	- GOERLI_WETH = 0xB4FBF271143F4FBf7B91A5ded31805e42b2208d6 (src/params/Parameters.sol#9)
	- GOERLI_WETH_ORACLE = 0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e (src/params/Parameters.sol#10)
	- GOERLI_FEE_RECIPIENT = 0xDeD796De6a14E255487191963dEe436c45995813 (src/params/Parameters.sol#12)
	- GOERLI_VAULT_MANAGER = 0xf3128Ac07005a5591dF997A8fBd6a75993827144 (src/params/Parameters.sol#13)
	- GOERLI_CHAINLINK_STETH = 0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e (src/params/Parameters.sol#16)
	- GOERLI_WSTETH = 0x6320cD32aA674d2898A68ec82e869385Fc5f7E2f (src/params/Parameters.sol#17)
	- GOERLI_DYAD = 0xCf0c2d6aeD80aFD8cB299e7E7F3f311F81C3a766 (src/params/Parameters.sol#18)
	- GOERLI_WETH_DYAD_UNI = 0x1F79BeD01b0fF658dbb47b4005F1B571Ef06D0FD (src/params/Parameters.sol#19)
	- MAINNET_OWNER = 0xDeD796De6a14E255487191963dEe436c45995813 (src/params/Parameters.sol#22)
	- MAINNET_DNFT = 0xDc400bBe0B8B79C07A962EA99a642F5819e3b712 (src/params/Parameters.sol#23)
	- MAINNET_WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2 (src/params/Parameters.sol#24)
	- MAINNET_WETH_ORACLE = 0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419 (src/params/Parameters.sol#25)
	- MAINNET_FEE_RECIPIENT = 0xDeD796De6a14E255487191963dEe436c45995813 (src/params/Parameters.sol#27)
	- MAINNET_VAULT_MANAGER = 0xfaa785c041181a54c700fD993CDdC61dbBfb420f (src/params/Parameters.sol#28)
	- MAINNET_CHAINLINK_STETH = 0xCfE54B5cD566aB89272946F602D76Ea879CAb4a8 (src/params/Parameters.sol#29)
	- MAINNET_WSTETH = 0x7f39C581F595B53c5cb19bD0b3f8dA6c935E2Ca0 (src/params/Parameters.sol#30)
	- MAINNET_DYAD = 0x305B58c5F6B5b6606fb13edD11FbDD5e532d5A26 (src/params/Parameters.sol#31)
	- MAINNET_WETH_DYAD_UNI = 0x1F79BeD01b0fF658dbb47b4005F1B571Ef06D0FD (src/params/Parameters.sol#32)
	- MAINNET_KEROSENE = 0xf3768D6e78E65FC64b8F12ffc824452130BD5394 (src/params/Parameters.sol#33)
	- MAINNET_STAKING = 0x8e0e695fEC31d5502C2f3E860Fe560Ea80b03E1D (src/params/Parameters.sol#34)
	- MAINNET_WETH_VAULT = 0xcF97cEc1907CcF9d4A0DC4F492A3448eFc744F6c (src/params/Parameters.sol#35)
	- MAINNET_WSTETH_VAULT = 0x7aE80418051b2897729Cbdf388b07C5158C557A1 (src/params/Parameters.sol#36)
	- MAINNET_VAULT_MANAGER_LICENSER = 0xd8bA5e720Ddc7ccD24528b9BA3784708528d0B85 (src/params/Parameters.sol#37)
	- SEPOLIA_OWNER = 0xEd6715D2172BFd50C2DBF608615c2AB497904803 (src/params/Parameters.sol#40)
	- SEPOLIA_DNFT = address(0) (src/params/Parameters.sol#41)
	- SEPOLIA_WETH = 0x7b79995e5f793A07Bc00c21412e50Ecae098E7f9 (src/params/Parameters.sol#42)
	- SEPOLIA_WETH_ORACLE = 0x694AA1769357215DE4FAC081bf1f309aDC325306 (src/params/Parameters.sol#43)
	- SEPOLIA_FEE_RECIPIENT = 0xDeD796De6a14E255487191963dEe436c45995813 (src/params/Parameters.sol#45)
	- SEPOLIA_VAULT_MANAGER = address(0) (src/params/Parameters.sol#46)
	- SEPOLIA_CHAINLINK_STETH = 0x694AA1769357215DE4FAC081bf1f309aDC325306 (src/params/Parameters.sol#49)
	- SEPOLIA_WSTETH = 0xB82381A3fBD3FaFA77B3a7bE693342618240067b (src/params/Parameters.sol#50)
	- SEPOLIA_DYAD = address(0) (src/params/Parameters.sol#51)
	- SEPOLIA_WETH_DYAD_UNI = 0x1F79BeD01b0fF658dbb47b4005F1B571Ef06D0FD (src/params/Parameters.sol#52)

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

### [G-13]<a name="g-13"></a> State variable read in a loop

Reading a state variable inside a loop can unnecessarily increase gas consumption, as each read operation from the blockchain state is costly. This inefficiency becomes pronounced in loops with many iterations. To optimize gas usage, it's advisable to read the state variable once before the loop starts, store its value in a local (memory) variable, and then use this local variable within the loop. This approach minimizes the number of state read operations, thereby reducing the gas cost associated with executing the contract function, making the smart contract more efficient and cost-effective to run.

*There are 3 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.getNonKeroseneValue(uint256) (src/core/VaultManagerV2.sol#250-267) reads state variables in loop: 
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#259)
	- vaultLicenser.isLicensed(address(vault)) (src/core/VaultManagerV2.sol#261)

/// @audit ************** Possible Issue Line(s) **************
	L#259,  L#261,  

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

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.liquidate(uint256,uint256) (src/core/VaultManagerV2.sol#205-228) reads state variables in loop: 
	- vault = Vault(vaults[id].at(i)) (src/core/VaultManagerV2.sol#223)

/// @audit ************** Possible Issue Line(s) **************
	L#223,  

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
VaultManagerV2.getKeroseneValue(uint256) (src/core/VaultManagerV2.sol#269-286) reads state variables in loop: 
	- vault = Vault(vaultsKerosene[id].at(i)) (src/core/VaultManagerV2.sol#278)
	- keroseneManager.isLicensed(address(vault)) (src/core/VaultManagerV2.sol#280)

/// @audit ************** Possible Issue Line(s) **************
	L#278,  L#280,  

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

### [G-14]<a name="g-14"></a> Unnecessary casting as variable is already of the same type

Unnecessary casting of a variable to the same type is redundant and can contribute to gas inefficiency and code clutter. This situation commonly arises when developers, perhaps due to oversight or misunderstanding, explicitly cast a variable to its existing type. For example, casting a `uint256` variable to `uint256` again does not change its type or value but adds unnecessary operations and gas.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

/// @audit ******************* Issue Detail *******************
VaultManagerV2.deposit(uint256,address,uint256) (src/core/VaultManagerV2.sol#119-131) performs same type cast
	- _vault.asset().safeTransferFrom(msg.sender,address(vault),amount) (src/core/VaultManagerV2.sol#129) casts (address) to (address).

/// @audit ************** Possible Issue Line(s) **************
	L#129,  

/// @audit ****************** Affected Code *******************
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

*GitHub* : [119-131](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119-L131)

### [G-15]<a name="g-15"></a> State variables that could be declared immutable

State variables that are not updated following deployment should be declared immutable to save gas.  **Recom:** Add the `immutable` attribute to state variables that never change or are set only in the constructor.

*There are 1 instance(s) of this issue:*

```solidity
File: src/staking/KerosineDenominator.sol

/// @audit ******************* Issue Detail *******************
KerosineDenominator.kerosine (src/staking/KerosineDenominator.sol#9) should be immutable 

/// @audit ************** Possible Issue Line(s) **************
	L#9,  

/// @audit ****************** Affected Code *******************
   9:   Kerosine public kerosine;

```

*GitHub* : [9-9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L9-L9)

### [G-16]<a name="g-16"></a> checks for zero uint should be done using assembly to save gas

Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations.

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

237:       if (_dyad == 0) return type(uint).max;

```


*GitHub* : [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237-L237)

### [G-17]<a name="g-17"></a> `>=` costs less gas than `>`

The compiler uses opcodes `GT` and `ISZERO` for solidity code that uses `>`, but only requires `LT` for `>=`, [which saves **3 gas**](https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde). If `<` is being used, the condition can be inverted. In cases where a for-loop is being used, one can count down rather than up, in order to use the optimal operator

*There are 11 instance(s) of this issue:*

```solidity
File: src/core/Vault.kerosine.unbounded.sol

58:       for (uint i = 0; i < numberOfVaults; i++) {

```



*GitHub* : [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58-L58)

```solidity
File: src/core/VaultManagerV2.sol

101:     if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();

113:     if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();

150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

165:     if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

167:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

222:       for (uint i = 0; i < numberOfVaults; i++) {

258:       for (uint i = 0; i < numberOfVaults; i++) {

277:       for (uint i = 0; i < numberOfVaults; i++) {

```


*GitHub* : [101](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L101-L101), [113](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L113-L113), [150](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L150-L150), [152](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L152-L152), [165](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L165-L165), [167](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L167-L167), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217-L217), [222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222-L222), [258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258-L258), [277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277-L277)

### [G-18]<a name="g-18"></a> Counting down in for statements is more gas efficient

Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

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

### [G-19]<a name="g-19"></a> Avoid transferring amounts of zero in order to save gas

Skipping the external call when nothing will be transferred, will save at least **100 gas**

*There are 1 instance(s) of this issue:*

```solidity
File: src/core/VaultManagerV2.sol

129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

```


*GitHub* : [129](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129-L129)