## QA Report


| S/N |Issue|
|-|-|
| L-01| Missing checks for `address(0)`| 
| L-02| `withdraw` Function is incorrectly declared as `view` | 
| L-03 | `withdraw` Function Always Reverts|
| L-04 |  Lack of Input Validation|
| L-05 |  Reentrancy Vulnerability in `withdraw` Function |
| L-06 | Lack of Input Validation in `setDenominator` Function |
| L-07 | Centralization Risk for trusted owners|
| L-08 | `public` functions not used internally could be marked `external` |
| L-09 | Define and use `constant` variables instead of using literals | 
| L-10 | Division operations precede multiplication operations | 



### L-01: Missing checks for `address(0)`

##### MintDyad Function Issues:
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L156

The `mintDyad` function does not validate that the `amount` to be minted is greater than zero, which could lead to unnecessary transactions where no tokens are actually minted. Additionally, it does not check if the `to` address is a valid address, potentially allowing tokens to be minted to the zero address.

Recommendation: 
- Ensure that the `amount` is greater than zero to prevent unnecessary transactions.
- Validate the `to` address to ensure it is not the zero address.

```solidity
require(amount > 0, "Amount must be greater than zero");
require(to != address(0), "Invalid recipient address");
```


##### BurnDyad Function Issues
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L172

The `burnDyad` function lacks a check to ensure that the `amount` to be burned is greater than zero, which could lead to unnecessary transactions where no tokens are actually burned.

Recommendation:
- Add a require statement to ensure that the `amount` is greater than zero.

```solidity
require(amount > 0, "Amount must be greater than zero");
```


##### RedeemDyad Function Issues
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L184
The `redeemDyad` function does not validate that the `amount` to be redeemed is greater than zero, which could lead to unnecessary transactions where no tokens are actually redeemed. Additionally, it does not check if the `to` address is a valid address, potentially allowing tokens to be redeemed to the zero address. Lastly, it does not check if the caller has enough Dyad tokens to redeem, which could lead to a situation where a user attempts to redeem more tokens than they own.

Recommendation:
- Ensure that the `amount` is greater than zero to prevent unnecessary transactions.
- Validate the `to` address to ensure it is not the zero address.
- Check if the caller has enough Dyad tokens to redeem before proceeding with the redemption.

```solidity
require(amount > 0, "Amount must be greater than zero");
require(to != address(0), "Invalid recipient address");
require(dyad.balanceOf(msg.sender, id) >= amount, "Insufficient Dyad tokens to redeem");
```





### L-02: `withdraw` Function is incorrectly declared as `view`
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L38

The `withdraw` function is declared with the `view` modifier, which means it's not supposed to modify the state of the contract. However, the function's name and parameters suggest that it's intended to perform a withdrawal operation, which inherently involves state changes (e.g., reducing the balance of the contract or the specified `to` address).

**Mitigation:** Remove the `view` modifier from the `withdraw` function to allow it to modify the state.

```solidity
function withdraw(
 uint    id,
 address to,
 uint    amount
) 
 external 
 onlyVaultManager
{
 revert NotWithdrawable(id, to, amount);
}
```


### L-03: `withdraw` Function Always Reverts
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L41

The `withdraw` function always reverts with the `NotWithdrawable` error, regardless of the input parameters. This means that the function is not functional as intended.

**Mitigation:** Implement the logic for the withdrawal operation within the `withdraw` function. This could involve transferring the specified `amount` of the asset to the `to` address and updating the internal state accordingly.

```solidity
function withdraw(
 uint    id,
 address to,
 uint    amount
) 
 external 
 onlyVaultManager
{
 // Implement withdrawal logic here
 // For example:
 // require(amount <= unboundedKerosineVault.balanceOf(address(this)), "Insufficient balance");
 // unboundedKerosineVault.transfer(to, amount);
 // Update internal state as necessary
}
```



### L-04: Lack of Input Validation

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L32
The `withdraw` function does not perform any input validation. It's crucial to validate inputs to prevent unexpected behavior and potential security vulnerabilities.

**Mitigation:** Add input validation to the `withdraw` function. For example, ensure that the `amount` is not zero and that the contract has sufficient balance to fulfill the withdrawal request.

```solidity
function withdraw(
 uint    id,
 address to,
 uint    amount
) 
 external 
 onlyVaultManager
{
 require(amount > 0, "Amount must be greater than 0");
 require(to != address(0), "Invalid recipient address");
 // Additional validation as necessary
}
```



