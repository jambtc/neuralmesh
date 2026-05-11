# NIP-072 — Autonomous AI Agents

- Status: 📋 Open
- Area: Decentralization / AI Agents
- Phase: 4
- Priority: Medium
- Date: 2026-05-11

## Context

Autonomous AI agents are a long-term goal described in the whitepaper and roadmap.
Agents run on the NeuralMesh network, pay for compute with NMC, and can earn NMC for services.
This creates an AI agent economy without human intervention.

## Proposal

Design and implement the autonomous AI agent framework:

### Sub-tasks

- [ ] NIP-072a: Define agent architecture (identity, wallet, task submission, result consumption)
- [ ] NIP-072b: Implement agent identity (distinct from node identity: agent keypair + NMC wallet)
- [ ] NIP-072c: Implement agent task submission API (agents submit tasks programmatically)
- [ ] NIP-072d: Implement agent reward earning (agents can register as workers)
- [ ] NIP-072e: Define agent registry (on-chain listing of available agents and their services)
- [ ] NIP-072f: Implement agent-to-agent communication protocol
- [ ] NIP-072g: Define agent sandboxing (agents cannot escape NeuralMesh economic rails)
- [ ] NIP-072h: Implement agent lifecycle management (deploy, pause, retire)
- [ ] NIP-072i: Publish agent SDK (Python and Go)

## Acceptance Criteria

- An agent can submit a task, receive the result, and pay in NMC autonomously.
- An agent can earn NMC by registering as a worker.
- Agent registry lists available agents with their service descriptions.
- Agent-to-agent communication is end-to-end encrypted.
- Agent SDK published with example agent (RAG pipeline, image captioner).

## Impact

- New: `neuralmesh-agent-sdk/` repository
- New: `docs/agents/agent-guide.md`

## Implementation Notes

- Agent identity: separate keypair from node identity (agents are portable across nodes).
- Economic rails: agents cannot withdraw NMC without human wallet confirmation (safety for Phase 4).
- Example agents: a RAG pipeline agent that indexes documents and answers queries using NeuralMesh LLM inference.

## Dependencies

- NIP-032 (LLM inference) — agents primarily consume LLM inference
- NIP-041 (Rewards) — agents earn and spend NMC
- NIP-043 (Marketplace) — agents use marketplace for task discovery
