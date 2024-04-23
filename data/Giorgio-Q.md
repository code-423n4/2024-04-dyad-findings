## If an actor has type(uint256).max / 2 + 1 of DYAD he becomes unliquidatable

## Vulnerability details

In order to liquidate a position the position being liquidated has to be bought by the liquidator. In the case an borrowing position equals to type(uint256).max / 2 + 1 of DYAD it will then become unliquidatable by default because there won't be enough DYAD to terminate it. However accumulating this much capital is not an easy task, almost impossible.

## Impact 

Humongous borrow position become unliquidatable, possibly dragging the protocol down if the position becomes insolvent. 

## Links

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L215

## Mitigation Route

In order to mitigate this issue set up a borrow limit of maybe 400 000 e18 DYAD per NFT.  


## Info: consider adding setUnboundedKerosineVault 

## Details

In the deployment script `setUnboundedKerosineVault()` is not called, which is crucial for the final setup of `BoundedKerosineVault`. However this can be done later and is not really an issue, it would just be more convenient to do it from the deployment script. 