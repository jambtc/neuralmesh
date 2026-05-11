# NIP-063 — Benchmark Publishing

- Status: 📋 Open
- Area: Community / Transparency
- Phase: 2
- Priority: Medium
- Date: 2026-05-11

## Context

Benchmarks demonstrate real performance, build credibility, and help node operators understand expected earnings.
They also provide data for the reward simulation (NIP-025) and tokenomics (NIP-040).

## Proposal

Produce and publish performance benchmarks:

### Sub-tasks

- [ ] NIP-063a: Define benchmark suite: task types × hardware tiers
- [ ] NIP-063b: Run LLM inference benchmarks (tokens/second): CPU, 4GB GPU, 8GB GPU, 16GB GPU
- [ ] NIP-063c: Run image generation benchmarks (images/minute): 4GB GPU, 8GB GPU, 16GB GPU
- [ ] NIP-063d: Run OCR benchmarks (pages/minute): CPU
- [ ] NIP-063e: Run STT benchmarks (real-time factor): CPU
- [ ] NIP-063f: Measure P2P latency overhead vs direct inference
- [ ] NIP-063g: Measure reward simulation results (expected NMC/hour per hardware tier)
- [ ] NIP-063h: Publish results in `docs/benchmarks/` with methodology
- [ ] NIP-063i: Create comparison table: NeuralMesh vs centralized API pricing

## Acceptance Criteria

- Benchmarks run on at least 4 distinct hardware configurations.
- Methodology is documented (hardware specs, OS, driver versions, model versions).
- Results are reproducible (benchmark scripts published in repository).
- Expected earnings per hardware tier published (simulation-based for Phase 1).
- Comparison table shows cost advantage vs OpenAI API.

## Impact

- New: `docs/benchmarks/`
- New: `tools/benchmark/` scripts

## Implementation Notes

- Run benchmarks on: AMD Ryzen 7 CPU only, NVIDIA RTX 3060 12GB, RTX 4070 Ti 16GB, RTX 4090 24GB.
- Publish raw numbers — no cherry-picking.
- Update benchmarks with each major release.
