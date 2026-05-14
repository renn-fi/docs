---
description: What can be used as collateral and when it gets locked.
icon: lock
---

# Collateral

## Collateral scope

At launch the protocol accepts **only BTC and ETH**. These are the two assets with the deepest liquidity, the most predictable market behaviour, and the lowest systemic risk.

Additional assets can be added later. Custom collateral configurations may also be introduced earlier for specific large borrowers or lenders.

## Collateral locking

Collateral is transferred to the protocol and **locked the moment the loan is created**, before funding begins.

{% hint style="info" %}
This commits the borrower up front and stops anyone from posting fake or unfunded loan requests.
{% endhint %}

## What happens to locked collateral

* **If the loan activates** (funding reaches the minimum threshold), collateral stays locked until the loan resolves — either through repayment, or through one of the recovery paths described in [How loans end](how-loans-end.md).
* **If the loan does not activate**, collateral is unlocked and returned.
* **If the borrower withdraws collateral before activation**, the loan request closes and any lenders who had already staked funds get them back.
