---
description: Owner-controlled cash accounts with delegated lending and on-chain funding criteria.
---

# Personal vaults

A Vault holds one owner's cash in a single ERC-20 ASSET and retains receipts for the loans it funds. A designated executor chooses funding amounts and submits lending transactions. The vault enforces the owner's criteria against each proposed loan's on-chain terms.

VaultFactory creates the instance, makes the caller its owner, and registers it for discovery. Each vault fixes its asset, LoanFactory, executor, and creating factory at deployment.

## Asset cycle

1. The owner deposits ASSET into the vault.
2. The executor funds an eligible registered loan using vault cash.
3. LoanV2 mints receipts to the vault, which holds them throughout the loan lifecycle.
4. The owner or executor refunds an unaccepted order or collects a settled claim.
5. Returned cash can be invested again or withdrawn by the owner.

The owner controls idle cash, rate and term criteria, collateral admission, and pause status. Funding is reserved to the fixed executor; an owner can fund when that owner is also the designated executor.

## Cash and claims

`freeBalance` reports the vault's current ASSET balance, including direct transfers. LoanToken balances identify its claims on individual loans. Refund and collection pay into the vault. Owner withdrawals pay idle cash to the current owner.

Continue with [creating a vault](creating-a-vault.md), [funding criteria](vault-rules.md), and [loan selection](loan-selection.md).
