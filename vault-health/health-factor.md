---
description: A signal for users. Nothing in the protocol depends on it.
icon: heart-pulse
---

# Health factor

Every vault shows a **health factor (HF)**.

{% hint style="info" %}
HF is computed **off-chain by the interface**. It is a **signal for users only**.

Nothing in the protocol depends on it. There are no liquidations triggered by it, no state changes, and no money movement. The interface uses any reliable price source (CEX aggregators, public market data) to compute it; since no protocol value is at stake, this is fine.
{% endhint %}

## How it's calculated

For each active loan:

$$
drawdown = \max\left(0,\ 1 - \frac{current\_collateral\_value}{collateral\_value\_when\_loan\_was\_issued}\right)
$$

Upside above the issuance price doesn't count.

A loan is **"stressed"** if drawdown is at or above **20%**.

$$
Vault\ HF = 100\% - \frac{capital\ in\ stressed\ loans}{total\ capital\ in\ active\ loans}
$$

## What HF tells you

HF only goes down when things get worse; it doesn't reward upside. A single number tells you what share of the vault's book is at risk.

| Drawdown level     | What it means                                                                                                                                  |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **At 50%**         | With the 50% LTV cap, collateral roughly covers the principal but the **interest portion is already impaired** (LTV is measured on principal only). |
| **Beyond 50%**     | **Principal itself is at risk.**                                                                                                               |

{% hint style="warning" %}
The **health factor UI is deferred from MVP**. It can be added off-chain at any time; it is not a launch requirement. See [MVP scope](../roadmap/mvp-scope.md).
{% endhint %}
