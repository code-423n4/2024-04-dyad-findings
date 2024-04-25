# [L-01] DNfts can make deposits and withdraws to and from unlicensed vaults or vaults that are not added, causing collaterals to be locked
## Impact
The normal flow of depositing collaterals is that DNfts add approved vaults and then deposit to them. However, if we check the [deposit](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119-L131) and [withdraw](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134-L153) functions we can see that they don't check if the DNft is interacting with unlicensed vault or if the vault is not added:
```solidity
// VaultManagerV2::deposit

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

// VaultManagerV2::withdraw

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
One possible impact of this is that DNfts can not withdraw their collateral after the deposit, because `getNonKeroseneValue` read from `vaults[id]` state that is updated only when [add](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L67-L78) vault is called (similar for unbounded kerosene vaults), so the `getNonKeroseneValue` will always return 0, making the withdraw transaction reverting [on this check](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L150), and the dyad mints revert [on this check](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L165)

Other impacts can occur, and the impacts depend on the vaults the DNft is interacting with. **Depositing to a vault that is unlicensed or is not added by the DNft is a common fault that DNfts might fall into**, so it is more secure to check the vault on `deposit` and `withdraw` functions.
## Recommended Mitigation Steps
Consider checking if the vault the DNft is interacting with is licensed/added or not.

# [L-02] DNfts can still deposit unbounded kerosine when TVL is less than Dyad total supply, in which the unbounded kerosine tokens become unwithdrawable for an undefined amount of time

## Impact
The asset price of unbounded kerosene tokens depends on the total USD value of all exogenous collateral in the protocol (TVL) as seen by the [UnboundedKerosineVault::assetPrice](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L50-L68) function:
```solidity
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
              * vault.assetPrice() * 1e18
              / (10**vault.asset().decimals()) 
              / (10**vault.oracle().decimals());
    }
    uint numerator   = tvl - dyad.totalSupply();
    uint denominator = kerosineDenominator.denominator();
    return numerator * 1e8 / denominator;
}
```
DNfts can deposit unbounded or bounded kerosine tokens as collateral by calling [VaultManagerV2::deposit](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L119-L131). The issue is that the function does not prevent DNfts from depositing unbounded Kerosine tokens when the TVL value goes below the total Dyad supply. In such situation, DNfts can not withdraw their unbounded kerosene or redeem their dyad tokens because both functions [call](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L146C34-L146C44) `UnboundedKerosineVault::assetPrice`, and `assetPrice` will [revert if TVL is less than dyad's total supply](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L65) because of underflow:
```solidity
uint numerator   = tvl - dyad.totalSupply();
```
This issue will be more likely to happen a lot after the upgrade using the deploy script, as both `ethVault` and `wstEth` vaults will be newly deployed and the total supply of dyad is already `632967400000000000000000`.

The amount of time for the TVL value to become more than dyad's total supply(and similarly, the amount time for DNfts to be able to withdraw their unbounded kerosene tokens) is undefined and can not be known, as it depends on the total USD value of all exogenous collateral in the protocol.

In addition, when the TVL value is lower than dyad's total supply, **it is more secure to prevent any deposits of unbounded tokens as the value of these tokens themselves depends strongly on TVL being greater than dyad's total supply.**

## Recommended Mitigation Steps
Consider preventing deposits of unbounded tokens when `tvl < dyad.totalSupply()`

# [L-03] `VaultManagerV2` and `UnboundedKerosineVault` may work with stale price
## Impact
Much of the math in the protocol is based on the data provided by Chainlink's token-USD feed. [VaultManagerV2::withdraw](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L146) and [UnboundedKerosineVault::assetPrice](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L60) interact with the underlying vault to fetch the price of the underlying asset.

The underlying vault [interact with Chainlink's oracle](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.sol#L91-L104) to fetch the USD price:
```solidity
function assetPrice() 
    public 
    view 
    returns (uint) {
    (
        ,
        int256 answer,
        , 
        uint256 updatedAt, 
    ) = oracle.latestRoundData();
        if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
        return answer.toUint256();
}
```
We can see that the underlying vault is vulnerable to stale data as it does not make the necessary checks against the data returned by the oracle to ensure that it is fresh and accurate. **In such cases where Oracle is returning stale data, the impact will propagate up to both `VaultManagerV2::withdraw` and `UnboundedKerosineVault::assetPrice()`.**


## Recommended Mitigation Steps
The impact of this issue is on the on-scope contracts, and the solve is on the `Vault` contract, which is out-of-scope. 

Consider checking the data returned by Chainlink's oracle in `Vault::assetPrice`. Below is a suggestion for an updated code:
```diff
function assetPrice() 
    public 
    view 
    returns (uint) {
    (
        ,
        int256 answer,
+        timeStamp
        , 
        uint256 updatedAt, 
    ) = oracle.latestRoundData();
        if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
+        if (answer <=0) revert StaleSata();
+        if (timeStamp == 0) revert StaleSata();
        return answer.toUint256();
}
```