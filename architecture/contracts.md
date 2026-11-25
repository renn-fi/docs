---
description: Responsibilities of the loan, hedging, vault, and infrastructure contracts.
---

# Contract roles

## Loan layer

**LoanFactory** deploys and initially collateralizes LoanV2 orders. It manages separate collateral and consideration whitelists, registers loans in `isLoan`, and forwards each registered loan's hedge request. It records the selected position in `hedgeOf` and provider in `strategyOf`.

**LoanV2** owns the fixed terms and lifecycle. It receives funding, records principal and accrued repayment, controls acceptance and settlement, and allocates lender and borrower assets.

**LoanHedging** is inherited by LoanV2. It connects loan accounting to the IHedging interface, funds opening premiums, grants temporary provider allowances, and measures recovery from token balance changes.

**LoanTokenEmitent** is inherited by LoanV2 and creates its LoanToken. It provides internal mint and burn operations and records cumulative emission. **LoanToken** is the transferable ERC-20 lender claim; only its deploying loan can mint or burn it.

## Hedging layer

**IHedging** defines loan-facing requests, premium quotes, position creation, opening, and realization. **HedgingMarkets** is the provider base that fixes settlement infrastructure and stores directional execution markets.

**Hedging** implements option-backed protection. It translates loan requests into Greek parameters, obtains Prop quotes, opens complete option trades, and chooses recovery through market sales or PUT exercise.

**GreekPositionDeployer** creates positions exclusively for its Hedging controller. **GreekPut** holds and exercises a loan's protective PUT. **GreekCollar** holds protective PUT tokens and covered CALL writer receipts, redeems the CALL claim, and exercises the PUT as directed by Hedging.

**NoHedgingFactory** and **NoHedging** provide a Uniswap-only test configuration. They create isolated zero-premium positions whose recovery uses collateral sales. The capped request selects collateral escrow in the test position.

## Vault layer

**VaultFactory** deploys private vaults owned by their creators and registers them in `isVault`.

**Vault** holds one owner's supplied asset and LoanToken receipts. Its immutable executor funds registered loans that satisfy the owner's current criteria. The owner and executor can refund or collect existing claims.

## Infrastructure and external dependencies

**PairPriceOracle** routes both directions of a token pair to its registered source. **UniswapTwapOracle** quotes a fixed pair using a fixed Uniswap V3 observation window. **TickMathV3** supplies tick-to-price arithmetic.

**UniswapSeller** executes bounded single-pool swaps through its pinned SwapRouter02 and returns proceeds to its caller. **IPriceOracle** and **ISwapRouter02** define the corresponding interfaces.

Prop routes option trades against maker pricers. The external Greek Factory supplies option/receipt pairs and processes backing, exercise, and redemption. The Greek settlement interfaces define the methods used by Renn's positions.

Continue with [custody and permissions](custody-and-permissions.md) and [hedging positions](../hedging/positions.md).
