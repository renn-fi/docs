---
description: How a vault handles loans that don't repay.
icon: triangle-exclamation
---

# Defaulted loans inside a vault

When a loan in a vault defaults, the manager has two ways to handle it. These are the same recovery paths described in [How loans end](../loans/how-loans-end.md), applied at the vault level.

## DEX sale

The collateral is sold on a supported DEX immediately. The vault receives the base asset:

1. **Principal** first.
2. **Interest** next.
3. **Any remainder** goes to the borrower.

## Take collateral

The vault takes the collateral at oracle price. It enters the vault as a **non-cash asset**.

* The manager can later sell it via a DEX sale at their discretion; proceeds go into the vault's base asset balance.
* While the collateral sits in the vault, it is **valued in NAV via the same TWAP oracle** used at origination. See [Where the price feed is used](../vaults/vault-rules.md#where-the-price-feed-is-used).

## Before recovery is triggered

Until the manager triggers either path, the defaulted loan token **sits in the vault as a non-cash asset**.

Anyone redeeming during this window receives their **pro-rata share of it in-kind**. That depositor can then trigger the recovery themselves on the part they hold. See [Exiting a vault → Pro-rata in-kind redemption](../vaults/exiting-a-vault.md#pro-rata-in-kind-redemption).

## The manager's discretion is bounded

The manager's only discretion is **timing** and **choice of path**. They **cannot**:

* Mark or value the collateral.
* Hold it indefinitely outside the redemption slice.
* Move it outside the vault.

{% hint style="info" %}
Manager actions are public on-chain. Past behaviour becomes part of the vault's reputation and informs future depositors.
{% endhint %}
