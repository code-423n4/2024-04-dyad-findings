# QA Report

## Low Severity Findings

### L-1 Possible divide by 0

## Impact

Due to the fact that KerosineDenominator is a contract and can be changed, its return value can change also. Its possible for KerosineDenominator to return 0 and the asset price of Kerosine vault will revert.

## Vulnerability details

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L67

## Recommended Mitigation Steps

Check if returned value is different from 0.

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
      if (denominator == 0) {
        // either assign it to 1
        // or something else
      }
      return numerator * 1e8 / denominator;
  }

```

### L-2 - Kerosine manager can be made immutable

## Impact

Lowers gas consumption when dealing with methods using keroseneManager.
`KerosineManager public keroseneManager` variable of `VaultManagerV2` is set via method `function setKeroseneManager(KerosineManager _keroseneManager) external initializer`. Initializer modifier makes the property be changed only once. Its simillar to immutable variable assigned in the constructor

## Recommended Mitigation Steps
```solidity

contract VaultManagerV2 is IVaultManager {
 // other code
KerosineManager public immutable keroseneManager;

constructor(DNft _dNft, Dyad _dyad, Licenser _licenser, KerosineManager _keroseneManager) {
        dNft = _dNft;
        dyad = _dyad;
        vaultLicenser = _licenser;
        keroseneManager = _keroseneManager;
    }
}
```

### L-3 - function setKeroseneManager lacks access modifier

## Impact

Calling `setKeroseneManager` in the DeployV2.s.sol can be front runned and malicious user can set its own implementation of KeroseneManager. Due to the `initializer` modifier, `setKeroseneManager` cant be called again. Thus leaving the protocol compromised.

## Vulnerability details

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59

## Recommended Mitigation Steps

Add some access modifier to VaultManagerV2 so only the script can set the KerosineManager

```solidity

contract VaultManagerV2 is Owned(msg.sender) IVaultManager {
 // other code
    function setKeroseneManager(
        KerosineManager _keroseneManager
    ) external onlyOwner initializer {
        keroseneManager = _keroseneManager;
    }
}

```

### L-4 - Kerosine vault (unbounded/bounded) can be added to KerosineManager

## Impact

`KerosineManager::add` accepts address property, which can be address of kerosine vault. This will enable the Notes to mint more dyad, than they should do.

## Recommended Mitigation Steps

Check if the address is Kerosine vault
