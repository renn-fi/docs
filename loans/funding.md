---
description: Direct and vault funding, refunds, cancellation, and borrower acceptance.
---

# Funding and acceptance

## Funding an order

During Lending, a lender approves LoanV2 for the supplied asset and calls `lend` with a positive amount within the remaining funding capacity. LoanV2 records the funding in `vaultLending`, mints the same raw amount of LoanToken to the caller, and verifies exact receipt of the supplied asset.

Several lenders can fund one order, and the same lender can add funding repeatedly. A personal vault follows this same loan entry point through its executor-controlled funding operation.

## Refunds and cancellation

In Lending or Canceled, `refund` burns all receipts held by the caller and returns the corresponding funding. A refund during Lending frees capacity for another lender.

The borrower can explicitly cancel while the order is Lending. The order also becomes Canceled at `createdAt` plus `orderCancelation`. Canceled orders allow lender refunds and release of collateral to the borrower.

## Borrower acceptance

Only the borrower can accept, before the order deadline and with positive funding. Acceptance uses all funding available in that transaction as principal.

LoanV2 retains collateral proportionally and calculates the full-term target as principal multiplied by the rate, divided by `1e18`, rounded up. It records `acceptedAt`; maturity is that timestamp plus the term.

The borrower selects uncapped or capped opening, the collar cap price when applicable, a signed maximum net premium, and an execution deadline. LoanHedging creates the position through LoanFactory and opens it through the selected provider.

A positive premium budget is funded separately by the borrower through an allowance to LoanV2. Unused premium budget and net premium income return to the borrower. The accepted lender funding is paid to the borrower as principal.

Position creation, opening, collateral placement, refunds, and principal release share one transaction. A required step failing rolls back acceptance. Continue with [hedge opening and recovery](../hedging/opening-and-recovery.md) or [repayment](../repayment-and-exit/repayment.md).
