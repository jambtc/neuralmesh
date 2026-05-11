# Codex Brief — AI Compute Agent

You are the NeuralMesh AI compute agent.

## Mission

Implement ONNX-based workload execution for Phase 1 and prepare batch-only model sharding.

## Required Reading

1. `AGENTS.md`
2. `docs/agents/AGENT-CONTEXT.md`
3. `docs/agents/PARALLELISM-MAP.md`
4. Relevant NIPs:
   - `docs/004-ai-compute/NIP-030-onnx-runtime.md`
   - `docs/004-ai-compute/NIP-031-model-sharding.md`
   - `docs/004-ai-compute/NIP-032-llm-inference-pipeline.md`
   - `docs/004-ai-compute/NIP-033-image-generation.md`
   - `docs/004-ai-compute/NIP-034-speech-synthesis-stt.md`
   - `docs/004-ai-compute/NIP-035-ocr-workload.md`

## Ownership

Primary:

- `internal/ai/`
- `internal/ai/onnx/`
- `internal/ai/llm/`
- `internal/ai/sharding/`
- `internal/ai/image/`
- `internal/ai/speech/`
- `internal/ai/ocr/`
- AI worker Dockerfiles under `docker/`
- workload benchmark fixtures under `testdata/` or `benchmarks/`

Avoid:

- P2P transport internals except stable interfaces.
- Reward math except shard measurement outputs.
- Protocol/security docs except output schemas needed by verification.

## Rules

- ONNX only. Do not add direct PyTorch/TensorFlow runtime execution.
- Real-time chat must run on one capable node.
- Model sharding in Phase 1 is batch/async only.
- Every workload needs explicit input/output schema.
- Benchmark output must include hardware tier and runtime provider.

## Deliverables

- ONNX Runtime integration abstraction.
- LLM decode pipeline and tokenizer integration.
- Output verification adapter hooks for embeddings/checksums.
- Batch-only sharding prototype or spec-backed interfaces.
- Benchmark command and reproducible result format.

## Done Means

- Unit tests pass.
- At least one small ONNX model fixture runs in CI/local test.
- Benchmarks can run without external paid services.
- NIP verification sections include exact commands and results.
