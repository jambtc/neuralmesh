# NIP-054 — Collusion Detection

- Status: 📋 Open
- Area: Security / Integrity
- Phase: 2–3
- Priority: Medium
- Date: 2026-05-11

## Context

Colluding nodes could coordinate to pass each other's fake results through validation consensus.
This is a sophisticated attack that requires network-level behavioral analysis to detect.

## Proposal

Implement collusion detection:

### Collusion Patterns

1. **Validator ring** — small group always validates each other's results positively
2. **Result sharing** — multiple nodes submit identical results (NIP-052 catches basic cases)
3. **Timing coordination** — nodes submit results within milliseconds of each other (pre-coordinated)
4. **IP clustering** — colluding nodes share IP subnet

### Sub-tasks

- [ ] NIP-054a: Implement validator co-occurrence tracking (track which nodes validate each other)
- [ ] NIP-054b: Implement co-occurrence anomaly detection (chi-square test on validator pairs)
- [ ] NIP-054c: Implement result submission timing analysis (flag millisecond-precision synchronization)
- [ ] NIP-054d: Implement IP clustering detection (flag groups sharing /24 subnet)
- [ ] NIP-054e: Implement collusion score per node (aggregated suspicion score)
- [ ] NIP-054f: Define collusion investigation protocol (evidence collection → council review)
- [ ] NIP-054g: Define collusion penalty (Phase 2: evidence and reputation action; Phase 3: stake slash for proven colluding nodes)

## Acceptance Criteria

- Co-occurrence tracking runs continuously on validation history.
- Anomalous co-occurrence triggers alert within 24h.
- Timing analysis flags synchronization within 100ms precision.
- IP clustering flags groups of ≥ 3 nodes in same /24 subnet.
- Collusion investigation protocol documented and actionable.

## Impact

- New package: `neuralmesh-client/internal/analytics/collusion/`
- New: `docs/security/collusion-detection.md`

## Implementation Notes

- Co-occurrence: sliding window of 7 days; flag if pair validates each other > 3x expected frequency.
- Timing analysis: flag if 3+ nodes submit results within 100ms for the same task.
- Phase 2: detection only (alerts, no automatic action).
- Phase 3: automatic collusion score feeds into governance penalty proposals.

## Dependencies

- NIP-050 (Verification) — co-occurrence data comes from verification history
- NIP-013 (Anti-Sybil) — IP clustering overlaps with Sybil detection
- NIP-042 (Staking) — Phase 3 collusion penalty includes stake slashing
- NIP-015 (Governance) — council reviews collusion evidence
