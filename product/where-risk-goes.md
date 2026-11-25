# Where risk goes

Each loan on Renn is a separate contract with its own collateral, its own put and its own lenders. Loans do not share a pool, and there is no protocol reserve. A problem in one loan affects only that loan's borrower and lenders.

The lender gives the full amount of the loan to the borrower. Pool lending protocols keep part of the deposits in reserve so that depositors can withdraw at any time. A loan on Renn has no such reserve. The lender cannot withdraw from the loan before maturity, but can sell the loan token.

## Risks by role

- **Borrower.** Pays the put premium. If a call was sold, the borrower does not receive the collateral's gains above the call price. If the loan is not repaid, the borrower loses collateral for the amount of the debt.
- **Lender.** Is repaid by the borrower, or from the collateral and the put. The lender can receive less than the full amount if settlement is sent after the put's window, or if the options venue does not deliver.

Renn does not hold lenders' or borrowers' funds and does not cover losses on loans.
