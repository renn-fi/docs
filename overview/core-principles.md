---
description: The design rules that shape every part of the protocol.
icon: compass
---

# Core principles

Renn Finance is built around a small set of rules that hold across loans, vaults, and recovery. Everything else follows from these.

## Fixed terms and fixed rates

Loans run for a fixed term at a fixed rate, set at loan creation. There is no variable-rate exposure during the loan's life and no rate change after origination.

## Collateral is locked at loan creation

The borrower transfers collateral to the protocol the moment the loan request is created. This commits the borrower up front and prevents fake or unfunded loan requests from sitting on the marketplace.

## No margin calls, no in-term liquidations

The protocol does not liquidate active loans. Price moves during the term do not trigger forced sales. A loan resolves only at maturity (or earlier, by mutual mechanics like early repayment or borrower-initiated sale-driven closure).

## The lender chooses how to recover on default

If a loan defaults:

* The lender can **trigger a DEX sale** through the contract. Proceeds cover principal first, then interest, with any remainder to the borrower.
* Or the lender can **take the collateral in-kind** at oracle price.

The borrower can also trigger a DEX sale during the term, but only if the collateral covers principal plus interest in full. See [How loans end](../loans/how-loans-end.md).

## The market sets prices, not the protocol

Interest rates and exit prices are set by the market. The protocol provides mechanism (auctions, AMMs, the OTC marketplace) but does not enforce or subsidise prices.

## Vault rules are immutable

Vault rules are set when the vault is created and cannot change afterward. A manager who wants different rules creates a new vault. The only allowed change is the one-way private-to-public conversion (see [Creating a vault](../vaults/creating-a-vault.md)).

## Oracle use is bounded

The price feed is used in only two places:

1. The initial **LTV check at admission**.
2. On default, to determine the collateral split if the lender chooses the **take-at-oracle** recovery path.

The oracle never marks live loans, never triggers liquidations, and never moves money on its own. See [Vault rules → Where the price feed is used](../vaults/vault-rules.md#where-the-price-feed-is-used).
