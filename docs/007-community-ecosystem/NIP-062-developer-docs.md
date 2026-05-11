# NIP-062 — Developer Documentation and Onboarding

- Status: 📋 Open
- Area: Community / Documentation
- Phase: 2
- Priority: High
- Date: 2026-05-11

## Context

Without clear developer documentation, contributors cannot onboard and users cannot run nodes.
Documentation quality directly determines community adoption velocity.

## Proposal

Produce complete developer documentation:

### Sub-tasks

- [ ] NIP-062a: Write node operator guide (install, configure, run, monitor)
- [ ] NIP-062b: Write task requester guide (submit tasks, check status, retrieve results)
- [ ] NIP-062c: Write developer integration guide (API reference, SDK usage)
- [ ] NIP-062d: Write architecture overview document (system diagram + component descriptions)
- [ ] NIP-062e: Write NIP contribution guide (how to propose a NIP)
- [ ] NIP-062f: Write troubleshooting guide (common errors and fixes)
- [ ] NIP-062g: Set up documentation site (MkDocs or Docusaurus deployed on GitHub Pages)
- [ ] NIP-062h: Add code examples for all API endpoints
- [ ] NIP-062i: Record a 5-minute "Getting Started" screencast

## Acceptance Criteria

- Node operator guide tested end-to-end on clean Ubuntu 24.04.
- API reference covers all endpoints with request/response examples.
- Documentation site is live at docs.neuralmesh.network (or similar).
- Troubleshooting guide covers at least 10 common issues.
- Getting started screencast linked from README and landing page.

## Impact

- New repository: `neuralmesh-docs`
- New: documentation site deployment

## Implementation Notes

- Use MkDocs Material (clean, searchable, free hosting via GitHub Pages).
- API reference: generate from OpenAPI spec if REST; from protobuf if gRPC.
- Screencast: record with OBS, publish on YouTube and embed in docs site.

## Dependencies

- NIP-004 (Technical spec) — API reference derived from spec
- NIP-060 (Open-source release) — docs must be complete before release
