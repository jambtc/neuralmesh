# NIP-023 — Docker Sandboxing Execution

- Status: 📋 Open
- Area: MVP Core / Security / Execution
- Phase: 1
- Priority: High
- Date: 2026-05-11

## Context

Task execution must be isolated from the host system.
A malicious task payload could compromise the worker's machine without sandboxing.

## Proposal

Implement Docker-based execution sandboxing:

### Sub-tasks

- [ ] NIP-023a: Define base Docker images per task type (AI inference, rendering, OCR)
- [ ] NIP-023b: Implement container lifecycle management (create, start, stop, remove)
- [ ] NIP-023c: Implement resource constraints (CPU limit, memory limit, GPU passthrough)
- [ ] NIP-023d: Implement filesystem isolation (no host mounts except task input/output volume)
- [ ] NIP-023e: Implement network isolation (containers have no network access by default)
- [ ] NIP-023f: Implement execution timeout enforcement (SIGKILL after deadline)
- [ ] NIP-023g: Implement output collection and hash generation post-execution
- [ ] NIP-023h: Define allowed Docker image registry (only signed, project-approved images)
- [ ] NIP-023i: Evaluate gVisor / seccomp profiles for additional kernel isolation

## Acceptance Criteria

- Container cannot access host filesystem outside designated volumes.
- Container has no outbound network access.
- CPU, memory, and GPU limits are enforced.
- Execution timeout kills the container reliably.
- Output is collected and hash is produced after every execution.
- Only images from the approved registry can be used.

## Impact

- New package: `neuralmesh-client/internal/sandbox/`
- New: `docker/` folder with base images per task type

## Implementation Notes

- Use Docker SDK for Go (`docker/docker`).
- CPU limit: `--cpus` flag; memory: `--memory`; GPU: `--gpus device=X`.
- No network: `--network none`.
- Image signing: use Docker Content Trust (DCT) or cosign.
- gVisor (`runsc`) adds kernel isolation at slight performance cost — evaluate for Phase 2.

## Dependencies

- NIP-022 (Scheduler) — dispatcher calls sandbox per task
- NIP-030 (ONNX runtime) — AI base images include ONNX runtime
