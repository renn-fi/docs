---
description: Liquidity comes from the market, not from the protocol.
icon: arrows-left-right
---

# Secondary market and arbitrage

**Liquidity comes from the market, not from the protocol.** When the system is under stress, vault and loan tokens trade at a discount. That creates arbitrage opportunities, which attract capital and pull prices back toward fair value.

{% hint style="info" %}
Arbitrage and market-making are **not enforced or subsidised** at the protocol level. The system is compatible with independent arbitrageurs, external market makers, and managers reallocating capital between vault generations.

Over time, the protocol may work with liquidity providers, support market-making, or add incentives if needed.
{% endhint %}

## Clean and dirty pricing for loan tokens

When a loan token trades on the secondary market, the price the buyer pays is what bond markets call the **dirty price**. It splits into:

* **Clean price.** What the loan is worth right now if you ignore accrued interest. The discounted value of the remaining payment at whatever yield the market is currently demanding.
* **Accrued interest.** The share of the loan's total interest that has built up from the loan's start date until the trade date, at the loan's issuance yield.

$$
dirty\_price = clean\_price + accrued\_interest
$$

The buyer pays the dirty price; the seller receives it.

{% hint style="info" %}
This split is a way to **think about pricing and report it**. On-chain, only the total transfer amount is recorded.
{% endhint %}
