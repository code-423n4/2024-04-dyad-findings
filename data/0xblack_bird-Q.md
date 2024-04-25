## [L-01] Deposit() can deposit to any vault might result in dos
in function `Deposit`takes a vault address & id as argument but doesnt perform any owner checks,possibly allowing anyone to deposit to any id corresponding vault.

```solidity

function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }

```
However,the vulnerability arises when a legitimate user wants to withdraw their funds 

```solidity

function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
      isDNftOwner(id)
  {
    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

```
In the withdraw function theres a check where it `(idToBlockOfLastDeposit[id] == block.number)` a malicious user can deposit a small amount to the legit user whos trying to withdraw their funds,reverting the transaction.
Consider adding a grace period or msg sender check.

## [L-02] Remove Vault can be susceptible to dos

in the function `remove` 

```solidity
  function remove(
      uint   id,
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
`if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();` will cause revertion if a attacker deposits to the vault making the user not be able remove the vault, resulting in dos.

## [L-03] BurnDyad() doesn't check if the right address in mapping is updated.

in `BurnDyad` function it uses `isValidDNft(id)` 

although it is burning tokens from the msg.sender 
the accouting is incorrect in the `mintedDyad[msg.sender][id] -= amount;` if an attacker passes an arbitrary id it might cause system to be in an unexpected state.

# recommendation 

use `isDNftOwner(id)` modifier

## [L-04] redeemDyad() doesn't check for minimum amount out.

in the `redeemDyad` function user doesn't have an input for a minimum expected output amount
 
```solidity
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
      uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;
      withdraw(id, vault, asset, to);
      emit RedeemDyad(id, vault, amount, to);
      return asset;
  }

```

Due to several external conditions it might be advised for a better user experiance ,to have a minimum amount output argument passed to the function to better the functionality.

## [L-05]: Solmate's SafeTransferLib does not check for token contract's existence

There is a subtle difference between the implementation of solmate's SafeTransferLib and OZ's SafeERC20: OZ's SafeERC20 checks if the token is a contract or not, solmate's SafeTransferLib does not.

# instances -

 - (src/core/Vault.kerosine.unbounded.sol#L13)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- (src/core/VaultManagerV2.sol#L13)
	```solidity
	import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

## [NC-01]: modifier barely used

```solidity
modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }

```

this modifier is barely used in the contract,use it more rather calling external contract.

## [NC-02]: wrong revert statement

```solidity

if (!vaults[id].remove(vault))     revert VaultNotAdded();

```
if vault is not removed it is supposed to say VaultNotRemoved rather than VaultNotAdded.