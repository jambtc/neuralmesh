# NIP-014 — Reputation Scoring System

- Status: 📋 Open
- Area: Protocol Design / Incentives
- Phase: 1–3
- Priority: High
- Date: 2026-05-11

## Context

Reputation is a key input to the reward function (NIP-010) and validator selection (NIP-012).
Without a well-designed reputation system, honest nodes can be disadvantaged and dishonest nodes can game the system.

## Proposal

Design a reputation scoring system with decay, growth, and slashing:

### Sub-tasks

- [ ] NIP-014a: Define reputation score range and initial value for new nodes
- [ ] NIP-014b: Specify score increase events (successful task, passed validation, uptime)
- [ ] NIP-014c: Specify score decrease events (failed task, failed validation, missed deadline, Sybil flag)
- [ ] NIP-014d: Define time-decay function (reputation decays without activity)
- [ ] NIP-014e: Specify slashing events and magnitude (dishonest behavior)
- [ ] NIP-014f: Define reputation checkpoints: thresholds that unlock capabilities
- [ ] NIP-014g: Design reputation leaderboard / public API
- [ ] NIP-014h: Define reputation recovery path after penalty

## Acceptance Criteria

- Score range defined (e.g., 0–1000).
- All increase and decrease events enumerated with delta values.
- Time-decay function specified with decay rate.
- Slashing events and magnitudes defined.
- At least 4 capability checkpoints defined.

## Impact

- New: `docs/protocol/reputation-scoring.md`
- Feeds: NIP-010 (reward function), NIP-012 (weighted consensus), NIP-013 (trust tiers)

## Implementation Notes

- Initial score: 100 (enough to participate as worker, not as validator).
- Validator threshold: score ≥ 500.
- Decay: -1 point/day of inactivity (floor at 50 for long-term inactive nodes).
- Slashing: dishonest validation costs 30% of current score (non-linear deterrent).
- Recovery: nodes can recover score through sustained honest behavior over time.

## Dependencies

- NIP-013 (Anti-Sybil) — Sybil detection triggers reputation penalty
- NIP-042 (Staking) — high reputation nodes may require lower stake
