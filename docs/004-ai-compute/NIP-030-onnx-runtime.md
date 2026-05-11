# NIP-030 — ONNX Runtime Integration

- Status: 📋 Open
- Area: AI Compute / Runtime
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

ONNX Runtime is a cross-platform, cross-hardware AI inference engine.
It supports CPU, CUDA, ROCm, and CoreML execution providers, making it ideal for heterogeneous consumer hardware.
All AI task types depend on this runtime.

## Proposal

Integrate ONNX Runtime as the primary AI execution engine:

### Sub-tasks

- [ ] NIP-030a: Define minimum ONNX Runtime version and supported execution providers
- [ ] NIP-030b: Build base Docker image with ONNX Runtime CPU (for all nodes)
- [ ] NIP-030c: Build base Docker image with ONNX Runtime CUDA (for NVIDIA GPU nodes)
- [ ] NIP-030d: Build base Docker image with ONNX Runtime ROCm (for AMD GPU nodes)
- [ ] NIP-030e: Implement execution provider detection at node startup
- [ ] NIP-030f: Define model input/output schema for task payloads (tensor names, shapes, dtypes)
- [ ] NIP-030g: Implement model loading from task payload (ONNX file hash + download)
- [ ] NIP-030h: Implement inference execution with timing measurement
- [ ] NIP-030i: Implement output serialization for result submission

## Acceptance Criteria

- CPU inference works on any x86-64 Linux node.
- CUDA inference works on NVIDIA GPU nodes with driver ≥ 525.
- Execution provider is auto-detected and logged at startup.
- Model loads from task payload within 30s for models up to 2GB.
- Inference output is serialized and hashed for verification.

## Impact

- New: `docker/base-images/onnx-cpu/`, `docker/base-images/onnx-cuda/`, `docker/base-images/onnx-rocm/`
- New package: `neuralmesh-client/internal/ai/onnx/`

## Implementation Notes

- ONNX Runtime version: 1.18+ (latest stable).
- CPU image: ~800MB; CUDA image: ~4GB (CUDA base included).
- Model download: verify SHA-256 of ONNX file before loading.
- Supported model formats: ONNX only (no PyTorch, no TF direct).
- Models must be pre-converted to ONNX by task requesters.
