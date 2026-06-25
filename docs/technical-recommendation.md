# Technical Recommendation

## Recommended stack
- React Native
- Expo
- TypeScript
- Supabase for backend services in the MVP

## Why this stack fits
React Native + Expo remains the best fit because the project is mobile first, needs Android and iOS support, and may later want web without starting over.

Supabase is the best current backend fit for the first build because it gives us:
- hosted Postgres
- authentication
- row-level security
- file storage for photos
- email-based invitation flows we can build on
- a straightforward TypeScript-friendly client experience

## Recommended architecture shape

### Frontend
- Expo-managed React Native app
- TypeScript throughout
- local on-device persistence for offline cache and sync queue
- navigation built for child timeline, entry detail, composer, and settings/invite flows

### Backend
- Supabase Postgres as the source of truth
- Supabase Auth for account access
- Supabase Storage for photo uploads
- SQL schema designed around households/families, caregivers, children, and memory entries

### Data model direction
Recommended core entities:
- users
- families
- family_memberships
- children
- entries
- entry_photos
- invitations
- sync_operations or mutation_queue (client-side primarily, optional server audit trail)

Recommended entry fields:
- id
- child_id
- created_by_user_id
- title
- notes
- observed_at
- recorded_at
- created_at
- updated_at
- status

## Collaboration model recommendation
Treat the shared space as a family or household rather than a single-user account with bolt-on sharing.

Suggested rules:
- one user creates the family space
- that user invites other caregivers by email
- invited caregivers join the same family space
- each entry records who created it
- permission model can start simple: all caregivers in a family can view and edit entries

If that later feels too loose, permissions can be narrowed by policy.

## Offline-first recommendation
The simplest robust model is:
- cache server data locally
- allow new entries to be created offline
- queue mutations locally
- sync queued mutations when connectivity returns

Important design choice:
Prefer append-heavy records over shared mutable milestone state.

In practice that means each memory entry is its own record. That greatly reduces conflict risk because two caregivers usually add separate memories instead of both trying to overwrite the same milestone object.

## Conflict handling recommendation
Use two levels of handling.

### Level 1: Simple default behaviour
- Creating separate new entries offline on different devices should never conflict
- If one entry is edited on one device only, sync normally
- For low-risk field collisions, use last-write-wins plus an edit history/audit trail if practical

### Level 2: Explicit conflict flow
When the same entry is edited on multiple devices while offline:
- mark the entry as conflicted after sync
- preserve both versions
- ask the caregiver to resolve the conflict in-app
- present a simple comparison, similar in spirit to a git merge but written for normal humans

This is better than silent overwrites, especially because these are sentimental records.

## Recommendation for MVP boundaries
For MVP, optimise for these flows:
1. parent creates account
2. parent creates child
3. parent invites another caregiver by email
4. either caregiver adds a memory entry with optional photo
5. app still works offline
6. queued entries sync later
7. rare same-entry edit conflicts are visible and recoverable

## Memory-book future-proofing
Design now so later printing is possible:
- keep full-resolution originals where practical
- generate derived/compressed assets separately for mobile display
- keep timestamps precise
- avoid storing important story text only inside photo captions or filenames
- ensure export can query entries by child and date range cleanly

## Practical note on web
Do not build the web app in the MVP.
But do:
- keep UI/business logic modular
- avoid mobile-only assumptions in core domain code
- keep backend/API design platform-neutral

That leaves the door open for Expo web later without making version 1 heavier than it needs to be.
