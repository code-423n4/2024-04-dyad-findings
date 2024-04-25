
| Type |  Title |
|------|-------|
| L-1    |  Redundant Price Calculation |
| L-2    |  DNFT Attack Vector and Price Model Impact on System |
| L-3    |  A Vault Price Failure Could Cause DOS to the System |
| N-1   |  Deposit and Withdraw Functions Do Not Check if the Vault is in the Vaults Mapping and Have Potential Reentrancy Risk |
| N-2    | Add Getter Functions for KeroseneVault |
| N-3    |  Failure to Throw Custom Errors for Underflow During Vault Withdrawals May Impact User Experience |
| N-4    | Consider deleting the `move` Function for Kerosene Vaults |
| N-5    |  Inconsistent Visibility of Contract Functions with Interface Function Definitions |
| N-6    |Adding a Function to Retrieve Minting Price for DNFTs |

# [L-1] Redundant Price Calculation

## Details
The `getKeroseneValue` function in the `VaultManagerV2` contract has highly redundant price calculations.  
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L277](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L277)
```solidity
        for (uint i = 0; i < numberOfVaults; i++) {
            Vault vault = Vault(vaultsKerosene[id].at(i));
            uint usdValue;
            if (keroseneManager.isLicensed(address(vault))) {
                usdValue = vault.getUsdValue(id);
            }
            totalUsdValue += usdValue;
        }
```

Assuming an NFT ID has 5 `keroseneVaults`, and there are 10 pricing vaults in `KerosineManager`. Let's calculate the number of computations for a single call to the `getKeroseneValue` function:  

Requesting assertPrice for 5 `keroseneVaults` -> Calculate LVT for 5 times -> Requesting assertPrice for 50 vaults -> Calling price oracle 50 times.  

Since the `KeroseneManager` for each `keroseneVault` is the same, the `assertPrice` for `keroseneVaults` needs to be calculated only once, as subsequent calculations will yield the same result. This design results in significant gas wastage.  

## Suggestion
Calculating the `assertPrice` for `keroseneVaults` only once can simplify the calculation to:  

Requesting assertPrice for 1 `keroseneVault` -> Calculate LVT once -> Requesting assertPrice for 10 vaults -> Calling price oracle 10 times.  

I add a function in Vault  
```solidity
    function getUsdValue(
        uint256 id,
        uint256 assertPrice
    ) public view returns (uint) {
        return (id2asset[id] * assertPrice) / 1e8;
    }
```
And then change the function 
```solidity
+        bool isGetAssertPrice;
+        uint256 kerosenePrice;
        for (uint i = 0; i < numberOfVaults; i++) {
            Vault vault = Vault(vaultsKerosene[id].at(i));
            uint usdValue;
+            if(!isGetAssertPrice){
+                kerosenePrice = vault.assetPrice();
+                isGetAssertPrice = true;
+            }
            if (keroseneManager.isLicensed(address(vault))) {
+                usdValue = vault.getUsdValue(id, kerosenePrice);
            }
            totalUsdValue += usdValue;
        }
```  

# [L-2] DNFT Attack Vector and Price Model Impact on System

## Details
Before using `Vault` and `VaultManager`, one needs to hold DNFT. The minting price of DNFT increases linearly, which may allow malicious arbitrageurs to artificially inflate the price, affecting genuine users. However, the minting of DNFT lacks reentrancy protection.  

This means that during the early stages of DNFT minting, arbitrageurs can mint enough DNFT in a single transaction to raise the DNFT price significantly. They can then sell DNFT at a profit below the minting price.  
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/DNft.sol#L22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/DNft.sol#L22)
```solidity
  function mintNft(address to)
    external 
    payable
    returns (uint) {
      uint price = START_PRICE + (PRICE_INCREASE * publicMints++);
      if (msg.value < price) revert InsufficientFunds();
      uint id = _mintNft(to);
      if (msg.value > price) to.safeTransferETH(msg.value - price);
      emit MintedNft(id, to);
      return id;
  }
  
```
Example:
Starting minting price is 0.1 ether. An arbitrageur mints 100 NFTs in a single transaction, costing 15 ether, and the transaction price rises to 0.2 ether. The arbitrageur sells DNFT at 0.19 ether, making a profit of 0.19 * 100 - 15 ether = 4 ether.  

## Suggestion
Add reentrancy protection to the `mintNFT` function. However, the root cause of this issue lies in the DNFT's price growth model. It is suggested to change the DNFT's price growth model to stabilize the price within a range.  

```solidity
    function mintNft(address to)
        external 
        payable
        returns (uint) nonReentrant() {
```

# [L-3] A Vault Price Failure Could Cause DOS to the System

## Details
The calculation of token values in the vault relies on traversing the added vaults, and if one vault fails to obtain a price, the entire system cannot function.   

For example, using a Chainlink oracle in a regular vault to obtain prices, if the oracle fails due to malfunction, causing price requests to fail, the entire system could be subjected to a denial-of-service (DOS) attack.
```solidity
      (
        ,
        int256 answer,
        , 
        uint256 updatedAt, 
      ) = oracle.latestRoundData();
```
## Suggestion
Utilize try-catch statements more frequently and verify the validity of price return values to mitigate the impact of faulty vaults on the system.

