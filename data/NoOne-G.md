https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/params/Parameters.sol#L4

All Parameters except these:
`address SEPOLIA_DNFT = address(0);`, 
`address SEPOLIA_VAULT_MANAGER = address(0);`,
`address SEPOLIA_DYAD = address(0);`
should be constatns. On other hand these 3 are not used anywhere



`Kerosine public kerosine;` should be immutable
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/staking/KerosineDenominator.sol#L9

 

`function should be view`
https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/test/Vault.wsteth.t.sol#L24





https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/DNft.sol#L22

 function mintNft(address to)
    external 
    payable
    returns (uint) {
     ` uint price = START_PRICE + (PRICE_INCREASE * ++publicMints);`
      if (msg.value < price) revert InsufficientFunds();
      uint id = _mintNft(to);
      if (msg.value > price) to.safeTransferETH(msg.value - price);
      emit MintedNft(id, to);
      return id;
  }

Using pre-increment (++i) or pre-decrement (--i) operators is more gas-efficient compared to their post counterparts (i++ or i--). This is because pre-increment/decrement operators avoid the need for an additional temporary variable that stores the original value of the iterator. This subtle difference results in saving of around 5 gas units per operation, which can accumulate to substantial savings in gas costs in contracts with frequent increment/decrement operations.


`All of these variables should be immutable`

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/governance/Governor.sol#L45

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/governance/TimelockController.sol#L34

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/security/Pausable.sol#L28

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/security/ReentrancyGuard.sol#L37

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC20/ERC20.sol#L42-L43

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/ERC721.sol#L24-L27

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/presets/ERC721PresetMinterPauserAutoId.sol#L45

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/solmate/src/tokens/ERC20.sol#L21-L25

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/solmate/src/tokens/ERC721.sol#L21-L24

`All of these constants should be private`

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/KerosineManager.sol#L14

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.sol#L19

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.wsteth.sol#L20

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManager.sol#L20-L22

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L22-L26

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/forge-std/src/console.sol#L5

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/forge-std/src/console2.sol#L10

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/access/AccessControlCrossChain.sol#L26

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/crosschain/arbitrum/LibArbitrumL2.sol#L26

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/crosschain/polygon/CrossChainEnabledPolygonChild.sol#L11

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/governance/Governor.sol#L34-L35

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/governance/TimelockController.sol#L27-L30

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC1155/presets/ERC1155PresetMinterPauser.sol#L29-L30

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC20/presets/ERC20PresetMinterPauser.sol#L29-L30

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/lib/openzeppelin-contracts/contracts/token/ERC721/presets/ERC721PresetMinterPauserAutoId.sol#L40-L41

