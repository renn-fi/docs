---
description: Discovery, current-state reads, event meanings, and transaction allowances.
---

# Events and integration

## Discover contracts

`LoanCreated` from LoanFactory identifies a registered loan, borrower, and receipt token. Verify registration with `isLoan`. At acceptance, factory `HedgingCreated` records the position and provider; provider events describe its creation and opening.

`VaultCreated` from VaultFactory identifies a registered vault, owner, loan factory, asset, executor, full initial criteria, and collaterals. Verify registration with `isVault` and track events from those instances.

## Read current state

| Information | Contract reads |
| --- | --- |
| Loan eligibility and timing | `state`, `terms`, `createdAt`, `acceptedAt` |
| Accepted debt and payment quote | `principal`, `repaymentTarget`, `repaymentDue`, `repaymentDueAt` |
| Position and strategy | Loan `hedge`, `hedging`, `hedgeCapped`; factory `hedgeOf`, `strategyOf` |
| Current lender claim | LoanToken `balanceOf`, `totalSupply` |
| Final allocation | Loan accounting buckets and `shortfall` |
| Vault controls and cash | `owner`, `criteria`, `collaterals`, `paused`, `freeBalance`, immutable configuration |
| Price route and execution market | PairPriceOracle `oracleOf`; provider `markets` |

Time-derived state changes become effective when their timestamps are reached. An event projection should refresh `state` near deadlines and before submitting a transaction. `stateUpdate` persists the transition and emits its event.

## Interpret lifecycle events

`Lent` records supplied funding, while LoanToken Transfer events identify receipt minting, transfers, and burns. Loan `Withdrawn` is emitted for both order refunds and final lender withdrawals; interpret it with lifecycle context.

`Accepted` records actual principal, the initial full-term target, retained collateral, and maturity. `Repaid` records a payer's cash payment. The target may then be lower than the initial target because interest freezes at repayment.

`DefaultInitiated` marks settlement with debt remaining. `DefaultCompleted` reports the lender allocation and shortfall. `LoanRepaid` marks completed settlement, including a shortfall. `BorrowerAssetsWithdrawn` records release of accounted borrower assets.

Provider `HedgeOpened` records actual option premiums. `HedgeCollateralSold` and UniswapSeller's `CollateralSold` record execution. Provider `Realized` reports assets returned in that operation; collateral left untouched in an uncapped loan remains part of its separate collateral accounting. Position events record PUT opening and exercise, collar opening, and CALL redemption.

Vault `CriteriaUpdated`, `CollateralWhitelisted`, `CollateralRemoved`, and `PauseUpdated` describe current funding rules. `LoanFunded`, `LoanRefunded`, and `LoanCollected` identify its loan activity. Refund and collection amounts are actual cash increases. Track Ownable2Step events for ownership changes.

## Prepare allowances

| Operation | Token owner | Approved spender |
| --- | --- | --- |
| Create an order | Borrower | LoanFactory for initial collateral |
| Fund directly | Lender | LoanV2 for supplied funding |
| Fund a positive opening premium | Borrower | LoanV2 for the positive premium budget |
| Repay debt | Payer | LoanV2 for the supplied repayment bound |
| Deposit vault cash | Owner | Vault for ASSET |

For bounded repayment, choose a future execution deadline, quote `repaymentDueAt` for that timestamp, and approve the bound. The loan recalculates and pulls the exact due amount at execution; an exceeded amount or time limit reverts. Unused payer allowance remains until spent or changed.

LoanHedging, Vault, providers, and the seller manage and clear their temporary execution allowances. Opening deadlines bound acceptance trades. Settlement deadlines bound swap execution when a sale occurs. Maturity and option exercise windows are separate lifecycle conditions.
