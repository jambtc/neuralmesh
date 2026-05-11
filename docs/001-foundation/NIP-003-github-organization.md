# NIP-003 — GitHub Organization Setup

- Status: 📋 Open
- Area: Foundation / DevOps
- Phase: 0
- Priority: High
- Date: 2026-05-11

## Context

No GitHub organization exists. The project needs a public presence for credibility and open-source collaboration.

## Proposal

Create and configure the NeuralMesh GitHub organization:

### Sub-tasks

- [ ] NIP-003a: Create GitHub organization `neuralmesh` (or `neuralmesh-network`)
- [ ] NIP-003b: Create repository `neuralmesh-core` (main protocol)
- [ ] NIP-003c: Create repository `neuralmesh-client` (desktop client)
- [ ] NIP-003d: Create repository `neuralmesh-docs` (documentation site)
- [ ] NIP-003e: Configure branch protection rules on `main`
- [ ] NIP-003f: Write `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md`
- [ ] NIP-003g: Set up issue templates (bug, feature, NIP proposal)
- [ ] NIP-003h: Configure GitHub Actions CI skeleton

## Acceptance Criteria

- Organization exists and is public.
- At least `neuralmesh-core` and `neuralmesh-docs` repos created.
- Branch protection on `main` requires PR + 1 review.
- `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` present in `neuralmesh-core`.
- Issue templates operational.

## Impact

- External: GitHub organization and public repositories
- New: `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `.github/ISSUE_TEMPLATE/`

## Implementation Notes

- Prefer `neuralmesh-network` org name if `neuralmesh` is taken.
- License: Apache 2.0 (permissive, AI/infra-friendly).
- Use GitHub Actions for CI (free tier sufficient for Phase 0).
