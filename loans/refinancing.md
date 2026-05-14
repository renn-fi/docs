---
description: Move a position from Aave, Euler, or similar protocols into Renn in one transaction.
icon: shuffle
---

# Refinancing an existing loan

Refinancing is designed for borrowers who want to swap a **variable-rate, liquidatable position** for a **fixed-rate, fixed-term one with no liquidations**.

## How it works

A borrower with an open position on another lending protocol (Aave, Euler, or similar) can move it into Renn in a single step:

1. The original debt is closed.
2. A new loan is opened against the same collateral, on the terms the borrower sets here.
3. The whole operation runs as **one transaction**.

## Supported protocols

At MVP, refinancing is supported only from **Aave**. Euler and similar protocols will be added later.

{% hint style="info" %}
Supported protocols for refinancing will expand over time. See the [MVP scope](../roadmap/mvp-scope.md) for what is in v0.
{% endhint %}
