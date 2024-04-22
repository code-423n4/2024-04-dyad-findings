## [L-1] Missing zero address validation
#### Description
Detect missing zero address validation.
#### Link of code 
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/periphery/Payments.sol#L41-L48
#### Recommendation
Check that the address is not zero.

## [NC-1] Missing events arithmetic
#### Description
Detect missing events for critical arithmetic parameters.
#### Link of code 
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/periphery/Payments.sol#L32-L39
#### Recommendation
Emit an event for critical parameter changes.

## [NC-2] Incorrect versions of Solidity
#### Description
solc frequently releases new compiler versions. Using an old version prevents access to new Solidity security checks. 
#### Link of code 
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/DNft.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Dyad.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/KerosineManager.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Licenser.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.wsteth.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManager.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IAggregatorV3.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IDNft.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IDyad.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IStaking.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IVault.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IVaultManager.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IWETH.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/interfaces/IWstETH.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/params/DNftParameters.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/params/Parameters.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/periphery/Payments.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/Kerosine.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/KerosineDenominator.sol#L2
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/staking/Staking.sol#L2
#### Recommendation
Deploy with a recent version of Solidity

