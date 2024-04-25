Events should reflect function name/actions

## ISSUE
Asides missing events in key functions, the naming convention used in events do not reflect the actions performed by the function. For example, `add()` and `addKerosene()` in `VaultManagerV2` use the same event name and do not state what is added.

## RECOMMENDATION
Let the event emitted state the action performed by the function. From the above example a convention can be: "AddedVault"/"AddedKeroseneVault" or "VaultAdded"/"KeroseneVaultAdded"