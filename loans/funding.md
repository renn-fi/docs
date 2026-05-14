---
description: How loan requests get filled by direct lenders or vaults.
icon: hand-holding-dollar
---

# Funding

Loan requests are listed on a marketplace. Lenders fund them either directly or through vaults. A single request can be:

* **Filled by a single lender** for the full amount, or
* **Split across several lenders**.

## Direct funding

Any wallet can fund a loan directly from the marketplace. The lender picks the loan, sends the funding amount, and receives loan tokens in return. See [Loan tokenisation](loan-tokenisation.md).

## Vault funding

A vault funds loans automatically based on its rules. Depositors deposit the vault's base asset and receive vault tokens; the vault holds the resulting loan tokens on their behalf.

See [Vaults](../vaults/introduction.md) for the full mechanics.

## Funding outcomes

{% tabs %}
{% tab title="Threshold reached" %}
The loan **activates**. The borrower receives the funds and lenders receive a token representing their share of the loan.
{% endtab %}

{% tab title="Threshold not reached" %}
The loan **does not activate**. The borrower's collateral is unlocked and returned.
{% endtab %}

{% tab title="Borrower withdraws collateral" %}
If the borrower withdraws their collateral before activation, the loan request **closes**. Any lenders who had already staked funds get them back.
{% endtab %}
{% endtabs %}

## How vaults and direct funding interact

* When a loan matches the rules of several vaults at once, capital is allocated across them **pro-rata**, not first-come-first-served. This keeps vaults diversified and prevents any single vault from concentrating the most attractive loans.
* Direct lender funding **skips the funding freeze** (if configured by a vault). The freeze applies only to automated, oracle-driven funding. See [Vault rules → Funding freeze](../vaults/vault-rules.md#funding-freeze).
