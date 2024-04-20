https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/params/Parameters.sol#L4

All Parameters except these:
`address SEPOLIA_DNFT = address(0);`, 
`address SEPOLIA_VAULT_MANAGER = address(0);`,
`address SEPOLIA_DYAD = address(0);`
should be constatns. On other hande these 3 are not used anywhere

https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/staking/KerosineDenominator.sol#L9

 Kerosine public kerosine; should be immutable


https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/test/Vault.wsteth.t.sol#L24

function should be view

Better gas optimization.
Immutable state.
Code clarity.
Preventing bugs.


