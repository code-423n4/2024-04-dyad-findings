# QA

### Name confusions

In KerosineManager 
`EnumerableSet.AddressSet private vaults;`

//@audit same name as the uint=>Enum mapping in VaultManagerV2
`mapping (uint => EnumerableSet.AddressSet) internal vaults; `

This may confuse offchain readings of these variables

---------------------------------------------------------------

### Vault.kerosine has getUsdValue that isn't virtual

This leads to assetPrice being overriden from an Oracle but not getUsdValue, in the event where the Oracle's decimals are being used. The getUsdValue has hardcoded decimals as 1e8 but this can change.

```solidity

 function getUsdValue(
    uint id
  )
    public
    view 
    //@audit override this too as the decimals can be fetched from an oracle from 
assetPrice
    returns (uint) {
@>      return id2asset[id] * assetPrice() / 1e8; 
  }

```

### onlyVaultManager can be removed in Vault.kerosine.unbounded as it's not necessary

```solidity
function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
    view
      onlyVaultManager //@audit remove this
  {
    revert NotWithdrawable(id, to, amount);
  }
```