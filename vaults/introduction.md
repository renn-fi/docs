---
description: A vault is a pool of capital that funds loans automatically under rules its manager sets at creation.
icon: vault
---

# Introduction

A vault is a **pool of capital** that funds loans automatically based on rules its manager sets at creation. Depositors put in the base asset; in return they get **vault tokens**, which represent their share of whatever the vault holds — base asset balance, loan tokens, defaulted positions, and AMM share.

## Vaults add three things

* **Automation.** Lenders don't have to evaluate every loan request manually. The vault matches loans to its rules and allocates capital on its own.
* **Management and risk control.** The manager runs the book, monitors exposure, and decides when to pause funding or trigger recovery on defaulted loans (see [How loans end](../loans/how-loans-end.md)). Depositors get that work done for them.
* **Liquidity.** Vault tokens trade on the AMM and redeem through inflow matching, giving the loan market a fast exit layer that individual loan tokens don't have on their own.

## Where to next

* [Creating a vault](creating-a-vault.md) — how vaults come into existence and the private/public rollout.
* [Vault rules](vault-rules.md) — what a manager configures at creation.
* [How vaults pick loans](loan-selection.md) — automated allocation across matching rules.
* [Vault tokens and NAV](tokens-and-nav.md) — how the vault is valued.
* [Entering a vault](entering-a-vault.md) and [Exiting a vault](exiting-a-vault.md) — the four ways in and four ways out.
* [Fees](fees.md) — performance fee and optional management fee.
