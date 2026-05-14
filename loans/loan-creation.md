---
description: What goes into a loan request and the LTV cap.
icon: file-plus
---

# Loan creation

A borrower opens a loan request directly through the protocol. The request specifies:

* **Collateral type.** BTC or ETH at launch.
* **Collateral amount.** How much they are posting.
* **Loan amount.** How much they want to borrow.
* **Loan term.** How long the loan runs.
* **Maximum interest rate.** The highest rate they are willing to pay.
* **Minimum funding threshold.** The loan does not activate below this amount.

## LTV cap

A borrower can borrow at most **50% of the value of their collateral**.

{% hint style="info" %}
**Example.** $100k of BTC supports at most a $50k loan.
{% endhint %}

The 50% cap applies to **loan principal only**; interest is not included in the LTV calculation. If at maturity the collateral barely covers the principal, the lender's interest is at risk before any principal loss.

## Choosing a rate

The borrower can either set a fixed rate they are willing to pay, or opt into an auction-based rate. See [Rate setting](../marketplace/rate-setting.md) and [The auction](../marketplace/auction.md).

## What happens next

Once created, the request is listed on the marketplace and lenders can begin funding it. See [Funding](funding.md) for the funding mechanics and [Collateral](collateral.md) for what gets locked and when.
