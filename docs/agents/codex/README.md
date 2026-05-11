# Codex Agent Briefs

These files are ready-to-use prompts for running parallel Codex agents on NeuralMesh.

## Use

1. Open the brief matching the work area.
2. Paste the full brief into a fresh Codex agent.
3. Assign one bounded task or NIP at a time.
4. Keep work areas separate to avoid merge conflicts.

## Briefs

| File | Agent |
|------|-------|
| `backend.md` | Go daemon, P2P, scheduler, database, Docker execution |
| `ai-compute.md` | ONNX Runtime, LLM pipeline, workload runners, sharding |
| `frontend.md` | CLI, local dashboard, optional GUI, landing page |
| `protocol-security.md` | PoUC, verification, anti-Sybil, replay, collusion |
| `testing.md` | Unit/integration/security tests, CI, fixtures, benchmarks |
| `documentation.md` | NIPs, protocol docs, developer docs, feasibility alignment |

## Coordination

- Read `AGENTS.md` first.
- Read `docs/agents/AGENT-CONTEXT.md`.
- Read `docs/agents/PARALLELISM-MAP.md`.
- Read the specific NIP before editing.
- Do not mark a NIP completed without tests or verifiable artifacts.
