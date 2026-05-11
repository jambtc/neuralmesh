# NeuralMesh — Codex Project Instructions

## Project Summary

NeuralMesh is a decentralized AI compute network.
Node operators contribute CPU/GPU resources; task requesters pay in NMC token; rewards are distributed through Proof of Useful Computation (PoUC).

## Working Language

All documentation, code comments, commit messages, and agent communication: **English only**.

## Documentation System

Tasks are tracked as NIP (NeuralMesh Implementation Plan) files under `docs/`.
Master index: `docs/NIP-INDEX.md`.

Structure:

```text
docs/
  001-foundation/          Phase 0
  002-protocol-design/     Phase 0-1, protocol specs
  003-mvp-core/            Phase 1, Go/Rust binaries
  004-ai-compute/          Phase 1-2, AI workload runners
  005-economic-layer/      Phase 3, token and economics
  006-security-validation/ Phase 1-3, security hardening
  007-community-ecosystem/ Phase 2, open source and community
  008-decentralization/    Phase 4, full P2P and governance
  agents/                  Agent orchestration files
```

## Before Starting Any Task

1. Read the relevant NIP file fully.
2. Read `docs/agents/AGENT-CONTEXT.md`.
3. Check dependencies in the NIP and in `docs/agents/PARALLELISM-MAP.md`.
4. Do not implement a NIP whose dependencies are not draft-complete or completed.
5. Check for dirty worktree changes and do not overwrite changes from other agents.

## Code Conventions

- Language: Go for network/daemon code; Rust only when a local package already uses it or performance requires it.
- No ORM. Use `sqlc` for type-safe SQL.
- No global mutable state. Pass `context.Context` and dependencies explicitly.
- Validate all external inputs at boundary.
- Test coverage target: at least 80% for packages under `internal/`.
- Docker images live in `docker/`, one folder per image.
- Protobuf definitions live in `proto/`, one file per service.
- Wire serialization uses Protocol Buffers unless a NIP explicitly says otherwise.

## Security Rules

- Never log secrets, tokens, private keys, task payload secrets, or seed material.
- All inter-node communication must be encrypted: TLS 1.3 or Noise protocol.
- Docker task containers must run without network access by default.
- Docker task containers must not mount host paths except designated readonly model/input volumes and controlled output volumes.
- Treat hardware fingerprints as soft signals only. Staking and reputation are the main Sybil deterrents.
- Treat PoUC verification as probabilistic, not cryptographic.

## Key Design Decisions

- Verification: redundant execution, hidden validation tasks, output similarity, and task nonces.
- P2P: libp2p-go with Kademlia DHT, QUIC transport, and Noise encryption.
- Task execution: Docker plus ONNX Runtime CPU/CUDA/ROCm variants.
- Database: PostgreSQL 16 for persistent state; Redis 7 for ephemeral queues and locks.
- Token standard: ERC-20 compatible in Phase 3, chain TBD.
- Model sharding: batch/async only in Phase 1. Real-time chat must use single-node execution.

## Out of Scope Unless a NIP Explicitly Opens It

- Direct PyTorch or TensorFlow execution. ONNX only.
- Project-run centralized API server as a long-term architecture.
- ICO, token speculation mechanics, or fundraising token sale copy.
- zkML as production verification before performance is practical.
- Real-time internet-wide model sharding.
- New workload types outside the approved NIP list.

## NIP Status Updates

When completing work on a NIP:

1. Update the NIP file status to `✅ Completed`.
2. Add a `## Verification` section listing files, tests, commands, and observed results.
3. Update `docs/NIP-INDEX.md`.
4. Update any affected agent brief if dependency or file ownership changed.

## Parallel Agent Rules

- Use `docs/agents/PARALLELISM-MAP.md` before starting.
- Prefer one agent per bounded file ownership area.
- Backend agents must not edit frontend docs except API contracts.
- Frontend agents must not edit protocol logic except typed API clients or mocks.
- Testing agents may add tests across packages but must not rewrite implementation unless asked.
- Documentation agents may edit docs and NIP files but must not mark code NIPs complete without implementation evidence.

## Git

- Do not run `git push` or open PRs unless explicitly requested by the human.
- Branch naming: `nip/NIP-XXX-short-description`.
- Commit message format: `NIP-XXX: short description`.
- Do not revert or overwrite changes made by another agent.
