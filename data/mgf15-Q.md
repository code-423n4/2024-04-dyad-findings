## [L-1] no check if `from` or `to` is zero address

Adding a check to ensure neither the from nor the to address is zero would enhance the safety of the move function. 

```solidity

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
```
[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47C3-L58C4)
## [L-2] no check if `from` == `to`

A check to verify if `from` is equal to `to` would prevent the function from erroneously transferring assets to and from the same address.

```solidity

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
```
[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L47C3-L58C4)

[L-3] denominator can be manipulated by send token to `MAINNET_OWNER`

Manipulation of the denominator by sending tokens to MAINNET_OWNER could lead to unexpected or unfair outcomes.


```solidity
function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```

[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L17C3-L22C5)

## [L-4] deposit not revert if the amount is 0

Reverting the transaction when the deposit amount is zero would prevent unnecessary gas expenditure and clarify the intent of the function. If the amount is zero, there's typically no meaningful action to perform, so reverting would provide immediate feedback to the caller.

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

## [N-1] Unused `modifier` definition 

The following modifiers are never used, consider to remove them.

```solidity
45:  modifier isLicensed(address vault) {
46:    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
47:  }
```
[Link](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L45-L47)