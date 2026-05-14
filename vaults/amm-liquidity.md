---
description: The vault token AMM pairs vault tokens against the base asset.
icon: chart-pie
---

# AMM liquidity

A configured share of vault capital (set in the [vault's rules](vault-rules.md#amm-allocation)) goes into an **AMM pool** so the vault token can trade on the secondary market.

## How the pool works

* The pool pairs the vault token against the base asset (for example, `rnVault/USDC`).
* The vault supplies **both sides**; the position belongs to depositors pro-rata.
* The pool's share is part of NAV. See [Vault tokens and NAV](tokens-and-nav.md).

{% hint style="info" %}
**Loan tokens do not trade on the AMM.** They trade OTC. See [Exit options](../repayment-and-exit/exit-options.md).
{% endhint %}

## The allocation trade-off

How much capital to allocate to the AMM is a trade-off:

{% columns %}
{% column %}
### More allocation

* **Tighter spreads** on the vault token.
* **Better instant exit** for depositors.
{% endcolumn %}

{% column %}
### Less allocation

* **More base asset** sitting in the vault.
* **Available directly for redemptions** at NAV.
{% endcolumn %}
{% endcolumns %}

Typical values:

* **\~5%** for public vaults.
* **0%** for private vaults — whitelisted participants don't typically need on-chain secondary liquidity.

{% hint style="warning" %}
AMM liquidity for vault tokens is **deferred from MVP**. Vaults at MVP stage do not seed AMM pools. See [MVP scope](../roadmap/mvp-scope.md).
{% endhint %}
