
Contract Name: src/core/Vault.kerosine.unbounded.sol


Issue:

The assetPrice function within the (Vault.kerosine.unbounded) contract may consume excessive gas, particularly when there is a large number of vaults. This is primarily due to redundant calculations and storage operations within the loop.


Recommendation:

Optimizing the assetPrice function is crucial to reduce gas consumption and improve the efficiency of the contract. This can be achieved by minimizing redundant calculations and storage operations within the loop.


Code Improvement:

The following code improvements are recommended to optimize the assetPrice function:




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
        uint vaultBalance = vault.asset().balanceOf(address(vault));
        uint assetPrice = vault.assetPrice();
        uint assetDecimals = 10**vault.asset().decimals();
        uint oracleDecimals = 10**vault.oracle().decimals();
        
        tvl += vaultBalance * assetPrice * 1e18 / assetDecimals / oracleDecimals;
    }
    uint numerator = tvl - dyad.totalSupply();
    uint denominator = kerosineDenominator.denominator();
    return numerator * 1e8 / denominator;
}



Explanation:

    
We optimized the assetPrice function by reducing redundant calculations and storage operations within the loop.
    
We introduced local variables vaultBalance, assetPrice, assetDecimals, and oracleDecimals to store the values retrieved from the Vault contract and reduce repetitive function calls within the loop.
    
By precomputing these values outside the loop, we minimized gas consumption and improved the efficiency of the function.