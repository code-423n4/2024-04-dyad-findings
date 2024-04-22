Impact
The BoundedKerosineVault contract contains a vulnerability where it does not perform checks for the "address(0)" value when assigning values to the unboundedKerosineVault address state variable. This can lead to unexpected behavior and potential security issues.

When an address is set to "address(0)", it represents the null address or an uninitialized address value. Interacting with "address(0)" can cause unintended consequences, such as preventing certain functions from executing or potentially breaking the contract's logic.

Proof of Concept
Here's an example of how this vulnerability can be exploited:

     contract Exploit {

      BoundedKerosineVault public boundedKerosineVault;

    constructor(address _boundedKerosineVault) {
        boundedKerosineVault = BoundedKerosineVault(_boundedKerosineVault);
    }

    function exploitSetUnboundedKerosineVault() external {
        boundedKerosineVault.setUnboundedKerosineVault(UnboundedKerosineVault(address(0)));
    }

}

Tittle 
Constants should be defined rather than using magic numbers.*(found additional instances of an issue listed in the automated findings report).

instances(13)
links :
file source: /src/core/Vault.kerosine.sol
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L66

file source: /src/core/Vault.kerosine.unbounded.sol
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L61
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L62
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L63
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L67

file source: /src/core/VaultManagerV2.sol
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L147
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L148
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L149
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L196
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L198
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L217
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L218
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L219