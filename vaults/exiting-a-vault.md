---
description: Idle-cash withdrawals, order refunds, settlement, and collection.
---

# Withdrawing and collecting

## Withdraw idle cash

Only the owner can withdraw ASSET, with a positive amount at most `freeBalance`. The transfer goes to that owner. Outbound payment uses SafeERC20, so net receipt follows the asset's transfer behavior.

Cash already funded into a loan returns through that loan's lifecycle before it becomes idle vault cash again.

## Refund an unaccepted order

The owner or executor calls Vault's `refund` while LoanV2 is Lending or Canceled. Vault checks registration and supplied-asset identity, then calls LoanV2's refund. The loan burns all receipts held by Vault and returns supplied funding to it.

Vault reports the actual ASSET balance increase in `LoanRefunded`. A transfer fee can reduce that net receipt, including to zero, while the receipt claim is closed.

## Collect a settled claim

The owner or executor calls `collect` once LoanV2 is Repaid. Vault calls the loan's lender withdrawal, burns its complete receipt position, and receives its portion of the supplied pool. `LoanCollected` reports the actual balance increase, including zero for a fully impaired claim.

Full repayment of an uncapped loan enables immediate collection. Other accepted loans first need a successful settlement transaction. Any caller, including the executor, may invoke LoanV2's public settlement when timing conditions are satisfied. An option-backed collar also waits for CALL redemption eligibility.

## Changes to funding rules

Refund and collection remain available while the vault is paused, after criteria changes, or after a collateral is removed. They validate the pinned registry and supplied asset and rely on the loan's lifecycle for payout eligibility.

Recovered assets remain in Vault until the owner withdraws or the executor funds another eligible loan.
