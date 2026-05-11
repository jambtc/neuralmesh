# NIP-025 — Reward Simulation Engine

- Status: 📋 Open
- Area: MVP Core / Economics
- Phase: 1
- Priority: Medium
- Date: 2026-05-11

## Context

Before deploying a real token, the reward mechanism must be validated through simulation.
Simulation allows testing economic balance, fairness, and attack resistance without financial risk.

This NIP also validates the budget estimates in the roadmap — Phase 3 token launch requires confirmed economic soundness from simulation results before proceeding.

## Proposal

Build a reward simulation engine:

### Sub-tasks

- [ ] NIP-025a: Implement configurable network simulation (N nodes, M tasks/hour)
- [ ] NIP-025b: Implement PoUC reward formula simulation (NIP-010)
- [ ] NIP-025c: Implement reputation score evolution over simulated time
- [ ] NIP-025d: Simulate Sybil attack scenarios (% of fake nodes)
- [ ] NIP-025e: Simulate honest vs dishonest node strategies (game theory)
- [ ] NIP-025f: Produce output metrics: Gini coefficient, reward per node type, attack ROI
- [ ] NIP-025g: Export simulation results to CSV and chart
- [ ] NIP-025h: Document simulation parameters and findings in `docs/simulation-report.md`

## Acceptance Criteria

- Simulation runs for configurable duration (e.g., 30-day equivalent).
- Gini coefficient of reward distribution is below 0.4 (reasonable fairness).
- Sybil attack with 20% fake nodes yields negative ROI for attacker.
- Dishonest node strategy yields lower long-term rewards than honest strategy.
- Results exported to CSV and at least 3 charts generated.

## Impact

- New tool: `neuralmesh-client/tools/simulate/`
- New: `docs/simulation-report.md`

## Implementation Notes

- Language: Go or Python (Python preferred for data analysis / matplotlib output).
- Monte Carlo approach: run 1000 simulations per parameter set.
- Gini target: < 0.35 (similar to Nordic countries income distribution).
- Publish findings before Phase 2 community launch for transparency.

## Dependencies

- NIP-010 (PoUC) — reward formula is the simulation input
- NIP-014 (Reputation) — reputation evolution is simulated
- NIP-041 (Reward distribution) — distribution algorithm feeds simulation
