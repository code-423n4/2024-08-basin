# Report


## Non Critical Issues


| |Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | Array indices should be referenced via `enum`s rather than via numeric literals | 13 |
| [NC-2](#NC-2) | Constants should be in CONSTANT_CASE | 1 |
| [NC-3](#NC-3) | `constant`s should be defined rather than using magic numbers | 104 |
| [NC-4](#NC-4) | Control structures do not follow the Solidity Style Guide | 14 |
| [NC-5](#NC-5) | Default Visibility for constants | 4 |
| [NC-6](#NC-6) | Consider disabling `renounceOwnership()` | 1 |
| [NC-7](#NC-7) | Function ordering does not follow the Solidity style guide | 2 |
| [NC-8](#NC-8) | Functions should not be longer than 50 lines | 19 |
| [NC-9](#NC-9) | NatSpec is completely non-existent on functions that should have them | 1 |
| [NC-10](#NC-10) | Incomplete NatSpec: `@param` is missing on actually documented functions | 2 |
| [NC-11](#NC-11) | Adding a `return` statement when the function defines a named return variable, is redundant | 9 |
| [NC-12](#NC-12) | Take advantage of Custom Error's return value property | 2 |
| [NC-13](#NC-13) | Contract does not follow the Solidity style guide's suggested layout ordering | 1 |
| [NC-14](#NC-14) | Use Underscores for Number Literals (add an underscore every 3 digits) | 1 |
| [NC-15](#NC-15) | Internal and private variables and functions names should begin with an underscore | 3 |
| [NC-16](#NC-16) | Constants should be defined rather than using magic numbers | 13 |
| [NC-17](#NC-17) | Variables need not be initialized to zero | 1 |
### <a name="NC-1"></a>[NC-1] Array indices should be referenced via `enum`s rather than via numeric literals

*Instances (13)*:
```solidity
File: ./src/functions/Stable2.sol

79:         if (reserves[0] == 0 && reserves[1] == 0) return 0;

86:         uint256 sumReserves = scaledReserves[0] + scaledReserves[1];

91:             dP = dP * lpTokenSupply / (scaledReserves[0] * N);

92:             dP = dP * lpTokenSupply / (scaledReserves[1] * N);

125:         (uint256 c, uint256 b) = getBandC(a * N * N, lpTokenSupply, j == 0 ? scaledReserves[1] : scaledReserves[0]);

354:         decimals[0] = decimal0;

355:         decimals[1] = decimal1;

393:         scaledReserves[0] = reserves[0] * 10 ** (18 - decimals[0]);

393:         scaledReserves[0] = reserves[0] * 10 ** (18 - decimals[0]);

393:         scaledReserves[0] = reserves[0] * 10 ** (18 - decimals[0]);

394:         scaledReserves[1] = reserves[1] * 10 ** (18 - decimals[1]);

394:         scaledReserves[1] = reserves[1] * 10 ** (18 - decimals[1]);

394:         scaledReserves[1] = reserves[1] * 10 ** (18 - decimals[1]);

```

### <a name="NC-2"></a>[NC-2] Constants should be in CONSTANT_CASE
For `constant` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

17:     address private immutable ___self = address(this);

```

### <a name="NC-3"></a>[NC-3] `constant`s should be defined rather than using magic numbers
Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

*Instances (104)*:
```solidity
File: ./src/functions/Stable2.sol

88:         for (uint256 i = 0; i < 255; i++) {

129:         for (uint256 i; i < 255; ++i) {

164:         uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));

194:         uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));

197:         uint256 parityReserve = lpTokenSupply / 2;

218:         for (uint256 k; k < 255; k++) {

222:             scaledReserves[i] = calcReserve(scaledReserves, i, lpTokenSupply, abi.encode(18, 18));

302:         for (uint256 k; k < 255; k++) {

305:             pd.newPrice = calcRate(scaledReserves, i, j, abi.encode(18, 18));

346:             decimal0 = 18;

349:             decimal1 = 18;

351:         if (decimal0 > 18 || decimal1 > 18) revert InvalidTokenDecimals();

381:         rate = _reserves[i] - calcReserve(_reserves, i, lpTokenSupply, abi.encode(18, 18));

393:         scaledReserves[0] = reserves[0] * 10 ** (18 - decimals[0]);

394:         scaledReserves[1] = reserves[1] * 10 ** (18 - decimals[1]);

403:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

```

```solidity
File: ./src/functions/StableLUT/Stable2LUT1.sol

20:         return 100;

38:                                         PriceData(0.27702e6, 0, 9.646293093274934449e18, 0.001083e6, 0, 2000e18, 1e18);

42:                                     0.30624e6, 0, 8.612761690424049377e18, 0.27702e6, 0, 9.646293093274934449e18, 1e18

51:                                         7.689965795021471706e18,

54:                                         8.612761690424049377e18,

61:                                         6.866040888412029197e18,

64:                                         7.689965795021471706e18,

70:                                     0.404944e6, 0, 6.130393650367882863e18, 0.370355e6, 0, 6.866040888412029197e18, 1e18

81:                                         5.473565759257038366e18,

84:                                         6.130393650367882863e18,

91:                                         4.887112285050926097e18,

94:                                         5.473565759257038366e18,

100:                                     0.516039e6, 0, 4.363493111652613443e18, 0.478063e6, 0, 4.887112285050926097e18, 1e18

106:                                     0.554558e6, 0, 3.89597599254697613e18, 0.516039e6, 0, 4.363493111652613443e18, 1e18

110:                                     0.59332e6, 0, 3.478549993345514402e18, 0.554558e6, 0, 3.89597599254697613e18, 1e18

123:                                         3.105848208344209382e18,

126:                                         3.478549993345514402e18,

133:                                         2.773078757450186949e18,

136:                                         3.105848208344209382e18,

142:                                     0.708539e6, 0, 2.475963176294809553e18, 0.670518e6, 0, 2.773078757450186949e18, 1e18

148:                                     0.746003e6, 0, 2.210681407406080101e18, 0.708539e6, 0, 2.475963176294809553e18, 1e18

152:                                     0.782874e6, 0, 1.973822685183999948e18, 0.746003e6, 0, 2.210681407406080101e18, 1e18

569:                 if (price < 2.01775e6) {

646:                                     2.01775e6, 0, 0.215671155821681004e18, 1.855977e6, 0, 0.245080858888273884e18, 1e18

652:                     if (price < 3.322705e6) {

653:                         if (price < 2.680458e6) {

654:                             if (price < 2.425256e6) {

655:                                 if (price < 2.206036e6) {

657:                                         2.206036e6,

660:                                         2.01775e6,

667:                                         2.425256e6,

670:                                         2.206036e6,

678:                                     2.680458e6, 0, 0.146973853900112583e18, 2.425256e6, 0, 0.167015743068309769e18, 1e18

682:                             if (price < 2.977411e6) {

684:                                     2.977411e6, 0, 0.129336991432099091e18, 2.680458e6, 0, 0.146973853900112583e18, 1e18

688:                                     3.322705e6, 0, 0.113816552460247203e18, 2.977411e6, 0, 0.129336991432099091e18, 1e18

693:                         if (price < 4.729321e6) {

694:                             if (price < 4.189464e6) {

695:                                 if (price < 3.723858e6) {

697:                                         3.723858e6,

700:                                         3.322705e6,

707:                                         4.189464e6,

710:                                         3.723858e6,

718:                                     4.729321e6, 0, 0.077562793638189589e18, 4.189464e6, 0, 0.088139538225215433e18, 1e18

722:                             if (price < 10.37089e6) {

724:                                     10.37089e6, 0, 0.035714285714285712e18, 4.729321e6, 0, 0.077562793638189589e18, 1e18

753:                                         2.410556040105746423e18,

756:                                         10.522774272309483479e18,

765:                                         2.337718072004858261e18,

768:                                         2.410556040105746423e18,

775:                                         2.26657220303422724e18,

778:                                         2.337718072004858261e18,

789:                                         2.196897480682568293e18,

792:                                         2.26657220303422724e18,

799:                                         2.128468246736633152e18,

802:                                         2.196897480682568293e18,

811:                                         2.061053544007124483e18,

814:                                         2.128468246736633152e18,

824:                                         2.061053544007124483e18,

2002:                     if (price < 2.209802e6) {

2085:                                         2.209802e6,

2097:                         if (price < 3.931396e6) {

2098:                             if (price < 2.878327e6) {

2099:                                 if (price < 2.505865e6) {

2101:                                         2.505865e6,

2104:                                         2.209802e6,

2111:                                         2.878327e6,

2112:                                         2.078928179411367427e18,

2114:                                         2.505865e6,

2121:                                 if (price < 3.346057e6) {

2123:                                         3.346057e6,

2124:                                         2.182874588381935599e18,

2126:                                         2.878327e6,

2127:                                         2.078928179411367427e18,

2133:                                         3.931396e6,

2134:                                         2.292018317801032268e18,

2136:                                         3.346057e6,

2137:                                         2.182874588381935599e18,

2144:                             if (price < 10.709509e6) {

2145:                                 if (price < 4.660591e6) {

2147:                                         4.660591e6,

2148:                                         2.406619233691083881e18,

2150:                                         3.931396e6,

2151:                                         2.292018317801032268e18,

2157:                                         10.709509e6,

2158:                                         3e18,

2160:                                         4.660591e6,

2161:                                         2.406619233691083881e18,

```

### <a name="NC-4"></a>[NC-4] Control structures do not follow the Solidity Style Guide
See the [control structures](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) section of the Solidity Style Guide

*Instances (14)*:
```solidity
File: ./src/WellUpgradeable.sol

9: import {IAquifer} from "src/interfaces/IAquifer.sol";

24:             address aquifer = aquifer();

25:             address wellImplmentation = IAquifer(aquifer).wellImplementation(address(this));

26:             require(wellImplmentation == ___self, "Function must be called by a Well bored by an aquifer");

68:         address aquifer = aquifer();

69:         address activeProxy = IAquifer(aquifer).wellImplementation(_getImplementation());

70:         require(activeProxy == ___self, "Function must be called through active proxy bored by an aquifer");

74:             IAquifer(aquifer).wellImplementation(newImplementation) != address(0),

```

```solidity
File: ./src/functions/Stable2.sol

5: import {IBeanstalkWellFunction, IMultiFlowPumpWellFunction} from "src/interfaces/IBeanstalkWellFunction.sol";

62:         if (lut == address(0)) revert InvalidLUT();

79:         if (reserves[0] == 0 && reserves[1] == 0) return 0;

98:                 if (lpTokenSupply - prevReserves <= 1) return lpTokenSupply;

100:                 if (prevReserves - lpTokenSupply <= 1) return lpTokenSupply;

351:         if (decimal0 > 18 || decimal1 > 18) revert InvalidTokenDecimals();

```

### <a name="NC-5"></a>[NC-5] Default Visibility for constants
Some constants are using the default visibility. For readability, consider explicitly declaring them as `internal`.

*Instances (4)*:
```solidity
File: ./src/functions/Stable2.sol

35:     uint256 constant N = 2;

38:     uint256 constant A_PRECISION = 100;

41:     uint256 constant PRICE_PRECISION = 1e6;

45:     uint256 constant PRICE_THRESHOLD = 100; // 0.01%

```

### <a name="NC-6"></a>[NC-6] Consider disabling `renounceOwnership()`
If the plan for your project does not include eventually giving up all ownership control, consider overwriting OpenZeppelin's `Ownable`'s `renounceOwnership()` function in order to disable it.

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

```

### <a name="NC-7"></a>[NC-7] Function ordering does not follow the Solidity style guide
According to the [Solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*Instances (2)*:
```solidity
File: ./src/WellUpgradeable.sol

1: 
   Current order:
   external init
   external initNoWellToken
   internal _authorizeUpgrade
   public upgradeTo
   public upgradeToAndCall
   public proxiableUUID
   external getImplementation
   external getVersion
   external getInitializerVersion
   
   Suggested order:
   external init
   external initNoWellToken
   external getImplementation
   external getVersion
   external getInitializerVersion
   public upgradeTo
   public upgradeToAndCall
   public proxiableUUID
   internal _authorizeUpgrade

```

```solidity
File: ./src/functions/Stable2.sol

1: 
   Current order:
   public calcLpTokenSupply
   public calcReserve
   public calcRate
   external calcReserveAtRatioSwap
   external calcReserveAtRatioLiquidity
   public decodeWellData
   external name
   external symbol
   internal _calcRate
   internal getScaledReserves
   private _calcReserve
   private getBandC
   internal updateReserve
   
   Suggested order:
   external calcReserveAtRatioSwap
   external calcReserveAtRatioLiquidity
   external name
   external symbol
   public calcLpTokenSupply
   public calcReserve
   public calcRate
   public decodeWellData
   internal _calcRate
   internal getScaledReserves
   internal updateReserve
   private _calcReserve
   private getBandC

```

### <a name="NC-8"></a>[NC-8] Functions should not be longer than 50 lines
Overly complex code can make understanding functionality more difficult, try to further modularize your code to ensure readability 

*Instances (19)*:
```solidity
File: ./src/WellUpgradeable.sol

26:             require(wellImplmentation == ___self, "Function must be called by a Well bored by an aquifer");

31:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

52:     function initNoWellToken() external initializer {}

63:     function _authorizeUpgrade(address newImplementation) internal view override onlyOwner {

70:         require(activeProxy == ___self, "Function must be called through active proxy bored by an aquifer");

99:     function upgradeTo(address newImplementation) public override {

110:     function upgradeToAndCall(address newImplementation, bytes memory data) public payable override {

124:     function proxiableUUID() public view override notDelegatedOrIsMinimalProxy returns (bytes32) {

128:     function getImplementation() external view returns (address) {

132:     function getVersion() external pure virtual returns (uint256) {

136:     function getInitializerVersion() external view returns (uint256) {

```

```solidity
File: ./src/functions/Stable2.sol

5: import {IBeanstalkWellFunction, IMultiFlowPumpWellFunction} from "src/interfaces/IBeanstalkWellFunction.sol";

341:     function decodeWellData(bytes memory data) public view virtual returns (uint256[] memory decimals) {

358:     function name() external pure returns (string memory) {

362:     function symbol() external pure returns (string memory) {

418:     function updateReserve(PriceData memory pd, uint256 reserve) internal pure returns (uint256) {

```

```solidity
File: ./src/functions/StableLUT/Stable2LUT1.sol

19:     function getAParameter() external pure returns (uint256) {

27:     function getRatiosFromPriceLiquidity(uint256 price) external pure returns (PriceData memory) {

740:     function getRatiosFromPriceSwap(uint256 price) external pure returns (PriceData memory) {

```

### <a name="NC-9"></a>[NC-9] NatSpec is completely non-existent on functions that should have them
Public and external functions that aren't view or pure should have NatSpec comments

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

31:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

```

### <a name="NC-10"></a>[NC-10] Incomplete NatSpec: `@param` is missing on actually documented functions
The following functions are missing `@param` NatSpec comments.

*Instances (2)*:
```solidity
File: ./src/WellUpgradeable.sol

93:     /**
         * @notice Upgrades the implementation of the proxy to `newImplementation`.
         * Calls {_authorizeUpgrade}.
         * @dev `upgradeTo` was modified to support ERC-1167 minimal proxies
         * cloned (Bored) by an Aquifer.
         */
        function upgradeTo(address newImplementation) public override {

104:     /**
          * @notice Upgrades the implementation of the proxy to `newImplementation`.
          * Calls {_authorizeUpgrade}.
          * @dev `upgradeTo` was modified to support ERC-1167 minimal proxies
          * cloned (Bored) by an Aquifer.
          */
         function upgradeToAndCall(address newImplementation, bytes memory data) public payable override {

```

### <a name="NC-11"></a>[NC-11] Adding a `return` statement when the function defines a named return variable, is redundant

*Instances (9)*:
```solidity
File: ./src/functions/Stable2.sol

67:     /**
         * @notice Calculate the amount of lp tokens given reserves.
         * D invariant calculation in non-overflowing integer operations iteratively
         * A * sum(x_i) * n**n + D = A * D * n**n + D**(n+1) / (n**n * prod(x_i))
         *
         * Converging solution:
         * D[j+1] = (4 * A * sum(b_i) - (D[j] ** 3) / (4 * prod(b_i))) / (4 * A - 1)
         */
        function calcLpTokenSupply(
            uint256[] memory reserves,
            bytes memory data
        ) public view returns (uint256 lpTokenSupply) {
            if (reserves[0] == 0 && reserves[1] == 0) return 0;

67:     /**
         * @notice Calculate the amount of lp tokens given reserves.
         * D invariant calculation in non-overflowing integer operations iteratively
         * A * sum(x_i) * n**n + D = A * D * n**n + D**(n+1) / (n**n * prod(x_i))
         *
         * Converging solution:
         * D[j+1] = (4 * A * sum(b_i) - (D[j] ** 3) / (4 * prod(b_i))) / (4 * A - 1)
         */
        function calcLpTokenSupply(
            uint256[] memory reserves,
            bytes memory data
        ) public view returns (uint256 lpTokenSupply) {
            if (reserves[0] == 0 && reserves[1] == 0) return 0;
            uint256[] memory decimals = decodeWellData(data);
            // scale reserves to 18 decimals.
            uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
    
            uint256 Ann = a * N * N;
            
            uint256 sumReserves = scaledReserves[0] + scaledReserves[1];
            lpTokenSupply = sumReserves;
            for (uint256 i = 0; i < 255; i++) {
                uint256 dP = lpTokenSupply;
                // If division by 0, this will be borked: only withdrawal will work. And that is good
                dP = dP * lpTokenSupply / (scaledReserves[0] * N);
                dP = dP * lpTokenSupply / (scaledReserves[1] * N);
                uint256 prevReserves = lpTokenSupply;
                lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply
                    / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));
                // Equality with the precision of 1
                if (lpTokenSupply > prevReserves) {
                    if (lpTokenSupply - prevReserves <= 1) return lpTokenSupply;
                } else {
                    if (prevReserves - lpTokenSupply <= 1) return lpTokenSupply;

67:     /**
         * @notice Calculate the amount of lp tokens given reserves.
         * D invariant calculation in non-overflowing integer operations iteratively
         * A * sum(x_i) * n**n + D = A * D * n**n + D**(n+1) / (n**n * prod(x_i))
         *
         * Converging solution:
         * D[j+1] = (4 * A * sum(b_i) - (D[j] ** 3) / (4 * prod(b_i))) / (4 * A - 1)
         */
        function calcLpTokenSupply(
            uint256[] memory reserves,
            bytes memory data
        ) public view returns (uint256 lpTokenSupply) {
            if (reserves[0] == 0 && reserves[1] == 0) return 0;
            uint256[] memory decimals = decodeWellData(data);
            // scale reserves to 18 decimals.
            uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
    
            uint256 Ann = a * N * N;
            
            uint256 sumReserves = scaledReserves[0] + scaledReserves[1];
            lpTokenSupply = sumReserves;
            for (uint256 i = 0; i < 255; i++) {
                uint256 dP = lpTokenSupply;
                // If division by 0, this will be borked: only withdrawal will work. And that is good
                dP = dP * lpTokenSupply / (scaledReserves[0] * N);
                dP = dP * lpTokenSupply / (scaledReserves[1] * N);
                uint256 prevReserves = lpTokenSupply;
                lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply
                    / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));
                // Equality with the precision of 1
                if (lpTokenSupply > prevReserves) {
                    if (lpTokenSupply - prevReserves <= 1) return lpTokenSupply;

106:     /**
          * @notice Calculate x[i] if one reduces D from being calculated for reserves to D
          * Done by solving quadratic equation iteratively.
          * x_1**2 + x_1 * (sum' - (A*n**n - 1) * D / (A * n**n)) = D ** (n + 1) / (n ** (2 * n) * prod' * A)
          * x_1**2 + b*x_1 = c
          * x_1 = (x_1**2 + c) / (2*x_1 + b)
          * @dev This function has a precision of +/- 1,
          * which may round in favor of the well or the user.
          */
         function calcReserve(
             uint256[] memory reserves,
             uint256 j,
             uint256 lpTokenSupply,
             bytes memory data
         ) public view returns (uint256 reserve) {
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             // avoid stack too deep errors.
             (uint256 c, uint256 b) = getBandC(a * N * N, lpTokenSupply, j == 0 ? scaledReserves[1] : scaledReserves[0]);
             reserve = lpTokenSupply;
             uint256 prevReserve;
     
             for (uint256 i; i < 255; ++i) {
                 prevReserve = reserve;
                 reserve = _calcReserve(reserve, b, c, lpTokenSupply);
                 // Equality with the precision of 1
                 // scale reserve down to original precision
                 if (reserve > prevReserve) {
                     if (reserve - prevReserve <= 1) {
                         return reserve / (10 ** (18 - decimals[j]));
                     }
                 } else {
                     if (prevReserve - reserve <= 1) {
                         return reserve / (10 ** (18 - decimals[j]));

106:     /**
          * @notice Calculate x[i] if one reduces D from being calculated for reserves to D
          * Done by solving quadratic equation iteratively.
          * x_1**2 + x_1 * (sum' - (A*n**n - 1) * D / (A * n**n)) = D ** (n + 1) / (n ** (2 * n) * prod' * A)
          * x_1**2 + b*x_1 = c
          * x_1 = (x_1**2 + c) / (2*x_1 + b)
          * @dev This function has a precision of +/- 1,
          * which may round in favor of the well or the user.
          */
         function calcReserve(
             uint256[] memory reserves,
             uint256 j,
             uint256 lpTokenSupply,
             bytes memory data
         ) public view returns (uint256 reserve) {
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             // avoid stack too deep errors.
             (uint256 c, uint256 b) = getBandC(a * N * N, lpTokenSupply, j == 0 ? scaledReserves[1] : scaledReserves[0]);
             reserve = lpTokenSupply;
             uint256 prevReserve;
     
             for (uint256 i; i < 255; ++i) {
                 prevReserve = reserve;
                 reserve = _calcReserve(reserve, b, c, lpTokenSupply);
                 // Equality with the precision of 1
                 // scale reserve down to original precision
                 if (reserve > prevReserve) {
                     if (reserve - prevReserve <= 1) {
                         return reserve / (10 ** (18 - decimals[j]));

169:     /**
          * @inheritdoc IMultiFlowPumpWellFunction
          * @dev `calcReserveAtRatioSwap` fetches the closes approximate ratios from the target price,
          * and performs newtons method in order to converge into a reserve.
          */
         function calcReserveAtRatioSwap(
             uint256[] memory reserves,
             uint256 j,
             uint256[] memory ratios,
             bytes calldata data
         ) external view returns (uint256 reserve) {
             uint256 i = j == 1 ? 0 : 1;
             // scale reserves and ratios:
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             PriceData memory pd;
             uint256[] memory scaledRatios = getScaledReserves(ratios, decimals);
             // calc target price with 6 decimal precision:
             pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];
     
             // get ratios and price from the closest highest and lowest price from targetPrice:
             pd.lutData = ILookupTable(lookupTable).getRatiosFromPriceSwap(pd.targetPrice);
     
             // calculate lp token supply:
             uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));
     
             // lpTokenSupply / 2 gives the reserves at parity:
             uint256 parityReserve = lpTokenSupply / 2;
     
             // update `scaledReserves` based on whether targetPrice is closer to low or high price:
             if (pd.lutData.highPrice - pd.targetPrice > pd.targetPrice - pd.lutData.lowPrice) {
                 // targetPrice is closer to lowPrice.
                 scaledReserves[i] = parityReserve * pd.lutData.lowPriceI / pd.lutData.precision;
                 scaledReserves[j] = parityReserve * pd.lutData.lowPriceJ / pd.lutData.precision;
                 // initialize currentPrice:
                 pd.currentPrice = pd.lutData.lowPrice;
             } else {
                 // targetPrice is closer to highPrice.
                 scaledReserves[i] = parityReserve * pd.lutData.highPriceI / pd.lutData.precision;
                 scaledReserves[j] = parityReserve * pd.lutData.highPriceJ / pd.lutData.precision;
                 // initialize currentPrice:
                 pd.currentPrice = pd.lutData.highPrice;
             }
     
             // calculate max step size:
             // lowPriceJ will always be larger than highPriceJ so a check here is unnecessary.
             pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
             for (uint256 k; k < 255; k++) {
                 scaledReserves[j] = updateReserve(pd, scaledReserves[j]);
     
                 // calculate scaledReserve[i]:
                 scaledReserves[i] = calcReserve(scaledReserves, i, lpTokenSupply, abi.encode(18, 18));
                 // calculate new price from reserves:
                 pd.newPrice = _calcRate(scaledReserves, i, j, lpTokenSupply);
     
                 // if the new current price is either lower or higher than both the previous current price and the target price,
                 // (i.e the target price lies between the current price and the previous current price),
                 // recalibrate high/low price.
                 if (pd.newPrice > pd.currentPrice && pd.newPrice > pd.targetPrice) {
                     pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / parityReserve;
                     pd.lutData.highPriceI = scaledReserves[i] * 1e18 / parityReserve;
                     pd.lutData.highPrice = pd.newPrice;
                 } else if (pd.newPrice < pd.currentPrice && pd.newPrice < pd.targetPrice) {
                     pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / parityReserve;
                     pd.lutData.lowPriceI = scaledReserves[i] * 1e18 / parityReserve;
                     pd.lutData.lowPrice = pd.newPrice;
                 }
     
                 // update max step size based on new scaled reserve.
                 pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
                 pd.currentPrice = pd.newPrice;
     
                 // check if new price is within PRICE_THRESHOLD:
                 if (pd.currentPrice > pd.targetPrice) {
                     if (pd.currentPrice - pd.targetPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));
                     }
                 } else {
                     if (pd.targetPrice - pd.currentPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));

169:     /**
          * @inheritdoc IMultiFlowPumpWellFunction
          * @dev `calcReserveAtRatioSwap` fetches the closes approximate ratios from the target price,
          * and performs newtons method in order to converge into a reserve.
          */
         function calcReserveAtRatioSwap(
             uint256[] memory reserves,
             uint256 j,
             uint256[] memory ratios,
             bytes calldata data
         ) external view returns (uint256 reserve) {
             uint256 i = j == 1 ? 0 : 1;
             // scale reserves and ratios:
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             PriceData memory pd;
             uint256[] memory scaledRatios = getScaledReserves(ratios, decimals);
             // calc target price with 6 decimal precision:
             pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];
     
             // get ratios and price from the closest highest and lowest price from targetPrice:
             pd.lutData = ILookupTable(lookupTable).getRatiosFromPriceSwap(pd.targetPrice);
     
             // calculate lp token supply:
             uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));
     
             // lpTokenSupply / 2 gives the reserves at parity:
             uint256 parityReserve = lpTokenSupply / 2;
     
             // update `scaledReserves` based on whether targetPrice is closer to low or high price:
             if (pd.lutData.highPrice - pd.targetPrice > pd.targetPrice - pd.lutData.lowPrice) {
                 // targetPrice is closer to lowPrice.
                 scaledReserves[i] = parityReserve * pd.lutData.lowPriceI / pd.lutData.precision;
                 scaledReserves[j] = parityReserve * pd.lutData.lowPriceJ / pd.lutData.precision;
                 // initialize currentPrice:
                 pd.currentPrice = pd.lutData.lowPrice;
             } else {
                 // targetPrice is closer to highPrice.
                 scaledReserves[i] = parityReserve * pd.lutData.highPriceI / pd.lutData.precision;
                 scaledReserves[j] = parityReserve * pd.lutData.highPriceJ / pd.lutData.precision;
                 // initialize currentPrice:
                 pd.currentPrice = pd.lutData.highPrice;
             }
     
             // calculate max step size:
             // lowPriceJ will always be larger than highPriceJ so a check here is unnecessary.
             pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
             for (uint256 k; k < 255; k++) {
                 scaledReserves[j] = updateReserve(pd, scaledReserves[j]);
     
                 // calculate scaledReserve[i]:
                 scaledReserves[i] = calcReserve(scaledReserves, i, lpTokenSupply, abi.encode(18, 18));
                 // calculate new price from reserves:
                 pd.newPrice = _calcRate(scaledReserves, i, j, lpTokenSupply);
     
                 // if the new current price is either lower or higher than both the previous current price and the target price,
                 // (i.e the target price lies between the current price and the previous current price),
                 // recalibrate high/low price.
                 if (pd.newPrice > pd.currentPrice && pd.newPrice > pd.targetPrice) {
                     pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / parityReserve;
                     pd.lutData.highPriceI = scaledReserves[i] * 1e18 / parityReserve;
                     pd.lutData.highPrice = pd.newPrice;
                 } else if (pd.newPrice < pd.currentPrice && pd.newPrice < pd.targetPrice) {
                     pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / parityReserve;
                     pd.lutData.lowPriceI = scaledReserves[i] * 1e18 / parityReserve;
                     pd.lutData.lowPrice = pd.newPrice;
                 }
     
                 // update max step size based on new scaled reserve.
                 pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
                 pd.currentPrice = pd.newPrice;
     
                 // check if new price is within PRICE_THRESHOLD:
                 if (pd.currentPrice > pd.targetPrice) {
                     if (pd.currentPrice - pd.targetPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));

258:     /**
          * @inheritdoc IBeanstalkWellFunction
          * @dev `calcReserveAtRatioLiquidity` fetches the closes approximate ratios from the target price,
          * and performs newtons method in order to converge into a reserve.
          */
         function calcReserveAtRatioLiquidity(
             uint256[] calldata reserves,
             uint256 j,
             uint256[] calldata ratios,
             bytes calldata data
         ) external view returns (uint256 reserve) {
             uint256 i = j == 1 ? 0 : 1;
             // scale reserves and ratios:
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             PriceData memory pd;
             uint256[] memory scaledRatios = getScaledReserves(ratios, decimals);
             // calc target price with 6 decimal precision:
             pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];
     
             // get ratios and price from the closest highest and lowest price from targetPrice:
             pd.lutData = ILookupTable(lookupTable).getRatiosFromPriceLiquidity(pd.targetPrice);
     
             // update scaledReserve[j] such that calcRate(scaledReserves, i, j) = low/high Price,
             // depending on which is closer to targetPrice.
             if (pd.lutData.highPrice - pd.targetPrice > pd.targetPrice - pd.lutData.lowPrice) {
                 // targetPrice is closer to lowPrice.
                 scaledReserves[j] = scaledReserves[i] * pd.lutData.lowPriceJ / pd.lutData.precision;
     
                 // set current price to lowPrice.
                 pd.currentPrice = pd.lutData.lowPrice;
             } else {
                 // targetPrice is closer to highPrice.
                 scaledReserves[j] = scaledReserves[i] * pd.lutData.highPriceJ / pd.lutData.precision;
     
                 // set current price to highPrice.
                 pd.currentPrice = pd.lutData.highPrice;
             }
     
             // calculate max step size:
             // lowPriceJ will always be larger than highPriceJ so a check here is unnecessary.
             pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
             for (uint256 k; k < 255; k++) {
                 scaledReserves[j] = updateReserve(pd, scaledReserves[j]);
                 // calculate new price from reserves:
                 pd.newPrice = calcRate(scaledReserves, i, j, abi.encode(18, 18));
     
                 // if the new current price is either lower or higher than both the previous current price and the target price,
                 // (i.e the target price lies between the current price and the previous current price),
                 // recalibrate high/lowPrice and continue.
                 if (pd.newPrice > pd.targetPrice && pd.targetPrice > pd.currentPrice) {
                     pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];
                     pd.lutData.highPrice = pd.newPrice;
                 } else if (pd.newPrice < pd.targetPrice && pd.targetPrice < pd.currentPrice) {
                     pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];
                     pd.lutData.lowPrice = pd.newPrice;
                 }
     
                 // update max step size based on new scaled reserve.
                 pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
                 pd.currentPrice = pd.newPrice;
     
                 // check if new price is within PRICE_THRESHOLD:
                 if (pd.currentPrice > pd.targetPrice) {
                     if (pd.currentPrice - pd.targetPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));
                     }
                 } else {
                     if (pd.targetPrice - pd.currentPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));

258:     /**
          * @inheritdoc IBeanstalkWellFunction
          * @dev `calcReserveAtRatioLiquidity` fetches the closes approximate ratios from the target price,
          * and performs newtons method in order to converge into a reserve.
          */
         function calcReserveAtRatioLiquidity(
             uint256[] calldata reserves,
             uint256 j,
             uint256[] calldata ratios,
             bytes calldata data
         ) external view returns (uint256 reserve) {
             uint256 i = j == 1 ? 0 : 1;
             // scale reserves and ratios:
             uint256[] memory decimals = decodeWellData(data);
             uint256[] memory scaledReserves = getScaledReserves(reserves, decimals);
     
             PriceData memory pd;
             uint256[] memory scaledRatios = getScaledReserves(ratios, decimals);
             // calc target price with 6 decimal precision:
             pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];
     
             // get ratios and price from the closest highest and lowest price from targetPrice:
             pd.lutData = ILookupTable(lookupTable).getRatiosFromPriceLiquidity(pd.targetPrice);
     
             // update scaledReserve[j] such that calcRate(scaledReserves, i, j) = low/high Price,
             // depending on which is closer to targetPrice.
             if (pd.lutData.highPrice - pd.targetPrice > pd.targetPrice - pd.lutData.lowPrice) {
                 // targetPrice is closer to lowPrice.
                 scaledReserves[j] = scaledReserves[i] * pd.lutData.lowPriceJ / pd.lutData.precision;
     
                 // set current price to lowPrice.
                 pd.currentPrice = pd.lutData.lowPrice;
             } else {
                 // targetPrice is closer to highPrice.
                 scaledReserves[j] = scaledReserves[i] * pd.lutData.highPriceJ / pd.lutData.precision;
     
                 // set current price to highPrice.
                 pd.currentPrice = pd.lutData.highPrice;
             }
     
             // calculate max step size:
             // lowPriceJ will always be larger than highPriceJ so a check here is unnecessary.
             pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
             for (uint256 k; k < 255; k++) {
                 scaledReserves[j] = updateReserve(pd, scaledReserves[j]);
                 // calculate new price from reserves:
                 pd.newPrice = calcRate(scaledReserves, i, j, abi.encode(18, 18));
     
                 // if the new current price is either lower or higher than both the previous current price and the target price,
                 // (i.e the target price lies between the current price and the previous current price),
                 // recalibrate high/lowPrice and continue.
                 if (pd.newPrice > pd.targetPrice && pd.targetPrice > pd.currentPrice) {
                     pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];
                     pd.lutData.highPrice = pd.newPrice;
                 } else if (pd.newPrice < pd.targetPrice && pd.targetPrice < pd.currentPrice) {
                     pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];
                     pd.lutData.lowPrice = pd.newPrice;
                 }
     
                 // update max step size based on new scaled reserve.
                 pd.maxStepSize = scaledReserves[j] * (pd.lutData.lowPriceJ - pd.lutData.highPriceJ) / pd.lutData.lowPriceJ;
     
                 pd.currentPrice = pd.newPrice;
     
                 // check if new price is within PRICE_THRESHOLD:
                 if (pd.currentPrice > pd.targetPrice) {
                     if (pd.currentPrice - pd.targetPrice <= PRICE_THRESHOLD) {
                         return scaledReserves[j] / (10 ** (18 - decimals[j]));

```

### <a name="NC-12"></a>[NC-12] Take advantage of Custom Error's return value property
An important feature of Custom Error is that values such as address, tokenID, msg.value can be written inside the () sign, this kind of approach provides a serious advantage in debugging and examining the revert details of dapps such as tenderly.

*Instances (2)*:
```solidity
File: ./src/functions/Stable2.sol

62:         if (lut == address(0)) revert InvalidLUT();

351:         if (decimal0 > 18 || decimal1 > 18) revert InvalidTokenDecimals();

```

### <a name="NC-13"></a>[NC-13] Contract does not follow the Solidity style guide's suggested layout ordering
The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be:

1) Type declarations
2) State variables
3) Events
4) Modifiers
5) Functions

However, the contract(s) below do not follow this ordering

*Instances (1)*:
```solidity
File: ./src/functions/Stable2.sol

1: 
   Current order:
   StructDefinition.PriceData
   VariableDeclaration.N
   VariableDeclaration.A_PRECISION
   VariableDeclaration.PRICE_PRECISION
   VariableDeclaration.PRICE_THRESHOLD
   VariableDeclaration.lookupTable
   VariableDeclaration.a
   ErrorDefinition.InvalidTokenDecimals
   ErrorDefinition.InvalidLUT
   FunctionDefinition.constructor
   FunctionDefinition.calcLpTokenSupply
   FunctionDefinition.calcReserve
   FunctionDefinition.calcRate
   FunctionDefinition.calcReserveAtRatioSwap
   FunctionDefinition.calcReserveAtRatioLiquidity
   FunctionDefinition.decodeWellData
   FunctionDefinition.name
   FunctionDefinition.symbol
   FunctionDefinition._calcRate
   FunctionDefinition.getScaledReserves
   FunctionDefinition._calcReserve
   FunctionDefinition.getBandC
   FunctionDefinition.updateReserve
   
   Suggested order:
   VariableDeclaration.N
   VariableDeclaration.A_PRECISION
   VariableDeclaration.PRICE_PRECISION
   VariableDeclaration.PRICE_THRESHOLD
   VariableDeclaration.lookupTable
   VariableDeclaration.a
   StructDefinition.PriceData
   ErrorDefinition.InvalidTokenDecimals
   ErrorDefinition.InvalidLUT
   FunctionDefinition.constructor
   FunctionDefinition.calcLpTokenSupply
   FunctionDefinition.calcReserve
   FunctionDefinition.calcRate
   FunctionDefinition.calcReserveAtRatioSwap
   FunctionDefinition.calcReserveAtRatioLiquidity
   FunctionDefinition.decodeWellData
   FunctionDefinition.name
   FunctionDefinition.symbol
   FunctionDefinition._calcRate
   FunctionDefinition.getScaledReserves
   FunctionDefinition._calcReserve
   FunctionDefinition.getBandC
   FunctionDefinition.updateReserve

```

### <a name="NC-14"></a>[NC-14] Use Underscores for Number Literals (add an underscore every 3 digits)

*Instances (1)*:
```solidity
File: ./src/functions/StableLUT/Stable2LUT1.sol

38:                                         PriceData(0.27702e6, 0, 9.646293093274934449e18, 0.001083e6, 0, 2000e18, 1e18);

```

### <a name="NC-15"></a>[NC-15] Internal and private variables and functions names should begin with an underscore
According to the Solidity Style Guide, Non-`external` variable and function names should begin with an [underscore](https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)

*Instances (3)*:
```solidity
File: ./src/functions/Stable2.sol

388:     function getScaledReserves(

406:     function getBandC(

418:     function updateReserve(PriceData memory pd, uint256 reserve) internal pure returns (uint256) {

```

### <a name="NC-16"></a>[NC-16] Constants should be defined rather than using magic numbers

*Instances (13)*:
```solidity
File: ./src/functions/Stable2.sol

136:                     return reserve / (10 ** (18 - decimals[j]));

140:                     return reserve / (10 ** (18 - decimals[j]));

164:         uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));

194:         uint256 lpTokenSupply = calcLpTokenSupply(scaledReserves, abi.encode(18, 18));

222:             scaledReserves[i] = calcReserve(scaledReserves, i, lpTokenSupply, abi.encode(18, 18));

247:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

251:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

305:             pd.newPrice = calcRate(scaledReserves, i, j, abi.encode(18, 18));

326:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

330:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

381:         rate = _reserves[i] - calcReserve(_reserves, i, lpTokenSupply, abi.encode(18, 18));

393:         scaledReserves[0] = reserves[0] * 10 ** (18 - decimals[0]);

394:         scaledReserves[1] = reserves[1] * 10 ** (18 - decimals[1]);

```

### <a name="NC-17"></a>[NC-17] Variables need not be initialized to zero
The default value for variables is zero, so initializing them to zero is superfluous.

*Instances (1)*:
```solidity
File: ./src/functions/Stable2.sol

88:         for (uint256 i = 0; i < 255; i++) {

```


## Low Issues


| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | Use a 2-step ownership transfer pattern | 1 |
| [L-2](#L-2) | Precision Loss due to Division before Multiplication | 1 |
| [L-3](#L-3) | `decimals()` should be of type `uint8` | 2 |
| [L-4](#L-4) | Division by zero not prevented | 19 |
| [L-5](#L-5) | Initializers could be front-run | 7 |
| [L-6](#L-6) | Possible rounding issue | 12 |
| [L-7](#L-7) | Loss of precision | 4 |
| [L-8](#L-8) | Solidity version 0.8.20+ may not work on other chains due to `PUSH0` | 3 |
| [L-9](#L-9) | Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership` | 1 |
| [L-10](#L-10) | Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions | 6 |
| [L-11](#L-11) | Upgradeable contract not initialized | 14 |
### <a name="L-1"></a>[L-1] Use a 2-step ownership transfer pattern
Recommend considering implementing a two step process where the owner or admin nominates an account and the nominated account needs to call an `acceptOwnership()` function for the transfer of ownership to fully succeed. This ensures the nominated EOA account is a valid and active account. Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

```

### <a name="L-2"></a>[L-2] Precision Loss due to Division before Multiplication
division operations can lead to a loss of precision as the fractional part is discarded. When the result of such a division operation is then multiplied, this loss of precision can be magnified, potentially leading to significant inaccuracies in the calculations.

*Instances (1)*:
```solidity
File: ./src/functions/Stable2.sol

411:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-3"></a>[L-3] `decimals()` should be of type `uint8`

*Instances (2)*:
```solidity
File: ./src/functions/Stable2.sol

341:     function decodeWellData(bytes memory data) public view virtual returns (uint256[] memory decimals) {

390:         uint256[] memory decimals

```

### <a name="L-4"></a>[L-4] Division by zero not prevented
The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.

*Instances (19)*:
```solidity
File: ./src/functions/Stable2.sol

91:             dP = dP * lpTokenSupply / (scaledReserves[0] * N);

92:             dP = dP * lpTokenSupply / (scaledReserves[1] * N);

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

136:                     return reserve / (10 ** (18 - decimals[j]));

140:                     return reserve / (10 ** (18 - decimals[j]));

188:         pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];

202:             scaledReserves[i] = parityReserve * pd.lutData.lowPriceI / pd.lutData.precision;

230:                 pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / parityReserve;

231:                 pd.lutData.highPriceI = scaledReserves[i] * 1e18 / parityReserve;

234:                 pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / parityReserve;

235:                 pd.lutData.lowPriceI = scaledReserves[i] * 1e18 / parityReserve;

251:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

277:         pd.targetPrice = scaledRatios[i] * PRICE_PRECISION / scaledRatios[j];

311:                 pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];

314:                 pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];

330:                     return scaledReserves[j] / (10 ** (18 - decimals[j]));

403:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

411:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

423:                 - pd.maxStepSize * (pd.targetPrice - pd.currentPrice) / (pd.lutData.highPrice - pd.lutData.lowPrice);

```

### <a name="L-5"></a>[L-5] Initializers could be front-run
Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment

*Instances (7)*:
```solidity
File: ./src/WellUpgradeable.sol

31:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

32:         __ERC20Permit_init(_name);

33:         __ERC20_init(_name, _symbol);

34:         __ReentrancyGuard_init();

35:         __UUPSUpgradeable_init();

36:         __Ownable_init();

52:     function initNoWellToken() external initializer {}

```

### <a name="L-6"></a>[L-6] Possible rounding issue
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator. Also, there is indication of multiplication and division without the use of parenthesis which could result in issues.

*Instances (12)*:
```solidity
File: ./src/functions/Stable2.sol

91:             dP = dP * lpTokenSupply / (scaledReserves[0] * N);

92:             dP = dP * lpTokenSupply / (scaledReserves[1] * N);

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

95:                 / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));

230:                 pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / parityReserve;

231:                 pd.lutData.highPriceI = scaledReserves[i] * 1e18 / parityReserve;

234:                 pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / parityReserve;

235:                 pd.lutData.lowPriceI = scaledReserves[i] * 1e18 / parityReserve;

311:                 pd.lutData.highPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];

314:                 pd.lutData.lowPriceJ = scaledReserves[j] * 1e18 / scaledReserves[i];

403:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

411:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-7"></a>[L-7] Loss of precision
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator

*Instances (4)*:
```solidity
File: ./src/functions/Stable2.sol

94:             lpTokenSupply = (Ann * sumReserves / A_PRECISION + (dP * N)) * lpTokenSupply

95:                 / (((Ann - A_PRECISION) * lpTokenSupply / A_PRECISION) + ((N + 1) * dP));

403:         return (reserve * reserve + c) / (reserve * 2 + b - lpTokenSupply);

411:         c = lpTokenSupply * lpTokenSupply / (reserves * N) * lpTokenSupply * A_PRECISION / (Ann * N);

```

### <a name="L-8"></a>[L-8] Solidity version 0.8.20+ may not work on other chains due to `PUSH0`
The compiler for Solidity 0.8.20 switches the default target EVM version to [Shanghai](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/#important-note), which includes the new `PUSH0` op code. This op code may not yet be implemented on all L2s, so deployment on these chains will fail. To work around this issue, use an earlier [EVM](https://docs.soliditylang.org/en/v0.8.20/using-the-compiler.html?ref=zaryabs.com#setting-the-evm-version-to-target) [version](https://book.getfoundry.sh/reference/config/solidity-compiler#evm_version). While the project itself may or may not compile with 0.8.20, other projects with which it integrates, or which extend this project may, and those projects will have problems deploying these contracts/libraries.

*Instances (3)*:
```solidity
File: ./src/WellUpgradeable.sol

3: pragma solidity ^0.8.20;

```

```solidity
File: ./src/functions/Stable2.sol

3: pragma solidity ^0.8.20;

```

```solidity
File: ./src/functions/StableLUT/Stable2LUT1.sol

3: pragma solidity ^0.8.20;

```

### <a name="L-9"></a>[L-9] Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership`
Use [Ownable2Step.transferOwnership](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol) which is safer. Use it as it is more secure due to 2-stage ownership transfer.

**Recommended Mitigation Steps**

Use <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol">Ownable2Step.sol</a>
  
  ```solidity
      function acceptOwnership() external {
          address sender = _msgSender();
          require(pendingOwner() == sender, "Ownable2Step: caller is not the new owner");
          _transferOwnership(sender);
      }
```

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

```

### <a name="L-10"></a>[L-10] Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions
See [this](https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps) link for a description of this storage variable. While some contracts may not currently be sub-classed, adding the variable now protects against forgetting to add it in the future.

*Instances (6)*:
```solidity
File: ./src/WellUpgradeable.sol

6: import {UUPSUpgradeable} from "ozu/proxy/utils/UUPSUpgradeable.sol";

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

35:         __UUPSUpgradeable_init();

80:         IERC20[] memory newTokens = WellUpgradeable(newImplementation).tokens();

88:             UUPSUpgradeable(newImplementation).proxiableUUID() == _IMPLEMENTATION_SLOT,

```

### <a name="L-11"></a>[L-11] Upgradeable contract not initialized
Upgradeable contracts are initialized via an initializer function rather than by a constructor. Leaving such a contract uninitialized may lead to it being taken over by a malicious user

*Instances (14)*:
```solidity
File: ./src/WellUpgradeable.sol

6: import {UUPSUpgradeable} from "ozu/proxy/utils/UUPSUpgradeable.sol";

7: import {OwnableUpgradeable} from "ozu/access/OwnableUpgradeable.sol";

16: contract WellUpgradeable is Well, UUPSUpgradeable, OwnableUpgradeable {

31:     function init(string memory _name, string memory _symbol) external override reinitializer(2) {

32:         __ERC20Permit_init(_name);

33:         __ERC20_init(_name, _symbol);

34:         __ReentrancyGuard_init();

35:         __UUPSUpgradeable_init();

36:         __Ownable_init();

52:     function initNoWellToken() external initializer {}

80:         IERC20[] memory newTokens = WellUpgradeable(newImplementation).tokens();

88:             UUPSUpgradeable(newImplementation).proxiableUUID() == _IMPLEMENTATION_SLOT,

136:     function getInitializerVersion() external view returns (uint256) {

137:         return _getInitializedVersion();

```


## Medium Issues


| |Issue|Instances|
|-|:-|:-:|
| [M-1](#M-1) | Centralization Risk for trusted owners | 1 |
### <a name="M-1"></a>[M-1] Centralization Risk for trusted owners

#### Impact:
Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*Instances (1)*:
```solidity
File: ./src/WellUpgradeable.sol

63:     function _authorizeUpgrade(address newImplementation) internal view override onlyOwner {

```
