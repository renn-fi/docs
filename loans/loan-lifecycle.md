---
description: From loan request to maturity or default — a tour of the loan lifecycle.
icon: arrows-rotate
---

# Loan lifecycle

A loan in Renn Finance moves through a predictable sequence of states. This page is a map of that sequence; each step links to the page with full mechanics.

{% stepper %}
{% step %}
### Loan creation

The borrower opens a loan request, specifying collateral type and amount, loan amount, term, maximum interest rate, and minimum funding threshold. Collateral is transferred to the protocol and locked the moment the request is created.

See [Loan creation](loan-creation.md) and [Collateral](collateral.md).
{% endstep %}

{% step %}
### Funding

The request is listed on the marketplace. Lenders fund it directly, or vaults fund it automatically based on their rules. Requests can be filled by a single lender or split across many.

If the minimum funding threshold is reached, the loan **activates**. The borrower receives funds and lenders receive loan tokens. If not, collateral is unlocked.

See [Funding](funding.md).
{% endstep %}

{% step %}
### Active life

The loan accrues interest. Each loan position is a transferable token, so holders can sell their share on OTC at any time. The protocol does not mark loans to market, and there are no liquidations during the term.

See [Loan tokenisation](loan-tokenisation.md).
{% endstep %}

{% step %}
### Resolution

A loan ends in one of two states:

* **Repaid.** The borrower pays principal plus interest. Collateral unlocks and is returned.
* **In default.** The loan was not repaid by maturity. The lender chooses how to recover — DEX sale, or take collateral in-kind at oracle price.

See [How loans end](how-loans-end.md).
{% endstep %}
{% endstepper %}

## Special paths

* **Refinancing.** A borrower can move a position from another protocol (Aave, Euler) into Renn in a single transaction. See [Refinancing](refinancing.md).
* **Early repayment.** The borrower can close their loan at any time during the term by paying principal plus full make-whole interest. See [How loans are repaid](../repayment-and-exit/repayment.md).
* **Sale-driven closure.** The borrower can close the loan early by triggering a DEX sale of the collateral, but only if proceeds cover principal plus full make-whole interest.
