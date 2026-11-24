---
description: How ERC-20 receipt transfers change refund and settlement ownership.
---

# Transferring claims

LoanToken is a transferable ERC-20 claim on one loan. A holder can transfer a receipt balance directly or authorize a spender using the token's allowance methods. The receiving address holds the corresponding refund or final payout rights.

## Claim ownership

Before acceptance, the current holder can refund while the order is Lending or Canceled. After acceptance, the holder participates in the actual lender pool once settlement is complete. Withdrawals use the holder's balance at execution.

A transfer changes receipt ownership while the loan's borrower, terms, maturity, and accounting remain the same. Any price paid for the transfer is separate from the loan's principal and repayment calculation.

## Reading a transferred claim

The relevant on-chain data is the loan's asset pair and terms, acceptance timestamp, current state, repayment target, and final shortfall when settled. The token's balance and current total supply determine a holder's share.

A receipt represents its share of the supplied payout pool. Residual borrower collateral and supplied surplus are allocated separately during [settlement](../loans/how-loans-end.md).
