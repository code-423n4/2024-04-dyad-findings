# QA Report for DYAD

## Table of Contents

| Issue ID                                                                   | Description                                                                            |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------|
| [QA-01](#qa-01-kerosene-vaults-shouldnt-be-licensed-by-licenser)           | Kerosene vaults shouldn't be licensed by licenser                                      |
| [QA-02](#qa-02-get-non-and-kerosine-value-can-be-simplified)               | Get Non and Kerosine value can be simplified                                           |
| [QA-03](#qa-03-unused-modifier-should-be-removed)                          | Unused modifier should be removed                                                      |
| [NC-01](#nc-01-naming-of-variables-can-be-improved)                        | Naming of variables can be improved                                                    |

## QA-01 Kerosene vaults shouldnt be licensed by licenser 

## Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L93-L96

```solidity
     vaultLicenser.add(address(ethVault));
    vaultLicenser.add(address(wstEth));
    vaultLicenser.add(address(unboundedKerosineVault));
    // vaultLicenser.add(address(boundedKerosineVault));
```

See this https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L44-L52

```solidity
   function isLicensed(
    address vault
  ) 
    external 
    view 
    returns (bool) {
      return vaults.contains(vault);
  }
```

And this https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L80-L91
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

Evidently the kerosene vaults are licensed by the kerosene manager not the licenser. 

### Recommended Mitigation Steps

Consider removing the kerosine vault licensing from the deploy script

## QA-02 Get Non and Kerosine value can be simplified

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L250C12-L286

```solidity
    function getNonKeroseneValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
    ..
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[id].at(i));
        uint usdValue;
        if (vaultLicenser.isLicensed(address(vault))) {
          usdValue = vault.getUsdValue(id);        
        }
        totalUsdValue += usdValue;
      }
    ..
  }

  function getKeroseneValue(
    uint id
  ) 
  ...
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaultsKerosene[id].at(i));
        uint usdValue;
        if (keroseneManager.isLicensed(address(vault))) {
          usdValue = vault.getUsdValue(id);        
        }
        totalUsdValue += usdValue;
      }
   ...
  }
```

### Recommended Mitigation Steps

Logic can be improved by slightly reworking the code 

```solidity
    function getNonKeroseneValue(
    uint id
  ) 
    public 
    view
    returns (uint) {
    ..
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[id].at(i));
        if (vaultLicenser.isLicensed(address(vault))) {
          uint usdValue = vault.getUsdValue(id);        
          totalUsdValue += usdValue;
        }
      }
    ..
  }

  function getKeroseneValue(
    uint id
  ) 
  ...
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaultsKerosene[id].at(i));
        if (keroseneManager.isLicensed(address(vault))) {
            uint usdValue = vault.getUsdValue(id);        
            totalUsdValue += usdValue;
        }
      }
   ...
  }
```


## QA-03 Unused modifier should be removed

### Proof of Concept

Take a look at 

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45C12-L47
```solidity
modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```

### Recommended Mitigation Steps

Unecessary piece of code and can be removed. 

## NC-01 Naming of variables can be improved       

Instance 1: 
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184-L202
```diff
  function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
    returns (uint) { 
      dyad.burn(id, msg.sender, amount);
      Vault _vault = Vault(vault);
-      uint asset = amount 
+      uint assetAmount = amount 
                        * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                        / _vault.assetPrice() 
                        / 1e18;
-     withdraw(id, vault, asset, to);
+     withdraw(id, vault, assetAmount, to);
      emit RedeemDyad(id, vault, amount, to);
      return asset;
  }
```

Instance 2: 
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L49-L53
```diff
-     Vault ethVault = new Vault(
+     Vault wethVault = new Vault(
      vaultManager,
      ERC20        (MAINNET_WETH),
      IAggregatorV3(MAINNET_WETH_ORACLE)
    );
```

Instance 3: 
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L19
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.wsteth.sol#L26
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.sol#L25

```diff
-  mapping(uint => uint) public id2asset;
+  mapping(uint => uint) public id2AssetAmount;
```