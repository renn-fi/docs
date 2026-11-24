---
description: Checks enforced before executor-selected funding enters a loan.
---

# How vaults fund loans

The executor selects a loan and funding amount. Vault validates eligibility in the funding transaction using current contract state.

## Validation sequence

1. Verify that the caller is EXECUTOR, the vault is active, and the amount is positive.
2. Check the proposed address in the pinned LoanFactory's `isLoan` registry before calling that loan.
3. Read the loan terms and require that its supplied token equals ASSET.
4. Require permitted collateral, a rate at least `minRate`, and a term within the inclusive configured range.
5. Require sufficient idle cash.
6. Approve the loan for the selected amount, call its lending operation, and clear the allowance.

LoanV2 enforces its current Lending state, remaining order capacity, and exact receipt of funding. Receipts are minted to the vault.

## Repeated and partial funding

The executor may fund part of an order and add more while it remains eligible. Every transaction checks the then-current owner criteria and loan state. A stale off-chain selection therefore cannot bypass a newly changed rule.

The maximum usable amount is constrained by free cash and the loan's remaining funding capacity. Actual accepted principal is established later by the borrower.

See [funding and acceptance](../loans/funding.md) for the loan side and [withdrawing and collecting](exiting-a-vault.md) for recovery.
