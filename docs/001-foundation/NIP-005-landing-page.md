# NIP-005 — Website Landing Page

- Status: 📋 Open
- Area: Foundation / Marketing
- Phase: 0
- Priority: Medium
- Date: 2026-05-11

## Context

No public website exists. A landing page is required for credibility, community sign-up, and investor interest.

## Proposal

Build and deploy a minimal landing page:

### Sub-tasks

- [ ] NIP-005a: Choose stack (Next.js static export or plain HTML/Tailwind)
- [ ] NIP-005b: Design page sections: hero, problem/solution, how it works, roadmap, team, CTA
- [ ] NIP-005c: Implement hero section with tagline and CTA button (waitlist / Discord)
- [ ] NIP-005d: Implement "How It Works" section (3-step visual)
- [ ] NIP-005e: Embed roadmap timeline (Phase 0–4)
- [ ] NIP-005f: Add email waitlist form (Mailchimp or self-hosted)
- [ ] NIP-005g: Configure domain and deploy (Vercel or Cloudflare Pages)
- [ ] NIP-005h: SEO meta tags and Open Graph setup

## Acceptance Criteria

- Page is publicly accessible on the chosen domain.
- Hero, how-it-works, roadmap, and CTA sections present.
- Email waitlist functional and storing submissions.
- Mobile-responsive layout.
- Page loads in under 2s (Lighthouse performance ≥ 80).

## Impact

- New repository: `neuralmesh-web`
- External: public domain deployment

## Implementation Notes

- Prefer Next.js static export for easy Vercel deployment.
- Domain candidates: neuralmesh.network, neuralmesh.io, neuralmesh.ai
- Keep Phase 0 page minimal — no whitepaper download until NIP-001 is complete.
- Dark theme aligned with brand identity (NIP-002).

## Dependencies

- NIP-002 (Brand identity) — logo and colors required
- NIP-001 (Whitepaper) — downloadable PDF once ready
