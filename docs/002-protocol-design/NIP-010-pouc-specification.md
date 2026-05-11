# NIP-010 — Proof of Useful Computation (PoUC) Specification

- Status: 📋 Open
- Area: Protocol Design / Consensus
- Phase: 0–1
- Priority: Critical
- Date: 2026-05-11

## Context

Traditional PoW wastes energy on cryptographic puzzles with no real-world value.
NeuralMesh replaces this with computation that produces verifiable, useful output (AI inference, rendering, simulation).

PoUC is the core consensus primitive of the entire protocol — nothing else can be designed without it.

## Proposal

Formally specify PoUC:

### Sub-tasks

- [ ] NIP-010a: Define "useful computation" — what qualifies, what does not
- [ ] NIP-010b: Define task types eligible for PoUC rewards (AI inference, rendering, OCR, simulation)
- [ ] NIP-010c: Define the PoUC reward function: `R = f(task_type, compute_units, verification_score, reputation)`
- [ ] NIP-010d: Specify compute unit measurement per task type (FLOPS, tokens/s, ms render time)
- [ ] NIP-010e: Define verification score range and how it affects reward
- [ ] NIP-010f: Specify difficulty adjustment mechanism (analogous to PoW difficulty)
- [ ] NIP-010g: Define minimum viable proof of execution (output hash + timing signature)
- [ ] NIP-010h: Document attack surfaces specific to PoUC and mitigations

## Acceptance Criteria

- PoUC reward function is formally defined with all variables explained.
- Compute unit measurement is defined for at least 3 task types.
- Difficulty adjustment mechanism is described with adjustment interval.
- Minimum viable proof of execution is specified.
- At least 3 attack vectors are identified with mitigations.

## Impact

- New: `docs/protocol/pouc-spec.md`
- Feeds: NIP-001 (whitepaper), NIP-012 (verification), NIP-041 (reward distribution)

## Implementation Notes

- Reference: Bittensor's incentive mechanism for distributed ML compute.
- Compute units should be normalized across hardware types to avoid GPU-only domination.
- Reward function should penalize low verification scores non-linearly (dishonest nodes lose more than they gain).
- Consider time-weighting: tasks completed faster within deadline earn bonus.

## ⚠️ Verification Caveat

PoUC verification is **probabilistic, not cryptographic**.
The current approach (redundant execution + output similarity + hidden benchmark tasks) provides measurable statistical confidence but does not produce a zero-knowledge proof of correct execution.

- P(cheat undetected per task) decreases as hidden task injection rate increases, but never reaches zero.
- zkML (cryptographic ML proof) exists in research prototypes but is 100x–10,000x slower than inference itself, making it impractical for production use in 2026.
- This must be disclosed clearly in the whitepaper and all public documentation.
- The verification model is sound for an MVP; zkML can be integrated as future research matures.

## Dependencies

- NIP-012 (Verification system) — verification score is an input to the reward function
- NIP-014 (Reputation scoring) — reputation is an input to the reward function
