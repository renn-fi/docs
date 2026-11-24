---
description: Loan states, recovery eligibility, final accounting, and withdrawals.
---

# Settlement and withdrawals

## Lifecycle states

| State | Meaning |
| --- | --- |
| Created | Loan deployed and awaiting collateral accounting |
| Lending | Collateral accounted; order open for funding and acceptance |
| Canceled | Borrower canceled or the order deadline was reached |
| Repaying | Funding accepted; maturity still ahead |
| Expired | Accepted loan reached maturity and awaits settlement |
| Repaid | Recovery and final allocation completed |

`state` derives Canceled and Expired from timestamps when their deadlines are reached. `stateUpdate` persists the derived transition and emits the corresponding event. Entry points use the derived state, so eligibility changes at the deadline without a separate update transaction.

## Final settlement

A fully repaid uncapped loan settles in its repayment transaction. Otherwise, any caller can request `settle` or `defaultLoan` at maturity. The borrower can request the same settlement using `repayFromCollateral`. A collar also waits until strictly after the CALL receipt's exercise deadline.

LoanV2 passes remaining debt and its accounted collateral budget to the pinned provider. The provider returns recovered supplied assets and residual collateral through its [recovery flow](../hedging/opening-and-recovery.md). LoanHedging measures the loan's actual balance changes.

## Allocating recovery

The lender pool is accounted repayments plus new supplied recovery, capped at `repaymentTarget`. Supplied assets above that target become borrower surplus. `shortfall` is the target less the lender allocation. Remaining accounted collateral belongs to the borrower.

The loan enters Repaid when this allocation completes, including a recovery below the target. A failing recovery transaction rolls back settlement and can be retried.

## Withdrawals

Each receipt holder calls `withdraw` to burn its full balance and receive its proportion of the remaining supplied lender pool, rounded down. The final holder receives the remaining rounding balance. A zero-value claim can still be burned and closed.

`withdrawBorrower` releases residual accounted collateral and supplied surplus to the fixed borrower. Any caller can trigger it. Lender and borrower withdrawals use separate accounting buckets and can occur in either order.

For canceled orders, use lender `refund` and `refundBorrower` instead. See [exit paths](../repayment-and-exit/exit-options.md).
