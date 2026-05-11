# NIP-040 — Token Design and Tokenomics

- Status: 📋 Open
- Area: Economic Layer / Token
- Phase: 3
- Priority: High
- Date: 2026-05-11

## Context

The NeuralMesh token represents AI compute value and is used for payments, rewards, governance, and staking.
Tokenomics must be designed to incentivize honest participation without enabling speculative abuse.

## Proposal

Design the complete tokenomics:

### Sub-tasks

- [ ] NIP-040a: Define token name, symbol, and decimals (e.g., NMC, 18 decimals)
- [ ] NIP-040b: Define total supply (fixed vs inflationary) and reasoning
- [ ] NIP-040c: Define supply distribution: mining rewards, team, ecosystem fund, investors, reserve
- [ ] NIP-040d: Define vesting schedule per allocation category
- [ ] NIP-040e: Define emission curve (block rewards over time: linear, exponential decay, halving)
- [ ] NIP-040f: Define token burn mechanisms (fee burning, slashing burns)
- [ ] NIP-040g: Define utility: compute payment, staking, governance, network security
- [ ] NIP-040h: Model inflation rate over 10 years
- [ ] NIP-040i: Legal review of token classification (utility vs security)

## Acceptance Criteria

- Total supply and distribution percentages are defined and sum to 100%.
- Vesting schedule defined for all non-mining allocations.
- Emission curve modeled with target year to reach 50% of supply.
- Inflation rate modeled over 10 years.
- At least 3 token burn mechanisms defined.
- Legal review completed (utility token classification confirmed or disclaimed).

## Impact

- New: `docs/tokenomics/NMC-tokenomics.md`
- Feeds: NIP-001 (whitepaper), NIP-041 (reward distribution), NIP-042 (staking)

## Implementation Notes

- Suggested distribution sketch:
  - 60% — mining rewards (distributed over 10+ years)
  - 15% — ecosystem fund
  - 10% — team (4-year vesting, 1-year cliff)
  - 10% — investors (2-year vesting)
  - 5% — reserve
- Emission: exponential decay (Bitcoin-like halvings every 2 years).
- Burn: 30% of task fees burned; 70% to reward pool.

## Dependencies

- NIP-010 (PoUC) — mining reward formula
- NIP-025 (Simulation) — tokenomics validated by simulation
- NIP-015 (Governance) — governance token mechanics
