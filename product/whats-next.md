# What's next

## Closing the hedge

First in line is the sale of the put on repayment. The loan will sell the put when the debt is repaid, and the proceeds will go to the borrower.

Next is the call. On repayment the loan will buy the call back, so the collateral is released at once. The same buyback changes how the call is settled when the collateral price is above the call price. It should cost the borrower only the difference, not the whole collateral. Each options venue needs its own solution for this. On the current venue the loan will buy the call back from its holder and pay the difference by selling part of the collateral. The borrower keeps the rest.

We also want the borrower to be able to buy the call back at any point during the term. The borrower pays for the buyback with new funds, not from the collateral. A borrower with no open call will be able to sell one during the term and earn the premium. This must not weaken the lender's protection, and the design is not final.

## Rate

Today Renn sets the rate. It will be set by the market, from two sides.

The first side is a reference rate with three parts.

- **Base rate.** A weighted median of borrow rates in onchain lending pools, smoothed over a published window.
- **Term premium.** Longer terms pay more.
- **Liquidity premium.** The lender's capital is locked until maturity, and the lender is paid for this.

The second side is the lender's offer. Each vault or lender adds its own spread on top. The spread is higher when most of the capital is lent out and lower when capital is idle. The borrower gets the best rate offered for the chosen term.

## Refinancing

A borrower will be able to move a loan from Aave or Morpho to Renn in one transaction.

## Tokenized vaults

A public vault will take deposits from anyone, and its share is a vault token. The token gives the lender liquidity. The lender can sell the vault token on a DEX, while the vault itself earns the fixed rate of long-term loans.
