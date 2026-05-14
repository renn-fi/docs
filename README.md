---
description: >-
  Renn Finance is a fixed-term, fixed-rate lending protocol with no margin
  calls and no liquidations during the loan term.
icon: hand-wave
---

# Welcome to Renn Finance

Renn Finance is a protocol for **fixed-term, fixed-rate loans** against BTC and ETH collateral. Borrowers lock collateral up front and take loans they can rely on: no margin calls, no liquidations during the term, and no surprise rate changes. Lenders fund loans directly or through vaults that pool capital and allocate it under rules set at vault creation.

{% hint style="info" %}
This documentation reflects the **v1 protocol specification**. Features explicitly marked _planned_ or _later_ are documented for context but are not part of the launch release. See [MVP Scope](roadmap/mvp-scope.md) for what ships first.
{% endhint %}

## Where to start

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4>Overview</h4></td><td>What Renn is and the principles that shape it.</td><td></td><td><a href="overview/introduction.md">introduction.md</a></td></tr><tr><td><h4>Loans</h4></td><td>How loans are created, funded, tokenised, and resolved.</td><td></td><td><a href="loans/loan-lifecycle.md">loan-lifecycle.md</a></td></tr><tr><td><h4>Vaults</h4></td><td>How vaults pool capital and allocate it into loans.</td><td></td><td><a href="vaults/introduction.md">introduction.md</a></td></tr><tr><td><h4>Marketplace &#x26; Pricing</h4></td><td>How loan rates are discovered and how the marketplace works.</td><td></td><td><a href="marketplace/rate-setting.md">rate-setting.md</a></td></tr><tr><td><h4>Stress scenarios</h4></td><td>How the protocol behaves under market stress.</td><td></td><td><a href="stress-scenarios.md">stress-scenarios.md</a></td></tr><tr><td><h4>Roadmap</h4></td><td>What launches first and what comes next.</td><td></td><td><a href="roadmap/mvp-scope.md">mvp-scope.md</a></td></tr></tbody></table>

## What v1 includes

* Fixed-term loans against BTC and ETH, up to **50% LTV**.
* Both fixed-rate and auction-based rate setting.
* **Loan tokenisation** and an OTC secondary market for loan tokens.
* **Vaults**, both private (at launch) and public (Stage 2).
* **Vault token AMM** for instant secondary exit.
* **Refinancing** of existing positions from Aave, Euler, and similar protocols.
* DEX-based collateral sale on default.

Coupon loans, maturity rollover, structured leverage, a native token, and additional collateral assets are planned for later. See the [Roadmap](roadmap/mvp-scope.md) and [Open Items](roadmap/open-items.md).

## Download the spec

{% file src=".gitbook/assets/renn-finance-spec-v1.pdf" %}
Renn Finance: Protocol Design Specification, v1
{% endfile %}
