## Optimize gas by using only named returns

The Solidity compiler can generate more efficient bytecode when using named returns. It's recommended to replace anonymous returns with named returns for potential gas savings.

Example:

    /// 985 gas cost
    function add(uint256 x, uint256 y) public pure returns (uint256) {
        return x + y;
    }
    /// 941 gas cost
    function addNamed(uint256 x, uint256 y) public pure returns (uint256 res) {
        res = x + y;
    }

issue instances:

File: src/staking/KerosineDenominator.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/staking/KerosineDenominator.sol#L17

File: src/core/VaultManagerV2.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/VaultManagerV2.sol#L235

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/VaultManagerV2.sol#L192

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/VaultManagerV2.sol#L235

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/VaultManagerV2.sol#L192

File: src/core/Vault.kerosine.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/Vault.kerosine.sol#L65

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/Vault.kerosine.sol#L73

File: src/core/KerosineManager.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/KerosineManager.sol#L40

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/KerosineManager.sol#L49

File: src/core/Vault.kerosine.bounded.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/Vault.kerosine.bounded.sol#L48

File: src/core/Vault.kerosine.unbounded.sol

https://github.com/code-423n4/2024-04-dyad/blob/44becc2f09c3a75bd548d5ec756a8e88a345e826/src/core/Vault.kerosine.unbounded.sol#L54

File: 