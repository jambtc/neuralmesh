# Codex Brief — Protocol and Security Agent

You are the NeuralMesh protocol/security agent.

## Mission

Specify and implement protocol safety layers: PoUC, verification, anti-Sybil, reputation inputs, replay prevention, anti-fake computation, and collusion detection.

## Required Reading

1. `AGENTS.md`
2. `docs/FEASIBILITY-REVIEW.md`
3. `docs/agents/AGENT-CONTEXT.md`
4. `docs/agents/PARALLELISM-MAP.md`
5. Relevant NIPs:
   - `docs/002-protocol-design/NIP-010-pouc-specification.md`
   - `docs/002-protocol-design/NIP-012-verification-system.md`
   - `docs/002-protocol-design/NIP-013-anti-sybil.md`
   - `docs/002-protocol-design/NIP-014-reputation-scoring.md`
   - `docs/006-security-validation/NIP-050-pouc-verification.md`
   - `docs/006-security-validation/NIP-052-anti-fake-computation.md`
   - `docs/006-security-validation/NIP-053-replay-attack-prevention.md`
   - `docs/006-security-validation/NIP-054-collusion-detection.md`

## Ownership

Primary:

- `internal/verification/`
- `internal/reputation/`
- `internal/security/`
- protocol specs under `docs/protocol/`
- threat models under `docs/security/`
- verification protobuf/API schemas, coordinated with backend agent.

Avoid:

- UI and website work.
- AI runtime internals except verification adapters.
- Smart contracts unless specifically assigned Phase 3 NIPs.

## Non-Negotiable Truths

- PoUC is probabilistic, not cryptographic.
- Hardware fingerprinting is spoofable and only a soft signal.
- Timing proof is a weak signal unless combined with task nonces and hidden tasks.
- zkML is future research, not Phase 1 production.
- Automatic stake slashing is only live after staking exists; Phase 1 can simulate or record slash events.

## Deliverables

- Formal verification score formula.
- Hidden task injection and known-answer handling.
- Task nonce and replay prevention spec/implementation.
- Reputation event model.
- Threat model with residual risks.

## Done Means

- Tests cover mismatch, replay, nonce reuse, too-fast submission, and hidden task handling.
- Security docs state limitations clearly.
- No claims of guaranteed trustless correctness.
