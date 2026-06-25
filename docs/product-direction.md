# Product Direction

## Product vision
A warm, collaborative mobile app for capturing baby developmental memories and achievements as they happen.

This is not primarily a medical, therapy, or formal developmental-assessment tool. The core value is helping caregivers quickly record exciting moments, keep them organised over time, and later turn them into a meaningful keepsake.

## Confirmed product decisions

### Naming
- Working app name: `SproutBook`
- This is the preferred working name unless a stronger option turns up later
- Recommended iOS bundle ID: `com.vvarden.sproutbook`
- Recommended Android application ID: `com.vvarden.sproutbook`

Why this is the current recommendation:
- it matches the existing GitHub owner/org naming cleanly
- it is lowercase and platform-safe
- it is specific enough to avoid generic naming problems
- using the same reverse-DNS identifier on both platforms keeps the early setup simple


### Users and collaboration
- The account starts with one primary parent/caregiver.
- That primary account holder can invite additional caregivers by email.
- Multiple caregivers can collaborate on the same child timeline.
- The product should support both password signup and magic-link access.
- Invite acceptance via magic link should be the smoothest/default path for joining a family.

### Core record model
When a caregiver notices a new skill, milestone, or achievement, they should be able to create a record with:
- title or short description
- date and time
- optional notes
- optional photo
- caregiver attribution
- child association

The emphasis is on memorable moments and achievements rather than clinical concern tracking.

### Platform scope
- Mobile first for MVP
- iOS + Android are the primary targets
- Web is deferred for now, but should remain technically possible later

### Sync and offline behaviour
- User data should sync to an online account
- Loss of connectivity must not lock the user out of the app
- A local cache should store existing data for browsing offline
- New records should be creatable offline and queued for sync
- If more than one device changes related data while offline, conflicts should be surfaced and resolved rather than silently overwritten

## Product principles
- Fast capture beats heavy form filling
- Memories first, analytics second
- Collaboration must feel safe and predictable
- Offline use is a feature, not an afterthought
- The first version should be simple enough for tired parents to use one-handed and quickly

## MVP scope recommendation
Include in MVP:
- email/password or magic-link account access
- child profile creation
- email invitation flow for additional caregivers
- create/edit milestone memory entries
- attach one photo per entry initially
- timeline view by child
- offline cache and queued sync
- basic conflict handling when two devices edit overlapping data

Defer until later:
- web app
- printing/shipping workflow for memory books
- rich milestone taxonomies and advanced filters
- notifications and reminders unless they become essential during design
- AI-generated summaries or captions

## Memory book feature direction
This should be treated as a later-phase premium or add-on workflow.

Future shape:
- select a date range, such as last 6 or 12 months
- choose one child
- generate a previewable memory-book layout from stored entries and photos
- let the user approve before printing/shipping

This feature should influence the data model now:
- entries need strong timestamps
- entries need stable ordering
- photo assets need durable storage
- notes should support longer-form text than a tiny caption-only field

## Open questions still to answer
- Brand/tone direction
- Whether entries should support multiple photos in MVP or later
- Whether caregivers can edit each other's entries freely or only comment/suggest changes
- Whether conflict resolution is manual-only or includes sensible defaults for simple cases
