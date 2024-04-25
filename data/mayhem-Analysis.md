# Overview
Dyad is a stablecoin minted through a collateralized debt position ecosystem. Users mint a dNFT as the entry point into the system. The dNFT allows users to deposit and withdraw collateral (wETH, wstETH), mint and redeem Dyad, and liquidate positions below 150% collateral ratios. 

The goal is to maintain a 150% collateralization ratio with the current accepted assets wETH and wstETH. This means that each Dyad is backed by $1.50. The extra collateralization gives value to another token in the ecosystem, an ERC20, Kerosene. The value of Kerosene is deterministic based the total USD value of all wETH and wstETH collateral, the total supply of Dyad stablecoins, and the total supply of Kerosene tokens.

The Dyad stablecoin is already live with 1M TVL. The project is implementing an updated vault management system and introducing the Kerosene token. Each type of collateral is placed within it's own vault. Kerosene can also be used as collateral, but it does not count towards the 150% collateralization ratio. 

This audit contest focuses on the new vault management system and Kerosene token.

# Architecture
## Actors
**User**
The user is represented through the `dNFT`. The `dNFT` allows users to deposit, withdraw, mint dyad, redeem dyad, and liquidate other `dNFT` positions. 

**Vaults**
The system revolves around vaults. A user's initial interaction with the system (after minting a `dNFT`) will be to deposit collateral. The collateral is stored in a vault. Currently there are two vaults: wETH and wstETH.  There are also two vaults related to the Kerosene token: unbounded and bounded vaults.  Mappings keep track of `dNFT` ids and their claim to assets in the vault.    

**Licenser**
The Licenser adds vaults to the system. In order for a vault to accept collateral, it must first be licensed. This occurs during deployment. The `msg.sender` of the Deploy script becomes the Licenser. After contracts are deployed and a Licenser is set, vaults are licensed by the Licenser. 

**Vault Manager/Kerosene Manager**
The vault manager allows `dNFTs` to participate in the vault system. The vault manager mediates interactions such as deposit and withdraw. When a user deposits collateral through their `dNFT`, the vault managers first has to check if the vault containing the asset is licensed. The Kerosene manager oversees the Kerosene vaults and performs the same checks as the Vault manager. 

