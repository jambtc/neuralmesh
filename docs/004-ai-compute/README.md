# 004 — AI Compute Layer

Phase 1 macro-area: the actual AI workload execution capabilities.
This is the core value proposition of NeuralMesh — what makes it different from generic compute networks.

## NIP Index

| ID | Title | Status |
|----|-------|--------|
| [NIP-030](NIP-030-onnx-runtime.md) | ONNX Runtime integration | 📋 Open |
| [NIP-031](NIP-031-model-sharding.md) | Model sharding (tensor shards) | 📋 Open |
| [NIP-032](NIP-032-llm-inference-pipeline.md) | LLM inference pipeline | 📋 Open |
| [NIP-033](NIP-033-image-generation.md) | Image generation workload | 📋 Open |
| [NIP-034](NIP-034-speech-synthesis-stt.md) | Speech synthesis / STT workload | 📋 Open |
| [NIP-035](NIP-035-ocr-workload.md) | OCR workload | 📋 Open |

## Priority Order

1. NIP-030 (ONNX) — baseline runtime, blocks all others
2. NIP-032 (LLM inference) — highest demand use case
3. NIP-031 (Model sharding) — enables batch/async participation for larger models
4. NIP-033 (Image generation) — second highest demand
5. NIP-034, NIP-035 — Phase 2 additions

## Dependencies

- NIP-023 (Docker sandboxing) — all workloads run inside Docker containers
- NIP-022 (Scheduler) — scheduler dispatches tasks to workload runners

## Sharding Constraint

Model sharding is not a Phase 1 real-time chat feature.
Use single-node execution for streaming and first-token latency targets.
Use sharding only for batch/async tasks until measured latency proves otherwise.
