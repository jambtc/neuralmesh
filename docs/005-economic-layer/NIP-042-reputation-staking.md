# NIP-042 — Reputation Staking Mechanism

- Status: 📋 Open
- Area: Economic Layer / Staking
- Phase: 3
- Priority: Medium
- Date: 2026-05-11

## Context

Staking aligns economic incentives: nodes that misbehave lose their stake.
Combined with reputation (NIP-014), staking creates a two-factor deterrent against dishonest behavior.

## Proposal

Design the reputation staking mechanism:

### Sub-tasks

- [ ] NIP-042a: Define minimum stake per node role (worker, validator, coordinator)
- [ ] NIP-042b: Define stake-to-reputation relationship (higher stake → faster reputation gain, optional)
- [ ] NIP-042c: Implement staking smart contract or on-chain equivalent
- [ ] NIP-042d: Implement stake lock period (unstaking requires N-day waiting period)
- [ ] NIP-042e: Define slashing events and slash percentage per event type
- [ ] NIP-042f: Implement partial slashing (graduated penalty, not all-or-nothing)
- [ ] NIP-042g: Define slashing fund destination (burn vs ecosystem fund)
- [ ] NIP-042h: Implement stake delegation (token holders delegate to trusted nodes)
- [ ] NIP-042i: Implement slashing appeals process (dispute window before slash executes)

## Acceptance Criteria

- Minimum stakes defined for all 3 node roles.
- Unstaking lock period defined and enforced.
- Slashing events and percentages enumerated.
- Slashed funds are disposed of as specified (burn vs ecosystem fund).
- Delegation allows non-operator token holders to participate in network security.

## Impact

- New: `contracts/staking/` (on-chain) or `docs/protocol/staking.md` (off-chain for Phase 1)
- Feeds: NIP-013 (Anti-Sybil), NIP-015 (Governance)

## Implementation Notes

- Minimum stake sketch:
  - Worker: 100 NMC
  - Validator: 500 NMC
  - Coordinator: 1,000 NMC
- Unstaking lock: 7 days (prevents stake-and-flee attacks).
- Slashing: 10% for missed deadline, 30% for dishonest validation, 100% for proven fraud.
- 50% of slashed amount burned; 50% to ecosystem fund.

## Dependencies

- NIP-040 (Token) — stake denominated in NMC
- NIP-014 (Reputation) — slash also triggers reputation penalty
- NIP-013 (Anti-Sybil) — Sybil detection triggers slashing
