# [L-01] No vault checks
   
## Detail
A depositor deposits tokens to the vault by calling the [VaultManagerV2.deposit()](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L128) function. 
```solidity
File: core\VaultManagerV2.sol
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   {
127:     idToBlockOfLastDeposit[id] = block.number;
128:     Vault _vault = Vault(vault);  // @audit-info vault can be any address.
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
130:     _vault.deposit(id, amount);
131:   }
```
Here, there is no check if `vault` is licensed or not. The depositor can create a fake `vault` contract and set the second parameter of the function `address vault` as the address of it. It can cause Reentrancy Attack.

It also happens in the [VaultManagerV2.withdraw()](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L145) function and the [VaultManagerV2.redeemDyad()](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/VaultManagerV2.sol#L145) function.
```
File: core\VaultManagerV2.sol
134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {
143:     if (idToBlockOfLastDeposit[id] == block.number) revert DepositedInSameBlock();
144:     uint dyadMinted = dyad.mintedDyad(address(this), id);
145:     Vault _vault = Vault(vault); // @audit-info vault can be any address.
146:     uint value = amount * _vault.assetPrice() 
147:                   * 1e18 
148:                   / 10**_vault.oracle().decimals() 
149:                   / 10**_vault.asset().decimals();
150:     if (getNonKeroseneValue(id) - value < dyadMinted) revert NotEnoughExoCollat();
151:     _vault.withdraw(id, to, amount);
152:     if (collatRatio(id) < MIN_COLLATERIZATION_RATIO)  revert CrTooLow(); 
153:   }


184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
193:       dyad.burn(id, msg.sender, amount);
194:       Vault _vault = Vault(vault); // @audit-info vault can be any address.
195:       uint asset = amount 
196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals())) 
197:                     / _vault.assetPrice() 
198:                     / 1e18;
199:       withdraw(id, vault, asset, to);
200:       emit RedeemDyad(id, vault, amount, to);
201:       return asset;
202:   }

```

## Recommendation
The address of `vault` must satisfies the condition.

```diff
File: core\VaultManagerV2.sol
119:   function deposit(
120:     uint    id,
121:     address vault,
122:     uint    amount
123:   ) 
124:     external 
125:       isValidDNft(id)
126:   {
+        require(vaults[id].contains(vault) || vaultsKerosene[id].contains(vault), "The address of vault is not correct");             
127:     idToBlockOfLastDeposit[id] = block.number;
128:     Vault _vault = Vault(vault);  
         requirevaults[id].contains(vault): 
129:     _vault.asset().safeTransferFrom(msg.sender, address(vault), amount);
130:     _vault.deposit(id, amount);
131:   }


134:   function withdraw(
135:     uint    id,
136:     address vault,
137:     uint    amount,
138:     address to
139:   ) 
140:     public
141:       isDNftOwner(id)
142:   {
+        require(vaults[id].contains(vault) || vaultsKerosene[id].contains(vault), "The address of vault is not correct");  
         [...]
153:   }


184:   function redeemDyad(
185:     uint    id,
186:     address vault,
187:     uint    amount,
188:     address to
189:   )
190:     external 
191:       isDNftOwner(id)
192:     returns (uint) { 
+        require(vaults[id].contains(vault) || vaultsKerosene[id].contains(vault), "The address of vault is not correct");  
         [...]
202:   }
```



# [L-02] Use `transfer` instead of  `safeTransferETH`

## Detail
In the function [DNft.mintNft()](https://github.com/code-423n4/2024-04-dyad/blob/cd48c684a58158de444b24854ffd8f07d046c31b/src/core/DNft.sol#L29), the `safeTransferETH` function of Solmate's SafeTransferLib may cause vulneralbility like Reentrancy Attack. Use the `transfer()` function instead of `safeTransferETH()` at L29.

```solidity
File: core\DNft.sol
22:   function mintNft(address to)
23:     external 
24:     payable
25:     returns (uint) {
26:       uint price = START_PRICE + (PRICE_INCREASE * publicMints++);
27:       if (msg.value < price) revert InsufficientFunds();
28:       uint id = _mintNft(to);
29:       if (msg.value > price) to.safeTransferETH(msg.value - price); 
30:       emit MintedNft(id, to);
31:       return id;
32:   }
```

## Recommendation
The address of `vault` must satisfy the condition.

```diff
File: core\DNft.sol
22:   function mintNft(address to)
23:     external 
24:     payable
25:     returns (uint) {
26:       uint price = START_PRICE + (PRICE_INCREASE * publicMints++);
27:       if (msg.value < price) revert InsufficientFunds();
28:       uint id = _mintNft(to);
-         if (msg.value > price) to.safeTransferETH(msg.value - price); 
+         if (msg.value > price) msg.sender.transfer(msg.value - price); 
30:       emit MintedNft(id, to);
31:       return id;
32:   }
```


# [L-03] Use OpenZeppelin's `SafeERC20` instead of Solmate `ERC20.safeTransferLib`

## Detail
In the `VaultManagerV2.sol`, `Vault.sol`, `Vault.wsteth.sol`, `Vault.kerosine.bounded.sol`, `Vault.kerosine.unbounded.sol`, Solmate `ERC20.safeTransferLib` was used.
Solmate `ERC20.safeTransferLib` do not check the contract existence and this opens up a possibility for a honeypot attack.

## Recommendation
Use OpenZeppelin's SafeERC20.