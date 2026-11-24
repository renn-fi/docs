---
description: The accounting and lifecycle rules shared across protocol components.
---

# Core principles

## Fixed terms, explicit acceptance

The borrower, asset pair, requested amount, full-term rate, funding duration, and term are fixed for each loan. The borrower explicitly accepts the current funding. Accepted principal and retained collateral reflect the actual funded amount.

## Receipts determine lender ownership

Every supplied unit deposited mints one raw LoanToken unit. Refund and final payout rights follow the current receipt holder. Each withdrawal burns the holder's complete receipt balance.

## Protection opens with the loan

Hedge creation, premium funding, option execution, collateral placement, and principal disbursement occur in the acceptance transaction. If any required step fails, acceptance rolls back.

## Interest follows time outstanding

The rate describes the full term. Interest accrues linearly from acceptance and stops at maturity or full repayment. Repayment freezes the target at principal plus the accrued interest paid.

## Settlement allocates actual assets

The loan accounts for supplied repayments and measured recovery. Lenders receive the resulting supplied pool proportionally. The borrower receives supplied surplus and residual collateral. A shortfall is recorded when recovery is below the target.

## Authority follows contract roles

Factory owners control token admission and future provider selection. Personal vault owners control cash and funding criteria. Executors select eligible loans and funding amounts. Recorded providers and positions enforce their respective caller permissions throughout the lifecycle.

See [custody and permissions](../architecture/custody-and-permissions.md) for the contract boundaries.
