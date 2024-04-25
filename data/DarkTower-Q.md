**[L-1] `assetPrice()` queries from Kerosene price to determine price will fail when TVL is 0**
-

In the case TVL is 0, the function will revert as it attempts a subtraction from 0 operation which runs into an underflow.
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L65
```solidity
function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
@>    uint numerator   = tvl - dyad.totalSupply(); // @audit revert if TVL resolves to 0
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }
```

Return 0 or implement a case where if the TVL is 0, return no price:
```diff
function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      uint tvl;
      address[] memory vaults = kerosineManager.getVaults();
      uint numberOfVaults = vaults.length;
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
        tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
+     if (tvl == 0) { return 0;}
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }
```

**[L-2] `NOTE` owner can pull other user' collateral assets tied to their `NOTE`**
-

Suppose Bob deposits `wETH` as backing collateral into Alice's `NOTE`, Alice can pull the funds from the vault tied to the `NOTE` for the amount deposited by Bob since during withdrawal of assets, one must be the `NOTE's` owner
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119
```solidity
function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id) // @note doesn't need to be the owner of the NOTE to put in collateral for it
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```

```solidity
function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
      isDNftOwner(id) // @note to pull back out the collateral however, need to be the NOTE owner
  {
    ...
  }
```

```solidity
function mintDyad(
    uint    id,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id) // @note and cannot mint DYAD for the NOTE provided collateral for too, if not the owner of the NOTE
  {
    ...
  }
```

This issue requires that Bob makes a dumb mistake or be tricked into depositing into Alice's `NOTE`

Potential fix for this is to allow depositers into a `NOTE` withdraw assets that were deposited since they don't even hold DYAD minted from the said `NOTE` and cannot mint since they are not the owner of the said `NOTE` in the first place. It would be a good safeguard for getting funds back to the right owner.