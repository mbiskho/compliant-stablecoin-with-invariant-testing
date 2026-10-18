# Compliant Stablecoin with Invariant Testing

A regulated stablecoin whose supply can't drift from its reserves.

> **Status:** Not started. This folder holds the project brief only; no code yet.

## What it is

An upgradeable fiat-backed stablecoin with the controls a regulated issuer actually needs: role-separated minting, freeze and blocklist, pausing, rate-limited mints, and an attestation hook that blocks minting above reported reserves. The correctness work is the point: fuzz and invariant tests run millions of random call sequences, and key properties are checked with a symbolic tool.

## Why it's worth building

Stablecoin regulation (MiCA, the US stablecoin rules) has made compliance controls mandatory, and banks are now issuing their own. The contracts are short; getting the roles, upgrades and supply invariants right is where issuers get burned.

## Scope

- UUPS-upgradeable ERC-20 with role-based access
- Freeze, blocklist and pause
- Per-minter rate limits
- Reserve attestation check on mint
- Fuzz and invariant test suite
- Symbolic checks on supply properties
- Upgrade safety tests (storage layout)

## Stack

| | |
|---|---|
| Languages | Solidity 0.8 |
| Frameworks | Foundry, OpenZeppelin Upgradeable, Halmos, Slither |
| Infrastructure | Sepolia testnet, GitHub Actions |

## Deliverables

- GitHub repo with verified testnet deployment
- threat model document
- invariant and coverage report
- role and upgrade runbook

## Done when

Supply never exceeds attested reserves across 10 million fuzzed calls, symbolic checks pass on the core properties, coverage above 95%, and an upgrade runs on testnet without breaking storage.

## Numbers to report

- Fuzz runs and invariant calls executed
- invariant violations (must be 0)
- line and branch coverage
- gas per transfer vs a plain ERC-20

## Build plan

| Phase | Work |
|---|---|
| Wk 1 | token, roles, freeze and pause. |
| Wk 2 | rate limits, attestation hook, upgrades. |
| Wk 3 | fuzz and invariant suite. |
| Wk 4 | symbolic checks, threat model, testnet deploy. |

## Where it gets hard

Writing invariants that mean something. It is easy to write ones that trivially pass. Start from the threat model and write one invariant per thing that would cost the issuer money.

## Stretch goals

Cross-chain version using a burn-and-mint messaging bridge. Add an independent security review from a friend or a contest and publish the findings.

## Prerequisites

- Testnet ETH
- Foundry

## Talking about it

- **Proves:** Secure contract engineering for regulated assets
- **One-liner:** The contract's 300 lines. The test suite is what lets me say the supply can't outrun the reserves.
- **CV bullet:** Built an upgradeable, compliance-controlled stablecoin in Solidity with supply-versus-reserve invariants verified across 10 million fuzzed calls and symbolic checks.
- **Who cares:** Stablecoin issuers, bank digital-asset teams, payment companies, audit firms

Effort M · 40-55 hours · priority High
