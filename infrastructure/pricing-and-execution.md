---
description: Pair price routing, fixed-window Uniswap TWAPs, and bounded swap execution.
---

# Pricing and execution

## Price interface

IPriceOracle converts a base-token amount into quote-token units with explicit upward or downward rounding. All inputs and outputs use native token units.

PairPriceOracle routes an unordered token pair to one registered oracle. Registration writes both directions and emits the sorted pair with its source. Routes are append-only, so an admitted pair keeps its source while additional pairs can be registered.

LoanFactory fixes the oracle address at deployment. HedgingMarkets providers read and fix that same address from their factory.

## Fixed-window TWAP

UniswapTwapOracle fixes one Uniswap V3 pool, its token pair, a window of at least 30 minutes, and a positive minimum harmonic liquidity. Its constructor verifies the pool's provenance against the supplied Uniswap factory.

Consultation uses cumulative ticks and seconds-per-liquidity over the full configured window. It derives the arithmetic mean tick, rounding negative tick division toward negative infinity, and checks harmonic liquidity plus nonzero current pool liquidity. Missing history, invalid observations, or insufficient liquidity causes the quote to revert.

TickMathV3 converts the mean tick to a price. Pool ticks encode token decimal differences. The oracle supplies a price quote; the recovery provider separately adjusts for the execution fee and its 1% allowance.

The observation pool and execution pool can have different fee tiers.

## Swap adapter

UniswapSeller pins a SwapRouter02 and performs V3 single-pool swaps. It pulls the current caller's collateral, grants temporary router approval, sends supplied proceeds to that caller, and clears approval.

**Exact input** sells a stated collateral amount for at least a positive supplied minimum. Completion requires the full input to be consumed and actual received output to meet the minimum.

**Exact output** buys an exact supplied target with at most a collateral budget. Unused collateral is refunded atomically. The seller checks actual spending and requires exact output receipt.

Both paths validate token addresses, distinct assets, positive amounts, and the caller's deadline. Existing seller balances stay outside the transaction's allocation. The provider chooses the execution pool fee and bounds described in [opening and recovery](../hedging/opening-and-recovery.md).
