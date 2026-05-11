# NIP-015 — Governance Model Design

- Status: 📋 Open
- Area: Protocol Design / Governance
- Phase: 3–4
- Priority: Medium
- Date: 2026-05-11

## Context

Decentralized governance is required to avoid whale domination and ensure protocol evolution is community-driven.
Current whitepaper mentions governance by token + reputation + participation, but no mechanism is defined.

## Proposal

Design a hybrid governance model:

### Governance Inputs

1. **Token ownership** — token holders vote on economic parameters
2. **Node reputation** — high-reputation nodes have amplified voting weight on technical proposals
3. **Participation history** — active contributors gain governance weight over time

### Sub-tasks

- [ ] NIP-015a: Define proposal types (protocol upgrade, parameter change, emergency action)
- [ ] NIP-015b: Define voting weight formula: `W = f(token_balance, reputation, participation_score)`
- [ ] NIP-015c: Specify quorum requirements per proposal type
- [ ] NIP-015d: Specify voting period duration per proposal type
- [ ] NIP-015e: Define proposal submission requirements (minimum stake + reputation)
- [ ] NIP-015f: Design veto mechanism for emergency actions (multisig council)
- [ ] NIP-015g: Define upgrade execution process (timelock + on-chain signal)
- [ ] NIP-015h: Specify governance parameter storage (on-chain vs off-chain)

## Acceptance Criteria

- All proposal types defined.
- Voting weight formula specified with cap on whale amplification.
- Quorum thresholds defined per proposal type.
- Veto / emergency mechanism specified.
- Timelock duration specified for protocol upgrades.

## Impact

- New: `docs/protocol/governance-model.md`
- Feeds: NIP-040 (token design), NIP-071 (distributed governance implementation)

## Implementation Notes

- Voting weight cap: no single entity can hold > 10% of total voting weight.
- Reputation amplification: capped at 2x for maximum reputation score.
- Emergency actions: require 5-of-9 multisig from elected council.
- Phase 3 starts with off-chain signaling (Snapshot); Phase 4 moves fully on-chain.

## Dependencies

- NIP-040 (Token design) — token supply and distribution affect governance power
- NIP-014 (Reputation) — reputation score feeds voting weight
