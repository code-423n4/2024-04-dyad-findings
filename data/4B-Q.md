## ISSUES

1. In `VaultManagerV2.sol` the [`MAX_VAULTS_KEROSENE = 5`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L23C24-L23C43) whilst In `KerosineManager.sol` the [`MAX_VAULTS = 10`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L14) this is a conflict between the declarations in the two contracts and might lead to a revert.

2. In `Vault.kerosine.unbounded.sol::withdraw` there is no check for the existence of `id` - https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L38

3. In `Staking.sol::setRewardsDuration` the `duration` param has to be checked against 0s to prevent reverts in the subsequent functions like `notifyRewardAmount` - https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/Staking.sol#L101

4. All functions in contracts need to have some natspec or comments to make the code easy to read and apprehend.

5. There should be a check for the ERC20 contracts imported since the solmate library does not really check if it is a contract.

6. In `VaultManagerV2.sol` there needs to be an event emitted when there's a [deposit](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L119) and [withdrawal](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134) for external purposes for instance integrations with frontends etc.

7. In `[VaultManagerV2.sol::withdraw`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L134) there should be a check on `amount` param to prevent zero withdrawals

8. In [`VaultManagerV2.sol::mintDyad`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156), [`VaultManagerV2.sol::burnDyad`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172), [`VaultManagerV2.sol::redeemDyad`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184) `amount` passed into these functions must be validated to prevent complications like zero transfer reverts which can lead to DOS 



