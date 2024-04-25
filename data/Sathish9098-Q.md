## 

## [L-1] The lack of dynamic re-checks of licensing status introduces several operational and security risks

## Impact

The VaultManagerV2 contract delegates the responsibility of ensuring that vaults meet specific standards to the KerosineManager and Licenser through a licensing mechanism. Vaults are required to be licensed before they can be added to vaults or vaultsKerosene mappings. However, once added, there is no mechanism within VaultManagerV2 to monitor or react to any subsequent changes in the licensing status of these vaults.

Once a vault is added to the system, its licensing status isn't dynamically checked during each operation it performs. This means that a vault, once added as licensed, could later be deemed unlicensed by KerosineManager or Licenser without VaultManagerV2 being aware or able to restrict its operations based on this new status.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

/// @inheritdoc IVaultManager
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
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L66-L91

## Recommended Mitigation
Implement an event-listening mechanism that reacts to changes in licensing status by KerosineManager and Licenser, ensuring the contract dynamically adjusts the operational status of vaults based on their current licensing.

##

## [L-2] Risks of Narrow Asset Checks in Vault Removal from VaultManagerV2

## Impact

The VaultManagerV2 contract allows vault owners to remove a vault using remove and removeKerosene functions if there are no assets associated with a particular DNft ID. This condition is checked using Vault(vault).id2asset(id) > 0, which only considers assets linked to a specific DNft ID. This approach does not account for other potential assets or liabilities that may be associated with the vault but not directly linked to that DNft ID.

#### Specific Concerns:

- The check is limited to assets tied directly to a specific DNft ID. This implies that other assets or collateral possibly held in the vault but under different identifiers or unlinked to any DNft are not considered in the removal process.

- Operations that may be indirectly linked to the vault, such as those pending settlement or part of ongoing multi-step transactions, are not accounted for. Removing a vault while such operations are in progress can disrupt these processes.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

 /// @inheritdoc IVaultManager
  function remove(
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
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L93-L116

##

## [L-3] Single Block Transaction Risks in mintDyad() and burnDyad() functions

- Without same-block checks, an attacker could potentially manipulate the market by minting a large number of Dyad tokens within a single block, possibly just after significant transactions like deposits. This could be used to artificially inflate the supply, affecting the token’s price or the collateralization ratios of the vaults.

- Similarly, an attacker could burn a substantial number of tokens in a strategically timed transaction that could coincide with other market activities (like large withdrawals), artificially reducing the supply and potentially causing a spike in token value or creating favorable conditions for other manipulative activities.

Both mintDyad and burnDyad are susceptible to flash loan attacks. In such an attack, an actor borrows a large amount of assets and uses them within the same block to influence the contract's state or outcome. For instance, an attacker could use borrowed funds to manipulate the collateral levels or market conditions, execute a mintDyad or burnDyad, and then settle the loan, all within one block. This rapid sequence of actions could be used to create temporary but exploitative conditions that benefit the attacker.

```soldiity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

  /// @inheritdoc IVaultManager
  function mintDyad(
    uint    id,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
  {
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
    dyad.mint(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
    emit MintDyad(id, amount, to);
  }

  /// @inheritdoc IVaultManager
  function burnDyad(
    uint id,
    uint amount
  ) 
    external 
      isValidDNft(id)
  {
    dyad.burn(id, msg.sender, amount);
    emit BurnDyad(id, amount, msg.sender);
  }

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L155-L181

### Recommended Mitigation
Consider adding the block checking mapping like ``idToBlockOfLastDeposit`` to mintDyad and burnDyad functions 

##

## [L-4] Lack of events in ``deposit()`` and ``withdraw()`` functions

The ``deposit()`` and ``withdraw()`` functions in the VaultManagerV2 contract are crucial for managing the flow of assets into and out of vaults. In Solidity, events are essential for creating searchable logs and providing external observers with a reliable way to track changes and interactions within the contract.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

 /// @inheritdoc IVaultManager
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

  /// @inheritdoc IVaultManager
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
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }


```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L118-L153

##

## [L-5] Discrepancy Between Revert Message and Original Check in ``withdraw() `` function

The withdraw function in your VaultManagerV2 contract includes a specific revert statement: revert DepositedInSameBlock();. This is used to prevent withdrawal transactions from being processed in the same block as a deposit for the same id. But the revert message like DepositedInSameBlock this is technically wrong for withdraw function .This should be WithdrawInSameBlock()

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

143: if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L143

##

## [L-6] Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

  idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L127-L130

##

## [L-7] Functions ``deposit``, ``withdraw``, ``mintDyad``, and ``redeemDyad`` vulnerable to reentrancy attack

Functions like deposit, withdraw, mintDyad, and redeemDyad interact with external contracts (Vault and ERC20). These should ideally include reentrancy guards to prevent potential attacks where callbacks from the called contracts could lead to unexpected behaviors or exploits.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

119:  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {

133: /// @inheritdoc IVaultManager
  function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
      isDNftOwner(id)

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L125

##

## [L-8] ``VaultManagerV2`` Contract is vulnerable to single oracle failures 

The VaultManagerV2 contract, like many decentralized finance (DeFi) applications, may rely on a single oracle for retrieving asset prices, which introduces a significant vulnerability to failures or manipulation associated with that oracle. The oracle that the VaultManagerV2 contract depends on fails, delivers incorrect data due to a bug, experiences downtime, or is subjected to tampering, the entire contract could operate on faulty data.

This could lead to several adverse outcomes, such as:
Incorrect pricing information being used for critical functions like collateral valuation, triggering incorrect liquidations or collateral calls.
Transactions being frozen if the oracle data is not available, affecting the contract's liquidity and user operations.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

 uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L146-L149

##

## [L-9] Asset Price Calculation is prone to rounding errors due to the division by powers of 10

### Impact

The method of calculating the asset value within the withdraw function is prone to rounding errors due to the division by powers of 10 related to the asset and oracle decimals. This can lead to significant inaccuracies in value calculations, especially with large numbers or assets with high decimal places.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

143:  uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();

195: uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L195-L198

### Recommendation 

Use ``FixedPointMathLib`` for all calculations involving decimals to ensure that rounding errors are minimized.

##

## [L-10] Inadequate Validation in Asset Withdrawal check

The withdraw function allows for asset transfers based on the collatRatio(id). If the price feed, which the collateral ratio depends on, is quickly changes due to market volatility, the collateral check might pass erroneously, allowing for under-collateralized withdrawals.

```solidity
FILE: 2024-04-dyad/src/core/VaultManagerV2.sol

152: if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 

```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L152

##

## [L-11] Use of the view Modifier in the withdraw Function

### Impact
The use of view could confuse developers and users about the function's capabilities and lead to incorrect assumptions about its effects on contract state.

The withdraw function is marked as view, which implies that it is intended only to read from the blockchain state and not modify it. However, the function is designed to revert transactions, which contradicts its intended use as a view function. This is likely a mistake in the function design.

```solidity
FILE: 2024-04-dyad/src/core/Vault.kerosine.bounded.sol

function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
    view
      onlyVaultManager


```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L39

##

## [L-12] Misleading Functionality of the ``withdraw()`` Function in BoundedKerosineVault Contract

### Impact
Keeping a non-functional withdrawal method could confuse or mislead users or developers, potentially affecting the contract's usability or integrations.

The withdraw function is designed to always revert, which raises questions about its purpose. If the function is not supposed to allow withdrawals, its presence can be misleading.

```solidity
FILE: 2024-04-dyad/src/core/Vault.kerosine.bounded.sol

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


```
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32-L39














 