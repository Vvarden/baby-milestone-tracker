# Baby Milestone Tracker

A cross-platform baby developmental milestone tracking app.

## Current direction
- Primary target: Android + iOS
- Nice-to-have: browser access via web app
- Constraint: no Mac available for local iOS builds/signing

## Working recommendation
Use React Native with Expo and TypeScript.

Why:
- One shared codebase for Android and iOS
- Web support is available through Expo for a later browser version
- Fastest path to shipping without a Mac on day one
- Can build/test much of the app from Linux, then use cloud EAS builds for iOS later if needed

## Repository conventions
- Local path: `/home/tony/projects/baby-milestone-tracker`
- Default branch: `main`
- Keep decisions in `PROJECT_STATUS.md`
- Keep deeper planning notes in `docs/`

## Next planning topics
1. Define user roles and core user journeys
2. Decide data model for children, milestones, observations, and reminders
3. Decide auth/offline/sync requirements
4. Decide MVP vs later features
