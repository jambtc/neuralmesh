# NIP-021 — P2P Networking Layer

- Status: 📋 Open
- Area: MVP Core / Networking
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

NeuralMesh requires a peer-to-peer network for node discovery, task distribution, and result delivery.
No networking layer exists.

## Proposal

Implement the P2P networking layer:

### Sub-tasks

- [ ] NIP-021a: Choose P2P library (libp2p-go vs custom vs Kademlia DHT)
- [ ] NIP-021b: Implement node discovery via DHT (Kademlia)
- [ ] NIP-021c: Implement bootstrap node list (hardcoded initial peers)
- [ ] NIP-021d: Implement peer connection management (max peers, connection pooling)
- [ ] NIP-021e: Implement message routing (task announce, result delivery, heartbeat)
- [ ] NIP-021f: Implement NAT traversal (hole punching, UPnP)
- [ ] NIP-021g: Implement peer reputation tracking at network layer (ban, downgrade)
- [ ] NIP-021h: Implement encrypted transport (TLS 1.3 or Noise protocol)
- [ ] NIP-021i: Define and implement gossip protocol for network state propagation

## Acceptance Criteria

- Two nodes on different networks can discover each other via bootstrap node.
- NAT traversal works for at least 80% of common router configurations.
- All peer communication is encrypted.
- Network layer handles peer disconnect and reconnect gracefully.
- Gossip propagation reaches 90% of network within 10 hops.

## Impact

- New package: `neuralmesh-client/internal/network/`

## Implementation Notes

- Use libp2p-go (battle-tested, supports DHT, QUIC, noise protocol).
- Bootstrap nodes hosted by project; list is configurable.
- QUIC transport preferred (better NAT traversal than TCP).
- Gossip interval: 5s for task announcements, 30s for heartbeats.

## Dependencies

- NIP-020 (Client architecture) — network layer is embedded in daemon
- NIP-013 (Anti-Sybil) — peer banning feeds from anti-Sybil detection
