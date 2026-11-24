---
description: Vault creation parameters, immutable configuration, registration, and ownership.
---

# Creating a vault

The creator calls VaultFactory with an asset, LoanFactory, executor, initial criteria, and initial allowed collaterals. The factory deploys a Vault owned by that creator, records `isVault`, and emits `VaultCreated` with the complete configuration.

## Initial configuration

| Parameter | Meaning |
| --- | --- |
| ASSET | Supplied ERC-20 held and lent by the vault |
| LOAN_FACTORY | Trusted registry for eligible LoanV2 instances |
| EXECUTOR | Address authorized to fund loans |
| `minRate` | Minimum full-term repayment multiplier, scaled by `1e18` |
| `minTerm`, `maxTerm` | Inclusive loan duration bounds in seconds |
| Collateral list | Nonempty initial set of permitted loan collateral tokens |

Asset and factory addresses must contain deployed code, and the executor must be nonzero. Minimum rate must be at least `1e18`; minimum term must be positive, and maximum term must be at least the minimum. Initial collaterals must be distinct deployed contracts different from ASSET.

## Fixed and owner-managed settings

ASSET, LOAN_FACTORY, EXECUTOR, and VAULT_FACTORY are immutable. The owner can update rate and term criteria, add or remove collateral, and pause new lending after creation.

Vault ownership uses a two-step transfer. The current owner nominates the next owner, who accepts ownership. The fixed executor remains the same across this transfer.

After creation, the owner can [deposit cash](entering-a-vault.md) and the executor can begin funding eligible loans.
