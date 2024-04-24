### [L-01] KerosineManager and Licenser have duplicate functionality
It is technically possible to have the state of `KerosineManager` and `Licenser` for the `isLicensed` function differ. All vaults are already added to `Licenser`, so having the same function in `KerosineManager` is redundant and should be avoided. Please also read **NC-01** for recommendation how to fix.

### [L-02] Users can deposit in a Vault that is not added to their dNFT
Allowing users to deposit in a Vault that's not added to their dNFT, means that they will put up collateral that will not improve their CR.
The issue would be exacerbated in the future, when a user reaches `MAX_VAULTS` for their dNFT collateral and is allowed to deposit in a 6th Vault. Then, they would not be able to make this 6th Vault contribute to CR.

### [NC-01] KerosineManager name is misleading
The `KerosineManager` contract works with normal vaults and having it Kerosine in the name is confusing. Kerosine vaults use it to calculate TVL and VaultManagerV2 for license checks. It doesn't control or manage in any way Kerosine vaults.

One way of doing it would be to replace it with a new `VaultLicenser` contract, that inherits from `Licenser` and can return an array of all the vaults it holds.

Also, rename `setKeroseneManager` in `VaultManagerV2`.

### [NC-02] assetPrice() function should be part of IVault

All vaults implement the function `assetPrice() returns (uint)`, but the function is missing from `IVault`. Having it as part of the interface would make integration with the protocol and future protocol updates easier.

### [NC-03] Inconsistent spelling of Kerosine vs Kerosene

Though both spellings can be considered as correct, code should avoid having them both. 
One concept should be given a consistent name everywhere.
From what we could find, the original spelling is Kerosene. Later, the alternative spelling came from american chemical manufacturers.

### [NC-04] isLicensed modifier in VaultManagerV2 is unused
The `isLicensed` modifier in `VaultManagerV2` should be deleted or applied in the appropriate places.

### [NC-05] Convert uint to uint256
While not explicitly required in the style guide, having the explicit type (`uint256`) is considered best practice.

### [NC-06] File names should be the same as the contract 
 As per the [solidity style guide for contract names](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names) - files should match contract names.

### [NC-07] Usage of unrecommended code alignment
Throughout the codebase the pattern where some parts of a line are left-aligned and others right-aligned (creating 2 columns) is often seen.
Here are some examples:
- [Deploy.V2.s.sol](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L78-L86), [function calls](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L90-L91)
- [KerosineManager.sol](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L24-L25)
- [Licenser.sol](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Licenser.sol#L12-L13) - on function declarations
- [VaultManagerV2.sol](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L74-L89), [on assignment](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L223)
- [IVault.sol](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/interfaces/IVault.sol#L6-L16)

Such alignment is not considered best practice. The Solidity Style guide recommends [1 space between operators](https://docs.soliditylang.org/en/latest/style-guide.html#other-recommendations), check out [recommended alignment](https://docs.soliditylang.org/en/latest/style-guide.html#maximum-line-length) for some of these situations in these sub-sections.

### [NC-08] OracleMock does not work with prices' decimals != 8, making some tests invalid
`OracleMock` can receive prices with various decimal places, ie `1e6` or `1000e8`, etc.
The issue is that it's `decimals()` value is hardcoded.

One example of a wrong test is `test_getTotalUsdValue`.

Here's a quick breakdown:
1e22 is 10_000e18
weth oracle price is 1000e8 with 8 decimals coming from oracle
price = 10_000_000e18 (10000000000000000000000000) - decimals are matching

dai oracle price is 1e6 with 8 decimals coming from oracle - which is wrong, should be 6
price = 100e18
should be = 10_000e18

This is why the test result should be different, than it is now:
Expected: 10000100000000000000000000
  Actual: 10010000000000000000000000 (when oracle decimals are correctly set to 6)

Here is a [suggestion](https://gist.github.com/georgiIvanov/7faf72a632ff975046cdae1f23d990e1) how to change the mock oracle implementation.

### [NC-09] Inconsistent naming convention for oracle addresses
One oracle address is named `MAINNET_WETH_ORACLE`, another `MAINNET_CHAINLINK_STETH`.
This is confusing to use and read.
We recommend a naming convention that describes the following things - blockchain, oracle origin, pair.
Example: `MAINNET_CL_ETH_USD`, `MAINNET_CL_STETH_USD`.

### [NC-10] Improve variable naming
`VaultManagerV2::redeemDyad` works with 2 currencies - DYAD and collateral asset (derived in the fn itself).
Currently, the variables for them are `amount` and `asset` respectively, which can be confusing for first time readers or people coming back to the code.
We recommend to be more explicit with the naming, like so: `amount` -> `dyadAmount`; `asset` -> `assetAmount` or `collateralAmount`.