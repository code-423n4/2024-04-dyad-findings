`KerosineManager`
- No events emitted when adding/removing kerosine vault.
`VaultManagerV2`
- `remove()` and `removeKerosene()` emit the same event.
- `add()` and `addKerosene()` emit the same event.
- It's better to use the `initializer` modifier on an `initialize()` function rather than `setKeroseneManager`
- `setKeroseneManager` does not emit an event.
- The modifier `isLicensed` is never used and should be removed.
- It's better to `_disableInitializers()`  in the constructor to prevent  the initialization of the implementation contract ( in this contract to prevent `setKeroseneManager` from being called on the implementation contract)

`KerosineDenominator`
- `kerosine` variable could be `immutable`

`Parameters`
- All the hardcoded variable in the `Parameters` contract can be `constant` to save gas.