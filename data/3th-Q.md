# Kerosene denominator can be manipulated

## Impact
- The kerosene denominator, used in the [calculation of the kerosene `assetPrice`](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L67), subtracts the kerosene remaining to be distributed from its total supply. It defines the former by querying the balance of the `MAINNET_OWNER`
- This makes it possible for an attacker to manipulate the `assetPrice` of kerosene, by sending kerosene to `MAINNET_OWNER` and increasing the value of the denominator. They could exploit this to force vaults into liquidatable states
- This is low-severity, because it would require a large amount of kerosene to be sent to the `MAINNET_OWNER` and lost forever. It is still worth fixing, however, because it is plausible that a vault on the brink of liquidation could have enough collateral at stake to compensate the attacker for their kerosene donation

## Recommended Mitigation Steps

Consider storing the distributed amount of kerosene as a state variable in the denominator.