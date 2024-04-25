## Low Issues

### [L-1] Possible underflow in `UnboundedKerosineVault::assetPrice()`

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

The following line might cause an underflow error to occur if the `DYAD` minted is more than the `TVL`:

```solidity
uint numerator = tvl - dyad.totalSupply();
```

This might happen in the case where a large position was liquidated and the `DYAD` is still held by the liquidated holder.

## Informational

### [I-1] `Kerosene` is spelled `Kerosine` in some places

`Kerosene` is spelled wrongly as `Kerosine` is some places throughout the contracts. I recommend aligning the spelling in all contracts.

### [I-2] Existing `Licenser` deployment can be used

In the deployment script for V2, a new `Licenser` is deployed. The same one is already deployed on Mainnet the address of which can be found in `Parameters.sol`. It could be re-used.
