# MVP Specification

## Purpose
This document defines the first build of Baby Milestone Tracker clearly enough to guide implementation.

The MVP is a mobile-first collaborative memory app for parents and caregivers. It is designed to capture meaningful baby achievements and moments quickly, keep them safely synced across caregivers, and continue working when the network disappears.

## Goals
- Let a primary caregiver create an account and family space
- Let that caregiver invite additional caregivers by email
- Let caregivers create and edit memory entries for a child
- Let entries include date/time, notes, and one optional photo in MVP
- Keep the app usable offline
- Sync changes when connectivity returns
- Surface true edit conflicts instead of silently losing sentimental data

## Explicit non-goals for MVP
- clinical milestone assessment
- therapy/development intervention workflows
- browser/web app
- printed memory-book ordering workflow
- advanced analytics or milestone scoring
- AI summaries
- push reminders unless they become essential later

## Primary user roles

### 1. Primary caregiver
The user who creates the family space.

Responsibilities/capabilities:
- create account
- create first child profile
- invite additional caregivers
- view and edit entries
- manage caregiver membership in the family

### 2. Invited caregiver
A caregiver invited by email into the same family space.

Responsibilities/capabilities:
- accept invite
- sign in or create account
- view children in that family
- create and edit entries
- upload one photo to an entry in MVP

## Core entities

### User
Represents a signed-in person.

Suggested fields:
- id
- email
- display_name
- created_at
- updated_at

### Family
Represents the shared collaboration space.

Suggested fields:
- id
- name
- created_by_user_id
- created_at
- updated_at

### FamilyMembership
Links a user to a family.

Suggested fields:
- id
- family_id
- user_id
- role (`owner`, `caregiver`)
- status (`active`, `invited`, `revoked`)
- invited_by_user_id
- created_at
- updated_at

### Child
Represents one child within a family.

Suggested fields:
- id
- family_id
- name
- birth_date
- avatar_photo_url (optional)
- created_at
- updated_at

### Entry
Represents one memory/achievement record.

Suggested fields:
- id
- family_id
- child_id
- created_by_user_id
- last_edited_by_user_id
- title
- notes
- observed_at
- recorded_at
- created_at
- updated_at
- deleted_at (nullable soft delete)
- sync_status (`synced`, `pending`, `conflicted`)

Notes:
- `observed_at` is when the moment happened
- `recorded_at` is when the caregiver saved it in the app
- keeping both fields matters for late entry and offline entry

### EntryPhoto
Represents one optional photo for MVP.

Suggested fields:
- id
- entry_id
- storage_path
- thumbnail_path (optional)
- width
- height
- uploaded_at

### Invitation
Represents a pending collaboration invite.

Suggested fields:
- id
- family_id
- email
- role (`caregiver`)
- invited_by_user_id
- token
- status (`pending`, `accepted`, `expired`, `revoked`)
- expires_at
- created_at
- updated_at

### SyncConflict
Represents a detected same-entry edit conflict.

Suggested fields:
- id
- entry_id
- server_version_snapshot
- client_version_snapshot
- detected_at
- resolved_at
- resolved_by_user_id
- resolution_strategy

## Permissions model for MVP
Keep it simple.

### Primary caregiver / owner
Can:
- create family
- invite caregivers
- revoke caregivers
- create child profiles
- edit all entries in the family
- resolve conflicts

### Caregiver
Can:
- view family children
- create entries
- edit entries
- upload photo for entries they create or edit
- resolve conflicts if we keep the model simple

Recommendation:
For MVP, allow all active caregivers in a family to edit all entries. This keeps collaboration friction low. If that proves too loose later, we can introduce more granular permissions.

## Entry rules for MVP
- one child per entry
- one optional photo per entry
- title required
- observed date/time required
- notes optional
- creator attribution always stored
- edit history is desirable, but not mandatory if it risks delaying MVP
- soft delete preferred over hard delete

## Key user flows

### Flow 1: Primary caregiver onboarding
1. User opens app
2. User creates account or signs in
3. User creates family space
4. User creates first child profile
5. User lands on empty child timeline
6. App prompts user to add first memory entry or invite another caregiver

Success condition:
A signed-in primary caregiver has an active family and at least one child profile.

### Flow 2: Invite caregiver by email
1. Primary caregiver opens family/caregiver settings
2. Enters invitee email
3. App creates invitation record and sends invite email
4. Invitee opens invite link
5. Invitee signs in or creates account
6. Invitee joins the existing family

Success condition:
The invited caregiver becomes an active family member and can see the child timeline.

