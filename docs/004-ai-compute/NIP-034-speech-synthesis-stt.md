# NIP-034 — Speech Synthesis / STT Workload

- Status: 📋 Open
- Area: AI Compute / Audio
- Phase: 2
- Priority: Low
- Date: 2026-05-11

## Context

Speech synthesis (TTS) and speech-to-text (STT) are high-value AI tasks with growing demand.
These workloads run efficiently on CPU nodes, broadening participation beyond GPU owners.

## Proposal

Implement TTS and STT workload support:

### Sub-tasks

- [ ] NIP-034a: Define supported STT model (Whisper variants in ONNX)
- [ ] NIP-034b: Define supported TTS model (Piper TTS or VITS in ONNX)
- [ ] NIP-034c: Define STT input schema (audio bytes, format, language hint)
- [ ] NIP-034d: Define STT output schema (transcript, word timestamps, confidence)
- [ ] NIP-034e: Define TTS input schema (text, voice_id, speed, pitch)
- [ ] NIP-034f: Define TTS output schema (audio bytes, format, duration)
- [ ] NIP-034g: Implement STT pipeline (audio decoding → ONNX inference → transcript)
- [ ] NIP-034h: Implement TTS pipeline (text tokenization → ONNX inference → audio encoding)
- [ ] NIP-034i: Implement verification adapters (WER for STT, MOS-proxy for TTS)

## Acceptance Criteria

- Whisper base transcribes 60s audio in under 10s on CPU node.
- TTS generates 10s speech audio in under 5s on CPU node.
- STT output includes word-level timestamps.
- Both pipelines run without GPU.

## Impact

- New package: `neuralmesh-client/internal/ai/audio/`
- New Docker image: `neuralmesh/worker-audio:latest`

## Implementation Notes

- Whisper ONNX export: use `whisper.cpp` ONNX export or HuggingFace optimum.
- Audio input: accept WAV and MP3; decode internally before inference.
- TTS verification: MOS proxy via a trained UTMOS model (small, CPU-only).

## Dependencies

- NIP-030 (ONNX Runtime) — inference backend
- NIP-023 (Docker sandboxing) — audio workloads run in container
