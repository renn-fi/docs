---
description: Two ways to acquire vault tokens.
icon: arrow-right-to-bracket
---

# Entering a vault

A new depositor has two ways to acquire vault tokens.

## Direct deposit at NAV

The depositor sends the base asset to the vault and receives vault tokens at **current NAV per token**. See [Vault tokens and NAV](tokens-and-nav.md).

* If a **redemption request is open at the same time**, the deposit is matched against it directly (peer transfer).
* Otherwise, the deposit **sits in the vault's base asset balance** until the vault funds new loans against it.

## Buy on the AMM

The depositor buys vault tokens from the [AMM pool](amm-liquidity.md) at market price.

{% hint style="info" %}
The AMM price can be **above or below NAV** depending on conditions. In stress, vault tokens typically trade at a discount.
{% endhint %}

## Planned: smart router

A smart router will automatically choose between the two entry paths.

If a new depositor wants to enter and there are active redemption requests at NAV that are **cheaper than the current AMM price**, the router matches them directly first, and only uses the AMM for the remainder.

This benefits both sides:

* The **new depositor** gets more vault tokens per dollar.
* The **redeemer** exits at NAV without paying the AMM spread.
