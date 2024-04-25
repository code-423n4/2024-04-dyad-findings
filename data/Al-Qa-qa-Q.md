## Summary

|ID|Title|
|:-:|-----|
|[L-01](#l-01-boundedkerosinevaultsetunboundedkerosinevault-is-not-fired-when-deploying-leading-to-dos-when-they-are-added)|`BoundedKerosineVault::setUnboundedKerosineVault` is not fired when deploying, leading to DoS when they are added|
|[L-02](#l-02-no-minimum-threshold-for-positions-makes-so-small-positions-unprofitable-to-get-liquidated)|No minimum threshold for positions makes so small positions unprofitable to get liquidated|
|[L-03](#l-03-maximum-kerosine-vaults-variable-is-written-wrongly)|Maximum kerosine vaults variable is written wrongly|
|[L-04](#l-04-funding-exogenous-vaults-manipulate-kerosine-price)|Funding Exogenous vaults manipulate kerosine price|
|[L-05](#l-05-the-user-can-liquidate-himself)|The user can liquidate himself|
|[L-06](#l-06-the-user-can-mint-0-dyad)|The user can mint 0 `DYAD`|
|[L-07](#l-07-no-way-to-change-mainnet_owner-in-kerosinedenominator)|No way to change `MAINNET_OWNER` in `KerosineDenominator`|
|[L-08](#l-08-boundedkerosinevault-is-not-added-as-a-license-vault)|boundedKerosineVault is not added as a license vault|
|||
|[NC&#8209;01](#nc-01-unused-modifier)|Unused Modifier|
|[NC&#8209;02](#nc-02-no-interface-for-vaultmanagerv2)|No interface for `VaultManagerV2`|
|[NC&#8209;03](#nc-03-code-structure-lacks-comments-and-formatting-and-test-suit-is-not-the-best)|Code Structure Lacks Comments and formatting, and test suit is not the best|
|||
|[GOV](#centralization-risk-and-admin-privileged-functions)|centralization risk and admin-privileged functions.|

---

## [L-01] `BoundedKerosineVault::setUnboundedKerosineVault` is not fired when deploying, leading to DoS when they are added.

For `BoundedKerosineVault` to return the `assetPrice`, it depends on the `UnBoundedkerosineVault` asset price, and multiply it by 2.

[Vault.kerosine.bounded.sol#L44-L50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44-L50)
```solidity
  function assetPrice() 
    public 
    view 
    override
    returns (uint) {
      return unboundedKerosineVault.assetPrice() * 2;
  }
```

And `unboundedKerosineVault` should be set by the owner of the contract.

[Vault.kerosine.bounded.sol#L23-L30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30)
```solidity
  function setUnboundedKerosineVault(
    UnboundedKerosineVault _unboundedKerosineVault
  )
    external
    onlyOwner
  {
    unboundedKerosineVault = _unboundedKerosineVault;
  }
```

In `Deploy.V2.s.sol`, the vault is not set before transferring the ownership from the Deployer to the `MAINNET_OWNER (multi-sig)`. which makes adding this vault leads to reverting when calling different functions in the `VaultManagerV2`, and DoS the protocol.

[Deploy.V2.s.sol#L78-L91](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L78-L91)
```solidity
  function run() public returns (Contracts memory) {
    ...

    UnboundedKerosineVault unboundedKerosineVault = new UnboundedKerosineVault( ... );

    BoundedKerosineVault boundedKerosineVault     = new BoundedKerosineVault( ... );

    KerosineDenominator kerosineDenominator       = new KerosineDenominator( ... );

    unboundedKerosineVault.setDenominator(kerosineDenominator);

    // @audit we did not set the unBoundedVault in `boundedKerosineVault` before transfering the ownership

    unboundedKerosineVault.transferOwnership(MAINNET_OWNER);
    boundedKerosineVault.  transferOwnership(MAINNET_OWNER);
}
```

### PoC

- The protocol Deployed into the mainnet.
- The ownership of the `boundedKerosineVault` transferred to `multi-sig`.
- `boundedKerosineVault` was added as licensed vaults.
- The owner of the dNFT owners added that vault.
- `VaultManagerV2::getNonKeroseneValue`, `VaultManagerV2::getKeroseneValue`, and `VaultManagerV2::getTotalUsdValue` will revert when getting called, as they call `getUsdValue` which calls `assetPrice`, which will make a call to the address(0), and it will revert.
  - If the vault is added as a NonKerosene vault `getNonKeroseneValue()` and `getTotalUsdValue()` will revert.
  - If the vault is added as Kerosene vault `getKeroseneValue()` and `getTotalUsdValue()` will revert
  - If the vault is added to both then all functions will get reverted (if it is a licensed vault as kerosene vault and normal vault).

This will make all the protocols in DoS, as these functions are called when minting, withdrawing, and liquidating.

In the Deployment script, all settings and configurations occur to all newly deployed contracts before transferring the ownership to `MAINNET_OWNER`, So we believe that this is an issue.

### Recommendations

Set the `unBoundedKeroseneVault` before transferring the ownership.

> Deploy.V2.s.sol L:89
```diff
  function run() public returns (Contracts memory) {
    ...

    unboundedKerosineVault.setDenominator(kerosineDenominator);

+   boundedKerosineVault.setUnboundedKerosineVault(unboundedKerosineVault);

    unboundedKerosineVault.transferOwnership(MAINNET_OWNER);
    boundedKerosineVault.  transferOwnership(MAINNET_OWNER);

    ...
  }

```

---

## [L-02] No minimum threshold for positions makes so small positions unprofitable to get liquidated

the owners of the dNFT can mint DYAD by providing collateral equal to `150%`. and if his position gets undercollateralized. people can liquidate him and get a reward for that.

But there is no minimum minting limit for the position. So if the NFT owner made a position with a small amount, and after time this position gets undercollateralized. it can be unprofitable to liquidate that position as the return may be too little compared to the gas that the liquidator will pay for the calling.

### POC
- The owner deposited an amount of ETH.
- The user minted some small DYAD tokens.
- The user removed most of his collateral but made an amount to make his position overcollateralized.
- since he mints small DYAD amounts he only needs to keep a small amount as collateral.
- The price of the collateral changes and the position is undercollateralized now.
- No one wants to liquidate that position, as he will pay a lot for gas compared to the value he will gain.

[VaultManagerV2.sol#L156-L169](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169)
```solidity
  // @audit no minimum amount to mint
  function mintDyad( ... ) external isDNftOwner(id) {
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
    dyad.mint(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
    emit MintDyad(id, amount, to);
  }
```

This can introduce issues where some positions can be undercollateralized, which is not a good thing for the protocol and coin stability, and there is no incentivize to liquidate the position.

### Recommendations

- Make a minimum amount for minting new DYAD when calling `VaultManagerV2::mintDyad()`.
- Make the burning failed if the position goes below the threshold you configured for minting when calling `VaultManagerV2::burnDyad()` .

---

## [L-03] Maximum kerosine vaults variable is written wrongly

In `KersineManager.sol`, `MAX_VAULTS` is set to `10`.

[KerosineManager.sol#L14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14)
```solidity
  uint public constant MAX_VAULTS = 10;
```

But in `VaultManagerV2`, The number is set to `5`.

[VaultManagerV2.sol#L23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23)
```solidity
  uint public constant MAX_VAULTS_KEROSENE = 5;
```

This will introduce issues if they are intended to add more than `5` vaults. and having the limit number different in two different locations is not good after all.

### Recommendations
Make the value the same in both, either make it `5` in both or `10` in both.

---

## [L-04] Funding Exogenous vaults manipulate kerosine price

`kerosine` value should represent `degree of DYAD’s overcollateralization`. as its value is determined using the total DYAD minted and the total value Locked.

[Vault.kerosine.unbounded.sol#L60-L65](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L60-L65)
```solidity
  function assetPrice() ... returns (uint) {
      ...
      for (uint i = 0; i < numberOfVaults; i++) {
        Vault vault = Vault(vaults[i]);
<@      tvl += vault.asset().balanceOf(address(vault)) 
                * vault.assetPrice() * 1e18
                / (10**vault.asset().decimals()) 
                / (10**vault.oracle().decimals());
      }
      uint numerator   = tvl - dyad.totalSupply();
      uint denominator = kerosineDenominator.denominator();
      return numerator * 1e8 / denominator;
  }
```

But the problem here is that `balanceOf` thinks that all the balance in the vault is used as collateral for `DYAD`.

If we donate the vaults, the donated funds will not be collateral funds, as they will be locked inside the Vault contract (can not be used to mint `DYAD`). This will make `kerosine` price deviate from the correct value it should represent (over-collateralization ratio), where the token price (`kerosine`) will increase thinking that there are a lot of collaterals for the stablecoin (`DYAD`), but in reality, these funds are locked in vaults and do not represent `DYAD` collaterals.

### Recommendations
It can be left as it is, as there are no impacts that can occur for that in my opinion. However, if the developers are interested in mitigation, they can track the balance internally.

---

## [L-05] The user can liquidate himself

In `VaultManagerV2::liquidate`, the function is not checking if the one he is firing `liquidate` is the owner of the dNFT ID to be liquidated or not.

[VaultManagerV2.sol#L205-L228](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205-L228)
```solidity
  function liquidate( ... ) external isValidDNft(id) isValidDNft(to) {
      ...
  }
```

This can make users liquidate themselves and prevent others from getting the reward for liquidating

### Recommendations
Prevent liquidation if the caller is the owner of the `dNFT` id position to get liquidated.

---

## [L-06] The user can mint 0 `DYAD`

There is no restrictions for a user to mint 0 amount `DYAD` when firing `VaultManagerV2::mintDyad()`.

[VaultManagerV2.sol#L156-L169](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156-L169)
```solidity
  function mintDyad( ... ) external isDNftOwner(id) {
    uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;
    if (getNonKeroseneValue(id) < newDyadMinted)     revert NotEnoughExoCollat();
    dyad.mint(id, to, amount);
    if (collatRatio(id) < MIN_COLLATERIZATION_RATIO) revert CrTooLow(); 
    emit MintDyad(id, amount, to);
  }
```

This may introduce some misbehaviours when using the protocol.

### Recommendations
Check that the `amount` provided is greater than `0`, and providing a minimum value to deposit will be better.

---

## [L-07] No way to change `MAINNET_OWNER` in `KerosineDenominator`

The denomenator is determined to be the TVL of Kerosen subtracting the Supply of the owner.

[staking/KerosineDenominator.sol#L21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L21)
```solidity
  function denominator() external view returns (uint) {
    // @dev: We subtract all the Kerosene in the multi-sig.
    //       We are aware that this is not a great solution. That is
    //       why we can switch out Denominator contracts.

    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```

There is no way to change the `MAINNET_OWNER` in `KerosineDenominator` contract. So if the team wants to mitigate the funds from the `MAINNET_OWNER` to another address, in case of normal changing or they think `MAINNET_OWNER (multisig)` addresses get compromised and they want to be sure everything is safe. They will be forced to change redeploy the contract and change VaultManager configurations, which is a lot of efforts.

### Recommendations

Make a function to change the `MAINNET_OWNER` by a trusted address.

---

## [L-08] boundedKerosineVault is not added as a license vault

In `Deploy.V2.s.sol`, there is a comment on the line that adds `boundedKerosineVault` in Licences vaults.

[Deploy.V2.s.sol#L96](https://github.com/code-423n4/2024-04-dyad/blob/main/script/deploy/Deploy.V2.s.sol#L96)
```solidity
  function run() public returns (Contracts memory) {
    ...

    vaultLicenser.add(address(ethVault));
    vaultLicenser.add(address(wstEth));
    vaultLicenser.add(address(unboundedKerosineVault));
    // @audit why commenting this
    // vaultLicenser.add(address(boundedKerosineVault));

    ...
  }

```

## Recommendations
Remove that comment and add the vault as a Licensed one. or delete the line totally if you do not intend to add it to the licensed vault.

---
---
---

## [NC-01] Unused Modifier

In `VaultManagerV2`, there is a modifier that checks if the vault is licenced or not.

[VaultManagerV2.sol#L45-L47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45-L47)
```solidity
  modifier isLicensed(address vault) {
    if (!vaultLicenser.isLicensed(vault)) revert NotLicensed(); _;
  }
```

This modifier was used in the prev Vault Manager. But as kerosine vaults introduced in `V2`, the team ignored using that modifier. And it is not used in the codebase.

### Recommendations
Remove it from the Codebase, and this will save some GAS too when deploying.

---

## [NC-02] No interface for `VaultManagerV2`

There is no interface for `VaultManagerV2`. and there are some new functions related to kerosene is added in the V2 which was not introduced in the previous `VaultManager`.

### Recommendation
Provide a separate interface for the `VaultManagerV2`.

---

## [NC-03] Code Structure Lacks Comments and formatting, and test suit is not the best

- The codebase has less number readable comments.
- Uses the same interface for more than one Contract which is not good.
- Code Format is not the best, behaves like C codebases, which is not the standard format in solidity.
- Testing Base is not the best, it checks only Simple and superficial things, without digging deep
- No fuzz Testing

### Recommendations
Improve the codebase and make it easy for new developers to understand it.

---
---
---

## Centralization risk and admin privileged functions
- Protocol Devs can change `Kerosine` price by calling [`setDenominator`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48
).
```solidity
  function setDenominator(KerosineDenominator _kerosineDenominator) 
    external 
      onlyOwner
  {
    kerosineDenominator = _kerosineDenominator;
  }
```
- [Unlicencing Vaults](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Licenser.sol#L12-L13) has a lot of impacts like position undercollateralization, and if there are no vaults DYAD can not be changed back into collaterals.
```solidity
  function add   (address vault) external onlyOwner { isLicensed[vault] = true; }
  function remove(address vault) external onlyOwner { isLicensed[vault] = false; }

```
- [`setUnboundedKerosineVault`](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30C4) can allow developers to manipulate kerosine price in `BoundedkerosineVaults`.
```solidity
  function setUnboundedKerosineVault(
    UnboundedKerosineVault _unboundedKerosineVault
  )
    external
    onlyOwner
  {
    unboundedKerosineVault = _unboundedKerosineVault;
  }
```