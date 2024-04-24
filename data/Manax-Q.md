## L-1: No Natspec in any of the code

Not having Natspec (Natural Language Specification) it makes a smart contract hard to document.

Adding Natspec makes a code base more readable, maintainable. It is particularly useful for developers working in teams. And When the codebase is complex, as they provide a human readable format that can be understood by others as the protocol gets updated in future version.

ADD NATSPEC IN THE CODEBASE!!!!!!!

## L-2: Centralization Risk for trusted owners

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

- Found in src/core/DNft.sol [Line: 37](src/core/DNft.sol#L37)

	```solidity
	      onlyOwner 
	```

- Found in src/core/DNft.sol [Line: 56](src/core/DNft.sol#L56)

	```solidity
	      onlyOwner
	```

## L-3: Solmate's SafeTransferLib does not check for token contract's existence

There is a subtle difference between the implementation of solmate's SafeTransferLib and OpenZeppelin's SafeERC20: OpenZeppelin's SafeERC20 checks if the token is a contract or not, solmate's SafeTransferLib does not.
checkout solmate repo
https://github.com/transmissions11/solmate/blob/main/src/utils/SafeTransferLib.sol#L9 
`@dev Note that none of the functions in this library check that a token has code at all! That responsibility is delegated to the caller`


- Found in src/core/DNft.sol [Line: 5](src/core/DNft.sol#L5)

	```solidity
	import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/Vault.kerosine.sol [Line: 8](src/core/Vault.kerosine.sol#L8)

	```solidity
	import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 13](src/core/Vault.kerosine.unbounded.sol#L13)

	```solidity
	import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/Vault.sol [Line: 10](src/core/Vault.sol#L10)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/Vault.wsteth.sol [Line: 11](src/core/Vault.wsteth.sol#L11)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/VaultManager.sol [Line: 12](src/core/VaultManager.sol#L12)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/core/VaultManagerV2.sol [Line: 13](src/core/VaultManagerV2.sol#L13)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/periphery/Payments.sol [Line: 9](src/periphery/Payments.sol#L9)

	```solidity
	import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";
	```

- Found in src/staking/Staking.sol [Line: 8](src/staking/Staking.sol#L8)

	```solidity
	import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";
	```


## L-4: Unsafe ERC20 Operations should not be used

Their are weird ERC20 tokens. some return values are not always meaningful. some are upgradable, some openup to reentrancy. So it is recommended to use OpenZeppelin's SafeERC20 library.

- Found in script/deploy/Deploy.Staking.sol [Line: 23](script/deploy/Deploy.Staking.sol#L23)

	```solidity
	    kerosine.transfer(
	```

- Found in script/deploy/Deploy.Staking.sol [Line: 31](script/deploy/Deploy.Staking.sol#L31)

	```solidity
	    kerosine.transfer(
	```

- Found in script/deploy/DeployBase.Kerosine.sol [Line: 43](script/deploy/DeployBase.Kerosine.sol#L43)

	```solidity
	    kerosine.transfer(
	```

- Found in script/deploy/DeployBase.Kerosine.sol [Line: 51](script/deploy/DeployBase.Kerosine.sol#L51)

	```solidity
	    kerosine.transfer(
	```

- Found in src/periphery/Payments.sol [Line: 88](src/periphery/Payments.sol#L88)

	```solidity
	    asset.approve(address(vaultManager), netAmount);
	```


## L-5: Solidity pragma should be specific, not wide

Consider using a specific version of Solidity in your contracts instead of a wide version. For example, instead of `pragma solidity ^0.8.0;`, use `pragma solidity 0.8.0;`

- Found in src/interfaces/IStaking.sol [Line: 2](src/interfaces/IStaking.sol#L2)

	```solidity
	pragma solidity ^0.8.17;
	```

- Found in src/staking/Staking.sol [Line: 2](src/staking/Staking.sol#L2)

	```solidity
	pragma solidity ^0.8.17;
	```


## L-6: Missing checks for `address(0)` when assigning values to address state variables

Check for `address(0)` when assigning values to address state variables.

- Found in src/core/Dyad.sol [Line: 34](src/core/Dyad.sol#L34)

	```solidity
	      mintedDyad[msg.sender][id] += amount;
	```

- Found in src/core/Dyad.sol [Line: 46](src/core/Dyad.sol#L46)

	```solidity
	      mintedDyad[msg.sender][id] -= amount;
	```

- Found in src/core/Vault.kerosine.bounded.sol [Line: 29](src/core/Vault.kerosine.bounded.sol#L29)

	```solidity
	    unboundedKerosineVault = _unboundedKerosineVault;
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 47](src/core/Vault.kerosine.unbounded.sol#L47)

	```solidity
	    kerosineDenominator = _kerosineDenominator;
	```

- Found in src/core/VaultManagerV2.sol [Line: 63](src/core/VaultManagerV2.sol#L63)

	```solidity
	      keroseneManager = _keroseneManager;
	```

- Found in src/periphery/Payments.sol [Line: 47](src/periphery/Payments.sol#L47)

	```solidity
	    feeRecipient = _feeRecipient;
	```

- Found in src/staking/KerosineDenominator.sol [Line: 14](src/staking/KerosineDenominator.sol#L14)

	```solidity
	    kerosine = _kerosine;
	```

- Found in src/staking/Staking.sol [Line: 72](src/staking/Staking.sol#L72)

	```solidity
	      balanceOf[msg.sender] += _amount;
	```

- Found in src/staking/Staking.sol [Line: 79](src/staking/Staking.sol#L79)

	```solidity
	      balanceOf[msg.sender] -= _amount;
	```


## L-8: Define and use `constant` variables instead of using literals

If the same constant literal value is used multiple times, create a constant state variable and reference it throughout the contract. this would make the code base more readable.

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 62](src/core/Vault.kerosine.unbounded.sol#L62)

	```solidity
	                / (10**vault.asset().decimals()) 
	```

- Found in src/core/Vault.kerosine.unbounded.sol [Line: 63](src/core/Vault.kerosine.unbounded.sol#L63)

	```solidity
	                / (10**vault.oracle().decimals());
	```

- Found in src/core/Vault.sol [Line: 87](src/core/Vault.sol#L87)

	```solidity
	              / 10**oracle.decimals() 
	```

- Found in src/core/Vault.sol [Line: 88](src/core/Vault.sol#L88)

	```solidity
	              / 10**asset.decimals();
	```

- Found in src/core/Vault.wsteth.sol [Line: 87](src/core/Vault.wsteth.sol#L87)

	```solidity
	              * 1e18 
	```

- Found in src/core/Vault.wsteth.sol [Line: 88](src/core/Vault.wsteth.sol#L88)

	```solidity
	              / 10**oracle.decimals() 
	```

- Found in src/core/Vault.wsteth.sol [Line: 89](src/core/Vault.wsteth.sol#L89)

	```solidity
	              / 10**asset.decimals();
	```

- Found in src/core/Vault.wsteth.sol [Line: 105](src/core/Vault.wsteth.sol#L105)

	```solidity
	             / 1e18;
	```

- Found in src/core/VaultManager.sol [Line: 139](src/core/VaultManager.sol#L139)

	```solidity
	                    / 1e18;
	```

- Found in src/core/VaultManager.sol [Line: 157](src/core/VaultManager.sol#L157)

	```solidity
	      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
	```

- Found in src/core/VaultManager.sol [Line: 158](src/core/VaultManager.sol#L158)

	```solidity
	      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
	```

- Found in src/core/VaultManager.sol [Line: 159](src/core/VaultManager.sol#L159)

	```solidity
	      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
	```

- Found in src/core/VaultManagerV2.sol [Line: 147](src/core/VaultManagerV2.sol#L147)

	```solidity
	                  * 1e18 
	```

- Found in src/core/VaultManagerV2.sol [Line: 148](src/core/VaultManagerV2.sol#L148)

	```solidity
	                  / 10**_vault.oracle().decimals() 
	```

- Found in src/core/VaultManagerV2.sol [Line: 149](src/core/VaultManagerV2.sol#L149)

	```solidity
	                  / 10**_vault.asset().decimals();
	```

- Found in src/core/VaultManagerV2.sol [Line: 196](src/core/VaultManagerV2.sol#L196)

	```solidity
	                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
	```

- Found in src/core/VaultManagerV2.sol [Line: 198](src/core/VaultManagerV2.sol#L198)

	```solidity
	                    / 1e18;
	```

- Found in src/core/VaultManagerV2.sol [Line: 217](src/core/VaultManagerV2.sol#L217)

	```solidity
	      uint cappedCr               = cr < 1e18 ? 1e18 : cr;
	```

- Found in src/core/VaultManagerV2.sol [Line: 218](src/core/VaultManagerV2.sol#L218)

	```solidity
	      uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);
	```

- Found in src/core/VaultManagerV2.sol [Line: 219](src/core/VaultManagerV2.sol#L219)

	```solidity
	      uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);
	```

- Found in src/staking/Staking.sol [Line: 65](src/staking/Staking.sol#L65)

	```solidity
	          (rewardRate * (lastTimeRewardApplicable() - updatedAt) * 1e18) /
	```

- Found in src/staking/Staking.sol [Line: 88](src/staking/Staking.sol#L88)

	```solidity
	              (rewardPerToken() - userRewardPerTokenPaid[_account])) / 1e18) +
	```

## L-11: Inconsistency in declaring uint256/uint (or) int256/int variables within a contract

Consider keeping the naming convention consistent in a given contract. for example instead of using int use int256 or int64, and for uint use uint256 or uint128. just name how many bytes your gonna use for the data type

- Found in src/core/Vault.sol [Line: 14](src/core/Vault.sol#L14)

	```solidity
	contract Vault is IVault {
	```

- Found in src/core/Vault.wsteth.sol [Line: 15](src/core/Vault.wsteth.sol#L15)

	```solidity
	contract VaultWstEth is IVault {
	```