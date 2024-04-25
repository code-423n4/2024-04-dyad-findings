# Low Risk Issues

### \[L-01\] Calls inside a loop might lead to a denial-of-service attack.

Calls inside a loop might lead to a denial-of-service attack.

```solidity
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

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50C2-L68C4

```solidity
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L222C1-L226C8

Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop

### \[L-03\] ownable2 should be used instead of ownable.

```solidity
import {Owned}         from "@solmate/src/auth/Owned.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L5

# NonCritical 

### \[N-01\] NatSpec: functions `@param` ,`@notice`, `@title`, `@dev`, tags are missing

*There are 22 instance(s) of this issue:*

```solidity
 function addKerosene(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
    emit Added(id, vault);
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80C2-L91C4

```solidity
 function removeKerosene(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
    emit Removed(id, vault);
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106C2-L116C4

```solidity
 function collatRatio(
    uint id
  )
    public 
    view
    returns (uint) {
      uint _dyad = dyad.mintedDyad(address(this), id);
      if (_dyad == 0) return type(uint).max;
      return getTotalUsdValue(id).divWadDown(_dyad);
  }

  function getTotalUsdValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
      return getNonKeroseneValue(id) + getKeroseneValue(id);
  }

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

  function getKeroseneValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
      uint totalUsdValue;
      uint numberOfVaults = vaultsKerosene[id].length(); 
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaultsKerosene[id].at(i));
        uint usdValue;
        if (keroseneManager.isLicensed(address(vault))) {
          usdValue = vault.getUsdValue(id);        
        }
        totalUsdValue += usdValue;
      }
      return totalUsdValue;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230C2-L286C4

```solidity
  function getVaults(
    uint id
  ) 
    external 
    view 
    returns (address[] memory) {
      return vaults[id].values();
  }

  function hasVault(
    uint    id,
    address vault
  ) 
    external 
    view 
    returns (bool) {
      return vaults[id].contains(vault);
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290C1-L307C4

```solidity
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

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L36C1-L74C2

```solidity
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18C3-L51C4

```solidity
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L23C2-L50C4

```solidity
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30C2-L68C4

### \[N-02\] Natspec @author is missing

all contracts

### \[N-03\] NatSpec: NatSpec: Functions `@return` tag is missing

*There are 14 instance(s) of this issue:*

```solidity
 function collatRatio(
    uint id
  )
    public 
    view
    returns (uint) {
      uint _dyad = dyad.mintedDyad(address(this), id);
      if (_dyad == 0) return type(uint).max;
      return getTotalUsdValue(id).divWadDown(_dyad);
  }

  function getTotalUsdValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
      return getNonKeroseneValue(id) + getKeroseneValue(id);
  }

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

  function getKeroseneValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
      uint totalUsdValue;
      uint numberOfVaults = vaultsKerosene[id].length(); 
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaultsKerosene[id].at(i));
        uint usdValue;
        if (keroseneManager.isLicensed(address(vault))) {
          usdValue = vault.getUsdValue(id);        
        }
        totalUsdValue += usdValue;
      }
      return totalUsdValue;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230C2-L286C4

```solidity
  function getVaults(
    uint id
  ) 
    external 
    view 
    returns (address[] memory) {
      return vaults[id].values();
  }

  function hasVault(
    uint    id,
    address vault
  ) 
    external 
    view 
    returns (bool) {
      return vaults[id].contains(vault);
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290C1-L307C4

```solidity
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

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60C1-L74C2

```solidity
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L37C3-L51C4

```solidity
  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L44C1-L50C4

```solidity
  function setDenominator(KerosineDenominator _kerosineDenominator) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43

### \[N-04\] In functions which accept an address as a parameter, there should be a zero address check to prevent bugs

In smart contract development, especially with Solidity, it's crucial to validate inputs to functions. When a function accepts an Ethereum address as a parameter, implementing a zero address check (i.e., ensuring the address is not `0x0`) is a best practice to prevent potential bugs and vulnerabilities. The zero address (`0x0`) is a default value and generally indicates an uninitialized or invalid state. Passing the zero address to certain functions can lead to unintended behaviors, like funds getting locked permanently or transactions failing silently. By checking for and rejecting the zero address, developers can ensure that the function operates as intended and interacts only with valid Ethereum addresses. This check enhances the contract's robustness and security.

*There are 14 instance(s) of this issue:*

```solidity
   function add(
      uint    id,
      address vault
  ) 

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67C1-L70C5

