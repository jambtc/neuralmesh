# NIP-032 — LLM Inference Pipeline

- Status: 📋 Open
- Area: AI Compute / LLM
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

LLM inference is the highest-demand AI task type.
It is the primary use case that will attract both task requesters and node operators.

## Proposal

Implement the LLM inference pipeline:

### Sub-tasks

- [ ] NIP-032a: Define supported model families for Phase 1 (LLaMA, Mistral, Phi variants in ONNX)
- [ ] NIP-032b: Define LLM task input schema (prompt, max_tokens, temperature, top_p, stop_sequences)
- [ ] NIP-032c: Define LLM task output schema (generated text, token count, finish_reason, timing)
- [ ] NIP-032d: Implement tokenizer loading and encoding (HuggingFace tokenizers compiled)
- [ ] NIP-032e: Implement ONNX-based autoregressive decode loop
- [ ] NIP-032f: Implement KV-cache management for long-context inference
- [ ] NIP-032g: Implement streaming output (token-by-token) for real-time tasks
- [ ] NIP-032h: Implement output verification adapter (embedding cosine similarity for NIP-012)
- [ ] NIP-032i: Benchmark: tokens/second per hardware tier (CPU, 4GB GPU, 8GB GPU, 16GB GPU)

## Acceptance Criteria

- LLaMA 3 8B runs successfully in ONNX on 8GB GPU node.
- LLaMA 3 1B runs successfully on CPU-only node.
- Output schema matches specification exactly.
- Token/s benchmark results published for 4 hardware tiers.
- Streaming output delivers first token within 2s of task start on single-node execution with sufficient hardware.

## Impact

- New package: `neuralmesh-client/internal/ai/llm/`
- New Docker image: `neuralmesh/worker-llm:latest`

## Implementation Notes

- Recommended: `llama.cpp` ONNX export for CPU; `onnxruntime-genai` for GPU.
- Tokenizer: use `tokenizers` Rust crate via CGO binding, or compile standalone binary.
- KV-cache: pre-allocate based on `max_context_length` × `n_layers` × `d_model`.
- Streaming: pipe generated tokens via local Unix socket to scheduler.

## Dependencies

- NIP-030 (ONNX Runtime) — execution backend
- NIP-023 (Docker sandboxing) — all inference runs in container
