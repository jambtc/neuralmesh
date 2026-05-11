# NIP-052 — Anti-Fake Computation

- Status: 📋 Open
- Area: Security / Integrity
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

The most direct attack on NeuralMesh is a node that claims to execute tasks but returns random or cached outputs.
Without countermeasures, a dishonest node could earn rewards without contributing real computation.

## Proposal

Implement countermeasures against fake computation:

### Attack Vectors Addressed

1. **Random output submission** — submit garbage as result
2. **Cached result replay** — return a real result from a previous identical task
3. **Partial execution** — run only part of the model and guess the rest
4. **Cross-node copying** — copy another worker's result before submitting own

### Sub-tasks

- [ ] NIP-052a: Implement task nonce (unique per-task random seed that changes output deterministically)
- [ ] NIP-052b: Implement timing proof (execution must complete within expected time window, not faster)
- [ ] NIP-052c: Implement intermediate checkpoint logging (prove model ran through all layers)
- [ ] NIP-052d: Implement hidden task cross-validation (NIP-050 hidden tasks catch garbage outputs)
- [ ] NIP-052e: Implement output uniqueness check (flag near-identical outputs from different workers)
- [ ] NIP-052f: Define penalty for detected fake computation (Phase 1: record slash event + reputation ban; Phase 3: execute stake slash after staking exists)

## Acceptance Criteria

- Task nonce is unique per execution and embedded in output hash.
- Timing proof flags results submitted faster than the calibrated hardware window; final rejection requires nonce/checkpoint/hidden-task corroboration.
- Intermediate checkpoint logging covers at least 25% of model layers.
- Near-identical output detection flags within 60s of result submission.
- Detected fake computation triggers automatic reputation penalty; stake slash is recorded in Phase 1 simulation and executed only after NIP-042 staking exists.

## Impact

- Updates: `neuralmesh-client/internal/sandbox/` (nonce injection)
- Updates: `neuralmesh-client/internal/verification/` (timing and checkpoint)

## Implementation Notes

- Task nonce: SHA-256(task_id + block_height + requester_pubkey) — unpredictable, per-task.
- Timing proof: node signs (start_timestamp, end_timestamp, task_id) — compare against calibrated hardware benchmark. Treat timing as a weak signal because cached outputs and clock manipulation can evade naive checks.
- Checkpoint: hash every Nth transformer layer output (N = total_layers / 4).
- Near-identical detection: cosine similarity > 0.999 between two workers' outputs → flag both.

## Dependencies

- NIP-050 (PoUC verification) — fake computation caught through verification pipeline
- NIP-042 (Staking) — Phase 3 executes stake slashes recorded by Phase 1 detection
- NIP-014 (Reputation) — ban on repeated fake computation