```solidity
  function addKerosene(
      uint    id,
      address vault
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80C2-L83C5

```solidity
  function remove(
      uint    id,
      address vault
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94C2-L97C5

```solidity
  function removeKerosene(
      uint    id,
      address vault
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L106C3-L109C5

```solidity
  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119C2-L123C5

```solidity
  function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134C3-L139C5

```solidity
  function mintDyad(
    uint    id,
    uint    amount,
    address to
  )
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156C1-L160C4

```solidity
  function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184C1-L189C4

```solidity
  function remove(
    address vault
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L28C1-L30C5

```solidity
  function isLicensed(
    address vault
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44C1-L46C5

```solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32C3-L36C5

```solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30C1-L34C4

### \[N-05\] Revert statements within external and public functions can be used to perform DOS attacks

In Solidity, 'revert' statements are used to undo changes and throw an exception when certain conditions are not met. However, in public and external functions, improper use of `revert` can be exploited for Denial of Service (DoS) attacks. An attacker can intentionally trigger these 'revert' conditions, causing legitimate transactions to consistently fail. For example, if a function relies on specific conditions from user input or contract state, an attacker could manipulate these to continually force reverts, blocking the function's execution. Therefore, it's crucial to design contract logic to handle exceptions properly and avoid scenarios where `revert` can be predictably triggered by malicious actors. This includes careful input validation and considering alternative design patterns that are less susceptible to such abuses.

*There are 10 instance(s) of this issue:*

```solidity
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67C2-L78C4

```solidity
  function addKerosene(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
    if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
    emit Added(id, vault);
  }
```  function remove(
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
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94C2-L104C4

```solidity
  function add(
    address vault
  ) 
    external 
      onlyOwner
  {
    if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
    if (!vaults.add(vault))            revert VaultAlreadyAdded();
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L18C1-L26C4

### \[N-06\] Private and internal state variables should have a preceding _ in their name unless they are constants

Add a preceding underscore to the state variable name, take care to refactor where there variables are read/wrote

*There are 1 instance(s) of this issue:*

```solidity
  EnumerableSet.AddressSet private vaults;

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L16

### \[N-07\] Contract lines should not be longer than 120 characters for readability

Consider spreading these lines over multiple lines to aid in readability and the support of VIM users everywhere.

[VaultManagerV2](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol)

### \[N-08\] Functions within contracts are not ordered according to the solidity style guide

The following order should be used within contracts

constructor

receive function (if exists)

fallback function (if exists)

external

public

internal

private

Rearrange the contract functions and contructors to fit this ordering

[VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol)

[KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol)

### \[N-09\] Interface imports should be declared first

Amend the ordering of imports to import interfaces first followed by other imports

*There are 5 instance(s) of this issue:*

```solidity
import {DNft}            from "./DNft.sol";
import {Dyad}            from "./Dyad.sol";
import {Licenser}        from "./Licenser.sol";
import {Vault}           from "./Vault.sol";
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "../../src/core/KerosineManager.sol";


import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L4C1-L15C89

```solidity
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "./KerosineManager.sol";
import {IVault}          from "../interfaces/IVault.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L4C1-L6C58

```solidity
import {KerosineVault}        from "./Vault.kerosine.sol";
import {IVaultManager}        from "../interfaces/IVaultManager.sol";
import {Vault}                from "./Vault.sol";
import {Dyad}                 from "./Dyad.sol";
import {KerosineManager}      from "./KerosineManager.sol";
import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L4C1-L10C73

```solidity
import {Parameters}             from "../../src/params/Parameters.sol";
import {VaultManagerV2}         from "../../src/core/VaultManagerV2.sol";
import {DNft}                   from "../../src/core/DNft.sol";
import {Dyad}                   from "../../src/core/Dyad.sol";
import {Licenser}               from "../../src/core/Licenser.sol";
import {Vault}                  from "../../src/core/Vault.sol";
import {VaultWstEth}            from "../../src/core/Vault.wsteth.sol";
import {IWETH}                  from "../../src/interfaces/IWETH.sol";
import {IAggregatorV3}          from "../../src/interfaces/IAggregatorV3.sol";
import {KerosineManager}        from "../../src/core/KerosineManager.sol";
import {UnboundedKerosineVault} from "../../src/core/Vault.kerosine.unbounded.sol";
import {BoundedKerosineVault}   from "../../src/core/Vault.kerosine.bounded.sol";
import {Kerosine}               from "../../src/staking/Kerosine.sol";
import {KerosineDenominator}    from "../../src/staking/KerosineDenominator.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L6C1-L19C82

### \[N-10\] Consider using named mappings

In Solidity version 0.8.18 and beyond mapping parameters can be named. This makes the purpose and function of a given mapping far clearer which in turn improves readability.

*There are 2 instance(s) of this issue:*

```solidity
  mapping (uint => uint) public idToBlockOfLastDeposit;
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L37

```solidity
  mapping(uint => uint) public id2asset;
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19

### \[N-11\] Style guide: Contract does not follow the Solidity style guide's suggested layout ordering

The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be 1) Type declarations, 2) State variables, 3) Events, 4) Modifiers, and 5) Functions, but the contract(s) below do not follow this ordering

