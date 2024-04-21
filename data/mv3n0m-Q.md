### Conditional storage checks are not consistent

When writing `require` or `if` conditionals that check storage values, it is important to be consistent to prevent off-by-one errors. There are instances found where the same storage variable is checked multiple times, but the conditionals are not consistent.

- Found in src/core/VaultManagerV2.sol [Line: 152](src/core/VaultManagerV2.sol#L152)

	```solidity
	    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
	```

- Found in src/core/VaultManagerV2.sol [Line: 214](src/core/VaultManagerV2.sol#L214)

	```solidity
	      if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
	```

Similar lines can be seen in other files too, which are not in scope.