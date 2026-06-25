# SproutBook

Working product name for the baby milestone tracking app.

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

## Current product decisions
- Working app name: `SproutBook`
- Recommended iOS bundle ID: `com.vvarden.sproutbook`
- Recommended Android application ID: `com.vvarden.sproutbook`
- Multiple caregivers are supported from the start via email invite
- The app is memory-first rather than clinical/medical-first
- Each achievement record should support date/time, notes, and an optional photo
- Mobile-first MVP
- Sync to an online account, but offline capture must keep working
- Conflicts from offline changes on multiple devices should be surfaced and resolved rather than silently overwritten

## Planning docs
- Product direction: `docs/product-direction.md`
- Technical recommendation: `docs/technical-recommendation.md`
- MVP specification: `docs/mvp-spec.md`

## Next planning topics
1. Choose app name, bundle identifiers, and tone/branding
2. Decide the exact MVP entry schema and permissions model
3. Decide the invite/auth flow details
4. Decide conflict-resolution UX and photo limits for MVP
5. Decide when to tackle memory-book export/print as a later phase
