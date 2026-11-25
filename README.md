---
description: Fixed-term, fixed-rate loans with no liquidations during the term.
---

# Welcome

Renn is a lending protocol for crypto and tokenized real-world assets. Borrowers take loans for a fixed term at a fixed rate. Lenders fund these loans and earn interest.

Its first product is a loan against collateral with no liquidations during the term. The lender is protected by a put option. The borrower can take a lower rate in exchange for a cap on the collateral's gains. Lenders fund these loans through a public tokenized vault or a private one.

**What the v0.1 private beta includes**

- The borrower posts an order with the collateral, amount, term and rate.
- Fixed-term, fixed-rate loans against ERC-20 collateral.
- Every loan is hedged with a put at the price that covers the loan plus the interest for the term. The borrower can also sell a call at a price above the current one, to cap the collateral's gains and get a lower rate.
- Repayment in full, at maturity or earlier. If the loan is not repaid, it is settled from the collateral and the put.
- The lender's claim is a transferable loan token.
- Private vaults. The lender deposits once, and the vault funds every loan that matches its parameters.
- Public tokenized vaults with secondary liquidity are coming soon.
