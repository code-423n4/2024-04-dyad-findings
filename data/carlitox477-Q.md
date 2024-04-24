# Low
## `DNft.mintNFT(address)`, `DNft.mintInsiderNft(address)`, `Dyad.mint(uint,address,uint)`, `UnboundedKerosineVault.withdraw(uint,address,uint)`, `Vault.withdraw(uint,address,uint)`,`VaultWstEth.withdraw(uint,address,uint)`, `VaultManager.withdraw(uint,address,uint,address)`,`VaultManager.mintDyad(uint,uint,address)`, `VaultManager.redeemDyad(uint,address,uint,address)`,`VaultManagerV2.withdraw(uint,address,uint,address)`,`VaultManagerV2.mintDyad(uint,uint,address)`, `VaultManagerV2.redeemDyad(uint,address,uint,address)`    lack of input validation
Check `to != address(0)` should be added

## `BoundedKerosineVault.setUnboundedKerosineVault` should check that new address correspond to a vault for the same asset
In order to assure querying the correct price in `assetPrice`, this function shoud check that `address(this.asset) == address(IVault(_unboundedKerosineVault).asset())`

## `VaultManager.deposit`, `VaultManager.withdraw`,`VaultManager2.deposit`, `VaultManager2.withdraw` lack of `vault` validation
This parameter in never validated to be contained in `vaults`. This can be used to perform phising attack by designed a front-end which calls kerosine Vault manager, but instead of depositing asset in a kerosine vault contract asset would be deposited in attacker contract.

# Info
## `Licenser`: lack of event emission when a vault is licensed/unlicensed
Methods `Licenser.add(address)` and `Licenser.remove(address)` are in charge on modifying a state mapping, however when doing this no event is emitted. In general, is a good practise to emit events when actions related to state changes.

## `KerosineManager`: lack of event emission when a vault is added/removed
Methods `KerosineManager.add(address)` and `KerosineManager.remove(address)` are in charge on modifying a state mapping, however when doing this no event is emitted. In general, is a good practise to emit events when actions related to state changes.

## `Dyad.mint` Add comment specifing `id` MUST be validated by caller
Currently there is no comment in `IDyad` specifying this critical invariant,

## `KerosineVault.getUsdValue(uint)` assumes that `assetPrice()` will always return a price with 18 decimals
While we know that kerosine has 18 decimals, given that `assetPrice` is pending to implement nothing assure at first sight that this function will return a price with 8 decimals. A comment should be added to `assetPrice()` that enforce devs to return a price with jsut 8 decimals.

## `KerosineDenominator.denominator`can be easily manipulated by sending Kerosine to multisig address
This can shrink denominator

# Lack of sequencer check for L2 when querying price from chainlink price feeds
Talking with the sponsor they stated that they expect to deploy the protocol in L2 in the future. To do this in appropiate way, apart from querying prices from chainlink oracle, they should also check for sequencer stalness.