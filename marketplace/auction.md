---
description: A price-down, yield-up auction that keeps loan tokens fungible.
icon: gavel
---

# The auction

The auction has to do two things at the same time: **discover the rate**, and **let several lenders share the loan in different-sized pieces**.

The obvious approach — moving the interest rate over time — breaks fungibility: early and late lenders would end up with tokens that pay different amounts, so they could not trade as the same instrument.

## How Renn solves it

The protocol keeps the loan's repayment terms **fixed** and moves the **entry price** instead. Every token from the loan pays out the same amount at maturity. The yield each lender locks in depends on the price they paid to enter.

* The **entry price drops over time**. The loan starts expensive (low yield for the lender, low cost for the borrower) and gets cheaper (higher yield, higher cost) until it is fully funded or the auction ends.
* **Early lenders** pay more and get a lower yield.
* **Later lenders** pay less and get a higher yield.
* All the resulting tokens are **interchangeable**: same maturity, same payout, just bought at different prices.

{% hint style="info" %}
The auction always runs **price-down / yield-up**; the reverse is not supported. Price moves in discrete steps, with the step size and timing configured at the interface level.
{% endhint %}

## Worked example

Consider a loan with these parameters:

* **Term**: 1 year
* **Starting rate**: 10%
* **Maximum rate**: 14%
* **Loan amount**: $100,000
* **Collateral**: $200,000 in ETH

The auction sells tokens that pay **$1.10 at maturity**, starting at par ($1.00) and dropping over time as funding fills. Three lenders each contribute $33,333 at different points:

| When  | Lender funds | Token price | Tokens bought | Yield |
| ----- | ------------ | ----------- | ------------- | ----- |
| Early | $33,333      | $1.0000     | 33,333        | 10%   |
| Mid   | $33,333      | $0.9821     | 33,939        | 12%   |
| Late  | $33,333      | $0.9649     | 34,545        | 14%   |

The borrower repays **$111,999 at maturity**, distributed pro-rata across token holders. Effective borrower rate: **12% annualised**. The exact final repayment is known only when the auction closes.

{% hint style="warning" %}
The price-based auction is **deferred from MVP**. At launch, only the fixed-rate path is available. See [MVP scope](../roadmap/mvp-scope.md).
{% endhint %}
