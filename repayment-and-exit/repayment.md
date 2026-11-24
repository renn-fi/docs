---
description: Linear interest accrual, bounded repayment, and uncapped versus collar settlement.
---

# Repayment and interest

## How interest accrues

A loan's rate is a full-term multiplier. At acceptance, LoanV2 computes the full-term target from actual principal and the rate, rounding up to a supplied atom. Full-term interest is that target less principal.

Accrued interest is full-term interest multiplied by elapsed seconds, capped at the term, divided by the term and rounded up. The repayment amount is principal plus accrued interest less accounted repayments.

For 1,000 supplied units at `1.1e18` over 30 days, the full-term target is 1,100. Repayment after 15 days is 1,050. In the acceptance block, only principal is due. Interest stops growing at maturity.

## Paying the current debt

Any payer can repay while the loan is Repaying or Expired. Each repayment pays the full current amount due. The loan pulls supplied assets from the payer and verifies the exact balance increase.

`repaymentDue` quotes the current amount. `repaymentDueAt` quotes a chosen timestamp using current loan accounting. The bounded repayment operation accepts a maximum amount and deadline, calculates the exact debt at execution, and reverts if either limit is exceeded. The parameterless repayment uses the same debt calculation with unrestricted amount and time bounds, subject to the payer's allowance.

A successful payment freezes `repaymentTarget` to principal plus the accrued interest paid. Subsequent repayment quotes return zero, including when a collar is still awaiting recovery.

## When payment completes the loan

For an uncapped loan, full repayment immediately settles the provider with zero debt and puts LoanV2 into Repaid. Retained collateral stays in the loan for borrower withdrawal, and lenders can withdraw their claims immediately. Unused PUT tokens remain in the position.

For a collar, repayment funds the lender pool and freezes interest. Final settlement still waits for maturity and a timestamp strictly after the CALL receipt's exercise deadline. CALL redemption then releases position assets for final allocation.

See [how loans end](../loans/how-loans-end.md) for settlement states and [events and integration](../operations/events-and-integration.md) for repayment allowances.
