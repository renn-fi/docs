---
description: Collateral admission, proportional retention, custody, and borrower withdrawals.
---

# Collateral

## Token admission

LoanFactory's collateral whitelist determines the tokens available for new orders. Consideration tokens have a separate whitelist. An order pairs an admitted collateral token with a distinct admitted consideration token.

Existing loans retain their asset pair when token admission changes. A loan's fixed collateral amount establishes its initial escrow; the borrower transfers it before funding begins.

## Acceptance and proportional retention

The borrower can accept partial funding. LoanV2 retains initial collateral multiplied by actual funding divided by the requested amount, rounded up to a collateral atom. The remaining collateral is returned during acceptance.

For example, one collateral token backing a request for 1,000 supplied units becomes 0.4 retained collateral when the borrower accepts 400 units. The other 0.6 returns to the borrower.

For uncapped protection, retained collateral stays in LoanV2. For a collar, Hedging locks it as covered CALL backing in Greek and gives the position its writer receipts. See [hedging positions](../hedging/positions.md).

## Returning collateral

If an order is canceled explicitly or expires before acceptance, `refundBorrower` releases its accounted collateral to the fixed borrower. Lender refunds are independent and can happen before or after this release.

After final settlement, `withdrawBorrower` releases remaining accounted collateral and supplied surplus. Any caller can trigger either borrower release, while the destination remains the borrower stored in the terms.

Settlement allocates the collateral remaining after position recovery and required sales. The [settlement flow](how-loans-end.md) explains how those assets are calculated.
