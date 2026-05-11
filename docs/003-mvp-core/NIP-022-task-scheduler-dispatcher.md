# NIP-022 — Task Scheduler and Dispatcher

- Status: 📋 Open
- Area: MVP Core / Scheduling
- Phase: 1
- Priority: Critical
- Date: 2026-05-11

## Context

The scheduler decides which tasks this node accepts, queues them for execution, and dispatches them to the execution sandbox.
Without a scheduler, tasks cannot be managed concurrently.

## Proposal

Implement the task scheduler and dispatcher:

### Sub-tasks

- [ ] NIP-022a: Define local task queue data structure (priority queue)
- [ ] NIP-022b: Implement task acceptance policy (resource fit check before accepting)
- [ ] NIP-022c: Implement task priority scoring (deadline proximity, reward size, task type)
- [ ] NIP-022d: Implement concurrent execution slots (configurable max parallel tasks)
- [ ] NIP-022e: Implement deadline monitoring and task cancellation
- [ ] NIP-022f: Implement result submission after execution completes
- [ ] NIP-022g: Implement task retry logic on transient execution failures
- [ ] NIP-022h: Expose scheduler status via local API (queue depth, active tasks, throughput)

## Acceptance Criteria

- Scheduler correctly rejects tasks that exceed available resources.
- Concurrent execution slots are respected (no over-commit).
- Tasks past deadline are cancelled and penalized correctly.
- Scheduler recovers cleanly from execution sandbox crash.
- Local API reports real-time scheduler status.

## Impact

- New package: `neuralmesh-client/internal/scheduler/`

## Implementation Notes

- Priority queue: max-heap ordered by `(reward / estimated_duration) * urgency_factor`.
- Resource fit check: available RAM, GPU VRAM, and CPU cores vs task requirements.
- Max parallel tasks: default 2 (CPU tasks) / 1 (GPU tasks); configurable.
- Result submission timeout: 60s after execution completes before marking as failed.

## Dependencies

- NIP-011 (Task lifecycle) — scheduler implements lifecycle state transitions
- NIP-023 (Docker sandboxing) — dispatcher invokes sandbox per task
- NIP-030 (ONNX runtime) — AI tasks routed through ONNX executor
