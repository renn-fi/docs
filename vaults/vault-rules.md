---
description: Mutable funding criteria, collateral admission, pause behavior, and permissions.
---

# Funding criteria and controls

## Rate and term criteria

The owner can replace the vault's criteria through `setCriteria`. Minimum rate is a full-term repayment multiplier with `1e18` scale. Minimum and maximum terms are inclusive durations in seconds from loan acceptance.

A minimum rate of `1.1e18` admits a loan promising 110% of principal at maturity. An earlier repayment follows the loan's accrued-interest calculation. Funding criteria compare the stated full-term multiplier directly.

## Collateral admission

The vault stores allowed collaterals in its `collaterals` mapping. Only the owner can add or remove them. Changing rate and term criteria preserves that mapping.

Collateral must be a deployed contract distinct from ASSET. Duplicate additions are rejected. The owner can remove the final allowed collateral, which prevents new matching until a collateral is added again.

## Pause behavior

The owner can pause or resume new lending. Pausing preserves the owner's idle-cash withdrawal and both operators' ability to refund or collect existing loan claims.

Criteria changes and collateral removal take effect on the next funding transaction. Existing claims remain recoverable using their original loan lifecycle.

## Authority

The owner controls deposits, idle-cash withdrawals, criteria, collateral admission, and pause status. The immutable executor controls lending. Both can refund and collect. All recovered supplied assets go to the vault, and owner cash withdrawals go to the current owner.

Loan selection reads the current criteria and terms on-chain for each proposed investment. See [how vaults fund loans](loan-selection.md).
