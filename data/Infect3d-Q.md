# L01 - Stale timeout should be configured by asset
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/Vault.sol#L19-L19

## Vulnerability details

```solidity
File: src/core/Vault.sol
14: contract Vault is IVault {
15:   using SafeTransferLib   for ERC20;
16:   using SafeCast          for int;
17:   using FixedPointMathLib for uint;
18: 
19:   uint public constant STALE_DATA_TIMEOUT = 90 minutes; 
```

Each vault uses a chainlink oracle to access the underlying asset price.
While it check for stale data as expected, the delay is a constant that cannot be set when deploying a new vault.
This is not correct, as depending on the oracle, the timeout to consider an answer as stale can be different.

## Recommended Mitigation Steps

Make STALE_DATA_TIMEOUT a constructor parameter, or add a setter function.

____________________________________

# L02 - price fetch should be in try/catch block
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/Vault.sol#L100-L100

## Vulnerability details

```solidity
File: src/core/Vault.sol
091:   function assetPrice() 
092:     public 
093:     view 
094:     returns (uint) {
095:       (
096:         ,
097:         int256 answer,
098:         , 
099:         uint256 updatedAt, 
100:       ) = oracle.latestRoundData();
101:       if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
102:       return answer.toUint256(); 
103:   }
```
## Recommended Mitigation Steps

Its common practice to make oracle calls inside a try/catch structure in case there's an issue with the oracle making it revert.
The issue is that withdrawal/liquidation in `VaultManagerV2` could be prevented in that case.
Part of this common practice is to have a fallback oracle (TWAP) or use a saved price (not the best choice though)


____________________________________

# L03 - No zero-value check for returned answer from oracle
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/Vault.sol#L100-L100

## Vulnerability details
Price feed might return zero and this must be handled as invalid.

```solidity
File: src/core/Vault.sol
091:   function assetPrice() 
092:     public 
093:     view 
094:     returns (uint) {
095:       (
096:         ,
097:         int256 answer,
098:         , 
099:         uint256 updatedAt, 
100:       ) = oracle.latestRoundData();
101:       if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
102:       return answer.toUint256(); 
103:   }
```

## Recommended Mitigation Steps
Ensure the returned price is not zero and act accordingly depending on your design choices.


____________________________________

# L04 - Missing setUnboundedKerosenVault initialization in deploy
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/script/deploy/Deploy.V2.s.sol#L89-L89

## Vulnerability details
`boundedKerosineVault` is deployed, but the `setUnboundedKerosenVault` is not called, which will cause a revert when `BounderKerosineVault::assetPrice()` will be called to price users kerosine collateral:

```solidity
File: src/core/Vault.kerosine.bounded.sol
22: 
23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }
31: 
...:
...:	/// ... some code ...
...:
44:   function assetPrice() 
45:     public 
46:     view 
47:     override
48:     returns (uint) {
49:       return unboundedKerosineVault.assetPrice() * 2;
50:   }
```