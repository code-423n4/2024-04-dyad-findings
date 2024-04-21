# QA

## Lack of redemption will cause issues with the peg

Due to a lack of open redemptions, it's highly likely that Dyad will trade below peg

Redemptions are a key mechanism for peg support as they are effectively "pre-liquidations"

They are problematic for high leverage users, but they are a safety mechanism for the peg and the system

## Sandwich Liquidation Risk

Because of how the check is written, a cdp could be opened that could be liquidatable a block after

## Re-org may cause different NFT ids to be owned

This finding is a scam finding that some colleagues may send and should be considered informational

A user could rush to mint an nft and sent tokens to it but in reality they would simply be using the system incorrectly

ID can cause a user to self-rekt but this should be informational


## Withdraw is view but it should probably not be

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.bounded.sol#L32-L42

```solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
    view
      onlyVaultManager
  {
    revert NotWithdrawable(id, to, amount);
  }
```

If inheritance was setup `withdraw` would most likely not be `view`


## Rounding Errors

A slight rounding error is present in the liquidations math

I'm not sure this can be eliminated, but below is a way to change it to be slightly more in favour of the liquidator

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.22;

import {Test} from "forge-std/Test.sol";
import {console2} from "forge-std/console2.sol";
import {FixedPointMathLib} from "./FixedPointMathLib.sol";


interface Ix {
  function transferFrom() external;
}
contract CryticToFoundry is Test {
  using FixedPointMathLib for uint;

  uint256 asssets = 120e18;

  uint256 LIQUIDATION_REWARD = 0.2e18;
  function testTheMath() public {
      uint cappedCr               = 1.20e18;

      // 20% Premium on 1.2 should be 0.24
      // It's off

      // 0.04
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD); /// @audit ????? 0 when 1e18 - 1e18
      console2.log("liquidationEquityShare", liquidationEquityShare);
      
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr); //// ?????
      console2.log("liquidatiliquidationAssetShareonEquityShare", liquidationAssetShare);

      uint  collateral = asssets.mulWadUp(liquidationAssetShare);
      console2.log("From asssets", asssets);
      console2.log("From collateral", collateral);
  }

}

```

```solidity
[PASS] testTheMath() (gas: 10805)
Logs:
  liquidationEquityShare 40000000000000000
  liquidatiliquidationAssetShareonEquityShare 866666666666666666
  From asssets 120000000000000000000
  From collateral 103999999999999999920
```


Changing the rounding to:

```solidity
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD); /// @audit ????? 0 when 1e18 - 1e18
      console2.log("liquidationEquityShare", liquidationEquityShare);
      
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadUp(cappedCr); //// ?????
      console2.log("liquidatiliquidationAssetShareonEquityShare", liquidationAssetShare);

      uint  collateral = asssets.mulWadDown(liquidationAssetShare);
      console2.log("From asssets", asssets);
      console2.log("From collateral", collateral);
```


Will change the result to:
```solidity
[PASS] testTheMath() (gas: 10805)
Logs:
  liquidationEquityShare 40000000000000000
  liquidatiliquidationAssetShareonEquityShare 866666666666666667
  From asssets 120000000000000000000
  From collateral 104000000000000000040
```