### Flow 3: Create entry online
1. Caregiver opens child timeline
2. Taps add entry
3. Enters title
4. Adjusts observed date/time if needed
5. Adds notes optionally
6. Adds one photo optionally
7. Saves entry
8. Entry appears in timeline immediately

Success condition:
The entry is persisted remotely and appears in timeline order.

### Flow 4: Create entry offline
1. Caregiver opens app with poor/no connectivity
2. Cached child timeline still loads
3. Caregiver creates a new entry
4. App saves entry locally with pending sync status
5. App shows clear pending sync state
6. When connectivity returns, app syncs queued entry automatically

Success condition:
The caregiver is never blocked from recording the memory, and the entry later becomes synced.

### Flow 5: Same-entry edit conflict after offline work
1. Two caregivers edit the same existing entry on separate devices while offline
2. Both devices queue changes locally
3. Connectivity returns
4. Server detects version mismatch / conflicting edit
5. Entry is marked conflicted
6. App shows a conflict resolution screen
7. User chooses which version to keep or merges fields manually
8. Resolved version is saved and conflict closes

Success condition:
No silent data loss, and the final chosen version is explicit.

## First screens for MVP

### 1. Welcome / auth screen
Purpose:
- sign in
- create account
- continue from invite link

### 2. Family setup screen
Purpose:
- create family name
- create first child profile

### 3. Child timeline screen
Purpose:
- default home screen after setup
- show entries in chronological order
- show pending/conflicted sync state clearly
- quick access to add entry

### 4. Add/edit entry screen
Purpose:
- create or update an entry
- capture title, observed_at, notes, and one photo

### 5. Entry detail screen
Purpose:
- view full memory details
- edit or soft-delete entry
- see attribution and sync status

### 6. Caregiver management / invites screen
Purpose:
- list caregivers
- invite by email
- show pending invites
- revoke caregiver access if needed

### 7. Conflict resolution screen
Purpose:
- compare conflicting versions
- keep mine / keep theirs / merge manually
- finalize resolved record

### 8. Settings screen
Purpose:
- account details
- sign out
- sync state/debug info
- family settings

## Timeline behaviour
- show newest-first by default
- group naturally by date
- visually identify pending entries
- visually identify conflicted entries
- show caregiver attribution on each card
- support quick tap into entry detail

## Offline and sync rules

### Local cache rules
- cache timeline, child, caregiver, and family data locally
- open app from cached data when offline
- never require a fresh network call just to read recent content

### Mutation queue rules
- creating/editing/deleting entries while offline writes to a local queue
- queue items are replayed in order when connectivity returns
- failed queue items remain visible and retryable

### Sync state labels
Use clear user-facing states:
- Synced
- Pending sync
- Conflict needs review
- Sync failed

### Conflict detection rule
Conflicts should only be raised when:
- the same existing entry has diverged on more than one device
- and both versions changed overlapping meaningful fields

Do not treat separate new entries as conflicts.

### Recommended default merge posture
- New entry vs new entry: both survive
- Edit vs no competing edit: sync automatically
- Same entry, non-overlapping safe changes: optionally auto-merge later, but do not rely on this for MVP
- Same entry, overlapping edits: create explicit conflict

## Data/storage decisions for MVP
- Remote source of truth: Supabase Postgres
- Photo storage: Supabase Storage
- Local storage/cache: device database or structured local persistence suited to React Native offline use
- Authentication: Supabase Auth

## API/backend behaviour requirements
- all child and entry reads must be family-scoped
- all writes must validate active membership in the family
- invitation acceptance must map the user into the correct family
- photo upload must be tied to a valid entry and family membership
- backend policies must prevent cross-family data leakage

## Suggested implementation order
1. auth + family creation
2. child creation + child timeline shell
3. create/edit entry without photo
4. invitation flow
5. photo attachment
6. offline cache
7. mutation queue sync
8. conflict detection + conflict resolution UI

## MVP success criteria
The MVP is successful if:
- a parent can create an account and child profile
- they can invite another caregiver by email
- both caregivers can add memories with notes and an optional photo
- the app still works offline for reading cached data and recording new entries
- queued entries sync later without drama
- true same-entry collisions are surfaced clearly instead of losing data silently

## Open implementation questions
- Should invites use magic links only, or allow password signup too?
- Should caregivers be allowed to edit all entries, or only their own, in the very first release?
- Should conflict resolution allow free-text manual merge in MVP, or only pick-a-version?
- What local persistence library should be chosen in the app scaffold?
- Do we want a visible per-entry audit history in MVP or phase 2?