### L-05: Reentrancy Vulnerability in `withdraw` Function

https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L38-L39
The `withdraw` function is susceptible to a reentrancy attack. This is because it first updates the state (`id2asset[id] -= amount;`) and then calls an external contract (`asset.safeTransfer(to, amount);`). If the `to` address is a malicious contract, it could call back into the `withdraw` function before the state is fully updated, potentially leading to double withdrawals.

**Mitigation:**

To mitigate this, you can use the Checks-Effects-Interactions pattern. This involves performing all external calls at the end of the function, after all state changes have been made.

```solidity
function withdraw(
 uint    id,
 address to,
 uint    amount
) 
 external 
    onlyVaultManager
{
 uint previousAmount = id2asset[id];
 require(previousAmount >= amount, "Insufficient balance");
 id2asset[id] -= amount;
 emit Withdraw(id, to, amount);
 asset.safeTransfer(to, amount);
}
```




### L-06: Lack of Input Validation in `setDenominator` Function
https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L43
The `setDenominator` function does not validate the input `_kerosineDenominator`. This could lead to unexpected behavior if a zero address or an uninitialized contract is set as the denominator.

**Mitigation:**

Add a require statement to ensure that the input is not a zero address.

```solidity
function setDenominator(KerosineDenominator _kerosineDenominator) 
 external 
    onlyOwner
{
 require(address(_kerosineDenominator) != address(0), "Invalid address");
 kerosineDenominator = _kerosineDenominator;
}
```











### L-07: Centralization Risk for trusted owners

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.


- Found in src/core/KerosineManager.sol [Line: 7](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L7)

	```solidity
	contract KerosineManager is Owned(msg.sender) {
	```

- Found in src/core/KerosineManager.sol [Line: 22](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L22)

	```solidity
	      onlyOwner
	```

- Found in src/core/KerosineManager.sol [Line: 32](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/KerosineManager.sol#L32)

	```solidity
	      onlyOwner
	```


- Found in src/core/Vault.kerosine.bounded.sol [Line: 27](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L27)

	```solidity
	    onlyOwner
	```

- Found in src/core/Vault.kerosine.sol [Line: 12](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L12)

	```solidity
	abstract contract KerosineVault is IVault, Owned(msg.sender) {
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 45](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L45)

	```solidity
	      onlyOwner
	```






### L-08: `public` functions not used internally could be marked `external`

Instead of marking a function as `public`, consider marking it as `external` if it is not used internally.


- Found in src/core/Vault.kerosine.bounded.sol [Line: 44](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L45)

	```solidity
	  function assetPrice() 
	```

- Found in src/core/Vault.kerosine.sol [Line: 36](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L40)

	```solidity
	  function deposit(
	```

- Found in src/core/Vault.kerosine.sol [Line: 60](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.sol#L63)

	```solidity
	  function getUsdValue(
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 50](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L51)

	```solidity
	  function assetPrice() 
	```







### L-09: Define and use `constant` variables instead of using literals

If the same constant literal value is used multiple times, create a constant state variable and reference it throughout the contract.

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 62](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L62)

	```solidity
	                / (10**vault.asset().decimals()) 
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 63](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L63)

	```solidity
	                / (10**vault.oracle().decimals());
	```


- Found in src/core/VaultManagerV2.sol [Line: 147](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L147)

	```solidity
	                  * 1e18 
	```

- Found in src/core/VaultManagerV2.sol [Line: 148](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L148)

	```solidity
	                  / 10**_vault.oracle().decimals() 
	```

- Found in src/core/VaultManagerV2.sol [Line: 149](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L149)

	```solidity
	                  / 10**_vault.asset().decimals();
	```

- Found in src/core/VaultManagerV2.sol [Line: 196](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L196)

	```solidity
	                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
	```

- Found in src/core/VaultManagerV2.sol [Line: 198](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L198)

	```solidity
	                    / 1e18;
	```

- Found in src/core/VaultManagerV2.sol [Line: 217](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L217)

	```solidity
	      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
	```

- Found in src/core/VaultManagerV2.sol [Line: 218](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L218)

	```solidity
	      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
	```

- Found in src/core/VaultManagerV2.sol [Line: 219](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L219)

	```solidity
	      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
	```




### L-10: Division operations precede multiplication operations

Always perform integer multiplication before division where possible.


https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L146-L149
```solidity
uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
```




https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L196-L199
```solidity
 uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;
```














