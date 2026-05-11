# NIP-051 — Anti-ASIC Design

- Status: 📋 Open
- Area: Security / Hardware Fairness
- Phase: 1
- Priority: Medium
- Date: 2026-05-11

## Context

ASIC domination would centralize NeuralMesh compute power in the hands of hardware manufacturers,
defeating the human-centric participation goal.
The protocol must remain economically accessible to consumer hardware.

## ⚠️ Scope Limitation

AI-specific hardware accelerators already exist and are mainstream: Apple Neural Engine, Google TPU, Intel Gaudi, Qualcomm AI 100, NVIDIA DGX.
These are not "ASICs" in the crypto sense but general AI accelerators — and they run ONNX models natively.

**Full ASIC resistance for AI workloads is not achievable.**
Purpose-built AI hardware will always outperform consumer GPUs on inference per watt.

The realistic goal of this NIP is **economic fairness** — ensuring consumer GPU nodes remain profitable enough to participate — not hardware parity with datacenters.
Dynamic workloads and memory requirements slow centralization but cannot prevent it indefinitely.

## Proposal

Implement anti-ASIC mechanisms:

### Sub-tasks

- [ ] NIP-051a: Implement dynamic workload rotation (slows optimization for any fixed hardware profile)
- [ ] NIP-051b: Enforce minimum model size per task type (memory-hard; limits advantage of bandwidth-optimized hardware)
- [ ] NIP-051c: Implement heterogeneous task graphs (random execution order)
- [ ] NIP-051d: Implement randomized model selection (coordinator assigns model variant, not requester)
- [ ] NIP-051e: Define throughput anomaly heuristics (claimed throughput > 10× hardware class median → flag)
- [ ] NIP-051f: Monitor hardware capability claims vs actual throughput ratios
- [ ] NIP-051g: Define economic fairness floor via governance: minimum reward ratio consumer GPU / best-in-class hardware ≥ 0.3×

## Acceptance Criteria

- Dynamic workload rotation changes task type distribution weekly.
- Minimum model size enforced per task type (minimum working set defined).
- Throughput anomaly heuristics defined with threshold values.
- Hardware throughput anomalies are logged and flagged.
- Economic fairness floor defined: consumer RTX 4070 earns ≥ 30% of what an H100 earns per hour.

## Impact

- Updates: `neuralmesh-client/internal/scheduler/` (task type rotation)
- New: `docs/protocol/anti-asic-policy.md`

## Implementation Notes

- Memory-hard: LLM inference naturally requires large RAM/VRAM; enforce minimum model size.
- Throughput ratio: if claimed throughput > 10x hardware class median → flag for review.
- Randomized model selection: requester specifies task type but not model variant — coordinator assigns variant.

## Dependencies

- NIP-022 (Scheduler) — task rotation implemented in scheduler
- NIP-013 (Anti-Sybil) — ASIC farm detection overlaps with Sybil detection
- NIP-015 (Governance) — ASIC policy changes go through governance
