# NIP-031 — Model Sharding (Tensor Shards)

- Status: 📋 Open
- Area: AI Compute / Distribution
- Phase: 1
- Priority: High
- Date: 2026-05-11

## Context

Large models (7B+ parameters) don't fit in consumer GPU VRAM (typically 4–16GB).
Model sharding splits inference across multiple nodes, enabling consumer hardware participation for large models.

## ⚠️ Latency Constraint — Batch Tasks Only

Layer-wise sharding across internet-connected nodes adds significant latency: **50–200 ms per layer boundary** depending on network conditions.

For a 32-layer 7B model split across 2 nodes: ~1.6–6.4 s added latency on top of compute time.

**Sharding is scoped to batch and async tasks only.**
Real-time tasks (chat, streaming inference, first-token latency < 2 s) must run on a single node with sufficient VRAM.
Sharding for real-time use is a Phase 4 research item, not a Phase 1 commitment.

## Proposal

Implement distributed model sharding:

### Sharding Approaches

1. **Layer-wise sharding** — transformer layers split across nodes (pipeline parallelism)
2. **Tensor sharding** — individual weight matrices split (tensor parallelism)
3. **Sequence sharding** — input tokens split across nodes (sequence parallelism)

### Sub-tasks

- [ ] NIP-031a: Define sharding strategy for Phase 1 (layer-wise first, simpler)
- [ ] NIP-031b: Implement model layer partitioning (split ONNX graph at layer boundaries)
- [ ] NIP-031c: Implement shard assignment protocol (coordinator assigns layers to workers)
- [ ] NIP-031d: Implement inter-node activation passing (output of layer N → input of layer N+1)
- [ ] NIP-031e: Implement shard failure handling (fallback: reassign failed layer to another node)
- [ ] NIP-031f: Define shard reward splitting formula (proportional to layers executed)
- [ ] NIP-031g: Measure latency overhead vs single-node inference; document clearly in API response (task must be flagged as `mode: batch` to use sharding)

## Acceptance Criteria

- A 7B parameter model runs successfully split across 2+ nodes (batch mode only).
- Shard failure is detected and the task is reassigned within 30s.
- Reward is split proportionally to layers completed.
- Task API rejects real-time tasks routed to sharded execution (returns error: `use_single_node`).
- Latency overhead for 2-node split is measured and documented (no target — just transparency).

## Impact

- New package: `neuralmesh-client/internal/ai/sharding/`
- New: `docs/protocol/model-sharding.md`

## Implementation Notes

- Start with layer-wise sharding (simpler to implement and verify).
- Activation tensors passed via gRPC streaming between nodes.
- Shard coordinator is the node that accepted the task originally.
- Minimum VRAM for sharded participation: 2GB.

## Dependencies

- NIP-030 (ONNX Runtime) — shard execution uses ONNX runtime
- NIP-021 (P2P networking) — activation passing uses P2P layer
- NIP-041 (Reward distribution) — shard reward splitting formula
