# Summary

## Low Risk Issues

| Number | Issues | Instances |
|:------:|:--------------|:-------:|
| [L-01](#l-01-minting-to-the-zero-address-should-be-avoided)  | Minting to the zero address should be avoided | 1 |

Total: 1 over 1 issues

## Non-Critical Issues

| Number | Issues | Instances |
|:------:|:--------------|:-------:|
| [N-01](#n-01-it-is-standard-for-all-external-and-public-functions-to-be-overridden-from-an-interface)  | It is standard for all external and public functions to be overridden from an interface | 26 |
| [N-02](#n-02-using-named-parameters-in-mapping-is-best-practice)  | Using named parameters in mapping is best practice | 4 |
| [N-03](#n-03-custom-error-has-no-error-information)  | Custom error has no error information | 3 |
| [N-04](#n-04-state-variable-declaration-should-include-comments)  | State variable declaration should include comments | 16 |
| [N-05](#n-05-change-uint-to-uint256)  | Change `uint` to `uint256` | 81 |
| [N-06](#n-06-natspec-documentation-for-function-is-missing)  | NatSpec documentation for function is missing | 24 |
| [N-07](#n-07-incorrect-formatting-of-braces-in-contracts-libraries-functions-or-structs)  | Incorrect formatting of braces in contracts, libraries, functions or structs | 31 |
| [N-08](#n-08-zero-address-check-is-missing-in-nonsetter-functions)  | Zero address check is missing in non-setter functions | 4 |
| [N-09](#n-09-constructor-missing-variable-check)  | Constructor missing variable check | 5 |
| [N-10](#n-10-setters-should-have-initial-value-check)  | Setters should have initial value check | 3 |
| [N-11](#n-11-setters-should-prevent-resetting-of-the-same-value)  | Setters should prevent re-setting of the same value | 3 |
| [N-12](#n-12-functions-that-alter-state-should-emit-events)  | Functions that alter state should emit events | 3 |
| [N-13](#n-13-change-public-to-external-for-functions-that-are-not-called-internally)  | Change `public` to `external` for functions that are not called internally | 4 |
| [N-14](#n-14-constants-should-be-defined-rather-than-using-magic-numbers)  | `constants` should be defined rather than using magic numbers | 9 |
| [N-15](#n-15-use-uppercase-for-immutables)  | Use uppercase for immutables | 7 |
| [N-16](#n-16-lack-of-space-near-the-operator)  | Lack of space near the operator | 5 |
| [N-17](#n-17-mapping-definitions-do-not-follow-the-solidity-style-guide)  | `mapping` definitions do not follow the Solidity Style Guide | 3 |
| [N-18](#n-18-constants-in-comparisons-should-appear-on-the-left-side)  | Constants in comparisons should appear on the left side | 2 |
| [N-19](#n-19-unused-modifier)  | Unused modifier | 1 |
| [N-20](#n-20-local-variables-should-be-named-using-mixedcase)  | Local variables should be named using mixedCase | 4 |
| [N-21](#n-21-incorrect-natspec-comment-style)  | Incorrect NatSpec comment style | 1 |
| [N-22](#n-22-contract-declarations-should-have-natspec-title-annotations)  | Contract declarations should have NatSpec @title annotations | 6 |
| [N-23](#n-23-contract-declarations-should-have-natspec-author-annotations)  | Contract declarations should have NatSpec @author annotations | 6 |
| [N-24](#n-24-contract-declarations-should-have-natspec-descriptions)  | Contract declarations should have NatSpec descriptions | 6 |
| [N-25](#n-25-error-declarations-should-have-natspec-descriptions)  | Error declarations should have NatSpec descriptions | 4 |
| [N-26](#n-26-modifier-declarations-should-have-natspec-descriptions)  | Modifier declarations should have NatSpec descriptions | 4 |
| [N-27](#n-27-function-declarations-should-have-natspec-param-annotations)  | Function declarations should have NatSpec @param annotations | 22 |
| [N-28](#n-28-contracts-should-have-full-test-coverage)  | Contracts should have full test coverage | 1 |
| [N-29](#n-29-consider-using-smtchecker)  | Consider using SMTChecker | 1 |
| [N-30](#n-30-function-ordering-does-not-follow-the-solidity-style-guide)  | Function ordering does not follow the Solidity style guide | 2 |
| [N-31](#n-31-contract-does-not-follow-the-solidity-style-guides-suggested-layout-ordering)  | Contract does not follow the Solidity style guide's suggested layout ordering | 2 |
| [N-32](#n-32-private-and-internal-variables-should-start-with-an-underscore)  | Private and internal variables should start with an underscore | 3 |
| [N-33](#n-33-contract-name-should-match-filename)  | Contract name should match filename | 3 |
| [N-34](#n-34) | Unnecessary additional bounding  | 1 |
| [N-35](#n-35) | The `initializer` modifier is redundant | 1 |

Total: 299 over 33 issues

# Findings

## [L-01] Minting to the zero address should be avoided

Minting tokens to the zero address in Solidity is a potential pitfall that should be avoided. The zero address is typically used as a default or uninitialized address. When tokens are minted to this address, they are effectively burned and permanently removed from the total supply, leading to unintended token loss. To prevent this, include a check in the minting function to ensure that the target address is not the zero address.

<details>
<summary><i>There is 1 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

166:     dyad.mint(id, to, amount);

```

[166](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L166). 

</details>


## [N-01] It is standard for all external and public functions to be overridden from an interface

Check that all public or external functions are override. This is iseful to make sure that the whole API is extracted in an interface.

<details>
<summary><i>There are 26 instance of this issue:</i></summary>

```solidity
File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17). 

```solidity
File: src/core/KerosineManager.sol

18:   function add(

28:   function remove(

37:   function getVaults() 

44:   function isLicensed(

```

[18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(

32:   function withdraw(

```

[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32). 

```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 

67:   function add(

80:   function addKerosene(

94:   function remove(

106:   function removeKerosene(

119:   function deposit(

134:   function withdraw(

156:   function mintDyad(

172:   function burnDyad(

184:   function redeemDyad(

205:   function liquidate(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(

```

[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 

```

[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43). 

</details>

## [N-02] Using named parameters in mapping is best practice

<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;

```

[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19). 

```solidity
File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```

[34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37). 

</details>

## [N-03] Custom error has no error information

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

```

[8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L10). 

</details>

## [N-04] State variable declaration should include comments

State variables should be commented to explain their purpose.

<details>
<summary><i>There are 16 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

9:   error VaultAlreadyAdded();
10:   error VaultNotFound();

11: 
12:   using EnumerableSet for EnumerableSet.AddressSet;

13: 
14:   uint public constant MAX_VAULTS = 10;

15: 
16:   EnumerableSet.AddressSet private vaults;

```

[9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L9-L10), [11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L11-L12), [13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L13-L14), [15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L15-L16). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

14: 
15:   UnboundedKerosineVault public unboundedKerosineVault;

```

[14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L14-L15). 

```solidity
File: src/core/Vault.kerosine.sol

14: 
15:   IVaultManager   public immutable vaultManager;
16:   ERC20           public immutable asset;

18: 
19:   mapping(uint => uint) public id2asset;

72:     virtual
73:     returns (uint);

```

[14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L14-L16), [18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L18-L19), [72](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L72-L73). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

17: 
18:   Dyad                 public immutable dyad;
19:   KerosineDenominator  public kerosineDenominator;

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L17-L19). 

```solidity
File: src/core/VaultManagerV2.sol

19:   using FixedPointMathLib for uint;
20:   using SafeTransferLib   for ERC20;

21: 
22:   uint public constant MAX_VAULTS          = 5;
23:   uint public constant MAX_VAULTS_KEROSENE = 5;

27: 
28:   DNft     public immutable dNft;
29:   Dyad     public immutable dyad;

31: 
32:   KerosineManager public keroseneManager;

33: 
34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 
35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;

36: 
37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```

[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L19-L20), [21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L21-L23), [27](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L27-L29), [31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L31-L32), [33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L33-L35), [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L36-L37). 

```solidity
File: src/staking/KerosineDenominator.sol

8: 
9:   Kerosine public kerosine;

```

[8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L8-L9). 

</details>

## [N-05] Change `uint` to `uint256`

The `uint` type is an alias for `uint256`. It is recommended to use `uint256` instead of `uint` for better readability.

<details>
<summary><i>There are 81 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

14:   uint public constant MAX_VAULTS = 10;

```

[14](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L14). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

33:     uint    id,

35:     uint    amount

48:     returns (uint) {

```

[13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13), [33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L33), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L35), [48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L48). 

```solidity
File: src/core/Vault.kerosine.sol

19:   mapping(uint => uint) public id2asset;

37:     uint id,

38:     uint amount

48:     uint from,

49:     uint to,

50:     uint amount

61:     uint id

65:     returns (uint) {

73:     returns (uint);

```

[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L19), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L37), [38](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L38), [48](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L48), [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L49), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L50), [61](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L61), [65](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L65), [73](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L73). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

31:     uint    id,

33:     uint    amount

54:     returns (uint) {

55:       uint tvl;

57:       uint numberOfVaults = vaults.length;

58:       for (uint i = 0; i < numberOfVaults; i++) {

65:       uint numerator   = tvl - dyad.totalSupply();

66:       uint denominator = kerosineDenominator.denominator();

```

[31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L31), [33](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L33), [54](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L54), [55](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L55), [57](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L57), [58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L58), [65](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L65), [66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L66). 

```solidity
File: src/core/VaultManagerV2.sol

19:   using FixedPointMathLib for uint;

22:   uint public constant MAX_VAULTS          = 5;

23:   uint public constant MAX_VAULTS_KEROSENE = 5;

25:   uint public constant MIN_COLLATERIZATION_RATIO = 1.5e18; // 150%

26:   uint public constant LIQUIDATION_REWARD        = 0.2e18; //  20%

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults;

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

68:       uint    id,

81:       uint    id,

95:       uint    id,

107:       uint    id,

120:     uint    id,

122:     uint    amount

135:     uint    id,

137:     uint    amount,

144:     uint dyadMinted = dyad.mintedDyad(address(this), id);

146:     uint value = amount * _vault.assetPrice()

157:     uint    id,

158:     uint    amount,

164:     uint newDyadMinted = dyad.mintedDyad(address(this), id) + amount;

173:     uint id,

174:     uint amount

185:     uint    id,

187:     uint    amount,

192:     returns (uint) {

195:       uint asset = amount

206:     uint id,

207:     uint to

213:       uint cr = collatRatio(id);

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

221:       uint numberOfVaults = vaults[id].length();

222:       for (uint i = 0; i < numberOfVaults; i++) {

224:           uint  collateral = vault.id2asset(id).mulWadUp(liquidationAssetShare);

231:     uint id

235:     returns (uint) {

236:       uint _dyad = dyad.mintedDyad(address(this), id);

237:       if (_dyad == 0) return type(uint).max;

242:     uint id

246:     returns (uint) {

251:     uint id

255:     returns (uint) {

256:       uint totalUsdValue;

257:       uint numberOfVaults = vaults[id].length();

258:       for (uint i = 0; i < numberOfVaults; i++) {

260:         uint usdValue;

270:     uint id

274:     returns (uint) {

275:       uint totalUsdValue;

276:       uint numberOfVaults = vaultsKerosene[id].length();

277:       for (uint i = 0; i < numberOfVaults; i++) {

279:         uint usdValue;

291:     uint id

300:     uint    id,

```

[19](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L19), [22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L22), [23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23), [25](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L25), [26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L26), [34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37), [39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42), [68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L68), [81](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L81), [95](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L95), [107](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L107), [120](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L120), [122](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L122), [135](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L135), [137](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L137), [144](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L144), [146](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L146), [157](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L158), [164](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L164), [173](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L185), [187](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L187), [192](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L192), [195](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L195), [206](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L207), [213](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L213), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L219), [221](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L221), [222](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L222), [224](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L224), [231](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L231), [235](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L235), [236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236), [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237), [242](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L242), [246](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L246), [251](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L251), [255](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L255), [256](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L256), [257](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L257), [258](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L258), [260](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L260), [270](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L270), [274](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L274), [275](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L275), [276](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L276), [277](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L277), [279](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L279), [291](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L291), [300](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L300). 

```solidity
File: src/staking/KerosineDenominator.sol

17:   function denominator() external view returns (uint) {

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L17). 

</details>

## [N-06] NatSpec documentation for function is missing

It is recommend to document all functions with NatSpec comments. This helps to understand the purpose of the function and its parameters. It also helps to generate documentation for the smart contract.

<details>
<summary><i>There are 24 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

17: 
18:   function add(

27: 
28:   function remove(

36: 
37:   function getVaults()

43: 
44:   function isLicensed(

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L17-L18), [27](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L27-L28), [36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L36-L37), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L43-L44). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

22: 
23:   function setUnboundedKerosineVault(

31: 
32:   function withdraw(

43: 
44:   function assetPrice()

```

[22](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L22-L23), [31](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L31-L32), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L43-L44). 

```solidity
File: src/core/Vault.kerosine.sol

35: 
36:   function deposit(

46: 
47:   function move(

59: 
60:   function getUsdValue(

68: 
69:   function assetPrice()

```

[35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L35-L36), [46](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L46-L47), [59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L59-L60), [68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L68-L69). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

29: 
30:   function withdraw(

42: 
43:   function setDenominator(KerosineDenominator _kerosineDenominator)

49: 
50:   function assetPrice()

```

[29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L29-L30), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L42-L43), [49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L49-L50). 

```solidity
File: src/core/VaultManagerV2.sol

58: 
59:   function setKeroseneManager(KerosineManager _keroseneManager)

79: 
80:   function addKerosene(

105: 
106:   function removeKerosene(

229: 
230:   function collatRatio(

240: 
241:   function getTotalUsdValue(

249: 
250:   function getNonKeroseneValue(

268: 
269:   function getKeroseneValue(

289: 
290:   function getVaults(

298: 
299:   function hasVault(

```

[58](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L58-L59), [79](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L79-L80), [105](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L105-L106), [229](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L229-L230), [240](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L240-L241), [249](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L249-L250), [268](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L268-L269), [289](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L289-L290), [298](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L298-L299). 

```solidity
File: src/staking/KerosineDenominator.sol

16: 
17:   function denominator() external view returns (uint) {

```

[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L16-L17). 

</details>

## [N-07] Incorrect formatting of braces in contracts, libraries, functions or structs

The braces denoting the body of a contract, library, functions and structs [should](https://docs.soliditylang.org/en/latest/style-guide.html#variable-declarations):

- Open on the same line as the declaration.

- Close on their own line at the same indentation level as the beginning of the declaration.

- The opening brace should be preceded by a single space.

<details>
<summary><i>There are 31 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

18:   function add(

28:   function remove(

37:   function getVaults()

44:   function isLicensed(

```

[18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L18), [28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L28), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L37), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L44). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(

32:   function withdraw(

44:   function assetPrice()

```

[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23), [32](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L32), [44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44). 

```solidity
File: src/core/Vault.kerosine.sol

36:   function deposit(

47:   function move(

60:   function getUsdValue(

69:   function assetPrice()

```

[36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36), [47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60), [69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L69). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(

43:   function setDenominator(KerosineDenominator _kerosineDenominator)

50:   function assetPrice()

```

[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30), [43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43), [50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50). 

```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager)

67:   function add(

80:   function addKerosene(

94:   function remove(

106:   function removeKerosene(

119:   function deposit(

134:   function withdraw(

156:   function mintDyad(

172:   function burnDyad(

184:   function redeemDyad(

205:   function liquidate(

230:   function collatRatio(

241:   function getTotalUsdValue(

250:   function getNonKeroseneValue(

269:   function getKeroseneValue(

290:   function getVaults(

299:   function hasVault(

```

[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L67), [80](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L80), [94](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L94), [106](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L106), [119](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L119), [134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156), [172](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L172), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184), [205](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L205), [230](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L230), [241](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L241), [250](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L250), [269](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L269), [290](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L290), [299](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L299). 

</details>

## [N-08] Zero address check is missing in non-setter functions

<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

30:   function withdraw(

```

[30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L30). 

```solidity
File: src/core/VaultManagerV2.sol

134:   function withdraw(

156:   function mintDyad(

184:   function redeemDyad(

```

[134](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L134), [156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156), [184](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L184). 

</details>

## [N-09] Constructor missing variable check

Variable checks in the `constructor` are important to ensure that the contract is initialized correctly.

<details>
<summary><i>There are 5 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

17:   constructor(
18:     IVaultManager   _vaultManager,
19:     ERC20           _asset, 
20:     KerosineManager _kerosineManager
21:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {}

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L17-L21). 

```solidity
File: src/core/Vault.kerosine.sol

26:   constructor(
27:     IVaultManager   _vaultManager,
28:     ERC20           _asset, 
29:     KerosineManager _kerosineManager 
30:   ) {
31:     vaultManager    = _vaultManager;
32:     asset           = _asset;
33:     kerosineManager = _kerosineManager;
34:   }

```

[26](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L26-L34). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

21:   constructor(
22:       IVaultManager   _vaultManager,
23:       ERC20           _asset, 
24:       Dyad            _dyad, 
25:       KerosineManager _kerosineManager
26:   ) KerosineVault(_vaultManager, _asset, _kerosineManager) {
27:       dyad = _dyad;
28:   }

```

[21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L21-L28). 

```solidity
File: src/core/VaultManagerV2.sol

49:   constructor(
50:     DNft          _dNft,
51:     Dyad          _dyad,
52:     Licenser      _licenser
53:   ) {
54:     dNft          = _dNft;
55:     dyad          = _dyad;
56:     vaultLicenser = _licenser;
57:   }

```

[49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L49-L57). 

```solidity
File: src/staking/KerosineDenominator.sol

11:   constructor(
12:     Kerosine _kerosine
13:   ) {
14:     kerosine = _kerosine;
15:   }

```

[11](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L11-L15). 

</details>

## [N-10] Setters should have initial value check

Setters should have initial value check to prevent assigning wrong value to the variable. Assignment of wrong value can lead to unexpected behavior of the contract.

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

22:   /// @audit Not validated: _unboundedKerosineVault

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }

```

[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

42:   /// @audit Not validated: _kerosineDenominator

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }

```

[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48). 

```solidity
File: src/core/VaultManagerV2.sol

58:   /// @audit Not validated: _keroseneManager

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }

```

[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L64). 

</details>

## [N-11] Setters should prevent re-setting of the same value

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(
24:     UnboundedKerosineVault _unboundedKerosineVault
25:   )
26:     external
27:     onlyOwner
28:   {
29:     unboundedKerosineVault = _unboundedKerosineVault;
30:   }

```

[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23-L30). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator) 
44:     external 
45:       onlyOwner
46:   {
47:     kerosineDenominator = _kerosineDenominator;
48:   }

```

[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43-L48). 

```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager) 
60:     external
61:       initializer 
62:     {
63:       keroseneManager = _keroseneManager;
64:   }

```

[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59-L64). 

</details>

## [N-12] Functions that alter state should emit events

Functions that alter state should emit events to notify users of the state change. This is especially important for functions that alter state and do not return a value.

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

23:   function setUnboundedKerosineVault(

```

[23](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L23). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

43:   function setDenominator(KerosineDenominator _kerosineDenominator)

```

[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L43). 

```solidity
File: src/core/VaultManagerV2.sol

59:   function setKeroseneManager(KerosineManager _keroseneManager)

```

[59](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L59). 

</details>

## [N-13] Change `public` to `external` for functions that are not called internally

Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from `external` to `public`.

<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

44:   function assetPrice()

```

[44](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L44). 

```solidity
File: src/core/Vault.kerosine.sol

36:   function deposit(

60:   function getUsdValue(

```

[36](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L36), [60](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L60). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

50:   function assetPrice()

```

[50](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L50). 

</details>

## [N-14] `constants` should be defined rather than using magic numbers

Magic numbers are numbers that appear without explanation in the code. They should be replaced with named constants.

<details>
<summary><i>There are 9 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

49:       return unboundedKerosineVault.assetPrice() * 2;

```

[49](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L49). 

```solidity
File: src/core/Vault.kerosine.sol

66:       return id2asset[id] * assetPrice() / 1e8;

```

[66](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L66). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

61:                 * vault.assetPrice() * 1e18

67:       return numerator * 1e8 / denominator;

```

[61](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L61), [67](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L67). 

```solidity
File: src/core/VaultManagerV2.sol

147:                   * 1e18

198:                     / 1e18;

217:       uint cappedCr               = cr < 1e18 ? 1e18 : cr;

218:       uint liquidationEquityShare = (cappedCr - 1e18).mulWadDown(LIQUIDATION_REWARD);

219:       uint liquidationAssetShare  = (liquidationEquityShare + 1e18).divWadDown(cappedCr);

```

[147](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L147), [198](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L198), [217](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L217), [218](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L218), [219](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L219). 

</details>

## [N-15] Use uppercase for immutables

Immutables should be in uppercase as stated [Solidity style guide](https://docs.soliditylang.org/en/latest/style-guide.html#constants).

<details>
<summary><i>There are 7 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

15:   IVaultManager   public immutable vaultManager;

16:   ERC20           public immutable asset;

17:   KerosineManager public immutable kerosineManager;

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L15), [16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L16), [17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L17). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

18:   Dyad                 public immutable dyad;

```

[18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L18). 

```solidity
File: src/core/VaultManagerV2.sol

28:   DNft     public immutable dNft;

29:   Dyad     public immutable dyad;

30:   Licenser public immutable vaultLicenser;

```

[28](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L28), [29](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L29), [30](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L30). 

</details>

## [N-16] Lack of space near the operator

Operators [should](https://docs.soliditylang.org/en/latest/style-guide.html#other-recommendations) be surrounded by a single space on either side.

<details>
<summary><i>There are 5 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.unbounded.sol

62:                 / (10**vault.asset().decimals())

63:                 / (10**vault.oracle().decimals());

```

[62](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L62), [63](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L63). 

```solidity
File: src/core/VaultManagerV2.sol

148:                   / 10**_vault.oracle().decimals()

149:                   / 10**_vault.asset().decimals();

196:                     * (10**(_vault.oracle().decimals() + _vault.asset().decimals()))

```

[148](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L148), [149](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L149), [196](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L196). 

</details>

## [N-17] `mapping` definitions do not follow the Solidity Style Guide

In variable declarations, do not separate the `keyword` mapping from its type by a space. Do not separate any nested `mapping` keyword from its type by whitespace.

https://docs.soliditylang.org/en/latest/style-guide.html#mappings

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults;

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene;

37:   mapping (uint => uint) public idToBlockOfLastDeposit;

```

[34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35), [37](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L37). 

</details>

## [N-18] Constants in comparisons should appear on the left side

Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html)

<details>
<summary><i>There are 2 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

43:     if (dNft.ownerOf(id) == address(0))   revert InvalidDNft(); _;

237:       if (_dyad == 0) return type(uint).max;

```

[43](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L43), [237](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L237). 

</details>

## [N-19] Unused modifier

Consider removing unused modifier or moving it to a higher level contract.

<details>
<summary><i>There is 1 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

45:   modifier isLicensed(address vault) {

```

[45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45). 

</details>

## [N-20] Local variables should be named using mixedCase

<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

128:     Vault _vault = Vault(vault);

145:     Vault _vault = Vault(vault);

194:       Vault _vault = Vault(vault);

236:       uint _dyad = dyad.mintedDyad(address(this), id);

```

[128](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L128), [145](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L145), [194](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L194), [236](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L236). 

</details>

## [N-21] Incorrect NatSpec comment style

NatSpec must begin with `///`, or use `/* ... */` syntax

<details>
<summary><i>There is 1 instance of this issue:</i></summary>

```solidity
File: src/staking/KerosineDenominator.sol

18:     // @dev: We subtract all the Kerosene in the multi-sig.

```

[18](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L18). 

</details>

## [N-22] Contract declarations should have NatSpec @title annotations

<details>
<summary><i>There are 6 instance of this issue:</i></summary>

```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7). 

```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7). 

```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12). 

```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15). 

</details>

## [N-23] Contract declarations should have NatSpec @author annotations

<details>
<summary><i>There are 6 instance of this issue:</i></summary>

```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7). 

```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7). 

```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12). 

```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15). 

</details>

## [N-24] Contract declarations should have NatSpec descriptions

<details>
<summary><i>There are 6 instance of this issue:</i></summary>

```solidity
File: src/staking/KerosineDenominator.sol

7: contract KerosineDenominator is Parameters {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/staking/KerosineDenominator.sol#L7). 

```solidity
File: src/core/KerosineManager.sol

7: contract KerosineManager is Owned(msg.sender) {

```

[7](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L7). 

```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12). 

```solidity
File: src/core/VaultManagerV2.sol

17: contract VaultManagerV2 is IVaultManager, Initializable {

```

[17](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L17). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15). 

</details>

## [N-25] Error declarations should have NatSpec descriptions

<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

8:   error TooManyVaults();

9:   error VaultAlreadyAdded();

10:   error VaultNotFound();

```

[8](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L8), [9](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L9), [10](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L10). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

13:   error NotWithdrawable(uint id, address to, uint amount);

```

[13](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L13). 

</details>

## [N-26] Modifier declarations should have NatSpec descriptions
<details>
<summary><i>There are 4 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

21:   modifier onlyVaultManager() {

```

[21](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L21). 

```solidity
File: src/core/VaultManagerV2.sol

39:   modifier isDNftOwner(uint id) {

42:   modifier isValidDNft(uint id) {

45:   modifier isLicensed(address vault) {

```

[39](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L39), [42](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L42), [45](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L45). 

</details>

## [N-27] Function declarations should have NatSpec @param annotations

<details>
<summary><i>There are 22 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

68:       uint    id,

69:       address vault

95:       uint    id,

96:       address vault

120:     uint    id,

121:     address vault,

122:     uint    amount

135:     uint    id,

136:     address vault,

137:     uint    amount,

138:     address to

157:     uint    id,

158:     uint    amount,

159:     address to

173:     uint id,

174:     uint amount

185:     uint    id,

186:     address vault,

187:     uint    amount,

188:     address to

206:     uint id,

207:     uint to

```

[68](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L68), [69](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L69), [95](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L95), [96](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L96), [120](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L120), [121](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L121), [122](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L122), [135](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L135), [136](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L136), [137](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L137), [138](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L138), [157](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L157), [158](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L158), [159](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L159), [173](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L173), [174](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L174), [185](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L185), [186](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L186), [187](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L187), [188](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L188), [206](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L206), [207](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L207). 

</details>

## [N-28] Contracts should have full test coverage

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

<details>
<summary><i>There is 1 instance of this issue:</i></summary>

```solidity
File: All files

```



</details>

## [N-29] Consider using SMTChecker

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

<details>
<summary><i>There is 1 instance of this issue:</i></summary>

```solidity
File: All files

```



</details>

## [N-30] Function ordering does not follow the Solidity style guide

Source: https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-layout

<details>
<summary><i>There are 2 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.sol

46:   /// @audit External function can not go after public function 
47:   function move(

```

[47](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L47). 

```solidity
File: src/core/VaultManagerV2.sol

155:   /// @audit External function can not go after public function 
156:   function mintDyad(

```

[156](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L156). 

</details>

## [N-31] Contract does not follow the Solidity style guide's suggested layout ordering

Inside each contract, library or interface, use the following order:

1. Type declarations
2. State variables
3. Events
4. Errors
5. Modifiers
6. Functions

Source: https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-layout

<details>
<summary><i>There are 2 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

11:   /// @audit Using for declaration can not go after custom error definition 
12:   using EnumerableSet for EnumerableSet.AddressSet;

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L12). 

```solidity
File: src/core/Vault.kerosine.bounded.sol

14:   /// @audit State variable declaration can not go after custom error definition 
15:   UnboundedKerosineVault public unboundedKerosineVault;

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L15). 

</details>

## [N-32] Private and internal variables should start with an underscore

Source: https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables.

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/KerosineManager.sol

16:   EnumerableSet.AddressSet private vaults;

```

[16](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/KerosineManager.sol#L16). 

```solidity
File: src/core/VaultManagerV2.sol

34:   mapping (uint => EnumerableSet.AddressSet) internal vaults; 

35:   mapping (uint => EnumerableSet.AddressSet) internal vaultsKerosene; 

```

[34](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L34), [35](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L35). 

</details>

## [N-33] Contract name should match filename

The name of the contract [should](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names) match the filename.

<details>
<summary><i>There are 3 instance of this issue:</i></summary>

```solidity
File: src/core/Vault.kerosine.bounded.sol

12: contract BoundedKerosineVault is KerosineVault {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.bounded.sol#L12). 

```solidity
File: src/core/Vault.kerosine.sol

12: abstract contract KerosineVault is IVault, Owned(msg.sender) {

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.sol#L12). 

```solidity
File: src/core/Vault.kerosine.unbounded.sol

15: contract UnboundedKerosineVault is KerosineVault {

```

[15](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/Vault.kerosine.unbounded.sol#L15). 

</details>

## [N-34] Unnecessary additional bounding 

The number of vaults is already limited in KerosineManager. The additional bounding in VaultManagerV2 is unnecessary. 

<details>
<summary><i>There 1 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

12: uint256 public constant MAX_VAULTS_KEROSENE = 5;

```

[12](https://github.com/code-423n4/2024-04-dyad/blob/main/src/core/VaultManagerV2.sol#L23). 

</details>

## [N-35] The `initializer` modifier is redundant

The `VaultManagerV2` is not an upgradeable contract. Check that the keroseneManager is zero address to ensure the function is called only once.
This will also remove the need for the inheriting `Initializable` contract.

<details>
<summary><i>There 1 instance of this issue:</i></summary>

```solidity
File: src/core/VaultManagerV2.sol

    function setKeroseneManager(KerosineManager _keroseneManager) external initializer {
        keroseneManager = _keroseneManager;
    }
```

</details>