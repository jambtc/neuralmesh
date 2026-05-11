# NIP-060 — Open-Source Release Strategy

- Status: 📋 Open
- Area: Community / Release
- Phase: 2
- Priority: High
- Date: 2026-05-11

## Context

Open-source release is required to build community trust, attract contributors, and demonstrate non-speculative intent.
The timing and completeness of the release matters: releasing too early (broken code) damages reputation.

## Proposal

Plan and execute the open-source release:

### Sub-tasks

- [ ] NIP-060a: Define release readiness criteria (code quality, test coverage, docs completeness)
- [ ] NIP-060b: Choose license (Apache 2.0 recommended)
- [ ] NIP-060c: Audit code for sensitive data before publish (keys, credentials, internal URLs)
- [ ] NIP-060d: Write `README.md` for each repository (quick start, architecture overview)
- [ ] NIP-060e: Write `CHANGELOG.md` with v0.1.0 entry
- [ ] NIP-060f: Tag v0.1.0 release on GitHub with binary artifacts
- [ ] NIP-060g: Publish Product Hunt launch post
- [ ] NIP-060h: Submit to Hacker News "Show HN"
- [ ] NIP-060i: Post to r/MachineLearning and r/selfhosted

## Acceptance Criteria

- All repositories are public with Apache 2.0 license.
- No sensitive data in git history (run `git-secrets` scan before publish).
- Each repository has a working quick start guide (verified on clean machine).
- v0.1.0 binary released for Linux x86-64.
- Product Hunt and HN posts published same day as GitHub release.

## Impact

- All `neuralmesh-*` repositories made public
- External: Product Hunt, HN, Reddit posts

## Implementation Notes

- Run `git-secrets` and `trufflehog` before making repos public.
- Quick start must work in under 10 minutes on a fresh Ubuntu 24.04 machine.
- Coordinate Product Hunt launch with Discord invite link live.

## Dependencies

- NIP-003 (GitHub org) — repos must exist and be configured
- NIP-061 (Community) — Discord must be live before launch
- NIP-062 (Developer docs) — docs must be complete before launch
