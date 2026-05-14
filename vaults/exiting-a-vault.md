---
description: Four ways out of a vault position.
icon: arrow-right-from-bracket
---

# Exiting a vault position

A depositor has four ways to exit.

## Sell on the AMM

Fastest path. The depositor sells their vault token on the [AMM](amm-liquidity.md) and gets the base asset immediately at whatever price the market is offering.

{% hint style="info" %}
The AMM price can be above or below NAV depending on conditions; in stress it trades at a discount.
{% endhint %}

## Inflow matching

When a **redemption request lines up with a new deposit**, the protocol settles them against each other at NAV:

* The **new depositor** pays in the base asset.
* The **redeemer** receives it.
* The redeemer's vault tokens transfer to the new depositor.

The vault's holdings and total vault-token supply don't change; the vault acts as **escrow**.

## Pro-rata in-kind redemption

The default path when neither AMM exit nor inflow matching applies.

The depositor's vault tokens are burned and they get their **proportional slice of every vault asset** at the moment of redemption:

* Base asset balance.
* Each loan token the vault holds (including defaulted ones not yet sold).
* The vault's AMM share.

{% hint style="warning" %}
The slice is **in-kind** — the redeemer cannot cherry-pick the liquid parts. Healthy loans tend to find buyers via OTC; stressed loans either sit with the redeemer or sell at a deeper discount.
{% endhint %}

## Hold to vault maturity

For **fixed-term vaults**, a depositor can simply hold their vault token until the vault winds down.

* At maturity, all loans have either been repaid or resolved via DEX sale.
* The vault distributes its remaining balance pro-rata to vault token holders and closes.
* **No action required** from the depositor.
