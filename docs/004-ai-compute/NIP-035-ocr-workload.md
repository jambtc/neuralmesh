# NIP-035 — OCR Workload

- Status: 📋 Open
- Area: AI Compute / OCR
- Phase: 2
- Priority: Low
- Date: 2026-05-11

## Context

OCR is mentioned in the whitepaper as a core use case.
It runs well on CPU nodes (low VRAM requirement), enabling broad participation.

## Proposal

Implement OCR workload support:

### Sub-tasks

- [ ] NIP-035a: Choose OCR backend (PaddleOCR ONNX export vs Tesseract vs TrOCR ONNX)
- [ ] NIP-035b: Define OCR input schema (image bytes, language hint, output_format)
- [ ] NIP-035c: Define OCR output schema (text blocks, bounding boxes, confidence scores)
- [ ] NIP-035d: Implement OCR pipeline (image preprocessing → ONNX inference → structured output)
- [ ] NIP-035e: Implement multi-language support (at least EN, IT, DE, FR, ES, ZH)
- [ ] NIP-035f: Implement verification adapter (character-level similarity for NIP-012)
- [ ] NIP-035g: Benchmark: pages/minute on CPU node

## Acceptance Criteria

- A4 document page with text is processed in under 5s on CPU node.
- Output includes bounding boxes and per-block confidence scores.
- At least 6 languages supported.
- Character-level accuracy ≥ 95% on standard benchmark (FUNSD or similar).

## Impact

- New package: `neuralmesh-client/internal/ai/ocr/`
- New Docker image: `neuralmesh/worker-ocr:latest`

## Implementation Notes

- Recommended: PaddleOCR ONNX (best accuracy-to-speed ratio, CPU-friendly).
- Image preprocessing: deskew, denoise, binarize before inference.
- Bounding boxes: output in normalized coordinates (0–1 relative to image size).

## Dependencies

- NIP-030 (ONNX Runtime) — inference backend
- NIP-023 (Docker sandboxing) — OCR runs in container
- NIP-012 (Verification) — character similarity verification
