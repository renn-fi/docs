---
description: Available asset recovery actions for borrowers, lenders, and vault owners.
---

# Exit paths

## Before acceptance

A receipt holder can refund its full current balance while the order is Lending or Canceled. LoanV2 burns the receipts and returns the corresponding supplied funding.

The borrower can cancel an active order before its deadline. Once the order is Canceled, accounted collateral can be released through `refundBorrower`. The supplied and collateral refunds are independent.

## After acceptance

A payer can repay the full current debt using supplied assets. Uncapped repayment immediately enables final lender and borrower withdrawals. Collar repayment freezes interest and funds the loan, while recovery waits for its settlement timing.

At maturity, the loan can settle through its pinned provider. After allocation completes, receipt holders withdraw supplied payouts, and borrower assets are released to the borrower.

Receipts remain transferable through their ERC-20 methods. Transferring a claim passes its refund or settlement rights to the recipient. See [transferring claims](secondary-market.md).

## Personal vault cash

A vault owner can withdraw idle ASSET held by the vault. Funding in an unaccepted loan returns through Vault's refund operation, and a settled claim returns through collection. Both return cash to the vault before an owner withdrawal.

See [withdrawing and collecting](../vaults/exiting-a-vault.md) for the personal vault cycle.
