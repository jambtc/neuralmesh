# 003 — MVP Core Infrastructure

Phase 1 macro-area: the minimum viable product.
Delivers a working node that can execute tasks, earn rewards, and communicate with peers.

## NIP Index

| ID | Title | Status |
|----|-------|--------|
| [NIP-020](NIP-020-desktop-client-architecture.md) | Desktop client architecture (Go/Rust) | 📋 Open |
| [NIP-021](NIP-021-p2p-networking.md) | P2P networking layer | 📋 Open |
| [NIP-022](NIP-022-task-scheduler-dispatcher.md) | Task scheduler and dispatcher | 📋 Open |
| [NIP-023](NIP-023-docker-sandboxing.md) | Docker sandboxing execution | 📋 Open |
| [NIP-024](NIP-024-database-setup.md) | Database setup (PostgreSQL + Redis) | 📋 Open |
| [NIP-025](NIP-025-reward-simulation.md) | Reward simulation engine | 📋 Open |

## Dependencies

- All NIPs in 002-protocol-design must be at least draft-complete.
- NIP-030 (ONNX) informs NIP-023 (sandboxing) and NIP-022 (scheduler).

## Budget Estimate (Phase 1)

- Out-of-pocket costs: 2,000€-5,000€
- Developer labor: 50,000€-150,000€
- Realistic total: 55,000€-155,000€
