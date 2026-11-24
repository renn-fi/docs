---
description: Owner deposits, free cash accounting, and funding allowances.
---

# Depositing cash

## Owner deposit

The owner approves Vault to spend ASSET, then calls `deposit` with a positive amount. The vault pulls the funds and verifies that its ASSET balance increased by exactly the amount deposited.

`Deposited` records the amount. Cash stays in the vault until an executor funds a loan or the owner withdraws it.

## Free cash

`freeBalance` is the full current ASSET balance. Direct transfers to the vault also become owner cash and are included in that read. Deposits remain available while the vault is paused; pause governs new lending.

## Deploying cash

The executor funds loans using the vault's cash, subject to [funding criteria](vault-rules.md). Vault temporarily approves each loan for the selected amount, invokes its lending operation, and clears the allowance. LoanToken receipts are minted to Vault.

Refunds and final collections increase free cash for reuse or owner withdrawal. See [withdrawing and collecting](exiting-a-vault.md).
