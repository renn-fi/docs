---
description: Questions still open for v1 and items deferred to v2 or later.
icon: clipboard-question
---

# Open items & future extensions

## Open questions for v1

### 1. TWAP oracle parameters

Window length, source aggregation, and minimum-confidence requirements for the LTV oracle (see [Where the price feed is used](../vaults/vault-rules.md#where-the-price-feed-is-used)).

{% hint style="info" %}
The cost to manipulate the oracle has to **exceed the harm it can do** — admitting one wrong loan into one vault.
{% endhint %}

### 2. Private-to-public conversion mechanics

The conditions and procedure for converting a private vault to public on Stage 2:

* AMM seeding.
* Liquidity bootstrap.
* Depositor onboarding.

To be detailed in a follow-up document.

## Deferred to v2 or later

### Maturity rollover edge case

What happens if the new loan in a [rollover](../repayment-and-exit/repayment.md#maturity-rollover) doesn't get funded by the original's maturity. Possible answers:

* A **grace period**.
* **Auto-funding from matching vault rules**.
* Letting **only part of the rollover** go through.

### Mark-to-market NAV

Conditions under which NAV could shift from accrued-based marking (see [Vault tokens and NAV](../vaults/tokens-and-nav.md)) to mark-to-market for some asset classes.

Needs:

* Reliable secondary liquidity.
* An oracle-free way to aggregate prices.

### Fee alignment with vault losses

In v1, [performance fee](../vaults/fees.md) is paid per repayment event and management fee tokens are claimable as minted, so a manager could collect fees on early successes before later defaults are realised.

v2 could add:

* **High-water mark** on performance fee, or
* **Vesting with slashing** on management fee tokens,

to keep the manager exposed to downside on pending compensation.
