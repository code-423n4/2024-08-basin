# Basin audit details
- Total Prize Pool: $7,750 in USDC
  - HM awards: $5,510 in USDC
  - QA awards: $240 in USDC
  - Judge awards: $1,500 in USDC
  - Scout awards: $500 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts August 23, 2024 20:00 UTC
- Ends August 27, 2024 20:00 UTC

## This is a Private audit

This audit repo and its Discord channel are accessible to **certified wardens only.** Participation in private audits is bound by:

1. Code4rena's [Certified Contributor Terms and Conditions](https://github.com/code-423n4/code423n4.com/blob/main/_data/pages/certified-contributor-terms-and-conditions.md)
2. C4's [Certified Contributor Code of Professional Conduct](https://code4rena.notion.site/Code-of-Professional-Conduct-657c7d80d34045f19eee510ae06fef55)

*All discussions regarding private audits should be considered private and confidential, unless otherwise indicated.*

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-08-basin/blob/main/4naly3er-report.md).

All findings in the following audit reports:

* 06/16/23: [Basin Halborn Report](https://arweave.net/1IKi4iqRvu3qu_GdcLY4f3u9PgvOMvuRltU7AIXAEyA) @ [e5441fc](https://github.com/BeanstalkFarms/Basin/tree/e5441fc78f0fd4b77a898812d0fd22cb43a0af55)
* 06/16/23: [Basin Cyfrin Report](https://arweave.net/usT3ClfjHwpX32OXnh5De1aH79csX1PMoXJCghXBaps) @ [e5441fc](https://github.com/BeanstalkFarms/Basin/tree/e5441fc78f0fd4b77a898812d0fd22cb43a0af55)
* 10/05/23: [Basin Code4rena Report](https://code4rena.com/reports/2023-07-basin) @ [7e51c02](https://github.com/code-423n4/2023-07-basin/tree/7e51c025d32aff3f2456842c83cda66cda274d11)
* All bug reports from the Immunefi program listed [here](https://community.bean.money/bug-reports).

_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

# Basin
![basin(green)-512x512 (1)](https://github.com/code-423n4/2024-07-basin/blob/main/basin(green)-512x512%20(1).png?raw=true) ![512x512-MF](https://github.com/code-423n4/2024-07-basin/blob/main/512x512-MF.png?raw=true)

Code Version: `1.0.0` 
Whitepaper Version: `1.0.0`

### Multi Flow

The Multi Flow Pump implementation is also included in this repository at [MultiFlowPump.sol](/src/pumps/MultiFlowPump.sol).

Code Version: `1.0.0` 
Whitepaper Version: `1.0.0`

## About

Basin is a composable EVM-native decentralized exchange protocol.

- [Audits](#audits)
- [Documentation](#documentation)
    - [Motivation](#motivation)
- [License](#license)

## Audits

* [Cyfrin Basin Audit](https://basin.exchange/cyfrin-basin-audit.pdf)
* [Halborn Basin Audit](https://basin.exchange/halborn-basin-audit.pdf)

## Documentation

* [Basin Whitepaper](https://basin.exchange/basin.pdf)
* [Multi Flow Whitepaper](https://basin.exchange/multi-flow-pump.pdf)
* [Basin Docs](https://docs.basin.exchange)

A [{Well}](/src/Well.sol) is a constant function AMM that allows the provisioning of liquidity into a single pooled on-chain liquidity position.

Each Well is defined by its Tokens, Well function, and Pump.
- The **Tokens** define the set of ERC-20 tokens that can be exchanged in the Well.
- The **Well function** defines an invariant relationship between the Well's reserves and the supply of LP tokens. See [{IWellFunction}](/src//interfaces/IWellFunction.sol).
- **Pumps** are an on-chain oracles that are updated upon each interaction with the Well. See [{IPump}](/src/interfaces/IPump.sol).

A Well's tokens, Well function, and Pump are stored as immutable variables during Well construction to prevent unnecessary SLOAD calls during operation.

Wells support swapping, adding liquidity, and removing liquidity in balanced or imbalanced proportions.

Wells maintain two components of state:
- a balance of tokens received through Well operations ("reserves")
- an ERC-20 LP token representing pro-rata ownership of the reserves

Well functions and Pumps can independently choose to be stateful or stateless.

Including a Pump is optional.

Each Well implements ERC-20, ERC-2612 and the [{IWell}](/src/interfaces/IWell.sol) interface.

### Motivation

Allowing composability of the pricing function and oracle at the Well level is a deliberate design decision with significant implications. 

In particular, a standard AMM interface invoking composable components allows for developers to iterate upon the underlying pricing functions and oracles, which greatly impacts gas and capital efficiency. 

However, this architecture shifts much of the attack surface area to the Well's components. Users of Wells should be aware that anyone can deploy a Well with malicious components, and that new Wells SHOULD NOT be trusted without careful review. This understanding is particularly important in the DeFi context in which Well data may be consumed via on-chain registries or off-chain indexing systems.

The Wells architecture aims to outline a simple interface for composable AMMs and leave the process of evaluating a given Well's trustworthiness as the responsibility of the user. To this end, future work may focus on development of on-chain Well registries and factories which create or highlight Wells composed of known components.

An example factory implementation is provided in [{Aquifer}](/src/Aquifer.sol) without any opinion regarding the trustworthiness of Well functions and the Pumps using it. Wells are not required to be deployed via this mechanism.

## License

[MIT](https://github.com/BeanstalkFarms/Basin/blob/master/LICENSE.txt)


## Links

- **Previous audits:**  All can be found [here](https://docs.basin.exchange/resources/audits)
- **Documentation:** https://docs.basin.exchange/
- **Website:** https://basin.exchange
- **X/Twitter:** https://twitter.com/basinexchange
- **Discord:** https://basin.exchange/discord

---

# Scope

*See [scope.txt](https://github.com/code-423n4/2024-08-basin/blob/main/scope.txt)*

🛑 All of the contracts below were audited in [Basin's July audit](https://github.com/code-423n4/2024-07-basin).  Here is a [commit](https://github.com/BeanstalkFarms/Basin/pull/143/commits/071cc41fbf1d9a40658c0337f2f642e19f942a7c) highlighting the changes.

### Files in scope

| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /src/functions/Stable2.sol | 1| **** | 209 | |src/interfaces/IBeanstalkWellFunction.sol<br>src/interfaces/ILookupTable.sol<br>src/functions/ProportionalLPToken2.sol<br>forge-std/interfaces/IERC20.sol|
| /src/functions/StableLUT/Stable2LUT1.sol | 1| **** | 2150 | |src/interfaces/ILookupTable.sol|
| /src/WellUpgradeable.sol | 1| **** | 74 | |src/Well.sol<br>ozu/proxy/utils/UUPSUpgradeable.sol<br>ozu/access/OwnableUpgradeable.sol<br>oz/token/ERC20/utils/SafeERC20.sol<br>src/interfaces/IAquifer.sol|
| **Totals** | **3** | **** | **2433** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2024-08-basin/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| ./mocks/functions/MockEmptyFunction.sol |
| ./mocks/functions/MockFunctionBad.sol |
| ./mocks/pumps/MockFailPump.sol |
| ./mocks/pumps/MockPump.sol |
| ./mocks/tokens/MockToken.sol |
| ./mocks/tokens/MockTokenFeeOnTransfer.sol |
| ./mocks/tokens/MockTokenNoName.sol |
| ./mocks/tokens/ReentrantMockToken.sol |
| ./mocks/wells/MockInitFailWell.sol |
| ./mocks/wells/MockReserveWell.sol |
| ./mocks/wells/MockStaticWell.sol |
| ./mocks/wells/MockWellUpgradeable.sol |
| ./script/deploy/Aquifer.s.sol |
| ./script/deploy/AquiferWell.s.sol |
| ./script/deploy/MockPump.s.sol |
| ./script/deploy/Well.s.sol |
| ./script/deploy/helpers/Logger.sol |
| ./script/helpers/WellDeployer.sol |
| ./script/simulations/stableswap/StableswapCalcRatiosLiqSim.s.sol |
| ./script/simulations/stableswap/StableswapCalcRatiosSwapSim.s.sol |
| ./src/Aquifer.sol |
| ./src/Well.sol |
| ./src/functions/ConstantProduct.sol |
| ./src/functions/ConstantProduct2.sol |
| ./src/functions/ProportionalLPToken.sol |
| ./src/functions/ProportionalLPToken2.sol |
| ./src/interfaces/IAquifer.sol |
| ./src/interfaces/IBeanstalkWellFunction.sol |
| ./src/interfaces/ILookupTable.sol |
| ./src/interfaces/IMultiFlowPumpWellFunction.sol |
| ./src/interfaces/IWell.sol |
| ./src/interfaces/IWellErrors.sol |
| ./src/interfaces/IWellFunction.sol |
| ./src/interfaces/pumps/ICumulativePump.sol |
| ./src/interfaces/pumps/IInstantaneousPump.sol |
| ./src/interfaces/pumps/IMultiFlowPumpErrors.sol |
| ./src/interfaces/pumps/IPump.sol |
| ./src/libraries/ABDKMathQuad.sol |
| ./src/libraries/LibBytes.sol |
| ./src/libraries/LibBytes16.sol |
| ./src/libraries/LibClone.sol |
| ./src/libraries/LibContractInfo.sol |
| ./src/libraries/LibLastReserveBytes.sol |
| ./src/libraries/LibMath.sol |
| ./src/libraries/LibWellConstructor.sol |
| ./src/libraries/LibWellUpgradeableConstructor.sol |
| ./src/pumps/MultiFlowPump.sol |
| ./src/utils/Clone.sol |
| ./src/utils/ClonePlus.sol |
| ./test/Aquifer.t.sol |
| ./test/LiquidityHelper.sol |
| ./test/Stable2/LookupTable.t.sol |
| ./test/Stable2/Well.Stable2.AddLiquidity.t.sol |
| ./test/Stable2/Well.Stable2.Bore.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidity.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidityImbalanced.t.sol |
| ./test/Stable2/Well.Stable2.RemoveLiquidityOneToken.t.sol |
| ./test/Stable2/Well.Stable2.Shift.t.sol |
| ./test/Stable2/Well.Stable2.Skim.t.sol |
| ./test/Stable2/Well.Stable2.SwapFrom.t.sol |
| ./test/Stable2/Well.Stable2.SwapTo.t.sol |
| ./test/SwapHelper.sol |
| ./test/TestHelper.sol |
| ./test/Well.AddLiquidity.t.sol |
| ./test/Well.AddLiquidityFeeOnTransfer.Fee.t.sol |
| ./test/Well.AddLiquidityFeeOnTransfer.NoFee.t.sol |
| ./test/Well.Bore.t.sol |
| ./test/Well.DuplicateTokens.t.sol |
| ./test/Well.FeeOnTransfer.t.sol |
| ./test/Well.ReadOnlyReentrancy.t.sol |
| ./test/Well.RemoveLiquidity.t.sol |
| ./test/Well.RemoveLiquidityImbalanced.t.sol |
| ./test/Well.RemoveLiquidityOneToken.t.sol |
| ./test/Well.Shift.t.sol |
| ./test/Well.Skim.t.sol |
| ./test/Well.SucceedOnPumpFailure.t.sol |
| ./test/Well.SwapFrom.t.sol |
| ./test/Well.SwapFromFeeOnTransfer.Fee.t.sol |
| ./test/Well.SwapFromFeeOnTransfer.NoFee.t.sol |
| ./test/Well.SwapTo.t.sol |
| ./test/Well.Sync.t.sol |
| ./test/Well.Tokens.t.sol |
| ./test/Well.UpdatePump.t.sol |
| ./test/WellUpgradeable.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct.calcReserveAtRatioSwap.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct2.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkConstantProduct2.calcReserveAtRatioSwap.t.sol |
| ./test/beanstalk/BeanstalkStable2.calcReserveAtRatioLiquidity.t.sol |
| ./test/beanstalk/BeanstalkStable2.calcReserveAtRatioSwap.t.sol |
| ./test/functions/ConstantProduct.t.sol |
| ./test/functions/ConstantProduct2.t.sol |
| ./test/functions/Stable2.t.sol |
| ./test/functions/WellFunctionHelper.sol |
| ./test/helpers/Users.sol |
| ./test/integration/GasMetering.sol |
| ./test/integration/IntegrationTestGasComparisons.sol |
| ./test/integration/IntegrationTestHelper.sol |
| ./test/integration/interfaces/ICurve.sol |
| ./test/integration/interfaces/IPipeline.sol |
| ./test/integration/interfaces/IUniswap.sol |
| ./test/invariant/Handler.t.sol |
| ./test/invariant/Invariants.t.sol |
| ./test/libraries/LibBytes.t.sol |
| ./test/libraries/LibBytes16.t.sol |
| ./test/libraries/LibContractInfo.t.sol |
| ./test/libraries/LibLastReserveBytes.t.sol |
| ./test/libraries/LibMath.t.sol |
| ./test/libraries/TestABDK.t.sol |
| ./test/pumps/Pump.CapReserves.t.sol |
| ./test/pumps/Pump.Fuzz.t.sol |
| ./test/pumps/Pump.Helpers.t.sol |
| ./test/pumps/Pump.Longevity.t.sol |
| ./test/pumps/Pump.NotInitialized.t.sol |
| ./test/pumps/Pump.TimeWeightedAverage.t.sol |
| ./test/pumps/Pump.Update.t.sol |
| ./test/pumps/PumpHelpers.sol |
| Totals: 117 |

## Scoping Q &amp; A

### General questions
### Are there any ERC20's in scope?: Yes

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".

Any (all possible ERC20s)


### Are there any ERC777's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



### Are there any ERC721's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



### Are there any ERC1155's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



✅ SCOUTS: Once done populating the table below, please remove all the Q/A data above.

| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| ERC20 used by the protocol              |       🖊️             |
| Test coverage                           | ✅ SCOUTS: Please populate this after running the test coverage command                          |
| ERC721 used  by the protocol            |            🖊️              |
| ERC777 used by the protocol             |           🖊️                |
| ERC1155 used by the protocol            |              🖊️            |
| Chains the protocol will be deployed on | Ethereum |

### ERC20 token behaviors in scope

| Question                                                                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| [Missing return values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values)                                                      |   Out of scope  |
| [Fee on transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer)                                                                  |  Out of scope  |
| [Balance changes outside of transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) | Out of scope    |
| [Upgradeability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens)                                                                 |   In scope  |
| [Flash minting](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens)                                                              | Out of scope    |
| [Pausability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens)                                                                      | Out of scope    |
| [Approval race protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections)                                              | Out of scope    |
| [Revert on approval to zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address)                            | Out of scope    |
| [Revert on zero value approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals)                                    | Out of scope    |
| [Revert on zero value transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                    | Out of scope    |
| [Revert on transfer to the zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address)                    | Out of scope    |
| [Revert on large approvals and/or transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers)                  | Out of scope    |
| [Doesn't revert on failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure)                                                   |  Out of scope   |
| [Multiple token addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                          | Out of scope    |
| [Low decimals ( < 6)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals)                                                                 |   Out of scope  |
| [High decimals ( > 18)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals)                                                              | Out of scope    |
| [Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists)                                                                | Out of scope    |

### External integrations (e.g., Uniswap) behavior in scope:


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| Enabling/disabling fees (e.g. Blur disables/enables fees) | No   |
| Pausability (e.g. Uniswap pool gets paused)               |  No   |
| Upgradeability (e.g. Uniswap gets upgraded)               |   No  |


### EIP compliance checklist
`src/WellUpgradeable.sol`: should comply with EIP-1822

✅ SCOUTS: Please format the response above 👆 using the template below👇

| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| src/Token.sol                           | ERC20, ERC721                |
| src/NFT.sol                             | ERC721                       |


# Additional context

## Main invariants

None

## Attack ideas (where to focus for bugs)
None

## All trusted roles in the protocol

N/A

## Describe any novel or unique curve logic or mathematical models implemented in the contracts:

With regard to the Stable 2 Well Function, a lookup table is used to assist the Newtonian estimation to decrease the computation needed to converge to an answer. See in line comments.

## Running tests

# foundry setup

foundryup
forge install
forge build

# setup python environment

python3 -m venv env 
source env/bin/activate 
python3 -m pip install -r requirements.txt

# gas report

forge test --ffi --gas-report

✅ SCOUTS: Please format the response above 👆 using the template below👇

```bash
git clone https://github.com/code-423n4/2023-08-arbitrum
git submodule update --init --recursive
cd governance
foundryup
make install
make build
make sc-election-test
```
To run code coverage
```bash
make coverage
```
To run gas benchmarks
```bash
make gas
```

✅ SCOUTS: Add a screenshot of your terminal showing the gas report
✅ SCOUTS: Add a screenshot of your terminal showing the test coverage

## Miscellaneous
Employees of Beanstalk Farms contributors and employees' family members are ineligible to participate in this audit.
