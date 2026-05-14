---
description: Bullet repayment, early repayment with make-whole, and sale-driven closure.
icon: money-bill-transfer
---

# How loans are repaid (v1)

## Bullet repayment

**Principal and interest are paid together at maturity.** There are no monthly or interim payments.

## Early repayment with full make-whole

A borrower can close their loan early at any time. To do so, they pay back:

* The **principal**, plus
* The **full interest** the loan would have earned **if it had run to maturity**.

{% hint style="info" %}
The lender gets exactly what they signed up for, regardless of when the borrower decides to close.
{% endhint %}

## Sale-driven closure

A borrower can also close the loan early by triggering a DEX sale of the collateral.

* The sale only executes if the proceeds **cover principal plus full make-whole interest**.
* The lender still gets exactly what they signed up for.
* The borrower gets whatever is left over after the loan is paid off.

See [How loans end → Who can trigger what, and when](../loans/how-loans-end.md#who-can-trigger-what-and-when) for the precise rules around borrower-initiated sales.

## Planned for v2

### Coupon loans

Periodic interest payments instead of bullet repayment, for longer-duration loans.

### Maturity rollover

At maturity, a borrower can **extend the loan instead of repaying**. Mechanically, this is opening a new loan against the same collateral, atomically:

* The new loan's funding pays off the original lenders.
* New lenders take the new loan.
* If the new loan can't find funding by the original maturity, the original loan resolves the normal way (repayment or default).

See [Open items](../roadmap/open-items.md) for the edge case of partial rollover funding.
