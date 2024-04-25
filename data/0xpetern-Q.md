1. # Title
**Initializer could be front-runned.**
## SUMMARY
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59C3-L64C4

The function [setkeroseneManager](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59) in VaultManagerV2.sol has an initializer which could be frontrunned by attackers. This poses a risk to the users.
```solidity
function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager;
  }
```
## Recoommended Mitigation Steps
Initializer should be called using a constructor.

2. # Title
**Input Validation**
## SUMMARY
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L49C3-L57C4

In the above section of the contract `VaultManagerV2.sol`, the constructor assigns the input parameters _dNft, _dyad, and _licenser directly to the corresponding state variables without any input validation. While it could be true that these parameters are correctly initialized before passing them to the constructor, it's good practice to include input validation to ensure that invalid or unexpected inputs are not accepted.
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
## Recommended Mitigation Steps
input validation should be introduced to ensure that invalid or unexpected inputs are not accepted.

3. # Title
**Revert Condition**
## SUMMARY 
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L214

The line if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh(); appears to be trying to revert the transaction if the collateral ratio is higher than a minimum collaterization ratio. However, revert should be followed by a string message. If CrTooHigh() is supposed to be a custom error function, it should be called without the revert keyword.
```Solidity
function liquidate(
    uint id,
    uint to
  ) 
    external 
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

      uint numberOfVaults = vaults[id].length();
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
      emit Liquidate(id, msg.sender, to);
  }
```
## Recommended Mitigation Steps
Revert should be followed by a string message. If CrTooHigh() is supposed to be a custom error function, it should be called without the revert keyword.