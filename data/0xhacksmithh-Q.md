

### [L-1] Current implementation for stoping flashloan attacks also stoping deposite and withdrawal from different vaults at same time

In current situation to stop flshloan attack there is a mapping `mapping (uint => uint) public idToBlockOfLastDeposit`
which set in `deposit()`
```solidity
idToBlockOfLastDeposit[id] = block.number;
```
and checked in `withdraw()`
```solidity
if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
```

so that in same block both `deposit` and `withdraw` not possible

But problem here is that A `id` can handle upto 10 `vaults`
```solidity
  uint public constant MAX_VAULTS          = 5;
  uint public constant MAX_VAULTS_KEROSENE = 5;
```

and mapping `idToBlockOfLastDeposit` directly tracks `id` not any specific `vaults`

So it possible that when user `deposits` to a `vault-A` he will unable to `withdraw` from `vault-B`


https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L127

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L143

#### Mitigation

we could change mapping to more specific
Like a tracking `Id => vault => blockNumber`



### [L-2] Unnecessary Precision because of how formulas are used in code, due to inbuilt nature of `/` in solidity

Here we see two formula (Actually one formula with 2 variantions) from `withdraw()` and `redeem()`

```solidity
  function withdraw( 
...
...
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals(); 
...
  }
```

So if we solve for `amount` from above equation
```
 amount = value *(10**(_vault.oracle().decimals() + _vault.asset().decimals()))/ (_vault.assetPrice() * 1e18)
```
Which should be the equation which will be used in case of `reedmDyad`

But equation implemented as follow

```solidity
  function redeemDyad(
...
...
      uint asset = amount 
                    * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
                    / _vault.assetPrice() 
                    / 1e18;
...
  }
```

Due to extra `/` extra precission loss happen due to division nature in solidity which is rounding down

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146-L149

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195-L198



### [L-3] User can liquidate himself by provideing (id == to) in liquidate function
Due to there is no validation checkl in `liquidation()` that `id != to` so user can simply liquidate its own vaults and transfer its own assets to same dnft and take bonus.

for example ::
1. id-1 has CR 1e18
2. User call liquidation with (liquidation(id-1, id-1))
3. CR fetched for id-1
4. dyad burn from user `dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));`
5. cappedCr = 1e18
6. liquidationEquityShare = 0
7. liquidationAssetShare = 0
8. vault move collateral from `id-1` to `id-1`
```solidity
  function move(
    uint from,
    uint to,
    uint amount
  )
    external
      onlyVaultManager
  {
    id2asset[from] -= amount;
    id2asset[to]   += amount;
    emit Move(from, to, amount);
  }
```
8. liqudatior Reward = 100%

```solidity
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
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L227


### [L-4] While going through `Vaults.sol`'s `assetPrice()` here price's staleness check not implemnted properly, As `VaultManagerV2.sol`'s `getNonKeroseneValue()` heavily depended on it. So its become vary crusial here

```solidity
```



### [L-5] Oracle Min-Max

```solidity
```




### [L-6] Hardcoding A single Haear Beat time period for all type Assets, will may be cause some issue during future upgrades where protocol may going to support multiple type of asset as collateral

```solidity
```



### [L-7] Made Zero address check when setting important address state variable

```solidity
 constructor(
    DNft          _dNft,
    Dyad          _dyad,
    Licenser      _licenser
  ) {
    dNft          = _dNft; // @audit L :: address0 check
    dyad          = _dyad;
    vaultLicenser = _licenser;
  }

  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager; // @audit NC :: setter check, no event
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L54-L56

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63




### [N-1] Missing Events after critical initialization.

Emitting an initialization event offers clear, on-chain evidence of the contract's initialization state, enhancing transparency and auditability. This practice aids users and developers in accurately tracking the contract's lifecycle, pinpointing the precise moment of its initialization. Moreover, it aligns with best practices for event logging in smart contracts, ensuring that significant state changes are both observable and verifiable through emitted events.
```solidity
  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager; 
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63

### [N-2] Consider using named returns 
Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L235
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L246
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L255
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L274
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L295
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L305
```solidity

  function getTotalUsdValue(
    uint id
  ) 
    public 
    view
    returns (uint) {


  ) 
    public 
    view
    returns (uint) {


    external 
    view 
    returns (address[] memory) {
      return vaults[id].values();
  }
```


### [N-3] Upgrade `openzeppelin` to the Latest vaersion - 5.0.0 
These contracts import contracts from @openzeppelin/contracts but they are not using the latest version. For more information, please visit: OpenZeppelin GitHub Releases It is recommended to always use the latest version to take advantage of updates and security fixes.

```solidity
     [submodule "lib/openzeppelin-contracts"]
	path = lib/openzeppelin-contracts
	url = https://github.com/openzeppelin/openzeppelin-contracts
	branch = v4.8.0
```




### [N-4] Consider adding emergency-stop functionality 

Smart contracts that hold significant value, interact with external contracts, or have complex logic should include an emergency-stop mechanism for added security. This allows pausing certain contract functionalities in case of emergencies, mitigating potential damages.

This contract seems to lack such a mechanism. Implementing an emergency stop can enhance contract security and reliability.




### [N-5] Consider marking contracts `upgradeable`
Contract uses a non-upgradeable design. Transitioning to an upgradeable contract structure is more aligned with contemporary smart contract practices. This approach not only enhances flexibility but also allows for continuous improvement and adaptation, ensuring the contract stays relevant and robust in an ever-evolving ecosystem.




### [N-6] Events that mark critical parameter changes should contain both the old and the new value

When emitting events that signify critical changes in parameters, it's important to include both the old and new values.

This aids in auditability, providing more complete information about the state change. It's especially necessary when the new value isn't required to be different from the old one, as this prevents ambiguity in event logs.

```solidity
  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager; 
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63


### [N-7] Unused imports, inheritance 

The contract contains import statements for libraries or other contracts that are not utilized within the code. Excessive or unused imports can clutter the codebase, leading to inefficiency and potential confusion. Consider removing any imports that are not essential to the contract's functionality.

`Initializable` never used

```solidity
contract VaultManagerV2 is IVaultManager, Initializable {
```
https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17



### [N-8] Setters should pevent re-setting of the same value 

Setter functions should include a condition to check if the new value being assigned is different from the current value. This practice prevents redundant state changes and the emission of unnecessary events, ensuring that changes only occur when actual updates to the values are made.

This not only helps to maintain the integrity of the contract's state but also keeps the event logs cleaner and more meaningful by avoiding the recording of identical consecutive values. Such an approach can improve the clarity and efficiency of debugging and data tracking processes.

```solidity
  function setKeroseneManager(KerosineManager _keroseneManager) 
    external
      initializer 
    {
      keroseneManager = _keroseneManager; // @audit NC :: setter check, no event
  }
```

https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L63


### [N-9] Contracts should have full test coverage 

It's recommended to have full test coverage for all contracts. While 100% code coverage does not guarantee absence of bugs, it can catch simple bugs and reduce regressions during code modifications. Moreover, to achieve full coverage, authors often have to refactor their code into more modular components, each testable separately. This leads to lower interdependencies, and results in code that is easier to understand and audit.



### [N-10] Implement formal verification proof to improve security 

Formal verification offers a mathematical proof confirming that your code operates as intended and is devoid of edge cases that may lead to unintended behavior. By leveraging this rigorous audit technique, you not only enhance the robustness of your code but also strengthen the trust of stakeholders in the safety of your contract.


