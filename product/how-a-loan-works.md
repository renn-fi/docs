# How a loan works

On Renn the borrower locks collateral, and lenders fund the loan and receive loan tokens. A vault is a lender like any other.

## 1. Order and funding

The borrower posts an order and locks the collateral in it. The borrower chooses the collateral, the amount, the term, and how long the order stays open. Renn sets the rate, and it is fixed for the whole term. The borrower manages the rate by selling a call, as section 3 describes. See [What's next](whats-next.md#rate).

Lenders fund the order until the amount is reached or the order expires. Each lender receives loan tokens for the amount they funded. Until the loan opens, a lender can withdraw and the borrower can cancel the order.

## 2. Opening

Funding does not oblige the borrower to take the loan. The borrower opens the loan only if the amount raised and the final premium suit them, and can open it on a [partly funded order](../loans/collateral.md). If not, the borrower cancels the order or lets it expire, and takes the collateral back. When the loan opens, the borrower pays the premium for the hedge and receives the principal. If the hedge cannot be bought, the loan does not open and no funds move.

## 3. Hedge

Every loan opens with a put on the collateral. The loan buys the put on an options venue when it opens, and the borrower pays the premium. The put runs for the whole term and expires at the loan's maturity. The put price follows the loan's LTV, so that the collateral at that price covers the principal and interest.

The borrower can manage the rate by selling a call on the collateral. The borrower chooses the call price. The call premium covers part of the borrower's costs and lowers the effective rate. In return, if the collateral rises above the call price, the gains go to the buyer of the call.

The rate is what lenders earn. The borrower's cost = rate + put premium − call premium, if a call was sold. Before the loan opens, the borrower sees an approximate cost. The exact cost depends on the option premiums at the moment the loan opens.

## 4. Term and repayment

During the term there are no margin calls and no liquidations.

The borrower can repay at any point during the term. Interest is charged only for the time the loan was open. A loan repaid halfway through the term pays half of the interest.

If the loan has no call, the borrower can take the collateral back on repayment. If the loan has a call, the collateral stays locked until the call is settled after maturity.

Today the put is not sold on repayment, and its remaining value is lost. If the collateral price is above the call price, the call is settled by delivery. Both are changing. See [What's next](whats-next.md#closing-the-hedge).

## 5. Settlement at maturity

At maturity the loan is settled. Settlement is a transaction that anyone can send. At the current stage Renn is the keeper that sends it. The call is settled first, then the debt.

- **The loan has a call and the price is above the call price.** The buyer of the call pays the call price and takes the collateral. The debt is paid from this cash, and the rest goes to the borrower.
- **The debt is not repaid and the collateral covers it.** Part of the collateral is sold on the market to cover the debt. The rest goes to the borrower. The put is not used.
- **The debt is not repaid and the collateral does not cover it.** The put is exercised, and the collateral is delivered at the put price. If any cash is left, it goes to the borrower.

On the current venue the put can be exercised for [two hours after maturity](../hedging/positions.md). If the loan has a call, the call is settled in the first hour. If settlement is sent after the put's window has closed, the collateral is sold at market price, and lenders may receive less than the full amount.
