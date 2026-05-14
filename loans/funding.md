---
description: How loan requests get filled by direct lenders or vaults.
icon: hand-holding-dollar
---

# Funding

Loan requests are listed on a marketplace. Lenders fund them either directly or through vaults. A request can be:

* **Filled by a single lender** for the full amount, or
* **Split across several lenders**.

## Direct funding

Any wallet can fund a loan directly from the marketplace. The lender picks the loan, sends the funding amount, and receives loan tokens.

## Vault funding

A vault funds loans automatically based on its rules. Depositors deposit the vault's base asset and receive vault tokens; the vault holds the resulting loan tokens on their behalf. See [Vaults](../vaults/introduction.md) for the full mechanics.

## End-to-end flow

{% stepper %}
{% step %}
### 1. Borrower creates a loan order

The borrower provides collateral; alternatively, an existing Aave debt is refinanced.
{% endstep %}

{% step %}
### 2a. Lender deposits into the vault

The lender provides stablecoins (USDC) to the vault and receives **rnVault** tokens representing their share in the vault.
{% endstep %}

{% step %}
### 2b. AMM liquidity is seeded

A portion of the vault's USDC and rnVault tokens are deposited into **Renn DEX** as liquidity for the AMM.
{% endstep %}

{% step %}
### 3. The vault fulfils the loan

Once the vault has sufficient funds, it fulfils the loan order on the Renn Debt Marketplace.
{% endstep %}

{% step %}
### 4. Optional early exit

The lender can exit early by selling rnVault tokens on Renn DEX.
{% endstep %}
{% endstepper %}

## Funding outcomes

{% tabs %}
{% tab title="Threshold reached" %}
The loan **activates**. The borrower receives the funds and lenders receive a token representing their share of the loan.
{% endtab %}

{% tab title="Threshold not reached" %}
The loan **does not activate**. The borrower's collateral is unlocked and returned.
{% endtab %}

{% tab title="Borrower withdraws collateral" %}
If the borrower withdraws their collateral before activation, the loan request **closes**. Any lenders who had already staked funds get them back.
{% endtab %}
{% endtabs %}
