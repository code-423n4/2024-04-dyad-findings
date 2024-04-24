### Bug in MintDyad Function Leads to Misleading Total Supply of DYAD Tokens

### Summary 
`VaultManagerV2::mintDyad` function causes incorrect reporting of the total supply of DYAD tokens when tokens are minted to the zero address (0x0). This operation does not actually mint new tokens but is recorded as an increase in the total supply

### Details 

[Code](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L166)

The contract uses solmate ERC20, which does not check for address(0x0)
The price of Kerosene = C-D/K
D(totalSupply of DYAD) increases but that amount is not in circulation.

Solmate's ERC20 :
``` 
function _mint(address to, uint256 amount) internal virtual {
        totalSupply += amount;

        // Cannot overflow because the sum of all user
        // balances can't exceed the max uint256 value.
        unchecked {
            balanceOf[to] += amount;
        }

        emit Transfer(address(0), to, amount);
    }
``` 

### Impact : 
Low as the chances/frequency of this is low

### Recommendation 
Implement a validation check within the mintDyad function to ensure that the to parameter is not the zero address.
