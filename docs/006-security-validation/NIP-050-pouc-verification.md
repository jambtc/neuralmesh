# NIP-050 — PoUC Verification Implementation

- Status: 📋 Open
- Area: Security / Verification
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

PoUC (NIP-010) and the verification system (NIP-012) are protocol designs.
This NIP covers the concrete implementation of verification in code.

## Proposal

Implement the full verification pipeline:

### Sub-tasks

- [ ] NIP-050a: Implement output hash comparison between redundant workers
- [ ] NIP-050b: Implement tensor checksum verification (SHA-256 on serialized intermediate tensors)
- [ ] NIP-050c: Implement embedding cosine similarity for LLM/image outputs
- [ ] NIP-050d: Implement hidden task injection into task stream (5% rate)
- [ ] NIP-050e: Implement known-answer database for hidden tasks (per task type)
- [ ] NIP-050f: Implement VRF-based validator selection
- [ ] NIP-050g: Implement majority vote consensus with reputation weighting
- [ ] NIP-050h: Implement verification score calculation and storage
- [ ] NIP-050i: Implement dispute flagging and escalation queue

## Acceptance Criteria

- Output hash comparison correctly identifies mismatched results.
- Tensor checksum catches bit-flips in intermediate computation.
- Hidden task injection rate is empirically verified at 5% ± 0.5%.
- VRF validator selection is unpredictable and verifiable.
- Verification score is computed and stored for every completed task.

## Impact

- New package: `neuralmesh-client/internal/verification/`

## Implementation Notes

- Embedding similarity: use sentence-transformers `all-MiniLM-L6-v2` for embedding generation.
- VRF: use `go-vrf` library (IETF ECVRF, Ed25519).
- Hidden task database: seeded from curated public benchmarks (MMLU, HumanEval, etc.).
- Dispute escalation: tasks with VS < 0.3 are flagged for manual/council review.

## Dependencies

- NIP-012 (Verification system design) — implements this design
- NIP-010 (PoUC) — verification score feeds reward function
- NIP-041 (Rewards) — reward held in escrow until verification completes
