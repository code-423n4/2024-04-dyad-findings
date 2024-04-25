# User can't withdraw until after 10 blocks 
## Details
This bug is related to the flashloan protection mechanic and affects the if check in the `withdraw` function in [`VaultManagerV2`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L143) :
```solidity
if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
```

The intended behavior is to prevent transactions from occurring in the same block to prevent a flashloan attack. This is done with the [`idToBlockOfLastDeposit`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37):
```solidity
mapping (uint => uint) public idToBlockOfLastDeposit;
```

Whenever a deposit is made, the [`deposit`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L127) function updates the `idToBlockOfLastDeposit` mapping:
```solidity
idToBlockOfLastDeposit[id] = block.number;
```

However, in the Foundry testing environment, the revert `DepositedInSameBlock()` throws if a withdraw is attempted before 10 blocks. 

## Proof of Concept
I added a getter function for `idToBlockOfLastDeposit` in [`VaultManagerV2.sol`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L127):
```solidity
function getBlockNumber(uint id) public view returns(uint) {
	return idToBlockOfLastDeposit[id];
}
```

I've also edited the the original [`VaultManagerHelper.t.sol`](https://github.com/code-423n4/2024-04-dyad/blob/main/test/VaultManager.t.sol).
- To the `deposit` helper function, I added a `console.log` to display the block number 
- I added a `withdraw` helper function to roll blocks forward and then withdraw:
```solidity
  function mintDNft() public returns (uint) {
    return dNft.mintNft{value: 1 ether}(address(this));
  }

  function addVault(uint id, address vault) public {
    vm.prank(vaultLicenser.owner());
    vaultLicenser.add(vault);
    vaultManager. add(id, vault);
  }

  function deposit(
    ERC20Mock token,
    uint      id,
    address   vault,
    uint      amount

  ) public {
    token.mint(address(this), amount);
    token.approve(address(vaultManager), amount);
    vaultManager.deposit(id, address(vault), amount);
    uint newLastBlock = vaultManager.getBlockNumber(id);
    console.log("deposit block: ", newLastBlock);
    emit log_uint(block.number);
  }

  function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) public {
    vm.roll(10);
    uint lastBlock = vaultManager.getBlockNumber(id);
    console.log("withdraw deposit block: ", lastBlock);
    emit log_uint(block.number);
    vaultManager.withdraw(id, vault, amount, to);
  }
```

This test that I created will correctly revert with `[FAIL. Reason: DepositedInSameBlock()]` as the withdraw occurs in the same block as the deposit.
- The console.log from the deposit helper function returns `1`
```solidity
function test_bug_withdraw() public {
    uint AMOUNT = 1e18;
    uint id = mintDNft();

    vaultManager.add(id, address(wethVault));

    deposit(weth, id, address(wethVault), AMOUNT);

    vaultManager.withdraw(id, address(wethVault), AMOUNT, RECEIVER);

    assertEq(vaultManager.getVaults(id)[0], address(wethVault));
  }
```

When I updated the test to use the `withdraw` helper function which rolls 10 blocks, we still get the same `[FAIL. Reason: DepositedInSameBlock()]` revert.
- The console.log from the deposit helper function returns `1`
- The console.log from the withdraw helper function returns `10`
```solidity
function test_bug_withdraw() public {
    uint AMOUNT = 1e18;

    uint id = mintDNft();
    vaultManager.add(id, address(wethVault));

    deposit(weth, id, address(wethVault), AMOUNT);
    withdraw(id, address(wethVault), AMOUNT, RECEIVER);
  }
```


When I updated the `withdraw` helper function and use a `vm.roll(11)`, the withdraw is successful. 
- The console.log from the deposit helper function returns `1`
- The console.log from the withdraw helper function returns `11`

## Tools Used
Manual Review

## Recommended Mitigation Steps
While this bug doesn't affect the overall functionality of the protocol, it could be useful information to disclose to users. Let them know that you can withdraw after 10 blocks. 