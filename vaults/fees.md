---
description: How vault managers are compensated.
icon: percent
---

# Fees

Vaults support two fee types. The performance fee is the primary mechanism.

## Performance fee (primary)

A share of the **realised returns** from loan repayments.

* Calculated on each repayment event as a percentage of the **realised gain** (proceeds minus the vault's cost basis on that loan).
* Paid out to the manager in the **base asset** when the loan resolves.

{% hint style="success" %}
This aligns the manager with what the vault **actually earned**, not paper marks.
{% endhint %}

## Management fee (optional)

An **annual percentage of NAV**, set at vault creation. Accrues continuously.

* The vault **mints new vault tokens to the manager** equal to the accrued fee value at current NAV.
* Paying in tokens rather than base asset avoids any need to hold cash reserves for fee payment.
* Spreads the cost evenly across depositors regardless of when they entered.

{% hint style="warning" %}
**Fees on vault activity are deferred from MVP.** Performance fee and management fee structures are designed but not turned on in MVP. See [MVP scope](../roadmap/mvp-scope.md).
{% endhint %}

## Future: fee alignment with vault losses

In v1, performance fee is paid per repayment event and management fee tokens are claimable as minted, so a manager could collect fees on early successes before later defaults are realised.

v2 could add:

* **High-water mark** on performance fee, or
* **Vesting with slashing** on management fee tokens,

to keep the manager exposed to downside on pending compensation. See [Open items](../roadmap/open-items.md).
