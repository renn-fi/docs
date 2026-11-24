---
description: Loan terms, token admission, collateral escrow, and order registration.
---

# Loan creation

## Loan terms

A borrower proposes a loan with fixed terms:

| Field | Meaning |
| --- | --- |
| `borrower` | Address authorized to accept and cancel, and recipient of borrower withdrawals |
| `collateral` and `collateralAmount` | ERC-20 collateral and initial escrow in native units |
| `supplied` and `amountToBorrow` | Supplied ERC-20 and maximum aggregate funding |
| `rate` | Full-term repayment multiplier, scaled by `1e18` |
| `orderCancelation` | Funding duration in seconds from order activation |
| `term` | Loan duration in seconds from acceptance |

Construction requires distinct assets, positive collateral and requested amounts, positive durations, a rate of at least `1e18`, and valid arithmetic bounds. The supplied and collateral tokens must also be admitted for their respective roles in LoanFactory.

## Creation flow

1. The borrower approves LoanFactory to spend the initial collateral.
2. The borrower calls `createLoan` with the terms and receipt token name and symbol. The caller must equal the terms' borrower.
3. The factory deploys LoanV2, which creates its dedicated LoanToken.
4. The factory transfers collateral directly from the borrower to LoanV2 and verifies the exact balance increase.
5. LoanV2 accounts for the collateral, records `createdAt`, and enters Lending. Any collateral balance above the stated initial amount is returned to the borrower.
6. LoanFactory records `isLoan` and emits `LoanCreated` with the loan, borrower, and receipt addresses.

The order can now receive [funding](funding.md). The borrower chooses when to accept the available positive funding before the order deadline. Actual principal is established at acceptance.

Token admission and executable hedge markets are separate configuration steps. [Configuration](../infrastructure/configuration.md) explains their roles.
