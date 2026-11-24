---
description: Option opening, asset recovery, market execution, and PUT exercise decisions.
---

# Opening and recovery

## Opening an uncapped position

1. LoanFactory requests a GreekPut position from Hedging, which records the request and current execution fee.
2. LoanHedging pulls the borrower's positive premium budget into LoanV2 and grants a temporary supplied allowance to Hedging. The uncapped premium limit must be nonnegative.
3. Hedging obtains a route for the complete PUT amount, buys it through Prop within the budget, and transfers the tokens to GreekPut.
4. GreekPut activates its tracked option inventory. Unused premium cash returns through the loan to the borrower, and temporary allowances are cleared.

Retained collateral stays in LoanV2. Principal is disbursed as part of the same acceptance transaction.

## Opening a collar

1. Hedging creates GreekCollar and records the request and execution fee.
2. LoanHedging grants temporary allowances for retained collateral and any positive borrower premium budget.
3. Hedging obtains routes for the full covered CALL sale and protective PUT purchase, checking their signed net premium against the borrower's limit.
4. Hedging locks the loan's retained collateral in Greek, mints the covered CALL, sells the CALL tokens through Prop, and transfers writer receipts to GreekCollar.
5. Hedging buys the full PUT using borrower funding plus CALL proceeds, transfers PUT tokens to GreekCollar, and activates the position.
6. Hedging checks the actual net premium again and returns remaining cash through LoanV2 to the borrower. The loan clears allowances and sets its accounted collateral bucket to zero until recovery.

Quotes and execution use Hedging's Prop admission. Complete option fills and operation-specific balance checks are required. A failure rolls back acceptance, including any CALL mint or premium transfer.

## Recovery timing

Full repayment of an uncapped loan realizes it immediately with zero debt. The provider marks it realized; retained collateral remains in LoanV2, and unused PUT tokens stay in GreekPut.

Unpaid uncapped loans become eligible at maturity. Collars require maturity and a timestamp strictly after the CALL receipt's exercise deadline, including when repayment already covered the lender target.

## Recovery decisions

1. **Release position assets.** Hedging pulls the uncapped loan's approved collateral budget or redeems a collar's CALL writer receipt. It measures the assets attributable to this loan.
2. **Count supplied recovery first.** CALL cash reduces the debt still needing collateral recovery. If cash covers the debt or no collateral remains, assets return to the loan for allocation.
3. **Try exact-output market execution.** An upward-rounded oracle quote determines collateral needed for the remaining supplied debt, adjusted for the pinned pool fee. With an available PUT, the fee-adjusted quote must be better than the PUT conversion. Spending is bounded by available collateral, the PUT limit, and a 1% execution allowance.
4. **Exercise the PUT if needed and available.** Hedging budgets collateral against remaining debt and remaining PUT tokens. The position exchanges the approved amount through Greek and returns supplied cash to Hedging.
5. **Sell residual collateral if debt remains.** An exact-input sale uses an oracle-derived minimum after the pool fee and 1% allowance. If rounding produces a zero minimum, that collateral returns to the loan.
6. **Return recovery.** All newly recovered supplied assets and unused collateral go to the same LoanV2 for [final allocation](../loans/how-loans-end.md).

The exact-output attempt runs in a restricted external self-call. A failed attempt rolls back its approvals, transfers, swap, and output checks before another route is attempted. A failure in required CALL redemption, PUT exercise, or final liquidation rolls back the settlement transaction.

After the PUT deadline, collateral sales can still complete recovery using actual proceeds and a recorded shortfall. CALL redemption remains part of collar recovery. Each successful loan settlement realizes its provider position once.
