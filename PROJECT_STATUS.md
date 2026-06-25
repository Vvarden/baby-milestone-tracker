# Project Status

Last updated: 2026-06-25 08:41:29 UTC

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

## Decisions made
- We want a baby developmental milestone tracking app
- Android and iOS support are preferred
- Web access is a nice-to-have
- No Mac is currently available for local iOS development
- Current best-fit recommendation: React Native + Expo + TypeScript

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
- App name / package name / bundle identifier
- Single-user family app or multi-caregiver collaboration from the start?
- Offline-first requirement?
- Account system needed for MVP?
- Notifications/reminders needed in MVP?
- Photo upload / attachment support needed?
- NHS/CDC/WHO milestone source preference?

## Resume workflow
When returning to this project:
1. Open this file first
2. Review `README.md`
3. Review any docs in `docs/`
4. Check git status/log
5. Continue from the latest open questions or agreed next task
