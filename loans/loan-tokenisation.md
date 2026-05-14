---
description: Each loan position is a transferable token.
icon: coins
---

# Loan tokenisation

Each loan position is a **transferable token**. The token records:

* A claim on **principal** and **interest**.
* The **maturity date**.
* A **reference to the underlying collateral**.
* **Accrued interest**.

## What accrued interest means

Accrued interest is the share of the loan's total interest that has built up since the loan started, **prorated by elapsed time**. This is the same idea as accrued coupon in a bond.

It is used in two places:

{% columns %}
{% column %}
### Secondary-market pricing

A buyer pays a **clean price plus accrued interest** — the same convention bond markets use.

See [Clean and dirty pricing](../repayment-and-exit/secondary-market.md#clean-and-dirty-pricing-for-loan-tokens).
{% endcolumn %}

{% column %}
### Vault NAV

A vault marks each loan token it holds at the **price the vault paid plus accrued interest** from that point.

See [Vault tokens and NAV](../vaults/tokens-and-nav.md).
{% endcolumn %}
{% endcolumns %}

## Why this matters

Because each loan position is a token, it can move freely:

* Direct lenders can sell their position on the OTC secondary market.
* Vaults can buy loan tokens at a discount on the secondary market and accrue them at a higher implied yield.
* When a loan token is split across multiple holders, each holder can independently choose how to recover on default. See [How loans end](how-loans-end.md).
