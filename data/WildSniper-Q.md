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

# [3] Hard-coded price feed addresses
  `IAggregatorV3 public immutable oracle;` in `Vault.sol` uses immutable hardcoded Chainlink PriceFeed that can be problematic, especially if they become deprecated

# [4] no event emitted for important operation
in `VaultManagerV2.sol` both functions `withdraw()` and `deposit()` don't have a special event emitted after executed which is not recommended 

# [5] Centralization risk related to the multisig wallet leading to indirect harm
insure that all founders are trusted and no 3/5 of people can harm protocol users by no mean or implement a DAO logic around editing protocol logic indirect harm examples are in [6]

# [6] in `Vault.kerosine.bounded.sol:UnboundedKerosineVault` should be immutable
centraliztion risk connected to leaving this as normal storage variable since the  `UnboundedKerosineVault` contract have the `assetPrice()` function of Kerosene token that is used in `Vault.kerosine.bounded.sol` to get 2x the value since this is Permanently locked Kerosene, but since this address is very important its better transperancy to set it in the constructor and make it immutable to raise questions about the integrity of the protocl
(suspected scenario) team reset the logic address of `UnboundedKerosineVault` to malicious one that returns very low `assetPrice()` affecting `VaultManagerV2.sol::getNonKerosineValue()` and the chain of functions that depends on it