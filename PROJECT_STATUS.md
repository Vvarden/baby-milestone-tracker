# Project Status

Last updated: 2026-06-25 13:04:28 UTC

## What exists now
- Local project directory created
- Local git repository initialized on `main`
- Local git identity configured for this repo (`tony <mascartony@gmail.com>`)
- Starter `.gitignore` added
- Initial project brief written
- Project workflow spellbook entry created in Hermes
- GitHub repository created: `https://github.com/Vvarden/baby-milestone-tracker`
- Git remote `origin` connected to the GitHub repository
- Local initial commit created: `7710cc5 chore: initialize project planning docs`
- Local follow-up commit created: `69cfb07 docs: record GitHub PAT push blocker`
- `main` has now been pushed successfully to GitHub and tracks `origin/main`
- Product direction, technical recommendation, and MVP spec docs created under `docs/`
- Working app name set to `SproutBook`

## Decisions made
- We want a baby developmental milestone tracking app
- Working app name: `SproutBook`
- Android and iOS support are preferred
- Web access is a nice-to-have
- No Mac is currently available for local iOS development
- Current best-fit recommendation: React Native + Expo + TypeScript
- The product is mobile-first for MVP
- The product supports multiple caregivers from the start via email invitation
- The product is memory-first rather than clinical/medical-first
- Each achievement record should support date/time, optional notes, and an optional photo
- Data should sync to an online account but remain usable offline with local caching and queued sync
- Offline conflicts between devices should be surfaced and resolved rather than silently overwritten
- A personalised printed memory-book workflow is a later-phase desirable feature

## Why this stack is the current favourite
- Shared codebase across Android and iOS
- Web can be added from the same app family
- Expo lowers setup friction and keeps the early product loop fast
- iOS cloud builds are possible later without owning a Mac full-time

## Known constraints
- `gh` GitHub CLI is not installed on this tower
- Flutter/Dart are not installed on this tower
- Node.js and npm are installed and usable
- iOS local builds/signing still need cloud tooling or Mac access later

## Open questions
- Package name / bundle identifier
- Brand/tone direction
- Whether invites should use magic links only, password signup, or both
- Whether caregivers can edit all entries in v1 or only their own
- Whether conflict resolution in MVP should allow manual field merge or only version-pick
- Which local persistence library should be chosen in the app scaffold
- Whether visible audit history belongs in MVP or phase 2
- When memory-book generation/printing should enter the roadmap

## Resume workflow
When returning to this project:
1. Open this file first
2. Review `README.md`
3. Review any docs in `docs/`
4. Check git status/log
5. Continue from the latest open questions or agreed next task
