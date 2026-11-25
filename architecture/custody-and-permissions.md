---
description: Asset locations, administrative authority, and transaction boundaries.
---

# Custody and permissions

## Where assets reside

Before acceptance, collateral and lender funding reside in LoanV2. Lenders, including private vaults, hold its receipts.

At acceptance, actual funding becomes principal and is paid to the borrower. With uncapped protection, retained collateral remains in LoanV2 and GreekPut holds the purchased PUT tokens. With a collar, retained collateral backs the covered CALL in Greek, while GreekCollar holds the writer receipts and protective PUT tokens.

During recovery, Hedging temporarily handles the loan's collateral and position proceeds. It returns measured supplied recovery and unused collateral to the calling loan. LoanV2 then holds the lender payout pool and borrower assets until withdrawal.

Private vault cash and loan receipts reside in each Vault. LoanFactory transfers initial collateral directly to the loan, and VaultFactory creates the vault instances. UniswapSeller uses the current caller's funds for a synchronous swap.

## Caller permissions

| Role | Authority |
| --- | --- |
| Borrower | Create their own order, cancel or accept it, and request maturity settlement through `repayFromCollateral` |
| Receipt holder | Refund during Lending or Canceled; withdraw a final claim in Repaid |
| Any payer | Repay the accepted loan's current amount due |
| Any caller | Persist time-derived state, request eligible settlement, or release borrower assets to the fixed borrower |
| LoanFactory owner | Manage token admission, select the provider for new positions, and manage provider execution markets |
| PairPriceOracle owner | Register new pair sources |
| Vault owner | Deposit, withdraw idle cash, change criteria and collateral admission, pause, refund, and collect |
| Vault executor | Fund eligible loans, refund orders, and collect settled claims |

LoanFactory, PairPriceOracle, and Vault use two-step ownership transfer. The proposed owner accepts before ownership changes.

## Pinned dependencies

LoanFactory fixes its seller and price oracle at deployment. Providers read and fix these addresses from that factory. Each accepted loan records its provider and position, and each position keeps its selected execution fee. A vault fixes its asset, loan factory, executor, and creating factory at deployment.

Factory registration is checked before a vault calls a proposed loan. LoanFactory verifies the asset pair in a registered loan's hedge request. Providers address opening and realization by the calling recorded loan. Greek positions accept management calls only from their controller.

## Accounting boundaries

LoanV2's `vaultCollateral`, `vaultLending`, `vaultRepaying`, and `vaultSurplus` are accounting buckets within the loan. They identify pledged collateral, unaccepted funding, lender payout cash, and borrower surplus. Raw balances may additionally contain direct transfers outside the lifecycle. A private Vault's `freeBalance` is its entire current ASSET balance, including direct transfers.

Asset-moving entry points use reentrancy guards. Incoming loan funding and repayments verify exact receipt. Hedging and Greek positions measure operation-specific balances, and temporary execution allowances are cleared. Outbound loan and owner cash transfers use SafeERC20; the recipient's net receipt follows the asset's transfer behavior.
