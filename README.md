---
description: Technical reference for Renn contracts, asset custody, and protocol flows.
---

# Renn Finance

Renn is a collateralized lending protocol built around individual fixed-term loans. Borrowers escrow collateral and propose a full-term repayment rate. Lenders fund orders directly or through personal vaults. Borrower acceptance opens the selected hedging position and releases the funded principal.

These pages describe the current LoanV2, Hedging, and personal Vault implementation. Asset support, execution markets, and the selected hedging provider are determined by each deployment's configuration.

## Explore the protocol

* [Protocol overview](overview/introduction.md) follows a loan from collateral deposit to final withdrawals.
* [Contract roles](architecture/contracts.md) explains the factories, loans, receipts, hedging positions, and infrastructure.
* [Custody and permissions](architecture/custody-and-permissions.md) identifies who controls each operation and where assets reside.
* [Loans](loans/loan-creation.md) covers terms, funding, acceptance, interest, and settlement.
* [Hedging](hedging/positions.md) explains protective PUTs, covered collars, and recovery.
* [Personal vaults](vaults/introduction.md) covers owner cash, executor funding, and collection.
* [Infrastructure](infrastructure/pricing-and-execution.md) describes price sources, swap execution, and configuration.
* [Events and integration](operations/events-and-integration.md) describes discovery, state reads, and transaction preparation.

## Terms and units

The **collateral** is the ERC-20 asset pledged by the borrower. The **supplied asset**, also called consideration, is the ERC-20 asset lent to the borrower and distributed to receipt holders. **Principal** is the funding actually accepted. **Maturity** is acceptance time plus the loan term.

A loan's **rate** is its full-term repayment multiplier, scaled by `1e18`. A value of `1.1e18` means principal plus 10% interest over the entire term. Interest accrues linearly until repayment or maturity.

Token amounts and oracle quotes use native token units. LoanToken receipt amounts equal the raw supplied units deposited. Option strikes and collar cap prices use 18-decimal fixed point. Times use Unix timestamps and durations in seconds.
