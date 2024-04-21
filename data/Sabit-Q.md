1. There is no need to add the ">" operator 

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L74

When adding a new vault, there is no need to have the ">" operator below:

  if (vaults[id].length() >= MAX_VAULTS) revert TooManyVaults();

This is because the vaults length of an "id" will never be greater than MAX_VAULTS as there is an "=" operator in the if statement. And MAX_VAULTS is already set to 5.

So, the correct check should be:

  if (vaults[id].length() == MAX_VAULTS) revert TooManyVaults();