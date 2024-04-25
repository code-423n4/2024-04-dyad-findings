### Low Risk

| Count | Title |
| --- | --- |
| [L-01] | VaultManagerV2::deposit/withdraw does not validate if vault isLicensed |
| [L-02] | KerosineManager::remove  and Licenser::remove will make all the positions liquidatable |
| [L-03] | Depositors using EOAs will have to deposit twice in order to mint the desired amount |
| [L-04] | VaultManagerV2::withdraw can be blocked at no cost |
| [L-05] | VaultManagerV2::remove and removeKerosene can be blocked for 1 wei. |
| [L-06] | Deployment script deploys bounded kerosine without calling setUnboundedKerosineVault |
| [L-07] | Lack of pausing functionality |

| Total Low Risk Issues | 7 |
| --- | --- |

### Non-Critical

| Count | Title |
| --- | --- |
| [NC-01] | Typos |
| [NC-02] | Wrong vault contract is used in VaultManagerV2 |
| [NC-03] | burn() doens’t check if have enough mintedDyad  |

| Total Non-Critical Issues | 3 |
| --- | --- |

## Low Risks

## [L-01] `VaultManagerV2::deposit/withdraw` does not validate if vault `isLicensed`

**Issue Description:**

Users can lose their assets if they deposit in the wrong vault because there is a missing `isLicensed` check.

`safeTransferFrom` doesn’t validate whether an asset is not `address(0)` and whenever users pass the wrong vault their entire deposit will be lost.

