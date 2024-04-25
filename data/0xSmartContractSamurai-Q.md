0. LOW/QA: `KerosineManager.sol`::`contract KerosineManager is Owned(msg.sender) {` - cannot pass argument during inheritance, should use constructor.

https://github.com/code-423n4/2024-04-dyad/blob/344a58bb84b24d6c281be038a5dff1631426e9c0/src/core/KerosineManager.sol#L7

Other occurrences:
`2024-04-dyad/src/core/Vault.kerosine.sol`:
https://github.com/code-423n4/2024-04-dyad/blob/344a58bb84b24d6c281be038a5dff1631426e9c0/src/core/Vault.kerosine.sol#L12

Standard approach is to instantiate the new owner in the constructor during deployment, and only use the `contract ContractName is BlahblahContract` for contract name and any inheritance declarations.

## IMPACT:
- Likelihood: high
- Impact: low, as it will do a compile error when trying to compile the contract...so probably zero risk to protocol
- Severity: medium

## Recommendation:
```solidity
contract KerosineManager is Owned {

    constructor() Owned(msg.sender) {
        // Additional initialization logic for KerosineManager contract
    }

    // Contract logic goes here
}
```
=======
=======

1. LOW/QA: `VaultManagerV2::redeemDyad()` - Whenever partial amounts are redeemed for same `id`, the returned price from oracle call seems to be affected by the % redeemed.

## Explanation:
Example:
If I redeem 100% of the minted tokens, the returned oracle price is:
`10000000000000000000000000000`
But if I redeem 90% of the minted tokens, the returned price is:
`9999910000000000000000000000`
And if I redeem 10% of the minted tokens, the returned price is:
`9999990000000000000000000000`

In fact, if I redeem smaller values where each value is say a 10th of the total value, and I redeem 10 times, then the returned oracle price "counts down" from:
`9999990000000000000000000000`
to:
`9999910000000000000000000000`

This is likely not intended behaviour but maybe expected behaviour?
(Maybe a perfect candidate for invariant fuzzing test to push the limits.)

## IMPACT:
- Likelihood: high, Impact: Low, Severity: Medium to Low

## PoC:

### Modified test function used:
```solidity
  function test_redeemDyad() public {
    uint id = mintDNft();
    //deposit(weth, id, address(wethVault), 1e22);
    deposit(weth, id, address(wethVault), 1e25); /// @audit added for PoC/testing purposes
    // vaultManager.mintDyad(id, 1e20, address(this));
    // vaultManager.redeemDyad(id, address(wethVault), 1e20, RECEIVER);
    vaultManagerV2.mintDyad(id, 1e23, address(this)); /// //audit added for PoC/testing purposes
    //vaultManagerV2.redeemDyad(id, address(wethVault), 1e23, RECEIVER); /// //audit added for PoC/testing purposes
    //vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    //vaultManagerV2.redeemDyad(id, address(wethVault), 9e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes
    vaultManagerV2.redeemDyad(id, address(wethVault), 1e22, RECEIVER); /// //audit added for PoC/testing purposes

  }
```
### Test Results:
```solidity
$ forge test --contracts test/VaultManager.t.sol --mt test_redeemDyad -vvvvv
[⠒] Compiling...
[⠆] Compiling 1 files with 0.8.17
[⠰] Solc 0.8.17 finished in 3.07s
Compiler run successful!

Ran 1 test for test/VaultManager.t.sol:VaultManagerTest
[PASS] test_redeemDyad() (gas: 792855)
Traces:
  [16655558] VaultManagerTest::setUp()
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999990000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999990000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999980000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999980000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999970000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999970000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999960000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999960000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999950000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999950000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999940000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999940000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999930000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999930000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999920000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999920000000000000000000000 [9.999e27]
.
.
.
    │   ├─ [3811] Vault::getUsdValue(0) [staticcall]
    │   │   ├─ [271] ERC20Mock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 18
    │   │   ├─ [144] OracleMock::decimals() [staticcall]
    │   │   │   └─ ← [Return] 8
    │   │   ├─ [420] OracleMock::latestRoundData() [staticcall]
    │   │   │   └─ ← [Return] 1, 100000000000 [1e11], 1, 1, 1
    │   │   └─ ← [Return] 9999910000000000000000000000 [9.999e27]
    │   ├─ emit RedeemDyad(id: 0, vault: Vault: [0x50EEf481cae4250d252Ae577A09bF514f224C6C4], amount: 10000000000000000000000 [1e22], to: Vault: [0x50EEf481cae4250d252Ae577A09bF514f224C6C4])
    │   └─ ← [Return] 10000000000000000000 [1e19]
    └─ ← [Stop] 

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 19.96ms (9.75ms CPU time)

Ran 1 test suite in 11.34s (19.96ms CPU time): 1 tests passed, 0 failed, 0 skipped (1 total tests)
```

## Recommendation:
- Not sure if this is acceptable behaviour or not? And not entirely sure what's causing it.
- So I cannot make a recommendation until more clarity.