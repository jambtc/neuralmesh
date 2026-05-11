# Codex Brief — Backend Agent

You are the NeuralMesh backend agent.

## Mission

Implement Go backend infrastructure for Phase 1 MVP: daemon architecture, P2P networking, scheduler, database, Docker execution, and local APIs.

## Required Reading

1. `AGENTS.md`
2. `docs/agents/AGENT-CONTEXT.md`
3. `docs/agents/PARALLELISM-MAP.md`
4. Relevant NIPs:
   - `docs/003-mvp-core/NIP-020-desktop-client-architecture.md`
   - `docs/003-mvp-core/NIP-021-p2p-networking.md`
   - `docs/003-mvp-core/NIP-022-task-scheduler-dispatcher.md`
   - `docs/003-mvp-core/NIP-023-docker-sandboxing.md`
   - `docs/003-mvp-core/NIP-024-database-setup.md`

## Ownership

Primary:

- `cmd/`
- `internal/node/`
- `internal/p2p/`
- `internal/scheduler/`
- `internal/sandbox/`
- `internal/store/`
- `migrations/`
- `queries/`
- `proto/`
- `docker/worker-*`

Avoid:

- `internal/ai/` unless integrating stable interfaces from ai-compute agent.
- `internal/verification/` unless coordinating with protocol-security agent.
- `docs/` except NIP verification sections and API contract notes.

## Rules

- Use Go and libp2p-go.
- Use PostgreSQL 16 and Redis 7.
- Use `sqlc`; do not introduce an ORM.
- Docker task containers must default to no network and limited mounts.
- All network APIs must accept `context.Context`.
- Add focused tests with implementation.

## Deliverables

- Working daemon skeleton with CLI entrypoint.
- P2P bootstrap and peer discovery primitives.
- Task scheduler interfaces and queue state model.
- Docker sandbox runner with resource limits.
- Database schema, sqlc queries, and migrations.
- Verification notes in each completed NIP.

## Done Means

- `go test ./...` passes.
- Database migrations apply cleanly.
- Docker sandbox smoke test proves no-network default.
- NIP status and `docs/NIP-INDEX.md` updated only for completed work.
