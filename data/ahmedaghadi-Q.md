## [L-01] Can't add `KerosineVault` through `VaultManagerV2::addKerosene` function.

The `VaultManagerV2::addKerosene` function is as follows ( [https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80) ):

```solidity
    function addKerosene(
        uint    id,
        address vault
    )
    external
        isDNftOwner(id)
    {
    if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE) revert TooManyVaults();
@-> if (!keroseneManager.isLicensed(vault))                 revert VaultNotLicensed();
    if (!vaultsKerosene[id].add(vault))                     revert VaultAlreadyAdded();
    emit Added(id, vault);
    }
```

`BoundedKerosineVault` and `UnboundedKerosineVault` are not licensed by `KerosineManager` contract in deployment script, also it's not possible to license them through `KerosineManager::licenseVault` function as `UnboundedKerosineVault::assetPrice` function loops through all the licensed vaults to calculate `kerosine` price and due to protocol constraints that `kerosine` price shouldn't consider kerosine but only exogenous assets. So, it's not possible to add `KerosineVault` through `VaultManagerV2::addKerosene` function.

For reference, `UnboundedKerosineVault::assetPrice` function is as follows ( [https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50) ):

```solidity
    function assetPrice()
    public
    view
    override
    returns (uint) {
        uint tvl;
@-->    address[] memory vaults = kerosineManager.getVaults();
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
        return numerator * 1e8 / denominator;
    }
```

Even though `unboundedKerosineVault` is already licensed with `vaultLicenser` contract in deployment script, `VaultManagerV2::addKerosene` function can't check for `vaultLicenser` instead of `keroseneManager` to check if the vault is licensed or not, as then user will be able to add `NON-KEROSENE` vaults as `KEROSENE` vaults through `VaultManagerV2::addKerosene` function because there's no distinction between `KEROSENE` and `NON-KEROSENE` vaults in the `vaultLicenser` contract.

It can be fixed by adding `EnumerableSet.AddressSet` variable for all the `KEROSENE` vaults in `keroseneManager` contract and then checking if the vault is in the set or not in the `VaultManagerV2::addKerosene` function.

Another issue is that as `wethVault` and `wstEth` are licensed by `keroseneManager` contract in the deployment script, so they can be added as `KEROSENE` vaults through `VaultManagerV2::addKerosene` function. But, as `weth` and `wstEth` are not `KEROSENE` vaults, so they shouldn't be added as `KEROSENE` vaults through `VaultManagerV2::addKerosene` function.

For reference, `wethVault` and `wstEth` are licensed by `keroseneManager` contract in the deployment script as follows ( [https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L64-L65](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L64-L65) ):

```solidity
    kerosineManager.add(address(ethVault));
    kerosineManager.add(address(wstEth));
```

## [L-02] `VaultManagerV2::withdraw` function has incorrect NatSpec.

The NatSpec for `VaultManagerV2::withdraw` function is as follows ( [https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134) ):

```solidity
    /// @inheritdoc IVaultManager
    /**
    * @notice Allows a dNFT owner to withdraw collateral from a vault
    * @param id The ID of the dNFT for which the withdraw is being made.
@-> * @param vault The vault where the assets will be deposited.
@-> * @param amount The amount of assets to be deposited.
    * @param to The address where the assets will be sent.
    */
```

In the place `withdraw` keyword, it consists of `deposit` keyword. So, it should be corrected.

## [L-02] `VaultManagerV2::withdraw` function won't let user withdraw any amount of `KEROSENE` assets if no exogenous assets is deposited as collateral.

The `VaultManagerV2::withdraw` function is as follows ( [https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134) ):

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
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice()
                    * 1e18
                    / 10**_vault.oracle().decimals()
                    / 10**_vault.asset().decimals();
@-> if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow();
    }
```

Here, if user has only deposited `KEROSENE` as collateral in the vault and haven't deposited any exogenous assets i.e `NON-KEROSENE` assets as collateral, then they won't be able to withdraw any amount of `KEROSENE` assets from the vault.

As `getNonKeroseneValue(id)` will be 0 whereas `value` will be greater than 0. So, `getNonKeroseneValue(id) - value` will underflow.

## Proof of Concept

For example, consider the following scenario:

- User has deposited some `KEROSENE` assets in the vault.
- User hasn't minted any `Dyad` tokens ( also they can't mint any `Dyad` tokens just using `KEROSENE` assets ).
- Thus, `dyadMinted` for user is 0.
- Now user wants to remove some amount of the collateral ( `KEROSENE` assets ) from the vault.
- In `VaultManagerV2::withdraw` function, `getNonKeroseneValue(id)` will be 0 and `value` will be greater than 0.
- Thus, `getNonKeroseneValue(id) - value` will underflow as `0 - value` where `value` is greater than 0 will underflow.
- Therefore, user won't be able to withdraw any amount of `KEROSENE` assets from the vault unless they deposit some exogenous assets as collateral in the vault.

Assets not at direct risk, but the function of the protocol or its availability could be impacted. Thus, the severity is medium.

## Recommended Mitigation Steps

It can be fixed by checking whether the vault from which withdrawal is to be done is `KEROSENE` vault or not. If it's a `KEROSENE` vault then the check for enough exogenous collateral should be skipped. So, a `EnumerableSet.AddressSet` variable can be defined which will contains all the `KEROSENE` vaults in `keroseneManager` contract and then it can be checked if the vault is in the set or not ( i.e a vault is `KEROSENE` vault or not ) in the `VaultManagerV2::withdraw` function.
