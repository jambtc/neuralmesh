# NIP-004 — Detailed Technical Specification

- Status: 📋 Open
- Area: Foundation / Documentation
- Phase: 0
- Priority: High
- Date: 2026-05-11

## Context

`docs/02_technical_architecture.md` is a high-level draft.
No formal spec exists covering wire protocols, data formats, API interfaces, or node behavior.

## Proposal

Produce a detailed technical specification document:

### Sub-tasks

- [ ] NIP-004a: Define node types (worker, validator, coordinator, client)
- [ ] NIP-004b: Specify wire protocol format (message types, serialization: protobuf vs msgpack)
- [ ] NIP-004c: Define REST/gRPC API surface for task submission
- [ ] NIP-004d: Specify task data format (input, output, metadata schema)
- [ ] NIP-004e: Document node discovery protocol (DHT, bootstrap nodes)
- [ ] NIP-004f: Specify reward calculation formula (formal notation)
- [ ] NIP-004g: Define hardware capability advertisement format
- [ ] NIP-004h: Document error codes and failure modes

## Acceptance Criteria

- All node types formally defined with roles and responsibilities.
- Wire protocol specified with at least one concrete serialization format.
- Task data schema documented with example JSON/protobuf.
- Node discovery protocol described step-by-step.
- Reward formula is unambiguous and reproducible.

## Impact

- New: `docs/05_technical_spec.md`
- Informs: NIP-020 (client), NIP-021 (P2P), NIP-022 (scheduler), NIP-041 (rewards)

## Implementation Notes

- Use protobuf as default serialization (cross-language, compact).
- API surface should support both HTTP/REST (simple clients) and gRPC (nodes).
- Node discovery: libp2p Kademlia DHT is the reference implementation.

## Dependencies

- NIP-010 (PoUC) — reward formula depends on PoUC definition
- NIP-011 (Task lifecycle) — task schema depends on lifecycle states