### \[N-12\] Constructors missing validation

In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.

*There are 4 instance(s) of this issue:*

```solidity
      constructor(
    IVaultManager   _vaultManager,
    ERC20           _asset, 
    KerosineManager _kerosineManager 
  ) {
    vaultManager    = _vaultManager;
    asset           = _asset;
    kerosineManager = _kerosineManager;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L26C1-L34C4

```solidity
  constructor(
      IVaultManager   _vaultManager,
      ERC20           _asset, 
      Dyad            _dyad, 
      KerosineManager _kerosineManager
  ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
      dyad = _dyad;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L21C1-L28C4

```solidity
  constructor(
    Kerosine _kerosine
  ) {
    kerosine = _kerosine;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L11C2-L15C4

```solidity
  constructor(
    DNft          _dNft,
    Dyad          _dyad,
    Licenser      _licenser
  ) {
    dNft          = _dNft;
    dyad          = _dyad;
    vaultLicenser = _licenser;
  }

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49C2-L57C4

### \[N-13\] Use a single contract or library for system wide constants

*There are 5 instance(s) of this issue:*

```solidity
  uint public constant MAX_VAULTS          = 5;
  uint public constant MAX_VAULTS_KEROSENE = 5;

  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%
  uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L22C1-L26C67

```solidity
  uint public constant MAX_VAULTS = 10;
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14

### \[N-14\] Consider using SMTChecker

The SMTChecker is a valuable tool for Solidity developers as it helps detect potential vulnerabilities and logical errors in the contract's code. By utilizing Satisfiability Modulo Theories (SMT) solvers, it can reason about the potential states a contract can be in, and therefore, identify conditions that could lead to undesirable behavior. This automatic formal verification can catch issues that might otherwise be missed in manual code reviews or standard testing, enhancing the overall contract's security and reliability.

### \[N-15\] `require()`/`revert()` statements should have descriptive reason strings

*There are 21 instance(s) of this issue:*

```solidity
    File: src/core/VaultManagerV2.sol

    74: if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
    75: if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
    76: if (!vaults[id].add(vault))            revert VaultAlreadyAdded();


    87: if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
    88: if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    89: if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

    101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
    102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();


    113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
    114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();

    143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

    150:    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

    152:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

    165:    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

    167:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

    214:    if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

    237:    if (_dyad == 0) return type(uint).max;



```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74C4-L76C71

```solidity
    File: src/core/KerosineManager.sol

        24: if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
        25: if (!vaults.add(vault))            revert VaultAlreadyAdded();

        34: if (!vaults.remove(vault)) revert VaultNotFound();
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24C1-L25C67

### [N-16\] for safty purpose the more less external call the less risk can appear 

### \[N-17\] Consider adding formal verification proofs

Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)

*There are 0 instance(s) of this issue:*

```solidity
File: Various Files
```

### \[N-18\] Lack Of Brace Spacing

Lack of brace spacing in coding refers to the absence of spaces around braces, which can hinder code readability. In Solidity, as in many programming languages, spacing can enhance the visual distinction between different parts of the code, making it easier to follow. A lack of spacing can lead to a dense, confusing appearance. The resolution to this issue is to follow a consistent style guide that defines rules for brace spacing. By including spaces around braces, such as `{ statement }` instead of `{statement}`, developers can ensure that the code is more legible and maintainable, especially in larger codebases.

*There are 35 instance(s) of this issue:*

```solidity
import {Parameters} from "../params/Parameters.sol";
import {Kerosine} from "../staking/Kerosine.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L4C1-L5C50

```solidity
import {DNft}            from "./DNft.sol";
import {Dyad}            from "./Dyad.sol";
import {Licenser}        from "./Licenser.sol";
import {Vault}           from "./Vault.sol";
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "../../src/core/KerosineManager.sol";

import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L4C1-L15C89

```solidity
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "./KerosineManager.sol";
import {IVault}          from "../interfaces/IVault.sol";
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {Owned}           from "@solmate/src/auth/Owned.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L4C1-L6C58

```solidity
import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Owned}         from "@solmate/src/auth/Owned.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L4C1-L5C59

```solidity
import {KerosineVault}          from "./Vault.kerosine.sol";
import {IVaultManager}          from "../interfaces/IVaultManager.sol";
import {Dyad}                   from "./Dyad.sol";
import {KerosineManager}        from "./KerosineManager.sol";
import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L4C1-L8C71

```solidity
import {KerosineVault}        from "./Vault.kerosine.sol";
import {IVaultManager}        from "../interfaces/IVaultManager.sol";
import {Vault}                from "./Vault.sol";
import {Dyad}                 from "./Dyad.sol";
import {KerosineManager}      from "./KerosineManager.sol";
import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L4C1-L13C72

### \[N-19\] If statement control structures do not comply with best practices

If statements which include a single line do not need to have curly brackets, however according to the Solidiity style guide the line of code executed upon the if statement condition being met should still be on the next line, not on the same line as the if statement declaration.

*There are 21 instance(s) of this issue:*

```solidity
    File: src/core/VaultManagerV2.sol

    74: if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();
    75: if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
    76: if (!vaults[id].add(vault))            revert VaultAlreadyAdded();


    87: if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
    88: if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    89: if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();

    101:    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();
    102:    if (!vaults[id].remove(vault))     revert VaultNotAdded();


    113:    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();
    114:    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();

    143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

    150:    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();

    152:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

    165:    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();

    167:    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 

    214:    if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();

    237:    if (_dyad == 0) return type(uint).max;



```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74C4-L76C71

```solidity
    File: src/core/KerosineManager.sol

        24: if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
        25: if (!vaults.add(vault))            revert VaultAlreadyAdded();

        34: if (!vaults.remove(vault)) revert VaultNotFound();
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24C1-L25C67

### \[N-20\] Missing events in sensitive functions

Sensitive setter functions in smart contracts often alter critical state variables. Without events emitted in these functions, external observers or dApps cannot easily track or react to these state changes. Missing events can obscure contract activity, hampering transparency and making integration more challenging. To resolve this, incorporate appropriate event emissions within these functions. Events offer an efficient way to log crucial changes, aiding in real-time tracking and post-transaction verification.

*There are 1 instance(s) of this issue:*

```solidity
   function setDenominator(KerosineDenominator _kerosineDenominator) 
    external 
      onlyOwner
  {
    kerosineDenominator = _kerosineDenominator;
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43C1-L48C4

### \[N-21\] Consider using a format prettier or forge fmt

Some comments use // X and others //X Amend comments to use only use // X or //X consistently such style inconsistencies can be resolved by running the project through a format prettier or by using forge fmt.

```solidity
4: /// // <= FOUND

```

### \[N-22\] Consider validating all user inputs

Validating user inputs in external and public functions is a critical security practice in smart contract development. This approach prevents malicious or erroneous data from compromising contract integrity or behavior. By checking inputs against expected formats, ranges, or conditions before processing, contracts can avoid common vulnerabilities like reentrancy, overflow/underflow, and unauthorized access.

\*\* All contracts \*\*

### \[N-23\] Consider using named returns

Using named returns in Solidity functions enhances code readability and clarity. By explicitly naming return variables in the function signature, developers can document what each return value represents, making the code easier to understand and maintain. This practice can also slightly optimize gas usage by avoiding extra variable declarations.

*There are 10 instance(s) of this issue:*

```solidity
  function denominator() external view returns (uint) {

```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L192

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L235

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L246

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L255

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L274

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L65

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L49

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L48

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L54

### \[N-24\] Errors should have parameters

In Solidity, custom errors with parameters offer a gas-efficient way to convey detailed information about issues encountered during contract execution. Unlike revert messages, which are strings consuming more gas, custom errors defined with parameters allow developers to specify types and details of errors succinctly. This method enhances debugging, provides clearer insights into contract failures, and improves the developer's and end-user's understanding of what went wrong, all while optimizing for gas usage and maintaining contract efficiency.

*There are 1 instance(s) of this issue:*

```solidity
  error TooManyVaults();
  error VaultAlreadyAdded();
  error VaultNotFound();
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L8C1-L10C25

### \[N-25\] Variables need not be initialized to zero

The default value for variables is zero, so initializing them to zero is superfluous.

```solidity
    file: src/core/VaultManagerV2.sol

    222:  for (uint i = 0; i < numberOfVaults; i++) {

    258:  for (uint i = 0; i < numberOfVaults; i++) {

    277:  for (uint i = 0; i < numberOfVaults; i++) {
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L222

```solidity
      for (uint i = 0; i < numberOfVaults; i++) {
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L58

### \[N-26\] Consider adding emergency-stop functionality

In the event of a security breach or any unforeseen emergency, swiftly suspending all protocol operations becomes crucial. Having a mechanism in place to halt all functions collectively, instead of pausing individual contracts separately, substantially enhances the efficiency of mitigating ongoing attacks or vulnerabilities. This not only quickens the response time to potential threats but also reduces operational stress during these critical periods. Therefore, consider integrating a 'circuit breaker' or 'emergency stop' function into the smart contract system architecture. Such a feature would provide the capability to suspend the entire protocol instantly, which could prove invaluable during a time-sensitive crisis management situation.

### \[N-27\] Generate perfect code headers every time

Description:  
I recommend using header for Solidity code layout and readability

```
/*//////////////////////////////////////////////////////////////
                           TESTING 123
//////////////////////////////////////////////////////////////*/
```

### \[N-28\] Use a more recent version of Solidity

For security, it is best practice to use the latest Solidity version.

For the security fix list in the versions: https://github.com/ethereum/solidity/blob/develop/Changelog.md

Recommended Mitigation Steps  
Old version of Solidity is used, newer version can be used .

### \[N-29\] For modern and more readable code; update import usages

Solidity code is also cleaner in another way that might not be noticeable: the struct Point. We were importing it previously with global import but not using it. The Point struct polluted the source code with an unnecessary object we were not using because we did not need it.  
This was breaking the rule of modularity and modular programming: only import what you need Specific imports with curly braces allow us to apply this rule better.  
*Recommendation*  
`import {contract1 , contract2} from "filename.sol";`

*There are 35 instance(s) of this issue:*

```solidity
import {Parameters} from "../params/Parameters.sol";
import {Kerosine} from "../staking/Kerosine.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L4C1-L5C50

```solidity
import {DNft}            from "./DNft.sol";
import {Dyad}            from "./Dyad.sol";
import {Licenser}        from "./Licenser.sol";
import {Vault}           from "./Vault.sol";
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "../../src/core/KerosineManager.sol";

import {FixedPointMathLib} from "@solmate/src/utils/FixedPointMathLib.sol";
import {ERC20}             from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
import {EnumerableSet}     from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Initializable}     from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L4C1-L15C89

```solidity
import {IVaultManager}   from "../interfaces/IVaultManager.sol";
import {KerosineManager} from "./KerosineManager.sol";
import {IVault}          from "../interfaces/IVault.sol";
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {Owned}           from "@solmate/src/auth/Owned.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L4C1-L6C58

```solidity
import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";
import {Owned}         from "@solmate/src/auth/Owned.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L4C1-L5C59

```solidity
import {KerosineVault}          from "./Vault.kerosine.sol";
import {IVaultManager}          from "../interfaces/IVaultManager.sol";
import {Dyad}                   from "./Dyad.sol";
import {KerosineManager}        from "./KerosineManager.sol";
import {UnboundedKerosineVault} from "./Vault.kerosine.unbounded.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L4C1-L8C71

```solidity
import {KerosineVault}        from "./Vault.kerosine.sol";
import {IVaultManager}        from "../interfaces/IVaultManager.sol";
import {Vault}                from "./Vault.sol";
import {Dyad}                 from "./Dyad.sol";
import {KerosineManager}      from "./KerosineManager.sol";
import {BoundedKerosineVault} from "./Vault.kerosine.bounded.sol";
import {KerosineDenominator}  from "../staking/KerosineDenominator.sol";
import {ERC20}           from "@solmate/src/tokens/ERC20.sol";
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L4C1-L13C72

## \[N-30\] Pragma version^0.8.17 version too recent to be trusted.

`0.8.17 (2022-09-08)`

> Unexpected bugs can be reported in recent versions;  
> Risks related to recent releases  
> Risks of complex code generation changes  
> Risks of new language features  
> Risks of known bugs

> Use a non-legacy and more battle-tested version  
> Use 0.8.10