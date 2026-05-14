---
description: How the protocol behaves under three illustrative market stress scenarios.
icon: cloud-bolt
---

# Stress scenarios

The protocol is designed to absorb stress through **market participation, not protocol intervention**. The three scenarios below show what happens — and what doesn't have to happen — when conditions deteriorate.

## Scenario 1: BTC/ETH falls 50%

{% tabs %}
{% tab title="Borrower" %}
With the collateral worth roughly the same as the loan, repaying may not make economic sense. **Many borrowers will default**, meaning they simply won't repay.
{% endtab %}

{% tab title="Lender" %}
After maturity, the lender can trigger recovery (DEX sale or take-at-oracle, see [How loans end](loans/how-loans-end.md)).

* The lender takes principal plus interest; the borrower takes the remainder if any.
* **If the collateral isn't worth enough to cover the loan, the lender takes everything and absorbs the shortfall as a loss.**
{% endtab %}

{% tab title="Vault" %}
* **Isolated defaults** are absorbed by diversification.
* **A broad decline** pushes the [health factor](vault-health/health-factor.md) past its threshold. At that point the manager can stop funding new loans. Defaults are handled per [Defaulted loans inside a vault](vault-health/defaulted-loans.md).
{% endtab %}
{% endtabs %}

## Scenario 2: Interest rates rise sharply

New loans are now issued at higher yields. Existing fixed-rate loans look less attractive by comparison.

What happens:

* **Loan tokens trade at a discount on OTC.** The dirty-price reference doesn't change, but actual trades clear below it because buyers want higher yield.
* **Vault tokens trade at a discount on the AMM.** NAV stays put (it's accrued-based, see [Vault tokens and NAV](vaults/tokens-and-nav.md)), but the market price reflects the now-relatively-low yield of the existing book.
* **Inflow matching dries up** where the discount is meaningful. Rational new depositors prefer the AMM (more vault per dollar) over peer matching at NAV.
* **Managers cannot change the rules of existing vaults.** They can launch new vaults under new rules. Capital that wants the new yields rotates into them through normal funding.

{% hint style="success" %}
**Nothing in the protocol has to react.** The yield gap is a market signal, and capital reallocates across vault generations on its own.
{% endhint %}

## Scenario 3: Many lenders exit at once

Direct lenders list their loan tokens on OTC. Healthy ones get picked up by vaults whose rules match; the price is whatever the market clears at.

Vault depositors pick between:

* **Selling on the AMM** (immediate base asset payout, at the discount the market is offering), and
* **Redeeming** (inflow matching if a deposit is coming in, pro-rata in-kind otherwise).

### What happens under load

{% stepper %}
{% step %}
### Fast exits hit the AMM first

The AMM discount **widens**. This is the visible signal that the vault is under pressure.
{% endstep %}

{% step %}
### Patient exits go through inflow matching first

As the AMM discount deepens, new capital prefers the AMM (more vault per dollar) over matching at NAV, so matching dries up. Most of the patient redemptions end up settling through **pro-rata in-kind redemption**.
{% endstep %}

{% step %}
### Redeemers get loan tokens and collateral in-kind, and put them on OTC

Healthy loans find buyers (vaults with matching rules); stressed loans either sit with the redeemer or sell at a deeper discount.
{% endstep %}

{% step %}
### Stressed exposure gets sorted

Healthy loan tokens handed out via redemption get picked up by other vaults whose rules fit; stressed ones sit with redeemers or sell at a deeper discount.

Over time this **reduces stressed exposure inside vaults that other vaults actively want to buy from**.

If too much of the vault is concentrated in stressed loans for this to keep up, the planned [twin vault](vault-health/twin-vault.md) mechanism would handle the rotation; in v1 the manager pauses new funding and opens a fresh vault.
{% endstep %}
{% endstepper %}

### Why equilibrium holds

Equilibrium comes from **market participation**:

* Wider AMM discounts attract arbitrage capital.
* Healthy loan tokens flow through OTC to vaults that want them.
* **No forced sales** of funded positions.
* **No governance pause** of existing loans.

The only protocol-level lever is **funding-freeze cancellation** (see [Vault rules → Funding freeze](vaults/vault-rules.md#funding-freeze)), which is limited to pre-activation oracle incidents and cannot touch funded loans or collateral.
