---
description: How direct lenders and vault depositors exit positions before maturity.
icon: door-open
---

# Exit options

## Direct lenders (holding individual loan tokens)

{% columns %}
{% column %}
### Hold to maturity

Wait for the full payout at maturity, then collect principal plus interest from the borrower's repayment (or trigger recovery on default).
{% endcolumn %}

{% column %}
### Sell on OTC

Sell the loan token to another buyer. Buyers are typically **vaults whose rules match the loan's remaining parameters** (collateral, remaining term, yield).

Price is negotiated. See [Clean and dirty pricing](secondary-market.md#clean-and-dirty-pricing-for-loan-tokens).
{% endcolumn %}
{% endcolumns %}

{% hint style="info" %}
**Loan tokens do not trade on the AMM.** They trade OTC. The AMM is for vault tokens only.
{% endhint %}

## Vault depositors

Vault depositors exit via the four paths described in [Exiting a vault](../vaults/exiting-a-vault.md):

1. **Sell on the AMM** — fastest path, market-clearing price.
2. **Inflow matching** — settle at NAV against an incoming deposit.
3. **Pro-rata in-kind redemption** — receive a proportional slice of every vault asset.
4. **Hold to vault maturity** — for fixed-term vaults, simply wait until the vault winds down.
