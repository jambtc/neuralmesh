# NIP-064 — External AI Integrations

- Status: 📋 Open
- Area: Community / Ecosystem
- Phase: 2–3
- Priority: Medium
- Date: 2026-05-11

## Context

Integrating NeuralMesh with popular AI frameworks lowers the barrier for developers to use the network.
It converts the network from a standalone protocol into part of the broader AI ecosystem.

## Proposal

Implement integrations with key AI frameworks and platforms:

### Target Integrations

1. **OpenAI-compatible API endpoint** — drop-in replacement for OpenAI API (most impactful)
2. **LangChain provider** — NeuralMesh as LangChain LLM provider
3. **LlamaIndex integration** — NeuralMesh as LlamaIndex inference backend
4. **Hugging Face Inference Endpoint** — list NeuralMesh as a provider option
5. **n8n / Make node** — no-code workflow integration

### Sub-tasks

- [ ] NIP-064a: Implement OpenAI-compatible REST API (`/v1/chat/completions`, `/v1/embeddings`)
- [ ] NIP-064b: Write LangChain LLM provider class (Python)
- [ ] NIP-064c: Write LlamaIndex custom LLM class (Python)
- [ ] NIP-064d: Publish `neuralmesh-python` SDK on PyPI
- [ ] NIP-064e: Publish `neuralmesh` npm package (JavaScript SDK)
- [ ] NIP-064f: Submit n8n community node
- [ ] NIP-064g: Write integration guides for each supported platform

## Acceptance Criteria

- OpenAI-compatible endpoint passes OpenAI API conformance test suite.
- LangChain integration example works in a Jupyter notebook.
- Python SDK published on PyPI with ≥ 90% test coverage.
- npm package published and installable.
- Integration guides published in documentation site (NIP-062).

## Impact

- New: `neuralmesh-python/` SDK repository
- New: `neuralmesh-js/` SDK repository
- New: OpenAI-compatible API layer in `neuralmesh-core`

## Implementation Notes

- OpenAI compatibility: implement `/v1/chat/completions` with streaming SSE.
- LangChain provider: extend `BaseLLM` class; publish to LangChain community hub.
- Python SDK: use `httpx` for async HTTP; `pydantic` for type-safe models.

## Dependencies

- NIP-032 (LLM inference) — required for OpenAI-compatible endpoint
- NIP-004 (Technical spec) — API surface defined in spec
- NIP-062 (Developer docs) — integration guides are part of documentation
