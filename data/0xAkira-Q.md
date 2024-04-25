# [LOW-01] - No possibility for the user to withdraw funds
## Impact
While using the withdrawal function,
 there is a check that “Withdrawal should not be in the same block as deposit”. 
```solidity
function withdraw(
    uint    id,
    address vault,
    uint    amount,
    address to
  ) 
    public
      isDNftOwner(id)
  {
    if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
    uint dyadMinted = dyad.mintedDyad(address(this), id);
    Vault _vault = Vault(vault);
    uint value = amount * _vault.assetPrice() 
                  * 1e18 
                  / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
    if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }
```

the `deposit()` function sets the `block.number`
```solidity 
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
 so the **attacker** can browse the `mempool` or run a loop for each block by specifying someone else's token id and passing `amount=0`, thus preventing the attacker from withdrawing funds to the user.
## Proof of Concept
```solidity
function testDeposit() public {
        deal(alice, 1 ether);
        uint256 id = contracts.vaultManager.dNft().mintNft{value: 1 ether}(
            alice
        );
        assertEq(alice, contracts.vaultManager.dNft().ownerOf(644));

        vm.prank(attacker);

        contracts.vaultManager.deposit(644, address(contracts.ethVault), 0);
        vm.prank(alice);

        contracts.vaultManager.withdraw(
            644,
            address(contracts.ethVault),
            10,
            alice
        );
    }
```
```bash
Failing tests:
Encountered 1 failing test in test/fork/v2.t.sol:V2Test
[FAIL. Reason: DepositedInSameBlock()] testDeposit() (gas: 213595)
```
## Tools Used
forge
## Recommended Mitigation Steps
Сonsider adding the `isDNftOwner(uint id)` modifier to the `deposit()` function