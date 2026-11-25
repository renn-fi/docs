---
description: Token admission, markets, oracle registration, onboarding, and provider rotation.
---

# Protocol configuration

## Administrative scope

| Configuration | Responsible authority | Effect |
| --- | --- | --- |
| Collateral and consideration whitelists | LoanFactory owner | New loan creation |
| Selected hedging provider | LoanFactory owner | New positions at acceptance |
| Directional execution market and pool fee | Current LoanFactory owner, on the provider | Quotes and new positions |
| Pair oracle registration | PairPriceOracle owner | Both quote directions for that fixed pair source |
| Prop tokens, taker admission, and pricer listings | Prop owner, with maker account approvals | Option quoting and trading |
| Private vault funding criteria | Vault owner | New funding from that vault |

LoanFactory, PairPriceOracle, and Vault each use their own ownership state.

## Token roles and markets

Collateral and consideration admission are independent. An order can pair admitted distinct tokens. Acceptance uses the selected provider's directional collateral-to-consideration market and, for option-backed Hedging, executable option routes.

HedgingMarkets fixes its seller and oracle from LoanFactory and stores an enabled execution fee for each directional pair. Fee units use a denominator of 1,000,000. Position creation snapshots that fee; subsequent configuration changes govern future positions.

## Onboarding flow

The token onboarding scripts operate on a specified role and explicit counterpart markets.

1. Validate chain, ownership, token metadata, provider dependencies, router factory, and each requested counterpart.
2. Validate pool provenance, execution liquidity, TWAP history and liquidity, and applicable Prop readiness before recording configuration transactions.
3. Deploy and register a new TWAP source, or verify and reuse the matching existing route. Check quotes in both directions.
4. Configure the directional execution market. Existing enabled markets must match the onboarding fee.
5. When explicitly configured, admit Prop tokens, admit the shared Hedging taker, and list maker pricers. Maker accounts provide pricer approvals.
6. Admit the token for its requested LoanFactory role.

An empty counterpart list supports initial role admission before the first market is configured. Matching configuration can be reused on reruns. Onboarding spans configuration transactions, with validation before the writes.

## Provider rotation

The factory owner may select an IHedging provider tied to that LoanFactory. A zero selection disables creation of new positions. Unaccepted orders use the provider selected when acceptance executes.

Accepted loans keep their recorded provider and position. Removing a market or changing its fee leaves existing positions using their stored execution fee. Token delisting affects new order creation while existing terms remain fixed.

A new option-backed provider needs its own market configuration and Prop taker admission. Existing positions continue recovery through their original provider.
