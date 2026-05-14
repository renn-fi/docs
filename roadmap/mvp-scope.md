---
description: A launch surface small enough to ship, audit, and observe in production before expanding.
icon: rocket-launch
---

# MVP scope

The MVP narrows the v1 spec to a launch surface small enough to ship, audit, and observe in production before expanding. Everything below is from earlier in the documentation; this is just the cut.

## In MVP

* **Peer-to-peer loans.** Borrower creates a request through the marketplace; any wallet can fund directly. BTC and ETH as collateral. 50% LTV cap, principal-only. See [Loan creation](../loans/loan-creation.md) and [Funding](../loans/funding.md).
* **Fixed-rate only.** Borrower defines the rate at creation. The [price-based auction](../marketplace/auction.md) is not in MVP.
* **Tokenised loans, transferable.** OTC secondary market between holders and other vaults. See [Loan tokenisation](../loans/loan-tokenisation.md).
* **Refinancing from Aave.** Single source for v0. Euler and similar protocols added later. See [Refinancing](../loans/refinancing.md).
* **Bullet repayment, early repayment with full make-whole, sale-driven closure.** See [How loans are repaid](../repayment-and-exit/repayment.md).
* **Default recovery: DEX sale and take-at-oracle.** With per-holder pro-rata when a loan is split. See [How loans end](../loans/how-loans-end.md).
* **Private vaults only.** Whitelist-controlled. Rules immutable at creation. Auto-funding, NAV via effective-yield amortization, pro-rata in-kind redemption. **No AMM** at private stage. **Inflow matching** mechanically available but rarely meaningful without continuous deposit flow.

## Not in MVP (per spec, deferred)

* Price-based [auction rate discovery](../marketplace/auction.md).
* **Public vaults** and [private-to-public conversion](../vaults/creating-a-vault.md#two-stage-rollout).
* [AMM liquidity for vault tokens](../vaults/amm-liquidity.md). Vaults at MVP stage do not seed AMM pools.
* Refinancing from Euler and other protocols beyond Aave.
* [Twin vault mechanism](../vault-health/twin-vault.md).
* [Health factor UI](../vault-health/health-factor.md). Can be added off-chain at any time; not a launch requirement.
* [Fees on vault activity](../vaults/fees.md). Performance fee and management fee structures are designed but not turned on in MVP.
* [Funding freeze](../vaults/vault-rules.md#funding-freeze). Protocol minimum stays at 0; managers do not configure individual freezes during MVP.
* [Coupon loans, maturity rollover](../repayment-and-exit/repayment.md#planned-for-v2).
* [Native token, structured leverage](../protocol-economics.md#later).

## What MVP demonstrates

**Fixed-rate, fixed-term lending against BTC/ETH** with tokenised loans, refinancing from Aave, and a **single-manager-curated private vault** to validate vault mechanics with a known, bounded set of depositors.

Everything else in the spec is the **documented expansion path** once MVP holds up in production.
