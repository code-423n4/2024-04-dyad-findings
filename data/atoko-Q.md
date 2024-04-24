## Low Issues

| Number |                   Issue                    | 
| ------ | :----------------------------------------: | 
| [L-01] |     Relience on `decimals()` function      |
| [L-02] |            Centralization Risk             |
| [L-03] |            Add donate function             |
| [L-04] | Not emitting events for critical functions |
| [L-05] |  Missing fallbacks for price feed oracle   |
| [L-06] |  Reentrancy   |
| [L-07] |  function missing input validation   |

## [L-01] Relience on `decimals()` function

relience on the ERC20 decimals() function for asset calculation, assuming that tokens conform to the ERC20 standard. If a token does not implement decimals(), the redemption process may fail, disrupting the protocol's functionality and causing inconvenience to users.

**Instances**

```javascript
VaultManagerV2.sol
function redeemDyad(
        uint id,
        address vault,
        uint amount,
        address to
    ) external isDNftOwner(id) returns (uint) {
        dyad.burn(id, msg.sender, amount);
        Vault _vault = Vault(vault);
        uint asset = (amount *
@--->            (10 ** (_vault.oracle().decimals() + _vault.asset().decimals()))) /
            _vault.assetPrice() /
            1e18;
        withdraw(id, vault, asset, to);
        emit RedeemDyad(id, vault, amount, to);
        return asset;
    }
```

```javascript
 function withdraw(
        uint id,
        address vault,
        uint amount,
        address to
    ) public isDNftOwner(id) {
        if (idToBlockOfLastDeposit[id] == block.number)
            revert DepositedInSameBlock();
        uint dyadMinted = dyad.mintedDyad(address(this), id);
        Vault _vault = Vault(vault);
        uint value = (amount * _vault.assetPrice() * 1e18) / //@audit----info chainlink
@--->            10 ** _vault.oracle().decimals() /
@--->            10 ** _vault.asset().decimals();
        if (getNonKeroseneValue(id) - value < dyadMinted)
            revert NotEnoughExoCollat();
        _vault.withdraw(id, to, amount);
        if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();
    }
```

## [L-02] Centralization Risk

The protocol overral operations relies on a centralized owner or parties, posing risks of owner bias and single point of failure.

## [L-03] Add donate function

When a users collateral falls below threshold they could be liquidated, and when not done in time it could lead to undercollateralization of the protocol. At the moment it will be difficult to solve this issue of undercollateralization.

Add a function to donate and help undercollateralization to the protocol so that when the issue arised some funds could be send to the protocol

## [L-04] Not Emitting Events for critical functions

Events help non-contract tools to track changes, and events prevent users from being surprised by changes. some important functions do not emit events

**Instances**

- KerosineManager.sol

```javascript
function add(address vault) external onlyOwner {
        if (vaults.length() >= MAX_VAULTS) revert TooManyVaults();
        if (!vaults.add(vault)) revert VaultAlreadyAdded();
    }

    function remove(address vault) external onlyOwner {
        if (!vaults.remove(vault)) revert VaultNotFound();
```

## [L-05] Missing fallbacks for price feed oracle

The DYAD protocol does not implement fallback solutions for price feed oracle. In case Chainlink's aggregators fail to update price data, the protocol will not work as expected since it will not be able to fetch prices as usual. implement fallback solutions, such as using other off-chain oracle providers and/or on-chain Uniswap's TWAP, for feeding price data in case Chainlink's aggregators fail.

## [L-05] Reentrancy

There is pottential Reentrancy vulnerability in the `deposit` function below

```javascript
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

consider adding a reentrancy guard in the functions and contracts to prevent this vulnerability

[L-07] function missing input validation
some functions in the contract are missing sufficient input validation, this could cause some vulnerabilities and unexpected behavior in the protocol

```javascript
 function add(address vault) external onlyOwner {
        if (vaults.length() >= MAX_VAULTS) revert TooManyVaults(); 
        if (!vaults.add(vault)) revert VaultAlreadyAdded();
    }

    function remove(address vault) external onlyOwner {
        if (!vaults.remove(vault)) revert VaultNotFound();
    }
```

## Non-Critical Issues

| Number        |          Issue           | 
| ------------- | :----------------------: | 
| [N-01]        | Missing Natspec comments |   
| [N-02]      |         functions can be made more simple  |    
| [N-03] |        public functions not called by contract should be external       |    
| [N-04] |        consider using named function arguments       |    
| [N-05] |        consider using named returns       |    
| [N-06] |        interfaces should each be defined in separate files       |    
| [N-07] |        Top-level declarations should be separated by at least two lines       |    

## [N-01] Missing Natspec Comments

NatSpec comments provide rich code documentation. The following functions miss NatSpec comments. Please consider adding NatSpec comments for these functions.

```javascript
function add(uint id, address vault)
function addKerosene(uint id, address vault)
 function remove(uint id, address vault)
function removeKerosene(uint id, address vault)
function deposit( uint id, address vault, uint amount)
function withdraw( uint id, address vault, uint amount, address to)
function mintDyad( uint id, uint amount, address to)
function burnDyad(uint id, uint amount)
function redeemDyad( uint id, address vault, uint amount, address to)
function liquidate(uint id,   uint to)
 function collatRatio(uint id)
function getNonKeroseneValue(uint id)
function getKeroseneValue(uint id)
function getVaults(uint id)
function hasVault(uint id, address vault)


```

add Natspec comments to all the functions in the contracts for better code documentation

[N-02] functions can be made more simple 

some functions could me made more simple to improve code readeability for instance the liquidate function contains some logic to check if the user can be liquidated, this can be made more simple by transferring the logic to a seperate function `isliquidatable to check if a user can be liquidated` this could be used in all other function eg `withdraw` ` mintDyad`

## [N-03]  public functions not called by contract should be external 

public functions not called by the contract should be declared external instead

**instances**

* BoundedKerosineVault.sol

```javascript
function assetPrice() public view override returns (uint) {
        return unboundedKerosineVault.assetPrice() * 2;
    }

```
## [N-04] consider using named function arguments  

When calling functions in external contracts with multiple arguments, consider using named function parameters, rather than positional ones.

**Instances**

* VaultManagerV2.sol

```javascript
  return getTotalUsdValue(id).divWadDown(_dyad);
  Vault vault = Vault(vaults[id].at(i));
   return vaults[id].contains(vault);
```

## [N-05] consider using named returns 

Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

**Instances**

* VaultManagerV2.sol


```javascript
 function hasVault(uint id, address vault) external view returns (bool) {
        return vaults[id].contains(vault);
    }

 function getKeroseneValue(uint id) public view returns (uint) 
 
 function getNonKeroseneValue(uint id) public view returns (uint)

 function getTotalUsdValue(uint id) public view returns (uint)

 function collatRatio(uint id) public view returns (uint)

 function redeemDyad( uint id, address vault, uint amount, address to) returns (uint)


```

* KerosineManager.sol
  
```javascript
  function isLicensed(address vault) external view returns (bool)
```
* UnboundedKerosineVault.sol
  
```javascript
  function assetPrice() public view override returns (uint)
```

## [N-06] interfaces should each be defined in separate files

The interfaces below should be defined in separate files, so that it’s easier for future projects to import them, and to avoid duplication later on if they need to be used elsewhere in the project

* VaultManagerV2.sol


```javascript
import {IVaultManager} from "../interfaces/IVaultManager.sol";
```

* UnboundedKerosineVault.sol

```javascript
import {IVaultManager} from "../interfaces/IVaultManager.sol";
```
## [N-07] Top-level declarations should be separated by at least two lines

Top-level declarations should be separated by at least two lines