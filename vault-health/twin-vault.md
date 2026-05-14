---
description: Planned mechanism to rotate active depositors out of a vault that's accumulated stressed loans.
icon: clone
---

# Twin vault

{% hint style="warning" %}
The twin vault mechanism is **planned for a later version**. It is not part of v1. Full mechanics will be specified in a follow-up document once operational data shows that secondary-market sorting alone is insufficient.
{% endhint %}

## The problem it solves

The twin vault is the planned mechanism for the **lemon problem in NAV pricing** (see [Vault tokens and NAV](../vaults/tokens-and-nav.md)).

When a vault accumulates stressed loans, depositors face a choice:

* **Exiting** — via pro-rata in-kind redemption that delivers them the stressed exposure.
* **Staying** — and accepting that incoming capital may dilute their share.

Neither is attractive.

## How it works

The twin spawns a **fresh vault under the same rules**.

* Incoming repayments from the original **auto-migrate into the twin**, rotating active depositors' exposure into a clean book without manual action.
* The original keeps **honouring redemptions** but funds no new loans.

This achieves the rotation a manager would otherwise do by opening a new vault and asking depositors to migrate themselves.

## Status

Not part of v1. The mechanism is documented in concept here; specification will follow once operational data justifies it.
