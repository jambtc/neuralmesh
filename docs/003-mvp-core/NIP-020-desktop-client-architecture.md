# NIP-020 — Desktop Client Architecture (Go/Rust)

- Status: 📋 Open
- Area: MVP Core / Client
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

The desktop client is the primary interface for node operators.
It manages node identity, resource contribution, task execution, and reward tracking.
No client exists yet.

## Proposal

Design and implement the desktop client:

### Sub-tasks

- [ ] NIP-020a: Choose language: Go vs Rust (performance vs developer tooling tradeoff)
- [ ] NIP-020b: Define client architecture (daemon + CLI + optional GUI)
- [ ] NIP-020c: Implement node identity management (key generation, storage, rotation)
- [ ] NIP-020d: Implement hardware capability detection (CPU cores, GPU VRAM, RAM, bandwidth)
- [ ] NIP-020e: Implement resource limit configuration (max CPU%, max GPU%, max bandwidth)
- [ ] NIP-020f: Implement P2P connection management (delegates to NIP-021)
- [ ] NIP-020g: Implement task execution runner (delegates to NIP-022, NIP-023)
- [ ] NIP-020h: Implement reward tracking and local stats dashboard
- [ ] NIP-020i: Package as binary for Linux, macOS, Windows
- [ ] NIP-020j: Write CLI reference documentation

## Acceptance Criteria

- Binary builds on Linux, macOS, and Windows.
- Node identity persists across restarts.
- Hardware detection correctly identifies CPU, GPU, RAM.
- Resource limits are respected during task execution.
- CLI shows current node status, active tasks, and earned rewards.

## Impact

- New repository: `neuralmesh-client`
- Main binary: `neuralmesh-node`

## Implementation Notes

- Recommended: Go (faster onboarding, good P2P library ecosystem via libp2p-go).
- Daemon listens on local socket; CLI communicates via RPC.
- Key storage: encrypted local file (age or nacl secretbox).
- GPU detection: use platform-specific APIs (NVML for NVIDIA, ROCm for AMD).

## Dependencies

- NIP-021 (P2P networking) — networking layer integrated into daemon
- NIP-022 (Task scheduler) — task execution managed by scheduler
- NIP-004 (Technical spec) — wire protocol and API surface
