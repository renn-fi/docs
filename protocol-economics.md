---
description: How the protocol earns. Early-stage monetisation is kept small.
icon: sack-dollar
---

# Protocol economics

Several revenue streams are possible. **Early-stage monetisation is kept small** to keep the system attractive to borrowers and competitive against other lending venues.

## Origination fee (main)

Around **0.25% of loan principal**, charged when the loan is funded.

* Comparable to typical on-chain transaction costs.
* Predictable baseline revenue.

## Swap and conversion fees

At maturity, borrowers often need to convert assets to repay the loan or reclaim collateral. The protocol can route those swaps through partner infrastructure and take a share of the swap fee (**around 0.25%**).

Recurring revenue tied to loan resolution.

## Collateral yield (optional)

If locked collateral is **restaked into other yield-generating protocols**, the protocol can take a share of that yield.

* Optional and configurable per vault. See [Vault rules → Restaking policy](vaults/vault-rules.md).
* Not part of the core design.

## Vault-level revenue

Possible share of vault activity (e.g. infrastructure fees). Secondary to [manager economics](vaults/fees.md).

## Later

### Native token

A protocol token may be introduced to:

* Subsidise lender yields.
* Fund liquidity programs.
* Align long-term participants.

{% hint style="info" %}
The token would **supplement** organic borrower-paid yield rather than replace it.
{% endhint %}

### Structured leverage products

See [Leveraged positions](roadmap/leveraged-positions.md).
