# NIP-033 — Image Generation Workload

- Status: 📋 Open
- Area: AI Compute / Image
- Phase: 1–2
- Priority: Medium
- Date: 2026-05-11

## Context

AI image generation (Stable Diffusion and variants) is the second most demanded AI task type.
GPU nodes with ≥ 6GB VRAM can participate; CPU-only nodes can run smaller models slowly.

## Proposal

Implement image generation workload support:

### Sub-tasks

- [ ] NIP-033a: Define supported models for Phase 1 (SD 1.5, SDXL Turbo in ONNX)
- [ ] NIP-033b: Define image generation task input schema (prompt, negative_prompt, width, height, steps, seed, model_id)
- [ ] NIP-033c: Define output schema (image bytes base64 or URL, seed, steps completed, timing)
- [ ] NIP-033d: Implement ONNX-based diffusion pipeline (UNet, VAE decoder, text encoder)
- [ ] NIP-033e: Implement seed-based determinism (same seed → reproducible output for verification)
- [ ] NIP-033f: Implement output verification adapter (perceptual hash + SSIM for NIP-012)
- [ ] NIP-033g: Benchmark: images/minute per hardware tier
- [ ] NIP-033h: Build Docker image with model weights cached (avoid re-download per task)

## Acceptance Criteria

- SD 1.5 generates 512×512 image in under 30s on 6GB GPU node.
- Same seed produces pixel-identical output (determinism verified).
- Output image hash is reproducible for verification.
- Docker image includes model weights and generates images offline.

## Impact

- New package: `neuralmesh-client/internal/ai/image/`
- New Docker image: `neuralmesh/worker-image:latest`

## Implementation Notes

- Use `onnxruntime` for UNet inference; VAE decoder is the memory bottleneck.
- Determinism: fix all random seeds including scheduler noise.
- VRAM minimum: 4GB for SD 1.5 (fp16); 8GB for SDXL.
- Model weights baked into Docker image to avoid per-task CDN dependency.

## Dependencies

- NIP-030 (ONNX Runtime) — diffusion pipeline uses ONNX runtime
- NIP-023 (Docker sandboxing) — image generation runs in container
- NIP-012 (Verification) — perceptual hash verification adapter
