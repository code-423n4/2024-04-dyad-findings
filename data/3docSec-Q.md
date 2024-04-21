# [L-01] Inconsistent rounding in VaultManagerV2.liquidate

https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/core/VaultManagerV2.sol#L218-L224

The `liquidate` function applies several calculations to calculate the `collateral` to seize from `cappedCr`.

```Solidity
File: VaultManagerV2.sol
218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
---
224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
```

If we consider that `cappedCr` is the only non-constant input that contributes to the `id2asset(id)` multiplier, we can see that:
- `collateral` is correctly rounded up to favor the liquidator (`mulWadUp` at L224)
- `liquidationAssetShare` is inconsistently rounded down, favoring the insolvent position (`divWadDown` at L219)
- `liquidationEquityShare` is also rounded down, again favoring the insolvent position (`mulWadDown` at L218)

Consider changing all of the above operations to round up.

# [L-02] BoundedKerosineVault is not licensed in the Deploy.V2 script

https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/script/deploy/Deploy.V2.s.sol#L96

The `BoundedKerosineVault` (in scope) is deployed by the `Deploy.V2` script (also in scope), but it's never added to the `VaultLicenser` instance, making the contract unusable with `VaultManagerV2`.

# [L-03] VaultManagerV2 provides insufficient liquidation incentives for the most insolvent positions

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L217-L224

If my math is correct, the incentive that is given to liquidators (ratio between collateral seized and debt repaid) is equal to `1 + (cappedCr - 1) * 20%`. This formula is somewhat counterintuitive because it provides higher rewards with higher `cappedCr`, that is for positions that are the least delinquent, and therefore the least valuable for the protocol to be liquidated.

Consider revisiting the formula to provide a higher incentive to liquidators taking off the most delinquent positions from the system, possibly with a curve that peaks closer to the minimum `cappedCr = 1` than the maximum `cappedCr = 1.5` where it peaks now. Of course the ideal peak would be at `cappedCr = 1` but that can't happen because at that level, the position has no extra collateral to distribute as reward, so something close to it would be probably best. 

# [L-04] Deploy.V2.s.sol script misses step to license the VaultManagerV2 contract

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/script/deploy/Deploy.V2.s.sol#L41-L47

The deployment script in scope seems insufficient to deploy an operational protocol because the created VaultManagerV2 contract is not licensed, and this will prevent minting DYAD tokens.

# [I-01] Unused `isLicensed` modifier in VaultManagerV2

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L45

The `isLicensed` modifier in the `VaultManagerV2` contract is never used and should be removed.

# [I-02] Unreachable code in `isValidDNft` modifier in VaultManagerV2

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L43

The `isValidDNft` modifier is designed to revert when the provided NFT is invalid, that is, has no owner:

```Solidity
File: VaultManagerV2.sol
42:   modifier isValidDNft(uint id) {
43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;
44:   }
```

The `revert InvalidDNft()` part however is unreachable, because since DNft inherits from OZ's ERC721 implementation, [it can't return `address(0)` because in this case it will revert with the `"ERC721: invalid token ID"` error instead](https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L70-L74).

# [G-01] Significant gas could be saved if Licenser/KeroseneManager `isLicensed` function accepted multiple inputs

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L261
https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L280

When calculating collateral values, VaultManagerV2 makes repeated calls to the same two contracts, up to 5 each.
If these contracts were able to validate 5 vaults in one call, i.e. by accepting an array of addresses and returning an array of booleans, this could save many external calls and the associated gas.

# [NC-01] Inconsistent spelling between `kerosene` and `kerosine`

In many places, including notable instances in file and contract names, `kerosene` is incorrectly spelled `kerosine`.