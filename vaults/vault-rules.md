---
description: What a manager configures at vault creation. Rules are immutable.
icon: list-check
---

# Vault rules

Vault rules are set at vault creation and **cannot change afterward**. The only allowed change is at private-to-public conversion, where the AMM allocation can be increased. A manager who wants different rules creates a new vault.

## The rules

* **Type.** Private or Public. Private vaults can be converted to public (one-way) once Stage 2 starts. See [Creating a vault](creating-a-vault.md).
* **Lifetime.** Fixed-term or open-ended.
* **Collateral type.** BTC or ETH at launch.
* **LTV range.** The minimum and maximum loan-to-value the vault will accept.
* **Rate range.** The yields the vault will fund at.
* **Term range.** The shortest and longest loan duration.
* **Restaking policy.** Whether locked collateral can be restaked into other protocols (e.g. Aave), and which venues are allowed.
* **Position-size limit** _(planned for later)._ The maximum a vault can put into a single loan.
* **Asset-exposure limit** _(planned for later)._ A cap on how much of a vault can be in one collateral type.
* **Funding freeze** _(optional)._ See below.
* **AMM allocation.** Share of vault capital seeded into the AMM pool. See below.

## Funding freeze

A delay between vault acceptance and funding activation, during which the loan is **on hold** (capital reserved, not sent).

* The manager sets any duration **at or above the protocol minimum** (default 0 at launch).
* During the freeze, the **vault manager** can cancel funding from their own vault.
* **Protocol owners** can cancel system-wide if an oracle issue is detected.
* If no cancellation happens, funding activates normally.
* The freeze applies only to **automated, oracle-driven funding**; direct lender funding skips it.

{% hint style="warning" %}
The funding freeze is **deferred from MVP**. The protocol minimum stays at 0, and managers do not configure individual freezes during MVP. See [MVP scope](../roadmap/mvp-scope.md).
{% endhint %}

## AMM allocation

Share of vault capital seeded into the AMM pool (see [AMM liquidity](amm-liquidity.md)). Sets the trade-off between:

* **Secondary liquidity** for the vault token, and
* **Base asset available for direct redemption**.

Typical values:

* **\~5%** for public vaults.
* **0%** for private vaults — whitelisted participants typically don't need on-chain secondary liquidity.

## Immutability

These rules are set at vault creation and cannot change afterward. The only allowed change is at **private-to-public conversion**, where the AMM allocation can be increased from its private-stage value to a public-stage level. A manager who wants different rules creates a new vault.

## Where the price feed is used

The protocol uses a **TWAP oracle** (a time-weighted average across multiple price sources) for LTV. It is read in two contexts, both with isolated risk:

{% columns %}
{% column %}
### At loan admission

When a loan is created, the contract records the LTV. When a vault is checking whether a loan matches its rules, it reads the same TWAP.
{% endcolumn %}

{% column %}
### At default recovery

On the **take-at-oracle** path (see [How loans end](../loans/how-loans-end.md)), the same TWAP determines how much collateral covers (principal + interest).

After a take-at-oracle, while seized collateral sits in the vault as a non-cash asset, NAV values it via the same TWAP. See [Defaulted loans inside a vault](../vault-health/defaulted-loans.md).
{% endcolumn %}
{% endcolumns %}

{% hint style="success" %}
The oracle **never** marks live loans, **never** triggers liquidations, and **never** moves money on its own. The lender, not the oracle, decides when and how to recover.
{% endhint %}

### Why this is not a systemic risk

* **At admission**, the worst manipulation can do is admit one mispriced loan into one vault. The harm is bounded to that vault, against that loan.
* **At recovery**, the loan is already in default; the borrower had the full term to repay and chose not to. Any oracle drift at recovery affects the split between the lender's take and the borrower's remainder on that loan only. The harm cannot cascade.

The TWAP window and source aggregation are set so that manipulation costs more than the harm it can do. Vault rules include sanity bounds (e.g. minimum implied collateral price) to reject wildly off oracle output.
