---
description: The participants and end-to-end lifecycle of a collateralized loan.
---

# Protocol overview

## Participants

The borrower fixes the loan terms, deposits collateral, and decides when to accept the available funding. Lenders contribute supplied assets and receive transferable LoanToken receipts. A private vault can act as a lender using its owner's cash and a designated executor.

LoanFactory creates and registers loans. A hedging provider manages the accepted loan's position. For option-backed protection, Hedging trades through Prop and controls a dedicated GreekPut or GreekCollar position.

## End-to-end flow

1. **Create an order.** LoanFactory deploys LoanV2 and its receipt token, transfers the borrower's collateral directly into the loan, and activates the funding period.
2. **Fund.** Lenders deposit the supplied asset and receive receipts. They can refund their receipts while the order is unaccepted.
3. **Accept.** The borrower accepts positive funding before the order deadline. Principal equals the amount funded at execution. Collateral is retained proportionally, and the rest returns to the borrower.
4. **Open protection.** Acceptance creates and opens the selected hedge, using a separate borrower premium budget. The transaction then releases principal to the borrower.
5. **Repay or recover.** A payer can repay principal plus accrued interest. At maturity, settlement can recover assets through the position and collateral sales.
6. **Withdraw.** After settlement, receipt holders claim supplied assets. Residual collateral and supplied surplus go to the borrower.

For uncapped protection, full repayment settles the loan immediately. A collar waits for maturity and completion of its CALL exercise window before final recovery, even after an earlier repayment.

## Separate loan accounting

Each loan has its own terms, collateral, receipts, repayment pool, and settlement result. Its `shortfall` records any unpaid part of the target after recovery. Repaid is the terminal state for completed allocation, including a settlement with a shortfall.

Private vaults retain the receipts for loans they fund. Their owner can withdraw idle cash, and the owner or executor can recover funds from orders or collect settled claims.

Continue with [contract roles](../architecture/contracts.md) or [loan creation](../loans/loan-creation.md).
