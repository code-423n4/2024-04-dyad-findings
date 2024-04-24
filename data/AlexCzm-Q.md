## Summary

| Count | Title |
|:-|:-|
| L-01 | vaultManagerV2's `setKeroseneManager` can be front-runned | 
| L-02 | Protocol can use stale price data| 
| L-03 | `vaultsKerosene` data isn't externally exposed  | 
| NC-01 |  Constant should be used instead of magic numbers  | 
| NC_02 |  Modifier not used | 
| NC-03 | Typos in the code |

## [L-01] vaultManagerV2.setKeroseneManager can be front-runned 

DeployV2 script is used to deploy new contracts and set initial state variables. 
Because deployment script is not deployed on chain, each new contract creation/ interaction will be a separate tx. 


A an malicious user  frontrun `vaultManagerV2.setKeroseneManager(kerosneManager)` and set the keroseneManager storage variable.
This will force protocol to deploy new contract/s making spend gas fees.

Foundry team give a [headup](https://book.getfoundry.sh/tutorials/solidity-scripting#high-level-overview) that transaction simulated in a script can differ than onchain tx.

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L62-L67
```solidity
contract DeployV2 is Script, Parameters {
    ...
    KerosineManager kerosineManager = new KerosineManager();

    kerosineManager.add(address(ethVault));
    kerosineManager.add(address(wstEth));

    vaultManager.setKeroseneManager(kerosineManager);//@audit can be front-runned
    ...
  ```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L59-L64
```solidity
//VaultManagerV2.sol

  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager;
  }
  ```
### Recommendations
Consider to protect `setKeroseneManager` with an `onlyOwner` modifier.

---
## [L-02] Protocol can use stale price data

Protocol is using Chainlink price feeds to get the [price](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.wsteth.sol#L92-L106) of assets used as collateral.


```solidity
  uint public constant STALE_DATA_TIMEOUT = 90 minutes; 

  function assetPrice() public view returns (uint) {
      (
        ,
        int256 answer,
        , 
        uint256 updatedAt, 
      ) = oracle.latestRoundData();
      if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
      return answer.toUint256()                        // 1e8
             * IWstETH(address(asset)).stEthPerToken() // 1e18
             / 1e18;
  }
  ```
  Even if stETH/USD price [feed](https://docs.chain.link/data-feeds/price-feeds/addresses?network=ethereum&page=1&search=steth%2Fusd) has a heartbeat of 3600s, protocol is using a 1.5x value to check if the price is stale.
  In case chainlink price feed does not update the price for more than one hour, protocol can still assume the price is healthy.

### Recommendations
Consider using a value closer to  feed's heartbeat. 

---
## [L-03] `vaultsKerosene` data isn't externally exposed

VaultManagerV2 exposes `vaults` information through `getVaults` and `hasVault` functions. 
There is `vaultsKerosene` internal [variable](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L35) that holds same type of information but its data in not exposed externally. 
```solidiy
    function getVaults(uint256 id) external view returns (address[] memory) {
        return vaults[id].values();
    }

    function hasVault(uint256 id, address vault) external view returns (bool) {
        return vaults[id].contains(vault);
        
    }
 ```
### Recommendations
Add 2 new function and expose `vaultsKerosene` data similar to how it's done for `vaults` mapping.

```solidiy
    function getKeroseneVaults(uint256 id) external view returns (address[] memory) {
        return vaultsKerosene[id].values();
    }

    function hasKeroseneVault(uint256 id, address vault) external view returns (bool) {
        return vaultsKerosene[id].contains(vault);
        
    }
 ```

---
## [NC-01] Constant should be used instead of magic numbers

There are a few places where magic numbers are used beside what [bot](https://github.com/code-423n4/2024-04-dyad/blob/main/4naly3er-report.md#nc-1-constants-should-be-defined-rather-than-using-magic-numbers) has found. 
This can be confusing especially when same value has different meaning, depending where it's used.

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L50-L68
```solidity
//Vault.kerosine.unbounded.sol
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
                * vault.assetPrice() * 1e18       //@audit-qa magic number
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;     // @audit-qa magic number
  }
```
---
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L60-L67
```solidity
//Vault.kerosine.sol
  function getUsdValue(
    uint id
  )
    public
    view 
    returns (uint) {
      return id2asset[id] * assetPrice() / 1e8;
  }
```
---
Link to [withdraw](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L147)

Link to [liquidate](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L217)

Link to [redeemDyad](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L195-L198)

```solidity
 function withdraw(uint256 id, address vault, uint256 amount, address to) public isDNftOwner(id) {
  ...
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
...

function liquidate(uint256 id, uint256 to) external isValidDNft(id) isValidDNft(to) {
  ...
        uint cappedCr               = cr < 1e18 ? 1e18 : cr;
  ...
}
function redeemDyad(uint256 id, address vault, uint256 amount, address to)
        external
        isDNftOwner(id)
        returns (uint256)
    {
      ...
      uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;
      ...
    }
```

---
## [NC-02] Modifier not used

VaultManagerV2's `isLicensed` [modifier](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47) is not used anywhere.
```solidity
    modifier isLicensed(address vault) {// @audit-qa modifier not used
        if (!vaultLicenser.isLicensed(vault)) revert NotLicensed();
        _;
    }
  ```
Instead same `if (!vaultLicenser.isLicensed(vault)) revert NotLicensed()` check is used in `add` function:
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
### Recommendations
Removing `isLicensed` modifier the check is required in one place only.

---
## [NC-03] Typos in the code

There are a few typos in code/ comments:

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L25

```solidity

//`MIN_COLLATERIZATION_RATIO` should be `MIN_COLLATERALIZATION_RATIO` (MIN_COLLATER *AL* IZATION_RATIO)
  uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%
  ```
  

Many places where `kerosine` is used instead of `kerosene`. I've leave some of the links:

[KerosineManager](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7) contract name plus where it's imported and used.

[KerosineVault](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12), [KerosineBounded](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L12), [KerosineUnbounded](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L15) contracts names + where they are imported and used