[VaultManagerV2.sol#L119-L131](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L131)

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

**Recommendation:**

Add the `isLicensed` modifier to the deposit function:

```diff
 function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
+     isLicensed(vault)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```

## [L-02] `KerosineManager::remove`  and `Licenser::remove` will make all the positions liquidatable

**Issue Description:**

Removing an vault which has non-zero deposits will make all the positions, in it appear as undercollateralized, because it won’t be accounted for in the `getKeroseneValue` and `getNonKeroseneValue` and the collateral of the user will appear as zero, when it is not. This will make the following check to return much lower collateral ratio and all the positions who has been deposited in this vault will be immediately liquidated:

[VaultManager.sol#L230-L239](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230-L239)

```solidity
  function collatRatio(
    uint id
  )
    public 
    view
    returns (uint) {
      uint _dyad = dyad.mintedDyad(address(this), id);
      if (_dyad == 0) return type(uint).max;
      return getTotalUsdValue(id).divWadDown(_dyad);//ISSUE in case of remove getTotalUsdValue(id) will be missing the removed asset, despite there are deposits into it.
      //Equation becomes: much lower number / same amount of dyad tokens minted against the real value of the collateral.
  }
```

**Recommendation:**

Add a check whether there are some deposits in this vault, if so, revert, otherwise remove it successfully.

## [L-03] Depositors using EOAs will have to deposit twice to mint the desired amount

**Issue Description:**

Due to missing function which deposits collateral and mints `DYAD` tokens at the same time, EOA users can be forced to deposit once again, if between the `deposit` and `mintDyad` functions price of the deposited collateral decreases. 

The ones who will face this issue most frequently are the **liquidators**, they will usually deposit and mint around 150% collateral ratio. Moreover, since the vault assets will be highly volatile (WETH and wstETH), slightly decrease in price in between the 2 transaction will make them undercollateralized and they either will have to deposit more, face the liquidation or intentionally burn their `DYAD` tokens, instead of successfully liquidating the desired dNft.

We can observe that there is a `redeemDyad` function that burns the `DYAD` tokens and withdraws from the `Vault` in the same transaction, but there isn’t for `deposit`.

[VaultManagerV2.sol#L119-L131](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L131)

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

[VaultManagerV2.sol#L156-L169](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156-L169)

```solidity
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
```

**Recommendation:**

Add function that deposit and mints in the same transaction.

## [L-04] `VaultManagerV2::withdraw` can be blocked at no cost

**Issue Description:**

Since everyone with minted dNft can call `VaultManagerV2::deposit`, front run protection which was added to the V2 of the `VaultManager` can be utilized by a griefer to block any call to `withdraw` function with 0 tokens transfer (if asset supports it, otherwise 1 wei is enough). When someone calls `deposit` function, `idToBlockOfLastDeposit[id]` is set to the current `block.number` .  After that `idToBlockOfLastDeposit[id]` is used in the `withdraw` function. Now anyone with a minted dNft can call deposit with 0 wei on behalf of a user, frontrunning his `withdraw` execution. The result will be a DoS for the `withdrawer` of the duration (or even more if the liquidator is financially incentivised to do it) of a block.

[VaultManagerV2.sol#L127](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L127C5-L127C47)

```solidity
  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number; //ISSUE set to current
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```

[VaultManagerV2.sol#L143](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L143)

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
    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();//ISSUE revert on current
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

**Recommendation:**

Check if the deposit occured at the same `block.number` as the withdraw is from the withdrawer itself, otherwise revert.

## [L-05] `VaultManagerV2::remove and removeKerosene` can be blocked for 1 wei

**Issue Description:**

Anyone can block removal of vault in the `VaultManagerV2` contract by simply depositing at least 1 wei, this will make the `id2asset` of this nftId non-zero and grief the removal.

The issue is possible because everyone can `deposit` to any dNft, even without having one.

[VaultManager.sol#L94-L116](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L116)

```solidity
 function remove(
      uint    id,
      address vault
  ) 
    external
      isDNftOwner(id)
  {
    if (Vault(vault).id2asset(id) > 0) revert VaultHasAssets();//ISSUE
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
    if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets();//ISSUE
    if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
    emit Removed(id, vault);
  }
```

**Recommendation:**

Instead of reverting when `id2asset` is a non-zero, just execute the `withdraw` function once again with the amount, this will send the donated tokens to the owner of that nft.

## [L-06] Deployment script deploys bounded kerosine without calling `setUnboundedKerosineVault`

**Issue Description:**

Deployment of the `BoundedKerosineVault` happens without calling `setUnboundedKerosineVault`, that will eventually make the price of the asset 0, when admin license it and users begin to use it. The consequences will be that it won’t support depositor’s collateral rate and will limit their minting capabilities.

[DeployV2.sol#L78-L82](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L78-L82)

```solidity
 BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault(
      vaultManager,
      Kerosine(MAINNET_KEROSENE), 
      kerosineManager
    );
```

**Recommendation:**

Despite that it is not going to be used for now, call the `setUnboundedKerosineVault` in the script as well.

## [L-07] Lack of pausing functionality

**Issue Description:**

All the contracts are lacking pausable functionality, which can be crucial for preventing potential exploits that can occur in the system. Currently, there is no way to freeze the system, unless there are no funds in it. In the other scenarios, contracts are completely helpless.

**Recommendation:**

The most straightforward solution would be to use the `Pausable` from `OpenZeppelin` - https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Pausable.sol

## **Non-Critical**

## **[N‑01] Typos**

**Issue Description:**

There are numerous typographical errors presented in the contracts in scope:

`ethVault`, should be `wethVault` - https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L49

`wstEth`, should be `wstEthVault` - https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L56

## [N-02] Wrong vault contract is used in `VaultManagerV2`

**Issue Description:** 

`KerosineVault` and Vault are two different base class. When cast kerosine vault address to use their function, it cast them to Vault, instead of `KerosineVault`.

[VaultManagerV2.sol#L94-L104](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L94-L104)

[VaultManagerV2.sol#L269-L286](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L269-L286)

```solidity
function removeKerosene(
    uint    id,
    address vault
) 
  external
    isDNftOwner(id)
{
  if (Vault(vault).id2asset(id) > 0)     revert VaultHasAssets(); // @audit - use KerosineVault
  if (!vaultsKerosene[id].remove(vault)) revert VaultNotAdded();
  emit Removed(id, vault);
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
      Vault vault = Vault(vaultsKerosene[id].at(i)); // @audit - use KerosineVault
      uint usdValue;
      if (keroseneManager.isLicensed(address(vault))) {
        usdValue = vault.getUsdValue(id);        
      }
      totalUsdValue += usdValue;
    }
    return totalUsdValue;
}
```

## [N-03] `burn()` doens’t check if have enough `mintedDyad`

**Issue Description:** 

`burn()` doens’t check if the amount passed is ≤ `mintedAmount`. Which will cause the function to revert, make it possible to burn the whole amount if pass higher amount.

[VaultManagerV2.sol#L172-L181](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172-L181)

```solidity
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