---
description: Anyone can create a vault. The creator is the manager.
icon: square-plus
---

# Creating a vault

Anyone can create a vault. The person who creates it is the **manager**. Each vault is one of two types:

{% tabs %}
{% tab title="Private" %}
Only **whitelisted wallets** can deposit. The manager controls the whitelist.

Private vaults are useful when a manager is running capital for a known set of LPs — institutional partners, an internal book, or an invited cohort.
{% endtab %}

{% tab title="Public" %}
**Open to outside depositors.** Anyone holding the base asset can deposit.

Public vaults rely on the vault token AMM and on-chain reputation to attract and retain capital.
{% endtab %}
{% endtabs %}

## Two-stage rollout

Public and private vaults launch in sequence:

{% stepper %}
{% step %}
### Stage 1, at launch: only private vaults work

We use this stage to observe the system under real flows. Public vault mechanics are designed but not yet enabled.
{% endstep %}

{% step %}
### Stage 2, after enough operational data: public vaults turn on

Once Stage 2 starts, a manager can **convert an existing private vault to public**.

The conversion is **one-way**; once a vault is public, it cannot be turned back into private. This stops a manager from accepting outside money and then shutting the door on those depositors.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
The AMM allocation for a vault is normally fixed at vault creation. At private-to-public conversion it is the **one rule that can be changed** — and only from the private-stage value to a public-stage level (typically increased to seed secondary liquidity). See [Vault rules → AMM allocation](vault-rules.md#amm-allocation).
{% endhint %}

## What's next

After deciding on the vault type, the manager configures the vault's [rules](vault-rules.md). These rules are set at creation and **cannot change afterward** (with the single exception above).
