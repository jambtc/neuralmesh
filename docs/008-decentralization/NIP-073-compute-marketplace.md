# NIP-073 — Autonomous Compute Marketplace

- Status: 📋 Open
- Area: Decentralization / Marketplace
- Phase: 4
- Priority: Medium
- Date: 2026-05-11

## Context

Phase 3 marketplace (NIP-043) uses fixed-price listings and project-run matching infrastructure.
Phase 4 evolves this into a fully autonomous, auction-based, decentralized marketplace.

## Proposal

Evolve the marketplace to full decentralization:

### Sub-tasks

- [ ] NIP-073a: Implement Dutch auction mechanism for task pricing (price starts high, decreases until a worker accepts)
- [ ] NIP-073b: Implement fully on-chain order book (task requests and worker bids recorded on-chain)
- [ ] NIP-073c: Implement automated market maker (AMM) for compute resource pricing
- [ ] NIP-073d: Remove project-run matching server dependency
- [ ] NIP-073e: Implement reputation-weighted matching (higher reputation workers get priority bids)
- [ ] NIP-073f: Implement SLA contracts (on-chain enforceable latency and quality commitments)
- [ ] NIP-073g: Implement automated refund on SLA breach
- [ ] NIP-073h: Implement marketplace analytics dashboard (decentralized, no central server)

## Acceptance Criteria

- Task submission to matching to execution requires no project infrastructure.
- Dutch auction completes in under 5s for standard task types.
- On-chain order book handles 100 tasks/minute without congestion.
- SLA breach triggers automatic refund within one consensus round.
- Analytics dashboard runs entirely from on-chain data queries.

## Impact

- Replaces: Phase 3 `neuralmesh-marketplace/` with fully decentralized implementation
- New: AMM contracts

## Implementation Notes

- Dutch auction interval: price drops 1% every 2s until accepted or timeout.
- AMM: bonding curve for compute unit pricing based on supply/demand.
- SLA: latency commitment enforced by timestamp difference on-chain.
- Analytics: build from event log queries on the ledger (no API server needed).

## Dependencies

- NIP-043 (Resource marketplace) — Phase 4 replaces Phase 3 marketplace
- NIP-040 (Token) — marketplace prices in NMC
- NIP-071 (Governance) — marketplace parameter changes go through governance
