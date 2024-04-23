# QA

## [Non-Critical] Missing function comment for `denominator()` in KerosineDenominator.sol
The `KerosineDenominator.sol` contract is missing a comment for the function `denominator()` which is externally accessible.

```

  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  }
 ```
 
 A comment should introduce the function as follows:
 ```
 /**
 * @notice Returns the share of the total supply which is not owned by the DYAD Multi-Sig.
 * @return uint256 difference between total supply of Kerosine and funds held in Multi-Sig.
 */
   function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
 ```


## [Typo] Misalignment of comment - KerosineDenominator.sol:
```
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```

"That" should be "This" and should be moved down to the following line for alignment.


Thus, should be:
```
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. 
    //       This is why we can switch out Denominator contracts.
    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```