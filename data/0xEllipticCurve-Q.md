Strict check on the ```Liquidate()``` function.

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L214

```
  function liquidate(
    uint id,
    uint to
  ) 
    external 
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);

      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh(); <---- @audit STRICT CHECK

      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

      uint numberOfVaults = vaults[id].length();
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
      emit Liquidate(id, msg.sender, to);
  }
``` 