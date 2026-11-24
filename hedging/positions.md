---
description: Protective PUT and covered collar structure, custody, pricing, and deadlines.
---

# Hedging positions

## Requests and providers

At acceptance, LoanV2 requests protection for its fixed asset pair, retained collateral, full-term repayment target, and maturity. LoanFactory forwards the request to its selected IHedging provider and records the returned position and strategy. The accepted loan retains that provider for later recovery.

The option-backed Hedging provider creates a dedicated GreekPut or GreekCollar through GreekPositionDeployer. Hedging is the controller and Prop taker. Positions hold the loan's option assets and execute authorized exercise or redemption.

## Protective PUT

An uncapped position buys a European PUT that exchanges loan collateral for supplied cash during its exercise window. GreekPut holds the purchased PUT tokens. The retained collateral stays in LoanV2 until repayment, recovery, or borrower withdrawal.

Greek PUT parameters reverse the loan asset roles: Greek's collateral is supplied cash and its consideration is the loan collateral. Hedging derives an inverse strike from retained collateral and target coverage, accounting for token decimals. Rounding the inverse strike down makes the required PUT amount cover at least the target under the receipt conversion.

## Covered collar

A collar combines a protective PUT with a covered CALL. Loan collateral backs the CALL in Greek. Hedging sells the CALL tokens and uses the proceeds toward the PUT premium. GreekCollar holds the CALL writer receipts and purchased PUT tokens.

The CALL strike, expressed as supplied per whole collateral token with `1e18` scale, must be above the reciprocal of the actual rounded PUT strike. CALL exercise can convert backing collateral into supplied cash. Redemption returns the position's resulting cash and/or collateral to Hedging.

## Premium limits

Quotes report supplied premium paid, premium received, and their signed difference. Positive net premium is a borrower payment; negative net premium is borrower income. The borrower's signed `maxNetPremium` bounds the highest accepted net cost.

For example, a limit of -10 supplied atoms requires at least 10 atoms of net income. Positive limits are temporarily funded by the borrower through LoanV2. Unused budget and net income return to the borrower during acceptance.

## Exercise windows

Hedging uses the loan maturity for both European legs, with a one-hour CALL window and two-hour PUT window. GreekCollar verifies that the actual PUT receipt deadline is later than the CALL receipt deadline.

PUT exercise is available from maturity through its actual receipt deadline, inclusive. CALL writer receipt redemption requires a timestamp strictly after its exercise deadline. These deadlines govern the [recovery flow](opening-and-recovery.md).

## Test provider

NoHedgingFactory creates a zero-premium NoHedging position per loan for Uniswap-only test flows. Uncapped requests retain collateral in LoanV2; capped requests escrow it in the test position. Recovery uses collateral sales and returns actual proceeds and unused collateral.
