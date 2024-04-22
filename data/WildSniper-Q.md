# [1] Price feed might return zero or Non accurate values in crash times and this must be handled as invalid.
since `VaultManagerV2.sol` and the protocol as a whole depends heavily on `Vault.assetPrice()` call its important to have extra Checks that the returned value is not 0 or that the price hasnt deviated more than 80% for example (which likely not going to happen with asset like ETH in one hour)

# [2] not used modifier

in `VaultManagerV2.sol`
```
modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```
was never used, consider removing it from the code or use it as intended

# [3] Hard-coded price feed addresses can be problematic, especially if they become deprecated
  `IAggregatorV3 public immutable oracle;` in `Vault.sol` uses immutable hardcoded Chainlink PriceFeed

# [4] no event emitted for important operation
in `VaultManagerV2.sol` both functions `withdraw()` and `deposit()` don't have a special event emitted after executed which is not recommended 