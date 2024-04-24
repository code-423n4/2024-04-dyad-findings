## Summary

### Low-Risk Issues
| |Issue|Instances|
|-|:-|:-:|
| [L&#x2011;01] | Solmate's `safeTransfer()` function does not check the existence of the contract. | 2 |
| [L&#x2011;02] | Chainlink Oracle data feed is insufficiently validated and may return stale data. | 1 |
| [L&#x2011;03] | Priority of division over multiplication leads to precision loss. | 1 |

Total: 4 instances over 3 issues


### Non-critical Issues
| |Issue|Instances|
|-|:-|:-:|
| [N&#x2011;01] | Use a more recent version of solidity


Note: The table above was created considering the **automatic findings** and thus, those are not included.



## Low-Risk Issues

### [L&#x2011;01]  Solmate's `safeTransfer()` function does not check the existence of the contract.
Solmate's safeTransfer() and safeTransferFrom() functions do not check the ext code size of the address of the recipient and so, it may lead to a miscalculation of funds as it returns true for addresses that do not have a contract inside them. If mistakenly the asset address is set to a future-deployed address, then the code won't recognize this situation and will transfer the funds. This unintended behavior
will result in fund loss.

*There are 2 instances of this issue:*

```Solidity
  function withdraw(
    uint    id,
    address to,
    uint    amount
  ) 
    external 
      onlyVaultManager
  {
    id2asset[id] -= amount;
    asset.safeTransfer(to, amount); 
    emit Withdraw(id, to, amount);
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L39

```Solidity
  function deposit(
    uint    id,
    address vault,
    uint    amount
  ) 
    external 
      isValidDNft(id)
  {
    idToBlockOfLastDeposit[id] = block.number;
    Vault _vault = Vault(vault);
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L129

Consider using OpenZeppelin's ERC20 token implementation or put a token existence pre-check before any token transfer.


### [L&#x2011;02]  Chainlink Oracle data feed is insufficiently validated and may return stale data.
There is no check for stale price and round completeness. Price can be stale and can lead to wrong answer return value.

*There is 1 instance of this issue:*

```Solidity
  function assetPrice() 
    public 
    view 
    returns (uint) {
      (
        uint80 roundID,
        int256 answer,
        , 
        uint256 updatedAt,
        uint80 answeredInRound 
      ) = oracle.latestRoundData();
      if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
      require(answer > 0, "invalid_oracle_answer");
      require(answeredInRound >= roundID, "ChainLink: Stale price");
      require(updatedAt > 0, "ChainLink: Round not complete");
      return answer.toUint256();
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.sol#L100-L101

Consider modifying the code:

```Solidity
  function assetPrice() 
    public 
    view 
    returns (uint) {
      (
        ,
        int256 answer,
        , 
        uint256 updatedAt, 
      ) = oracle.latestRoundData();
      if (block.timestamp > updatedAt + STALE_DATA_TIMEOUT) revert StaleData();
      return answer.toUint256();
  }
```

### [L&#x2011;03]  Priority of division over multiplication leads to precision loss.

Solidity rounds down the result of an integer division, and because of that, it is always recommended to multiply before dividing to avoid that precision loss. In the case of a prior division over multiplication, the final result may face serious precision loss as the first answer would face truncated precision and then multiplied to another integer.
We can see this behavior in the `liquidate()` function.

```Solidity
  function liquidate(
    uint id,
    uint to
  ) 
    external 
      isValidDNft(id)
      isValidDNft(to)
    {
      uint cr = collatRatio(id);
      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
      dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

      uint numberOfVaults = vaults[id].length();
      for (uint i = 0; i < numberOfVaults; i++) {
          Vault vault      = Vault(vaults[id].at(i));
          uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);
          vault.move(id, to, collateral);
      }
      emit Liquidate(id, msg.sender, to);
  }
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228

Consider prioritizing the multiplication before any division in the calculation of the `collateral` variable.

## Non-critical Issues

### [L&#x2011;01]  Use a more recent version of solidity.

Consider updating the solidity version of the contracts to a more recent version. Some game-changing updates (like the transient storage) are implemented in the most recent version of the Solidity compiler.