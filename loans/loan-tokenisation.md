---
description: Transferable lender claims, receipt units, burns, and proportional payouts.
---

# Loan receipts

Each LoanV2 deploys a dedicated LoanToken. A funding deposit mints receipts to the lender; only that loan can mint and burn them. The current holder owns the refund or final settlement claim.

## Amounts and display

Receipt minting uses raw supplied units one-for-one. Funding 100 USDC with six decimal places mints 100,000,000 raw receipt units. LoanToken reports the ERC-20 default of 18 display decimals, so applications should interpret the claim quantity using the supplied token's decimals.

LoanTokenEmitent's `emission` records cumulative minting. Current outstanding claims use LoanToken's `totalSupply`, which decreases when receipts are burned.

## Claim lifecycle

Before acceptance, a receipt holder can refund while the order is Lending or Canceled. The loan burns the holder's complete balance and returns the corresponding supplied funding.

After acceptance, receipts participate in the final lender pool. Once the loan is Repaid, a holder withdraws its share of the remaining pool, calculated from its receipt balance and the remaining total supply, rounded down. The loan burns that complete receipt balance. As the pool and supply shrink together, the final holder receives any rounding remainder.

Receipt burns during refunds and withdrawals are performed by LoanV2 and require the holder to call that loan. A separate receipt-token allowance is unnecessary.

## Transfers

LoanToken uses ordinary ERC-20 transfers and allowances. A recipient acquires the lifecycle claim represented by the transferred balance. The final payout is in the loan's supplied asset and depends on the actual settled pool.

See [transferring claims](../repayment-and-exit/secondary-market.md) and [settlement](how-loans-end.md).
