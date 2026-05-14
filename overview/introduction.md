---
description: A high-level overview of how Renn Finance works.
icon: book-open
---

# Introduction

Borrowers stake BTC or ETH as collateral and take **fixed-term, fixed-rate loans** against it. There are no margin calls and no liquidations during the term. A loan has two possible outcomes at maturity: **repaid** or **in default**.

{% hint style="info" %}
**Default** in this documentation means the loan was not repaid by maturity. The protocol does not classify reasons.
{% endhint %}

## What happens at maturity

If the loan is repaid, the lender gets principal plus interest and the borrower gets their collateral back.

If it defaults, the lender chooses how to recover:

* **Trigger a DEX sale** through the contract. Proceeds cover principal first, then interest; any remainder goes to the borrower.
* **Take the collateral in-kind** at oracle price.

See [How loans end](../loans/how-loans-end.md) for the full mechanics.

## Loans, vaults, and the marketplace

Loans are issued as **transferable tokens**. They can be bought directly on the marketplace or via vaults.

**Vault managers** pool capital and allocate it into loans that match a fixed set of rules they declare at vault creation. Depositors put in a base asset (USDC at launch) and receive vault tokens representing their share.

A borrower can either open a new loan, or **refinance an existing position** from another lending protocol (Aave, Euler, or similar). Refinancing is a core feature, designed for borrowers who want to swap a variable-rate, liquidatable position for a fixed-rate, fixed-term one with no liquidations.

## What v1 includes

* Fixed-term loans against BTC and ETH, up to 50% LTV.
* Both fixed-rate and auction-based rate setting.
* Loan tokenisation and OTC secondary market for loan tokens.
* Vaults, both private (at launch) and public (Stage 2, see [Creating a vault](../vaults/creating-a-vault.md)).
* Vault token AMM for instant secondary exit.
* Refinancing of existing positions from Aave, Euler, and similar protocols.
* DEX-based collateral sale on default.

Coupon loans, maturity rollover, structured leverage, a native token, and additional collateral assets are planned for later. See the [Roadmap](../roadmap/mvp-scope.md).
