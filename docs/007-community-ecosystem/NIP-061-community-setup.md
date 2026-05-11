# NIP-061 — Discord / Community Setup

- Status: 📋 Open
- Area: Community / Channels
- Phase: 2
- Priority: High
- Date: 2026-05-11

## Context

Discord is the primary real-time community hub.
The server must be live and moderated before the open-source release (NIP-060) to capture early adopters.

## Proposal

Set up and configure the community presence:

### Sub-tasks

- [ ] NIP-061a: Create Discord server with channel structure
- [ ] NIP-061b: Configure Discord channels: #announcements, #general, #node-setup, #dev, #rewards, #governance, #off-topic
- [ ] NIP-061c: Set up Discord bots: moderation, welcome, role assignment, GitHub notifications
- [ ] NIP-061d: Create Discord roles: Member, Node Operator, Developer, Contributor, Council
- [ ] NIP-061e: Write community guidelines and Code of Conduct for Discord
- [ ] NIP-061f: Create X/Twitter account @neuralmesh (or @neuralmesh_ai)
- [ ] NIP-061g: Create Reddit community r/neuralmesh
- [ ] NIP-061h: Set up GitHub Discussions as async community forum

## Acceptance Criteria

- Discord server live with all channels configured.
- At least 3 moderators assigned before launch.
- Welcome bot greets new members with rules and getting started guide.
- X/Twitter account created and linked from all official materials.
- Community guidelines posted in Discord and GitHub Discussions.

## Impact

- External: Discord server, X/Twitter account, Reddit community

## Implementation Notes

- Use MEE6 or Carl-bot for moderation.
- GitHub notification bot: use GitHub's official Discord integration.
- Launch Discord with invite link embedded in landing page (NIP-005) and README files.

## Dependencies

- NIP-060 (Open-source release) — Discord must be ready before release day
- NIP-005 (Landing page) — landing page embeds Discord invite
