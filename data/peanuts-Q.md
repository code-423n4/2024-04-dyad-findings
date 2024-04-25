### [L-01] No partial repayment option will be disadvantageous for the protocol. Whales can potentially not get liquidated at all.

When a user's collateral ratio is below 150%, the user can be liquidated. The liquidator will burn all the dyad minted in exchange for collateral funds.

```
  /// @inheritdoc IVaultManager
  function liquidate(
    uint id,
    uint to
  ) 
    external 
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
>     dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
```

The issue is that the liquidator MUST burn all the dyad that the user had minted. If the user is a whale, and has minted 1 million dyad worth ~1M, only other whales can liquidate him because most people don't have the capital to do so.

The other whales is not incentivize to liquidate also since if whales are starting to fall below the collateral ratio, it means that there is a flash crash happening to the price of the collateral, which will drive the price of DYAD down. 

For whales to liquidate other whales, they have to bear the burden of having ~1M DYAD that they need to burn in order to get back their original collateral. Having this debt in a time of flash crashes is not a good idea.

Consider having partial liquidation so that users with smaller balances can still liquidate without needed to burn so much DYAD.

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L205

### [L-02] There is no margin for error for collateral ratio and liquidation

If the user has 150% collateral and above, they can mint DYAD. The moment the collaterization ratio dips below 150%, they are immediately set for liquidation. 

Usually, in lending protocols, there is a treshold for collateral ratio and another lower threshold for liquidation ratio. For example, in AAVE, they have an Loan-to-Value ratio of 70% (1 eth of collateral == 0.7 ETH of corresponding currency) and their liquidation threshold is ~80% (no more than 10-15% above LtV). 

In the same way, the protocol should have a lower liquidation ratio, eg 140%, for a collaterization ratio of 150%.

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L230-L238

### [L-03] Kerosine price can be manipulated by a coordinated attack, leading to undesirable liquidations

The price of kerosene is deterministically calculated.

It takes (TVL - DYAD total supply) / Kerosene supply.

When minting DYAD, users need to have at least a 100% collateral ratio between exogeneous collateral (WSTETH/WETH).

```
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
    dyad.mint(id, to, amount);
```

Users then need to have at least 150% collateral ratio to prevent liquidation.

Kerosene can be used as extra collateral to mint more DYAD. 

When minting 1000 DYAD, users can have
- 1500 USD worth of exogenous collateral (WETH)
- 1000 USD worth of exogeneous collateral and 500 USD worth of kerosene

Users cannot have 
- 1500 USD worth of kerosene

With that being said, this is how the attack works.

Let's say there are a bunch of people that has both exogenous collateral and kerosene as collateral.

The price of kerosene is (TVL - DYAD total supply) / Kerosene supply.

Assume TVL is 10M and DYAD total supply is ~4M. The whales can come together and purposely burn their DYAD to bring down the DYAD total supply, leaving some DYAD to liquidate a particular user that has a lot of kerosene as collateral. 

Having a deterministic price may not be a good idea because it brings about many potential issues. Consider get the price through a TWAP on a liquidity pool instead.

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L57-L65

### [L-04] 1 wei griefing possible to increase gas fee during liquidation

When a user is liquitable and he does not have enough to keep himself solvant, he can purposely deposit 1 wei of tokens in all of the vaults that is available. When it is time to collect the collateral, the liquidator has to run the function that goes through all of the vault and get the collateral amount inside the vault. If `liquidationAssetShare` is not 1e18 (below), then (1 * 0.877e18) / 1e18 = 0. 

User's and liquidator's vault amount will not decrease or increase due to the truncation to zero. `move()` does not do anything. User can simply waste the liquidator's gas fee. If there are more vaults available in the far future, then this function may even lead to out of gas error, but right now the vault limit is capped so OOG is unlikely.

```
 for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
```

In worse case scenarios, there may be a truncation issue if the user deposits >1 wei.

If the user deposits 100 wei at a 0.778e18 liquidationAssetShare, then (100 * 0.7778e18) / 1e18 = 77.78 which equals to 77. 

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L223-L226

### [L-05] Checking collatRatio before burning DYAD may reflect the wrong collatRatio of the user.

```
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
```

When liquidating a user, the function checks the `collatRatio()` of the user before burning the DYAD owed.

The issue is that the price of kerosene is affected by the amount of DYAD avaiable. When DYAD is burned, the price of kerosene will go down, leading to a lower collateral ratio than previously calculated if the user has kerosene as a collateral.

In `redeem()`, the DYAD is burned first before `withdraw()` is called which checks the collateralRatio of the user. The same should be done when liquidating.

Burn DYAD first before checking the collateral ratio.

```
 /// @inheritdoc IVaultManager
  function liquidate(
    uint id,
    uint to
  ) 
    external 
      isValidDNft(id)
      isValidDNft(to)
    {
+     dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));        
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
-     dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));
```

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L213-L215

### [L-06] The sole reliance on the Chainlink oracle system can result in sandwich oracle attacks, frontrunning oracles or undesirable liquidation due to oracle update times.

The exogenous vaults fetches its price from Chainlink. Chainlink updates each oracle differently, with different heartbeat and at different times. Sometimes, it takes the oracle 24 hours to update one time. Users can also notice the change and do something before / after it.

For example, if there is a flash crash and the oracle updates every hour, then the user can capitalize on the issue and quickly exit their position / liquidate others.

Also, because all the oracle updates at different times, the exact collateralization ratio is extremely hard to determine. If the price of one oracle increases and the price of another oracle decreases, then if the oracle were to update at the same time, the person may not face liquidation but because the oracle updates one at a time, the person will face liquidation.

It would be good to have a dual oracle system, or even better, get the real time TWAP price of each vault token.

### [NC-01] Integrations with weird ERC20 as vaults will cause accounting issue

Note that the vault calculation does not involve fee-on-transfer and rebasing tokens. The protocol must confirm that the tokens that is accepted by the vault is not a fee-on-transfer and rebasing token. Special consideration for USDT, since it is a stablecoin which is good for collateral, but USDT has a fee-on-transfer-mechanism.

### [NC-02] Shifting the denominator may cause undesired liquidation

The denominator is calculated as such: 

```
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
  ```

If the `MAINNET_OWNER` moves his kerosine balance else where, there will be a huge influx of kerosine that is now counted which will affect the price of kerosine. 

