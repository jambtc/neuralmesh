# NIP-071 — Distributed Governance Implementation

- Status: 📋 Open
- Area: Decentralization / Governance
- Phase: 4
- Priority: High
- Date: 2026-05-11

## Context

Phase 3 governance uses off-chain signaling (Snapshot) with a council executing decisions.
Phase 4 moves governance fully on-chain, removing the council as a trust dependency.

## Proposal

Implement fully on-chain distributed governance:

### Sub-tasks

- [ ] NIP-071a: Design on-chain voting contract (or equivalent on chosen ledger)
- [ ] NIP-071b: Implement proposal submission with stake requirement
- [ ] NIP-071c: Implement voting with weight formula from NIP-015
- [ ] NIP-071d: Implement timelock for approved proposals (7-day execution delay)
- [ ] NIP-071e: Implement automatic proposal execution after timelock
- [ ] NIP-071f: Implement emergency multisig veto with 5-of-9 council override
- [ ] NIP-071g: Implement governance parameter upgrades (change any protocol param via vote)
- [ ] NIP-071h: Migrate Phase 3 governance data to on-chain state
- [ ] NIP-071i: Audit smart contract / on-chain logic (external security audit required)

## Acceptance Criteria

- Proposal submission, voting, timelock, and execution are all on-chain.
- Voting weight formula matches NIP-015 specification exactly.
- Emergency veto requires 5-of-9 multisig and executes within 24h.
- Governance parameter change propagates to all nodes within 1 consensus round.
- External audit completed with no critical findings unresolved.

## Impact

- New: `contracts/governance/` (on-chain governance contracts)
- Updates: all nodes must upgrade to support governance parameter updates

## Implementation Notes

- External audit: budget 20,000–50,000€ for production audit.
- Timelock prevents rushed malicious proposals.
- Governance upgrades are backward-compatible via feature flags where possible.

## Dependencies

- NIP-015 (Governance model design) — implements this design
- NIP-040 (Token) — voting weight uses token balance
- NIP-042 (Staking) — proposal submission requires stake
