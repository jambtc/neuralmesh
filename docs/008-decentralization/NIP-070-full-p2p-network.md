# NIP-070 — Full P2P Network (No Bootstrap Dependency)

- Status: 📋 Open
- Area: Decentralization / Networking
- Phase: 4
- Priority: High
- Date: 2026-05-11

## Context

Phase 1 P2P networking (NIP-021) relies on project-run bootstrap nodes for initial peer discovery.
This is a centralization point: if the project shuts down, new nodes cannot join.
Phase 4 eliminates this dependency.

## Proposal

Transition to a fully decentralized peer discovery mechanism:

### Sub-tasks

- [ ] NIP-070a: Implement DNS-based peer seeding (publish well-known peer list via DNS TXT records)
- [ ] NIP-070b: Implement IPFS-based peer list publication (peer list stored on IPFS, content-addressed)
- [ ] NIP-070c: Implement peer exchange protocol (nodes share peer lists with each other)
- [ ] NIP-070d: Remove hard-coded bootstrap node dependency from client
- [ ] NIP-070e: Implement super-node election (high-reputation, high-uptime nodes become bootstrap peers)
- [ ] NIP-070f: Implement network partition detection and recovery
- [ ] NIP-070g: Stress test with 1000+ simulated nodes
- [ ] NIP-070h: Document measured network resilience properties and residual centralization risks

## Acceptance Criteria

- Network bootstraps without relying on a single project-run bootstrap server.
- A new node discovers the network within 60s using at least one seed channel (DNS, IPFS peer list, peer exchange snapshot, or user-provided peer).
- Network recovers from 50% node loss within 10 minutes.
- Super-node election is deterministic and based on verifiable reputation data.

## Impact

- Updates: `neuralmesh-client/internal/network/` (bootstrap removal)
- New: DNS TXT record publishing tooling

## Implementation Notes

- DNS TXT record: `_neuralmesh._tcp.neuralmesh.network` listing 10 seed peers. DNS is a convenience seed channel, not the only discovery mechanism.
- IPFS peer list: updated weekly by governance vote.
- Peer exchange: every 60s, nodes share 5 random peers with each connected peer.
- Super-node threshold: uptime > 90% over 30 days AND reputation > 700.

## Dependencies

- NIP-021 (P2P networking) — builds on Phase 1 implementation
- NIP-014 (Reputation) — super-node election uses reputation scores
