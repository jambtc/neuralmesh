# NIP-013 — Anti-Sybil Mechanisms Design

- Status: 📋 Open
- Area: Protocol Design / Security
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

A Sybil attack occurs when one entity creates many fake identities to dominate the network.
In NeuralMesh, this could allow a single actor to control validation consensus or drain rewards.

## ⚠️ Hardware Fingerprint Limitation

Hardware fingerprints (CPU/GPU serial hashes) are a **soft signal only**, not a hard proof of distinct physical hardware.

On Linux, GPU serials are readable by any process with NVML access and can be spoofed in software.
A determined attacker can run 100 virtual nodes on 2 physical GPUs with different spoofed fingerprints.

**Primary Sybil deterrent: economic collateral (staking).**
Running 100 fake identities requires staking 100× the minimum — this is the actual cost that makes Sybil attacks unprofitable.
Hardware fingerprinting is a secondary heuristic that raises the effort bar slightly.

## Proposal

Design a layered anti-Sybil system:

### Mechanisms (ordered by effectiveness)

1. **Economic collateral** — stake requirement is the primary deterrent; fake identities cost real money
2. **Reputation scoring** — new nodes start with low trust; trust is earned over time (cannot be faked cheaply)
3. **Hardware entropy** — soft signal: raises effort bar, not a hard proof
4. **Bandwidth analysis** — traffic patterns distinguish real nodes from co-located clones
5. **Proof-of-human extensions** — optional social/identity verification for higher trust tier

### Sub-tasks

- [ ] NIP-013a: Define node identity scheme (public key + hardware fingerprint as soft signal)
- [ ] NIP-013b: Specify hardware entropy collection (CPU/GPU serial hash, TPM if available) — treat as heuristic, not proof
- [ ] NIP-013c: Define minimum stake requirement for validator role
- [ ] NIP-013d: Design bandwidth fingerprinting to detect co-located nodes
- [ ] NIP-013e: Define trust tiers (new, verified, trusted, elite) with capabilities per tier
- [ ] NIP-013f: Specify proof-of-human integration (optional: email, GitHub OAuth, phone)
- [ ] NIP-013g: Define rate limiting per identity for task submission and validation

## Acceptance Criteria

- Node identity scheme is specified with at least 2 entropy sources (treated as heuristics).
- Hardware fingerprinting method defined with explicit caveat: spoofable, soft signal only.
- Minimum stake for validator role specified.
- Trust tiers defined with entry requirements and capabilities.
- Rate limiting rules specified.

## Impact

- New: `docs/protocol/anti-sybil.md`
- Feeds: NIP-012 (validator selection), NIP-014 (reputation), NIP-042 (staking)

## Implementation Notes

- Hardware fingerprinting must not leak personally identifiable information.
- Stake slashing (partial loss) for provably dishonest behavior.
- Co-located node detection: same IP subnet + similar latency patterns = flagged.
- Proof-of-human is optional but unlocks higher trust tier faster.

## Dependencies

- NIP-014 (Reputation) — trust tiers feed reputation system
- NIP-042 (Staking) — economic collateral implementation
