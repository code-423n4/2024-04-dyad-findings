### Low -01 Donation attacks can manipulate kerosine price.
**Instances(1)**
The current implementation of kerosine price is dependent on a [denominator](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L66) value which is [kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER)](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L21), this is the kerosine that is actually circulating (e.g. earned from staking rewards).

Based on [Vault.kerosine.unbounded::assetPrice](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.unbounded.sol#L65-L67),
kerosine price = (tvl- dyad.totalSupply()) / (kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER))

However, using `kerosine.balanceOf(MAINNET_OWNER)` to compute the denominator is vulnerable, because `balanceOf` can be manipulated by any user donating kerosine to MAINNET_OWNER.
```solidity
//src/staking/KerosineDenominator.sol
  function denominator() external view returns (uint) {
|>    return kerosine.totalSupply() - kerosine.balanceOf(MAINNET_OWNER);
  } 
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/staking/KerosineDenominator.sol#L21)

Such donation attack might be profitable in some circumstances such as arbitrage. Based on [doc](https://dyadstable.notion.site/DYAD-design-outline-v6-3fa96f99425e458abbe574f67b795145), kerosine can be traded on a secondary market, and arbitrage is allowed. 

>The secondary market may trade Kerosene above its deterministic protocol-defined value. ...

Donating kerosine to MAINNET_OWNER when kerosine price is low, might be relatively low cost which encourages arbitrage through price manipulation.

Recommendations:
Consider using a different state variable in place of `kerosine.balanceOf(MAINNET_OWNER))`. 

### Low -02 Missing deployment step - setUnboundedKerosineVault needs to be called by the owner during migration.
**Instances(1)**
In Deploy.V2.s.sol, all related contract deployment and initialization steps are performed. According to [readme](https://github.com/code-423n4/2024-04-dyad?tab=readme-ov-file#migration), 
>The only transaction that needs to be done by the multi-sig after the deployment is licensing the new Vault Manager.

However, this is not true because [Deploy.V2.s.sol missed setting UnbouldedKerosineVault contract address](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L36) in Vault.kerosine.bounded.sol.
```solidity
//src/core/Vault.kerosine.bounded.sol
    function setUnboundedKerosineVault(
        UnboundedKerosineVault _unboundedKerosineVault
    ) external onlyOwner {
        unboundedKerosineVault = _unboundedKerosineVault;
    }
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/Vault.kerosine.bounded.sol#L29)

As a result, the multi-sig needs to call setUnboundedKerosineVault after the migration to enable bounded kerosine vault.

Recommendations:
In [Deploy.V2.s.sol::run](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L36), add `boundedKerosineVault.setUnboundedKerosineVault(address(unboundedKerosineVault))`

### Low -03 Insufficient checks in VaultManagerV2 might allow users to deposit/withdraw from any unlicensed / potentially malicious vault, user might lose funds.
**Instances(3)**
In VaultManagerV2::deposit / VaultManagerV2::withdraw /VaultManagerV2::redeemDyad , no checks on input `vault` arguments. As a result, any `_vault` can be used. 

In case of unlicensed vault is used for deposit, users deposit will not be accounted as collaterals. 

In case of malicious vault address is used for deposit, the user might lose funds.
(1)
```solidity
//src/core/VaultManagerV2.sol
    function deposit(
        uint id,
        address vault,
        uint amount
    ) external isValidDNft(id) {
    idToBlockOfLastDeposit[id] = block.number;
 |>   Vault _vault = Vault(vault); //@audit no check on vault is added /licensed
    _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
    _vault.deposit(id, amount);
  }
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L128)
(2)
```solidity
//src/core/VaultManagerV2.sol
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
|>  Vault _vault = Vault(vault); //@audit no check on vault is added /licensed
...
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L145)
(3)
```solidity
//src/core/VaultManagerV2.sol
  function redeemDyad(
    uint    id,
    address vault,
    uint    amount,
    address to
  )
    external 
      isDNftOwner(id)
    returns (uint) { 
      dyad.burn(id, msg.sender, amount);
|>    Vault _vault = Vault(vault); //@audit no check on vault is added /licensed
...
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L194)
Recommendations:
In deposit / withdraw / redeemDyad, check input vault is added in NOTE id and is licensed.

### Low -04 Kerosine vault is not licensed in KerosineManager during migration. 
**Instances(1)**
In [Deploy.V2.s.sol::run](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L36), kerosine vault ([unboundedKerosineVault](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L71)) is not added to kerosineManager. Based on VaultManagerV2.sol, any kerosine vault needs to be licensed in `kerosineManager` first to be allowed as kerosine collateral through `addKerosene()`.
```solidity
//src/core/VaultManagerV2.sol
    function addKerosene(uint id, address vault) external isDNftOwner(id) {
        if (vaultsKerosene[id].length() >= MAX_VAULTS_KEROSENE)
            revert TooManyVaults();
        //@audit-info note: any kerosene vault needs to be licensed in keroseneManger first before allowing to be deposited as kerosine collateral in VaultManagerV2
 |>     if (!keroseneManager.isLicensed(vault)) revert VaultNotLicensed();
        if (!vaultsKerosene[id].add(vault)) revert VaultAlreadyAdded();
        emit Added(id, vault);
    }
```
(https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L88)

As a result, protocol multisig has to manually license kerosine vaults after migration

Recommendations:
In [Deploy.V2.s.sol::run](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/script/deploy/Deploy.V2.s.sol#L36), add a line to license `unboundedKerosineVault`.

