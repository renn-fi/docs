---
description: Automated allocation across all matching vaults, pro-rata.
icon: filter
---

# How vaults pick loans

A vault funds loans automatically against the [rules its manager set at creation](vault-rules.md). The selection is fully automated; the manager does not pick individual loans.

## Pro-rata allocation across matching vaults

When a loan matches the rules of **several vaults at once**, capital is allocated across them **pro-rata, not first-come-first-served**.

{% hint style="info" %}
This keeps vaults diversified and prevents any single vault from concentrating the most attractive loans.
{% endhint %}

## One-click loan creation

Because vault rules are **public on-chain**, interfaces can:

* Show borrowers **which vaults would match** a loan request.
* Suggest the **parameters (rate, term, size)** that would secure an instant match for the amount they want.

This allows one-click loan creation for borrowers, with funding already routed to matching vaults at the moment of activation.