## System Design
![Dyad](https://i.ibb.co/dr7Yhx2/dyad-map.png)

# Codebase 
## Analysis
The codebase is well organized. It utilizes interfaces and libraries from OpenZeppelin and Solmate. While not all files have comments, the interface files have comments and describe the purpose of each function. 

Concerns are logically separated into different files:
- A single file defines the parameters of vault. 
- All of the interactions a `dNFT` can initiate are handled in a vault manager file. 
- Kerosene vaults have their own file. 

## Files
### `VaultManagerV2`
- Inherits `IVaultManager`, `Initializable`

This file handles the majority of user interactions. When a dNFT owner wants to add or withdraw collateral, mint or redeem Dyad, or liquidate another dNFT holder's position, `VaultMangerV2` handles all of that logic. 

The ecosystem is based on vaults. Each type of collateral has its own vault. The vaults are managed by two mappings: `vaults` and `vaultsKerosene`. `dNFT` ids are mapped to a set using the `EnumerableSet` library. The interactions with the functions in this file updates mappings, but the actual asset amount in `vault` is handled in a different file `Vault.sol`.

So this file associated a `dNFT` id with `vault` addresses.

| Function              | Access                                    | Effects                                                                                                                                                                                          |
| --------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `setKeroseneManager`  | `initializer`, `external`                 | Used in the deploy script to set address for the `KerosineManger` file                                                                                                                           |
| `add`                 | `isDNftOwner`, `external`                 | Updates `vaults` mapping with `dNFT` id and `vault` address                                                                                                                                      |
| `addKerosene`         | `isDNftOwner`, `external`                 | Updates `vaultsKerosene` mapping with `dNFT` id and `vault` address                                                                                                                              |
| `remove`              | `isDNftOwner`, `external`                 | Removes a `vault` from associated `dNFT` if it doesn't have any assets                                                                                                                           |
| `removeKerosene`      | `isDNftOwner`, `external`                 | Removes a kerosene `vault` from associated `dNFT` if it doesn't have any assets                                                                                                                  |
| `deposit`             | `isValidDNft`, `external`                 | Adds the amount to the `vault` address mapped to the `dNFT` id                                                                                                                                   |
| `withdraw`            | `isDNftOwner`, `public`                   | Withdraws selected amount to a selected wallet address from the `vault` address mapped to the `dNFT` id                                                                                          |
| `mintDyad`            | `isDNftOwner`, `external`                 | If the collateralization remains above 150% for the associated `dNFT` id, the amount of Dyad is sent to selected address                                                                         |
| `burnDyad`            | `isValidDNft`, `external`                 | The `burn` function from the `Dyad.sol` file is called. The input amount is removed from the `mintedDyad` mapping                                                                                |
| `redeemDyad`          | `isDNftOwner`, `external`                 | The `burn` function from the `Dyad.sol` file is called. Converts decimal amount of asset. Calls `withdraw` function                                                                              |
| `liquidate`           | `isValidDNft`,  `isValidDNft`, `external` | Checks collateral ratio. Transfers collateral from id of `dNFt` being liquidated to id of `dNFT` performing liquidation. This is done by moving collateral between `vaults` found in `Vault.sol` |
| `collatRatio`         | `public`                                  | Returns a `uint` that is the division of the total usd value and the amount of Dyad minted using the `FixedPointMathLib` library.                                                                |
| `getTotalUsdValue`    | `public`                                  | Returns a `uint` of the total usd value of both kerosene, and non kerosene vaults for the associated `dNFT` id                                                                                   |
| `getNonKeroseneValue` | `public`                                  | Returns a `uint` of the total usd value of wETH/wstETH vaults for the associated `dNFT` id                                                                                                       |
| `getKeroseneValue`    | `public`                                  | Returns a `uint` of the total usd value of kerosene vaults for the associated `dNFT` id                                                                                                          |
| `getVaults`           | `external`                                | Returns an array of vault addresses for the associated `dNFT` id                                                                                                                                 |
| `hasVault`            | `external`                                | Returns a `boolean` on whether the `dNFT` id contains the `vault` address                                                                                                                        |

### `KerosineManager`
- Inherits `Owned`. Owner is set to `msg.sender`

This files manages Kerosene vaults. A maximum amount of 10 vaults can be created. The vaults are stored in `vaults` which is a private `EnumerableSet.AddressSet` from the `EnumerableSet` library.

| Function     | Access                  | Effects                                                          |
| ------------ | ----------------------- | ---------------------------------------------------------------- |
| `add`        | `onlyOwner`, `external` | Adds a `vault` address to `vaults`                               |
| `remove`     | `onlyOwner`, `external` | Removes a `vault` address from `vaults`                          |
| `getVaults`  | `external`              | Returns an array of all the `vault` addresses in `vaults`        |
| `isLicensed` | `external`              | Returns a boolean on whether `vaults` contains a `vault` address |

### `Vault.kerosine`
- Inherits `Ivault`, `Owned`. Owner is set to `msg.sender`

This file is meant to be inherited by the other Kerosine vault files. It is responsible for tracking the assets associated with a `dNFT` id. This is done through the `id2asset` mapping which maps a `dNFT` id to an asset amount.

| Function      | Access                         | Effects                                                                                         |
| ------------- | ------------------------------ | ----------------------------------------------------------------------------------------------- |
| `deposit`     | `onlyVaultManager`, `public`   | Increments an amount to the associated `dNFT` id in the `id2asset` mapping.                     |
| `move`        | `onlyVaultManager`, `external` | Moves the asset amount from a `dNFT` id to another `dNFT` id updating the `id2asset` mapping.   |
| `getUsdValue` | `public`                       | Returns a `uint` of the usd value of the assets associated with the `dNFT` id                   |
| `assetPrice`  | `public`, `virtual`            | This function will be overriden when used by the other Kerosene vault files and return a `uint` |

### `Vault.kerosine.bounded.sol`
- Inherits `KerosineVault` (`Vault.Kerosine`)

This is a vault for Kerosene ERC20. Kerosene can be bounded or unbounded. This file handles bounded Kerosene vault. Bounded Kerosene can't be withdrawn and it is double the price of regular Kerosene. 

| Function                    | Access                         | Effects                                                                                                                                 |
| --------------------------- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `setUnboundedKerosineVault` | `onlyOwner`, `external`        | Sets the vault address for `UnboundedKerosineVault`                                                                                     |
| `withdraw`                  | `onlyVaultManager`, `external` | "Bounded" Kerosene is not withdrawable. This is seems to be related to staking.                                                         |
| `assetPrice`                | `piblic`, `override`           | Calls the `assetPrice` function from `UnboundedKerosineVault` function. Return a `uint`. Bounded Kerosene is 2x the price of unbounded. |

### `Vault.kerosine.unbounded`
- Inherits `KerosineVault` (`Vault.Kerosine`)

Unlike "bounded" Kerosene, this vault is withdrawable tracking "unbounded" Kerosene. It tracks assets with the `id2asset` mapping.

| Function         | Access                         | Effects                                                                                                                    |
| ---------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `withdraw`       | `onlyVaultManager`, `external` | Decrements the select amount from the `id2asset` associated with a `dNFT` id. Transfers the amount to the select `address` |
| `setDenominator` | `onlyOwner`, `external`        | Sets the address for the `KerosineDenominator` file                                                                        |
| `assetPrice`     | `public`, `override`           | Returns a `uint` which is an asset price derived from the Dyad total supply divided by the total supply of Kerosene  
      |
### `KerosineDenominator`
- Inherits `Parameters`

This file exists to return the total supply of Kerosene tokens. The `MAINNET_OWNER`'s supply is subtracted from the total supply. 

| Function      | Access     | Effects                                                                                                                         |
| ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `denominator` | `external` | Returns a `uint` of the total supply of Kerosene tokens. The `MAINNET_OWNER` total amount is subtracted to arrive at the total. |

### `Deploy.V2.sol`
- Inherits `Script`, `Parameters`.

The deploy script handles the creation of `vault`s and the `vaultLicenser`. The `Licenser` is not in the scope of this audit, but all `vaults` must be "licensed" in order to handle deposits/withdrawals. This deploy script creates the vaults, sets an address for the `vaultLicenser`, and "licenses" the vaults.


# Review
**Comments**
Interface files have comments, but the files in scope for this audit do not have comments. The `@inheritdoc` tag is used, which can be an effective way to avoid repeating comments in multiple files. 

However, key aspects of the codebase don't have any comments. The out of scope `Ivault.sol` file does not have any comments. The in scope vault files that inherit `Ivault.sol` are also without comments. The quality of audits can be improved with the addition of NatSpec comments so auditors can understand the developer's intentions. 

**Licensing**
The licensing mechanic doesn't seem necessary. The Licenser will be the `msg.sender` of the deployment script which centralizes this system to the deployer of the contract.

There is a check when a `dNFT` tries to `add` a vault. It is unclear when `add` is actually called. But when it is called, it checks that the vault is licensed:
```solidity
if (!vaultLicenser.isLicensed(vault))  revert VaultNotLicensed();
```

It would help if it is more clear why Licensing is necessary. This step adds a gas cost that could be avoided if Licensing was not a part of the system. Licensing also centralizes this system
 
**`dNFT`**
While not in scope, it is unclear why there is a cost to minting a `dNFT`. 

The entry point into the system is the `dNFT`. The price to mint the `dNFT` increases each mint:`START_PRICE + (PRICE_INCREASE * publicMints++)`. As of this review, the price to mint is 0.63 ETH. There are also "Insider NFTs" that are free mints which can only be minted by the owner. The intentions of this design is unclear, but forcing users to pay a price to enter the system while insiders can mint for free raises questions.

**Testing**
The testing coverage, especially for the files in scope, is not very strong:

| File                         | % Lines         | % Statements    | % Branches    | % Funcs       |
| ---------------------------- | --------------- | --------------- | ------------- | ------------- |
| VaultManagerV2.sol           | 1.19% (1/84)    | 0.64% (1/156    | 0.00% (0/44)  | 4.76% (1/21)  |
| KerosineManager.sol          | 60.00% (3/5)    | 45.45% (5/11)   | 33.33% (2/6)  | 50.00% (2/4)  |
| Vault.kerosine.bounded.sol   | 0.00% (0/3)     | 0.00% (0/5)     | 100.00% (0/0) | 0.00% (0/4)   |
| Vault.kerosine.unbounded.sol | 7.14% (1/14)    | 4.35% (1/23)    | 100.00% (0/0) | 25.00% (1/4)  |
| Vault.kerosine.sol           | 0.00% (0/10)    | 0.00% (0/15)    | 0.00% (0/2)   | 0.00% (0/5)   |
| KerosineDenominator.sol      | 50.00% (1/2)    | 60.00% (3/5)    | 100.00% (0/0) | 50.00% (1/2)  |
| Deploy.V2.s.sol              | 100.00% (22/22) | 100.00% (31/31) | 100.00% (0/0) | 100.00% (1/1) |

Auditors have to make a lot of assumptions because not all behavior is made clear through documentation and comments. It would be helpful to know why licensing is necessary. Why do users have to pay an increasing fee to mint a `dNFT` while insiders can mint for free? While the `dNFT` and Licensing mechanic aren't in the scope of this audit, they are valid centralization concerns that indirectly affect this audit.   



### Time spent:
24 hours