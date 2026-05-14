# Onboarding - Phase 1 MVP

Created: 2026-04-28  
Last Updated: 2026-05-14  
Status: MVP delivery tracker

This file is the git-tracked source of truth for the current Phase 1 scope and progress.

## Table of Contents

- [1. MVP Goal](#1-mvp-goal)
- [2. Product Scope](#2-product-scope)
- [3. Core User Journeys](#3-core-user-journeys)
- [4. MVP Stories](#4-mvp-stories)
- [5. Deferred After MVP](#5-deferred-after-mvp)
- [6. MVP1 Scope](#6-mvp1-scope)
- [7. Repos Involved](#7-repos-involved)
- [8. Functional Test Gate](#8-functional-test-gate)
- [9. Deployment Model](#9-deployment-model)

## 1. MVP Goal

Phase 1 MVP is considered complete only when the Android app works end to end with Render-hosted APIs for this core flow:

1. User registers at app level.
2. User signs in.
3. User searches temples.
4. User creates temple access request.
5. Temple admin reviews pending requests.
6. Temple admin approves or rejects the request.
7. Approved user signs in again and lands directly on temple home.
8. User can log out.

## 2. Product Scope

### MVP done now

- Multi-temple platform support
- Temple onboarding from backend systems
- Executive committee or trustee capture in backend services
- Bulk temple admin onboarding from backend services
- Public home screen with `Register User` and `Existing User? Sign in`
- App-level user registration with no app admin approval
- App-level sign-in with `contact number + password`
- Approved temple is stamped into identity during admin approval so sign-in can route directly without waiting on registration
- Direct routing to temple home when approved temple access exists
- Searchable `Add Temple` discovery for users without approved temple access
- Temple subscription request creation
- Temple admin pending request review for own temple only
- Temple admin approve and reject actions
- Simple devotee temple home for approved members
- Devotee `Home`, `Book`, `Donate`, and `Chat` temple sections
- Shantidhara bookings are available only for the next 30 days
- Each day exposes up to two 8:00 AM Shantidhara slots from DB-backed availability
- Booked Shantidhara slot moves to QR payment and screenshot submission flow
- Donation flow starts with user-entered amount, then shows temple QR payment with screenshot submission
- Payment screenshot submission notifies temple admins
- Admin can publish `Information` updates to temple members
- Admin can publish `Wall of Fame` updates to temple members
- Temple admin uses the same temple home layout as devotee with an extra `Admin` tab
- Temple home now uses an image-led carousel with a separate `More information` panel for timings and temple details
- Temple home now uses an in-image info action plus utility shortcut icons for notifications, live streaming, events, activities, donation, and sharing
- Temple home now includes a left-side `My Profile` panel for user details, donation access, booking access, and sharing
- `Information` updates are now presented to users as clickable `Announcements` cards with progressive loading
- Current visual direction uses a bright white base with Jain-flag yellow as the primary accent and red only for sacred emphasis
- Temple gallery images and temple detail fields are owned by temple records in backend data, not bundled in the mobile app
- Temple onboarding now supports storing temple gallery images inside temple-admin-owned backend data for app display
- Temple assistant now runs live through the gateway-hosted AI runtime, with `temple-ai-service` kept as the target dedicated service split
- Chat tab now uses a RAG-backed temple assistant with citations and action cards under the name `Aagam Mitra`
- Logout from discovery, devotee home, and admin flow
- Android app using Render APIs as the default runtime backend

### Deferred after MVP

- Full real-device validation of push notification delivery
- Payment integration
- Rich chat experience beyond placeholder state
- Cross-temple activity feed richness
- Extra theme refinement beyond the current reviewed direction
- iPhone end-to-end acceptance

## 3. Core User Journeys

### Devotee journey

1. User opens the app.
2. User taps `Register User`.
3. User submits `Name`, `Contact Number`, `Native City`, `Local Area`, `Occupation`, and `Password`.
4. App creates the user account immediately.
5. User signs in with contact number and password.
6. If the user has no approved temple access, app opens `Add Temple`.
7. User searches temples.
8. User requests access to a temple.
9. User waits for temple admin approval.
10. After approval, user signs in again.
11. App opens temple home directly.
12. User can log out.

### Temple admin journey

1. Temple admin signs in.
2. Admin opens pending temple access requests.
3. Admin sees only requests for the admin's temple.
4. Admin approves or rejects a request.
5. Admin can send `Information` updates.
6. Admin can publish `Wall of Fame` updates.
7. Approved devotee can sign in and reach temple home.

## 4. MVP Stories

Use `[x]` only when the story is functionally re-tested after the code change.

| Done | Story ID | Story Name | Status | Repos |
|---|---|---|---|---|
| [x] | MVP-001 | Temple can be onboarded from backend with temple details | Done | `temple-admin-service`, `temple-api-gateway` |
| [x] | MVP-002 | Temple executive committee or trustee data can be captured | Done | `temple-admin-service` |
| [x] | MVP-003 | Temple admins can be onboarded from backend | Done | `temple-admin-service`, `temple-identity-service`, `temple-api-gateway` |
| [x] | MVP-004 | Public home shows `Register User` and `Existing User? Sign in` | Done | `temple-frontend` |
| [x] | MVP-005 | User can register at app level without approval | Done | `temple-frontend`, `temple-api-gateway`, `temple-identity-service` |
| [x] | MVP-006 | User can sign in with contact number and password | Done | `temple-frontend`, `temple-api-gateway`, `temple-identity-service` |
| [x] | MVP-007 | User without approved temple can search active temples | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP-008 | User can raise temple access request | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service` |
| [x] | MVP-009 | Duplicate active temple request is blocked | Done | `temple-registration-service` |
| [x] | MVP-010 | Temple admin can view pending requests for own temple | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP-011 | Temple admin can approve request | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service`, `temple-registration-service`, `temple-identity-service` |
| [x] | MVP-012 | Temple admin can reject request | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service`, `temple-registration-service` |
| [x] | MVP-013 | Approved devotee lands directly on temple home after sign-in | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service`, `temple-identity-service` |
| [x] | MVP-014 | Logout works from devotee and admin flows | Done | `temple-frontend` |
| [ ] | MVP-015 | Android + Render end-to-end flow is re-tested after this MVP simplification pass | In Progress | `temple-frontend`, all backend repos |

## 5. Deferred After MVP

These items are not part of the current acceptance target:

- Shantidhara slot browsing and booking
- Payment handling
- Separate `News`, `Wall of Fame`, `Book`, and `Donate` navigation in the member app
- Rich cross-temple home dashboard
- Extended social or community modules
- Additional UI beautification beyond stable usability

## 6. MVP1 Scope

`MVP1` is locked to the first post-MVP temple engagement release.

### MVP1 includes

- richer approved-devotee temple home
- content-backed `Home`, `News`, and `Recognitions` views
- data loaded from existing temple APIs already deployed on Render
- safe empty states when temple content is not yet populated

### MVP1 excludes

- Shantidhara booking
- donation flow
- payment flow
- cross-temple home aggregation
- extra member navigation beyond working content views

### MVP1 stories

| Done | Story ID | Story Name | Status | Repos |
|---|---|---|---|---|
| [x] | MVP1-001 | Approved devotee sees richer temple home summary | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP1-002 | Approved devotee can view temple news feed | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP1-003 | Approved devotee can view temple recognitions or wall of fame | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |

### Next locked scope after MVP1

`MVP2` should cover:

- Shantidhara slot browsing
- Shantidhara booking creation
- donation amount entry and QR payment initiation
- payment-pending confirmation flow

### MVP2 stories

| Done | Story ID | Story Name | Status | Repos |
|---|---|---|---|---|
| [x] | MVP2-001 | Approved devotee can view available Shantidhara slots | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP2-002 | Approved devotee can create Shantidhara booking | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service` |
| [x] | MVP2-003 | Approved devotee can enter donation amount and start QR payment | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service` |
| [x] | MVP2-004 | Approved devotee can submit donation payment screenshot and notify temple admins | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service`, `temple-admin-service` |
| [x] | MVP2-005 | Booking and donation remain in `payment_pending` state for the current phase | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service` |

## 7. MVP3 Scope

`MVP3` is currently focused on polish and temple communication instead of payments.

### MVP3 includes

- simpler reviewed auth flow
- white-base UI direction with warm accent surfaces
- improved no-temple discovery flow
- admin-side temple notification publishing
- two temple notification categories:
  - `Information`
  - `Wall of Fame`
- temple-scoped content visible to approved devotees

### MVP3 excludes

- real push notification delivery
- payment gateway work
- full chat implementation

### MVP3 stories

| Done | Story ID | Story Name | Status | Repos |
|---|---|---|---|---|
| [x] | MVP3-001 | Auth UI is simplified for login-first flow | Done | `temple-frontend` |
| [x] | MVP3-002 | Devotee without temple sees minimal discovery and add-temple path | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP3-003 | Temple admin can publish information notifications | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [x] | MVP3-004 | Temple admin can publish wall of fame notifications | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service` |
| [ ] | MVP3-005 | Real mobile push delivery to enrolled users | In Progress | `temple-frontend`, `temple-api-gateway`, `temple-identity-service`, `temple-registration-service`, `temple-admin-service` |
| [x] | MVP3-006 | Shantidhara booking uses next-30-days DB-backed slot availability | Done | `temple-frontend`, `temple-api-gateway`, `temple-admin-service`, `temple-registration-service` |
| [x] | MVP3-007 | Book and Donate support QR payment screenshot submission | Done | `temple-frontend`, `temple-api-gateway`, `temple-registration-service`, `temple-admin-service` |
| [ ] | MVP3-008 | Chat module beyond placeholder state | Planned | `temple-frontend`, future chat service |

## AI Foundation Scope

The first AI slice is now in progress.

### AI foundation includes

- dedicated `temple-ai-service`
- temple-scoped assistant API
- persisted temple knowledge documents and chunks in service-owned AI storage
- embeddings-backed retrieval with local fallback if OpenAI embeddings are unavailable
- tool-backed status lookups for:
  - membership
  - Shantidhara bookings and slot availability
  - donations and payment instructions
  - latest information and wall-of-fame updates
- action-card responses for `Home`, `Book`, `Donate`, and `Admin`
- frontend Chat tab connected to the assistant route
- current deployed path runs the assistant runtime inside `temple-api-gateway` so Chat can work before the dedicated AI repo is provisioned on GitHub and Render

### AI foundation next steps

- provision and deploy dedicated `temple-ai-service`
- move AI storage from local SQLite dev default to production Postgres
- improve admin drafting assistant
- add chat session persistence and audit logs

## 8. Repos Involved

### `temple-frontend`

- Android app
- public auth screens
- temple discovery
- devotee temple home
- admin request review screens

### `temple-api-gateway`

- single `/api/v1` entry point
- routing to downstream services
- Render cold-start-tolerant upstream timeout handling
- service prewarm endpoints for Render cold starts

### `temple-identity-service`

- app-level registration
- app-level sign-in
- user identity and role lookup
- device push token storage

### `temple-registration-service`

- temple subscription request creation
- temple subscription status lookup
- duplicate request prevention
- booking and donation pending records
- approved temple member lookup for notification fanout

### `temple-admin-service`

- backend temple onboarding data
- active temple list
- temple admin request review workflow
- temple information feed storage
- temple wall-of-fame storage
- temple notification publishing
- push notification fanout to approved temple members

### `temple-infra`

- deployment notes
- environment references
- git-tracked product requirements and architecture docs

## 9. Functional Test Gate

Every MVP check-in must include these functional checks:

### Render health

- Gateway health returns `ok`
- Identity health returns `ok`
- Registration health returns `ok`
- Admin health returns `ok`

### Direct API verification

- `POST /api/v1/auth/signup`
- `POST /api/v1/auth/signin`
- `GET /api/v1/temples/active`
- `GET /api/v1/temple-subscriptions/me`
- `POST /api/v1/temple-subscriptions`
- `GET /api/v1/admin/temple-subscriptions`
- `POST /api/v1/admin/temple-subscriptions/:id/approve`
- `POST /api/v1/temples/:templeId/news-feed`
- `POST /api/v1/temples/:templeId/wall-of-fame`

### Android verification

1. Open landing page
2. Register new user
3. Sign in as devotee without approved temple
4. Search temple
5. Request access
6. Sign in as temple admin
7. Approve request
8. Sign in again as devotee
9. Confirm direct route to temple home
10. Log out

## 10. Deployment Model

- Android app as the primary acceptance path
- React Native + Expo frontend
- Render-hosted Python APIs
- Service-owned databases by backend boundary
- No MVP step should depend on local backend services

## 11. Push Notification Plan

Current mobile push delivery path:

- Expo app collects device push token
- backend stores token per approved user device
- temple admin publishes `Information` or `Wall of Fame`
- backend sends push via Expo Push Service
- Expo relays to:
  - `FCM` for Android
  - `APNs` for iPhone

Current implementation status:

- app-side token registration is implemented
- identity-side token persistence is implemented
- admin publish flow now triggers push fanout through approved temple members
- final delivery still requires validation on a real Android or iPhone device
- emulator and web are not enough for push acceptance
