| ID    | Title |number of issue|
| -------- | ------- |---------------|
| 01 | SOLMATE SAFETRANSFER AND SAFETRANSFERFROM DOES NOT CHECK THE CODESIZE OF THE TOKEN ADDRESS, WHICH MAY LEAD TO FUND LOSS | 8 |


## [01] SOLMATE SAFETRANSFER AND SAFETRANSFERFROM DOES NOT CHECK THE CODESIZE OF THE TOKEN ADDRESS, WHICH MAY LEAD TO FUND LOSS

Solmate safetransferFrom doesn’t check the existence of code at the token address, all contract below that use SafeTransferLib and and all safeTransfer and safeTransferFrom has the issue below . The impacted function and LOC is linked above.            (See warden's original submission for the impacted function and LOC)https://github.com/code-423n4/2023-01-astaria-findings/issues/113
```

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L13
import {SafeTransferLib}   from "@solmate/src/utils/SafeTransferLib.sol";

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L20
  using SafeTransferLib   for ERC20;

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/VaultManagerV2.sol#L129
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.sol#L8
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.sol#L13
  using SafeTransferLib for ERC20;

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L13
import {SafeTransferLib} from "@solmate/src/utils/SafeTransferLib.sol";

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L16
  using SafeTransferLib for ERC20;

https://github.com/code-423n4/2024-04-dyad/blob/4a987e536576139793a1c04690336d06c93fca90/src/core/Vault.kerosine.unbounded.sol#L39
    asset.safeTransfer(to, amount); 

```

This is a known issue while using solmate’s libraries.
Hence this may lead to miscalculation of funds and may lead to loss of funds , because if safetransfer() and safetransferfrom() are called on a token address that doesn’t have contract in it, it will always return success, bypassing the return value check.

If a underlying token is self-destructed, the code may consider the transfer because the lack of contract existence contract.

Due to this protocol will think that funds has been transferred and successful , and records will be accordingly calculated, but in reality funds were never transferred

So this will lead to miscalculation and possibly loss of funds

Recommended Mitigation Steps
Use openzeppelin’s safeERC20 or implement a code existence check.




