---
description: Repayment, default, and the recovery paths available to the lender.
icon: flag-checkered
---

# How loans end

A loan ends in one of two states: **repaid**, or **in default**.

{% hint style="info" %}
**Default** means the loan was not repaid by maturity. The protocol does not classify reasons.
{% endhint %}

## Repaid

The borrower can repay at any time during the loan term. They pay principal plus interest, and their collateral unlocks and is returned.

For early-repayment mechanics (full make-whole), see [How loans are repaid](../repayment-and-exit/repayment.md).

## In default

The contract holds the collateral. The lender chooses how to recover:

{% tabs %}
{% tab title="DEX sale" %}
The contract sells the collateral on a supported DEX. Proceeds are applied in order:

1. **Principal** first.
2. **Interest** next.
3. **Any remainder** goes to the borrower.

Post-default DEX sales execute **at best available price**; the lender absorbs any shortfall.
{% endtab %}

{% tab title="Take collateral at oracle price" %}
The lender takes a quantity of collateral equal to:

$$
\frac{principal + interest}{oracle\_price}
$$

The borrower keeps the remainder. The oracle is the same TWAP used at origination. See [Where the price feed is used](../vaults/vault-rules.md#where-the-price-feed-is-used).
{% endtab %}
{% endtabs %}

### When the loan token is split across holders

When a loan token is held by multiple parties, each holder triggers recovery on **their own share independently**:

* **Holder N%** who chooses DEX sale: that share of collateral is sold on DEX; proceeds go to them.
* **Holder M%** who chooses take-at-oracle: that share of collateral transfers to them in-kind at the oracle price.

The two paths can run **in parallel for the same loan**; no coordination between holders is required. The borrower's remainder is calculated on total recovered value across paths.

## Who can trigger what, and when

{% columns %}
{% column %}
### During the loan term

The **borrower** can trigger a sale at any time (sale-driven closure). The contract checks that the sale will produce enough to cover principal plus full interest as if the loan ran to maturity:

* **If yes**, the sale executes and the loan closes.
* **If not**, the sale is rejected and the loan continues.

If a borrower-triggered sale clears the contract check but the actual swap result falls short of debt by more than a configurable tolerance, the sale aborts. This protects the lender if DEX state diverges from the oracle at execution.
{% endcolumn %}

{% column %}
### After maturity

Each **loan-token holder** can trigger their own recovery path (DEX sale or take-at-oracle) for their share.

The **borrower** can trigger only a DEX sale for the whole position, and only if the oracle price indicates the collateral covers principal plus interest in full. This prevents the borrower from forcing a loss-realising sale on the lender.
{% endcolumn %}
{% endcolumns %}

## If the collateral doesn't cover the loan

If collateral value isn't enough to cover the loan, the lender takes everything and absorbs the shortfall.
