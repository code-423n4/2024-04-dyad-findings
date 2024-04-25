# **Dyad Analysis Report**

# **Overview**

- DYAD is the First Truly Cost Effective Decentralized Stablecoin.

- Traditionally, Two Costs Make Stablecoins Inefficient:


  a)   `Excess Collateral` 

  b)   `DEX Liquidity`


- DYAD Minimizes Both of These Costs through Kerosene.

- Now What is Kerosene?? 

`(token That Lowers the Individual Cost to Mint DYAD)`



### **Analysis of Contracts (Files in Scope)**

Let's take a look on contracts to know how they works


## 🔗 KerosineDenominator.sol

In this kerosine denominater contract, there's only one function named as `denominator`that returns difference between totalSupply & `balanceof(MAINNET_OWNER)`


## 🔗 VaultManagerV2.sol

this contract includes functions named as, setKeroseneManager which works as an initializer for `keroseneManager`
- some vault management functions for adding/removing vaults
- then there are deposit/withdraw func.
- minting, burning & redeem functions that are responsible for minting , burning DYAD.
- It also handles liquidation in case of insufficient collateral.

## 🔗 Vault.kerosine.sol

this contract has some following functions:

`deposit func`

- Allows to deposit assets by taking parameters, then it
- Increments the asset balance associated with the given vault ID.
- Emits a Deposit event 

`move func`

Allows to transfer balance between vaults.
Decrements the asset balance from the source vault (from) and increments the asset balance of the destination vault (to).
Emits a Move event

`getUsdValue func`

Calculates the USD value of assets held in a specific vault ID.
Calculates the USD value by multiplying the asset balance with the asset price and dividing by 1e8 (1e8 represents the decimal precision of the asset price).

`assetPrice func`

function that returns the price of the asset in USD.

## 🔗 KerosineManager.sol

so whats happening in this contract is explained below:

`add func.` to add vault with two check requirements whether the vault length dont exceed & checks if it is already added or not.

`remove func.` to remove vaults , also checks if the vault has already been removed.

`getVaults` retrives the addresses of vaults

`isLicensed func.` returns boolean whether the vault is licensed or not.

## 🔗 Vault.kerosine.bounded.sol

 - This has `setUnboundedKerosineVault` func. which sets state variable. 
 - A withdraw func. excessed by `onlyVaultManager`.
 - `assestPrice` func. which returns the price by multiplying it by 2.
 

 ## 🔗 Vault.kerosine.unbounded.sol

 This contract contains three functions for withdraw, setDenominator & assetPrice func.

  ## 🔗 Deploy.V2.s.sol

  It deploys kerosine vaults, controls kerosine processes via KerosineManager, and initializes a VaultManagerV2 with licensed vaults for ETH and WstETH. Contracts are approved for functioning properly and ownership is transferred.


  # Risk Factor Analysis

  - `Admin Abuse Risks`

  There are many Chances of Admin Abuse Risks Such as (manuplating, Withdrawing Funds Improperly) as Many Functions are Owned by Owners, Also There Must Be Some Access Control Function to Avoid Such Vulnerabilities.

  - `Centralization Risks`

  Thus the Protocol Heavily Relies on Centralization, Single Point of Failure Can Affect the Whole System.

  - `Technical Risks`

   Increased Complexity Can Make the Contracts Harder to Understand, Maintain, and Audit, Potentially Leading to Overlooked Bugs or Vulnerabilities during Development & Updates. So , the Contract Should Be Simple, Clear and Readable.

  - `Integration Risks`
  
  The Protocol May Be Affected from External Contracts like `solmate,openzeplin` as It Interacts with Them.

   - `Non-Standard Token Risks`

 The Protocol Have No Properly Verify the ERC-20 Tokens, If ERC-20 Tokens Compliance with the Standard Isn't Confirmed, There May Be Vulnerabilities Such as Loss of Funds, or Unexpected Token Behavior.


 ## 

 Hope This Helps! 

### Time spent:
14 hours