# [N-1] deposit and withdraw functions do not check if the vault is in the vaults mapping and have potential reentrancy risk

## Details
Users can deposit into a vault that is not in the `mapping(uint => EnumerableSet.AddressSet) internal vaults` mapping via VaultManagerV2. The reason for this issue is the lack of validation for the `address vault` parameter.
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119)
```solidity
    function deposit(
        uint id,
        address vault,
        uint amount
    ) external isValidDNft(id) {
        idToBlockOfLastDeposit[id] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }
```

## Suggestion
Add checks in the deposit and withdraw functions to ensure that the vault is in the mapping, thus mitigating potential reentrancy risks.  
```solidity
    function deposit(
        uint id,
        address vault,
        uint amount
    ) external isValidDNft(id) {
+        require(hasVault(id) || vaultsKerosene[id].contains(vault), "Not In Vault");
        idToBlockOfLastDeposit[id] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }
```
# [N-2] Add getter functions for keroseneVault

## Details
The `mapping(uint => EnumerableSet.AddressSet) internal vaultsKerosene` mapping is of internal type and lacks getter methods similar to the vaults mapping.  
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L290)
```solidity
    function getVaults(uint id) external view returns (address[] memory) {
        return vaults[id].values();
    }

    function hasVault(uint id, address vault) external view returns (bool) {
        return vaults[id].contains(vault);
    }
```
This inconvenience users.

## Suggestion
It is recommended to add getter functions for the keroseneVault mapping to allow users to conveniently retrieve relevant information.
```solidity
    function getKerosineVaults(uint id) external view returns (address[] memory) {
        return vaultsKerosene[id].values();
    }

    function hasKerosineVault(uint id, address vault) external view returns (bool) {
        return vaultsKerosene[id].contains(vault);
    }
```

# [N-3] Failure to throw custom errors for underflow during vault withdrawals may impact user experience

## Details
There are potential instances within the system where underflows occur during withdrawals without triggering custom error messages. This can lead to user confusion. For example, in the withdrawal function, if the withdrawal amount exceeds the deposit in the vault, underflow occurs.   
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L30)
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
  ```
Without custom error handling, users may be left puzzled by the unexpected behavior.
## suggestion

```solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
      onlyVaultManager
  { 
    require( id2asset[id] < amount,"Insufficient Balance");
    unchecked{
        id2asset[id] -= amount;
    }
    asset.safeTransfer(to, amount); 
    emit Withdraw(id, to, amount);
  }
```
## [N-4] Deleting the `move` Function for Kerosene Vaults

## Details
In the design of the system, the kerosene vault will be added to the `vaultsKerosene` mapping. Therefore, the kerosene vault will not participate in the liquidation function, and its assets will not be `move`.  
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47)
```solidity
    function move(uint from, uint to, uint amount) external onlyVaultManager {
        id2asset[from] -= amount;
        id2asset[to] += amount;
        emit Move(from, to, amount);
    }
```

## Suggestion
I'm unsure if the kerosene vault should participate in liquidation in the system design. If it should, I suggest including the kerosene vaults from the vaultsKerosene mapping in the liquidation traversal. If it shouldn't, I suggest deleting the move function for the kerosene vault.

## [N-5] Inconsistent Visibility of Contract Functions with Interface Function Definitions

## Details
The `withdraw` function defined in `IVaultManager` has a visibility of `external`.
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/interfaces/IVaultManager.sol#L55](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/interfaces/IVaultManager.sol#L55)
```solidity
  function withdraw(uint id, address vault, uint amount, address to) external;
```  
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134)
```solidity
    function withdraw(
        uint id,
        address vault,
        uint amount,
        address to
    ) public isDNftOwner(id) { 
```
The inconsistency between interface definition and implementation is a poor practice, especially when there are discrepancies between `calldata` and `memory`.

## Suggestion
Update the visibility of the `withdraw` function in the `IVaultManager` contract.
```solidity
  function withdraw(uint id, address vault, uint amount, address to) external;
```  
## [N-6] Adding a Function to Retrieve Minting Price for DNFTs

## Details
DNFT minting price changes linearly with the supply but there's no convenient function to retrieve its price.   
Github:[https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/DNft.sol#L22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/DNft.sol#L22)
```solidity
  function mintNft(address to)
    external 
    payable
    returns (uint) {
      uint price = START_PRICE + (PRICE_INCREASE * publicMints++);
      if (msg.value < price) revert InsufficientFunds();
      uint id = _mintNft(to);
      if (msg.value > price) to.safeTransferETH(msg.value - price);
      emit MintedNft(id, to);
      return id;
  }
```
This inconvenience affects users.

## Suggestion
Add a function to retrieve the DNFT minting price.
```solidity
  function getMintPrice() public returns(uint256){
    return START_PRICE + (PRICE_INCREASE * publicMints);
  }
```