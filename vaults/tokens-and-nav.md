---
description: How a vault is valued — accrued-yield amortization, not mark-to-market.
icon: calculator
---

# Vault tokens and NAV

Depositors get a **vault token**. It represents their share of the vault. They can hold it, sell it on the secondary market, or redeem it. See [Exiting a vault](exiting-a-vault.md).

## What goes into NAV

A vault's total value at any moment is the sum of three components:

### 1. Loan tokens

Each loan token is marked as:

$$
mark = entry\_price + (maturity\_payment - entry\_price) \times \frac{days\_held}{days\_to\_maturity\_at\_purchase}
$$

This is the **standard effective-yield amortization** used in bond fund accounting: the mark grows linearly from the vault's purchase price toward the maturity payment.

{% hint style="info" %}
The formula fairly reflects each vault's actual yield-to-maturity: loans bought at a discount on the secondary market accrue at a higher implied yield than loans funded at origination, and NAV reflects that difference from day one rather than realising it only at maturity.
{% endhint %}

### 2. Base asset balance

Whatever the vault is holding in the base asset (USDC at launch, other assets possible later).

### 3. AMM pool share

Valued at the pool's current composition. See [AMM liquidity](amm-liquidity.md).

## NAV per vault token

$$
NAV\ per\ vault\ token = \frac{total\ NAV}{vault\ tokens\ in\ circulation}
$$

## Why NAV is accrual-based, not mark-to-market

NAV is based on **linear accrual**, not current market prices. The vault doesn't re-mark loans against the current rate environment. The mark grows steadily toward the maturity payment for healthy loans.

If a loan **defaults**, its mark **freezes at the maturity date value** until the vault triggers recovery (DEX sale or take-at-oracle). The realised proceeds then replace the frozen mark and any difference is recognised as gain or loss. See [Defaulted loans inside a vault](../vault-health/defaulted-loans.md).

This pricing keeps NAV **stable and predictable**. The downside is that NAV doesn't reflect deteriorating loans in real time.

{% hint style="warning" %}
**The lemon problem.** When the underlying portfolio gets worse than the accrued-yield mark suggests, new capital avoids the vault and the AMM trades at a discount, but NAV itself doesn't catch up. The planned [twin vault](../vault-health/twin-vault.md) mechanism is designed to address this.
{% endhint %}
