# NIP-053 — Replay Attack Prevention

- Status: 📋 Open
- Area: Security / Network
- Phase: 1
- Priority: High
- Date: 2026-05-11

## Context

A replay attack occurs when a valid message (task result, reward claim, validation vote) is captured and re-submitted later to gain illegitimate rewards or disrupt consensus.

## Proposal

Implement replay attack prevention:

### Sub-tasks

- [ ] NIP-053a: Implement message sequence numbers per peer connection
- [ ] NIP-053b: Implement nonce-based message deduplication (nonce window: last 1000 messages per peer)
- [ ] NIP-053c: Implement timestamp-bound message validity (reject messages older than 60s)
- [ ] NIP-053d: Implement task result linking (result must reference task_id + block_height at assignment time)
- [ ] NIP-053e: Implement reward claim nonce (each claim is single-use, recorded in ledger)
- [ ] NIP-053f: Implement signature freshness verification (signature timestamp checked against local clock ± 30s)

## Acceptance Criteria

- Replayed task result from a previous execution is rejected.
- Messages older than 60 seconds are rejected.
- Reward claim nonces are stored and checked (double-claim rejected).
- Signature freshness check rejects signatures with stale timestamps.
- Sequence number gaps are detected and trigger peer investigation.

## Impact

- Updates: `neuralmesh-client/internal/network/` (message dedup and sequence)
- Updates: `neuralmesh-client/internal/rewards/` (claim nonce)

## Implementation Notes

- Nonce window: sliding window of last 1000 message nonces per peer (ring buffer in memory).
- Block height binding: each task result references the block height at assignment — replayed results reference wrong height.
- Clock skew tolerance: ± 30s (accounts for NTP drift on consumer hardware).
- Persistent nonce store: claim nonces stored in PostgreSQL (survive restarts).

## Dependencies

- NIP-021 (P2P networking) — message layer implements sequence numbers
- NIP-041 (Rewards) — reward claims use single-use nonces
