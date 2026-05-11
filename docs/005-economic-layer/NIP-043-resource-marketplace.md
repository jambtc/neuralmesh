# NIP-043 — Resource Marketplace Design

- Status: 📋 Open
- Area: Economic Layer / Marketplace
- Phase: 3–4
- Priority: Medium
- Date: 2026-05-11

## Context

A resource marketplace allows task requesters to browse available compute capacity and bid for it.
It enables price discovery and efficient allocation of compute resources.

## Proposal

Design the decentralized resource marketplace:

### Sub-tasks

- [ ] NIP-043a: Define marketplace listing schema (node capabilities, price per compute unit, availability)
- [ ] NIP-043b: Define task bidding protocol (open auction vs fixed price vs Dutch auction)
- [ ] NIP-043c: Implement node capability advertisement (broadcast listing to network)
- [ ] NIP-043d: Implement task request matching (requester broadcasts need → nodes bid)
- [ ] NIP-043e: Implement price oracle (historical price per task type per hardware tier)
- [ ] NIP-043f: Implement escrow for task payment (requester locks funds before execution)
- [ ] NIP-043g: Implement automated price floor (protocol minimum to prevent race-to-bottom)
- [ ] NIP-043h: Design marketplace UI (web dashboard for task requesters)
- [ ] NIP-043i: Implement analytics: compute supply/demand, price trends

## Acceptance Criteria

- Node can publish a listing with capabilities and price.
- Task requester can discover nodes matching requirements.
- Matched task is escrowed before execution begins.
- Price oracle provides historical price data for at least 7 days.
- Automated price floor prevents pricing below protocol minimum.

## Impact

- New: `neuralmesh-marketplace/` repository
- New: `docs/marketplace/marketplace-design.md`

## Implementation Notes

- Phase 3: fixed-price listings (simpler, lower latency).
- Phase 4: auction mechanism (dynamic price discovery).
- Price oracle: median of last 100 completed tasks per task type.
- Escrow: multisig release on successful verification.

## Dependencies

- NIP-040 (Token) — marketplace prices in NMC
- NIP-041 (Rewards) — reward distribution feeds from marketplace price
- NIP-011 (Task lifecycle) — task matching follows task lifecycle states
