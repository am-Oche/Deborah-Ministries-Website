# Deborah Ufedejo Ministries

A premium, cinematic Christian music ministry website with a professional invitation experience and a visually integrated management **demonstration**.

## Goals and visual direction

- Christ-centered worship, music, ministry and transformed lives.
- Original ink, lavender and warm-neutral identity; oversized DM Sans editorial typography; atmospheric concert photography; rounded compositions; generous spacing.
- Spectrum.Life was downloaded and visually reviewed during design research. Its light lavender, dark ink, large typography and rounded editorial layout informed the visual system. No reference branding, copy, imagery or downloaded source is included in the finished project.
- Public website, invitation experience, management foundation and table schemas have distinct responsibilities.

## Implementation environment

This project is **static HTML, CSS and vanilla JavaScript**, not Next.js/TypeScript/Tailwind or a custom server. Its managed Table API is the available database equivalent. There are no API keys, database credentials, server processes, payment processors or LLM calls in the frontend.

### Important production boundary

**This is not a production-secured ministry management platform.** Platform access-rule setup returned `membership_required` (Plus or higher). Setup stopped; no fake JavaScript authentication was added. No access descriptor was saved and no deployment was performed.

Invitation and contact collection are deliberately in **preview mode**. No real personal information should be entered. The dashboard is a public demo. The frontend never fetches private invitation, contact or internal-note tables, and never posts personal data to them.

A platform upgrade alone does not implement secure anonymous intake, method-level authorization, server validation, spam prevention or record-level permissions. Those require an appropriate trusted backend and policy design. Do not enable private-data writes merely by changing a client-side flag.

## Completed features

### Public website

- Image-rich cinematic homepage with slow image scale, carefully layered overlays and large responsive headlines.
- Editorial introduction, multi-image worship composition and clearly labeled temporary artist portrait.
- About, Ministry, Events, Invite, Give and Contact pages.
- Exact supplied mission and vision statements.
- Four ministry expressions; potential engagement categories explicitly distinguished from past achievements.
- Public upcoming/past event rendering and individual event detail route.
- Honest, polished empty event states with no invented events.
- Spotify, YouTube, Apple Music and Audiomack placeholder labels, not fake links.
- Giving information placeholders; no invented accounts or active payment collection.
- Draft preview-specific privacy and terms pages.
- Responsive full-screen mobile menu, keyboard close, focus handling, skip link, visible focus styles, semantic form labels, reduced-motion support.
- Image assets stored locally for reliable first render; replaceable independently of layouts.

### Invitation experience

- Eight logical sections: Organization, Event, Attendance, Assignment, Technical, Logistics, Support, Additional Information.
- All requested input fields.
- Browser validation: required fields, email type, future/local event date, positive numeric attendance, lengths, trimmed required strings and preview consent.
- New sample requests receive status `New`.
- Clearly disclosed session-only demo storage and a success message that does not imply delivery to the ministry.
- Real production submission and server-side validation are **not enabled**.

### Management foundation

- Overview metrics for new, under review, pending decision, confirmed/preparing and completed samples.
- Upcoming-events metric explicitly shows **not connected**, rather than inventing a count.
- Invitation list with search and status filtering.
- Complete invitation detail views.
- All nine requested statuses and persistent per-tab demo status changes.
- Approve, decline/close and request-more-information demo actions; none send notifications.
- Sample internal notes stored in the same browser session; rendered as text to avoid injected HTML.
- Upload-document control visibly disabled as planned.
- Event management foundation with protected publishing deliberately deferred.
- Clear-all-demo-data control.

## Entry URIs

All paths are relative to the deployed project root. Navigation uses a query router supported on basic static hosts; direct HTML entries also work.

| Feature | Entry |
| --- | --- |
| Home | `/index.html` or `/index.html?page=home` |
| About | `/about.html` or `/index.html?page=about` |
| Ministry | `/ministry.html` or `/index.html?page=ministry` |
| Events | `/events.html` or `/index.html?page=events` |
| Event detail | `/event.html?id=<public-event-id>` or `/index.html?page=event&id=<public-event-id>` |
| Invitation form | `/invite.html` or `/index.html?page=invite` |
| Give | `/give.html` or `/index.html?page=give` |
| Contact | `/contact.html` or `/index.html?page=contact` |
| Privacy | `/index.html?page=privacy` |
| Terms | `/index.html?page=terms` |
| Dashboard demo | `/dashboard.html` or `/index.html?page=dashboard` |
| Invitation list demo | `/index.html?page=invitations` |
| Invitation detail demo | `/index.html?page=invitation&id=<session-demo-id>` |
| Event management foundation | `/index.html?page=manage-events` |
| Automated browser smoke tests | `/tests.html` (noindex) |

Unknown page parameters show a friendly not-found state. Missing invitation/event IDs show an appropriate unavailable state. Query-based dashboard routes are **not suitable for path-only protection**: migrate the real workspace to a dedicated `/management/` path and protect its APIs when implementing production authentication.

## Public URLs and API endpoints

- Production/custom domain: **not supplied, not deployed**.
- Design reference: https://www.spectrum.life/
- Public event collection: `GET tables/events?page=1&limit=100` (relative URL).
- Subsequent event pages are loaded until the total is reached, with a safety ceiling of 100 pages.
- Event details are resolved from the fetched approved public-event collection.
- Reserved private endpoints, **not used by current frontend**: `tables/invitations`, `tables/contact_messages`, `tables/invitation_notes`.
- No verified Deborah social, music, telephone, email or giving URLs have been supplied; these remain transparent placeholders.

## Data models and storage

Schemas are managed in `.tables/schema.json` by the platform's schema tools. **No seed rows were created.**

### `invitations` (reserved; currently empty)

`id`, `organization_name`, `contact_name`, `phone`, `email`, `event_name`, `event_type`, `event_date`, `event_time`, `venue`, `city`, `event_theme`, `scripture_theme`, `expected_attendance`, `expected_duration`, `assignment_description`, `technical_requirements`, `transportation`, `accommodation`, `feeding`, `financial_support`, `additional_information`, `status`.

- `expected_attendance`: number.
- `event_date`: local date `YYYY-MM-DD`; `event_time`: local venue time.
- Remaining user fields are text.
- `created_at` and `updated_at` are automatically managed system fields (milliseconds) in the Table API; do not duplicate them in the custom schema.
- Future trusted intake must enforce initial `New` status, not trust a supplied browser status.
- Statuses: New, Under Review, More Information Required, Pending Decision, Approved, Confirmed, Preparing, Completed, Closed.

### `events` (public-only)

`id`, `name`, `event_date`, `event_time`, `location`, `description`, `event_type`, `image_url`, `published`.

- Store **only information safe for the public to retrieve**, including every API-returned field.
- `published` controls UI visibility, **not access authorization**. Do not put private drafts or internal logistics in this publicly readable table.
- `event_date` is `YYYY-MM-DD`; include timezone context in the public time field where appropriate.
- Use an approved public image URL or `images/...` path; invalid image URLs fall back to local photography.
- Upcoming/past grouping is based on the visitor's local calendar date, including today as upcoming.
- Publishing events through a protected management backend is future work. Preview rows may be added with approved platform data tools once genuine event details are supplied.

### `contact_messages` (reserved; empty)

`id`, `name`, `email`, `subject`, `message`, `status`. System timestamps automatic.

### `invitation_notes` (reserved; empty)

`id`, `invitation_id`, `body`, `author_id`. System timestamps automatic. Future backend must enforce the parent invitation relationship and author identity; a text field alone does not create relational authorization.

### Current demo storage

- `sessionStorage['du_ministry_demo_v1']`: JSON array of sample invitation objects, status, ISO demo timestamps and `notes: [{text, at}]`.
- Lives in the current browser tab/session, not a shared or secure server inbox.
- Closing the tab normally ends the storage lifetime, but browser session restoration can retain it. Use the explicit clear button when finished.
- Contact preview does not store or transmit messages.
- No offline caching, service worker or marketing analytics.

### Preview versus Hosted database

Preview rows reside in the platform preview data store. Hosted deployment creates a separate Cloudflare D1 database from the schema and does not automatically copy preview rows. Future public-event transfer should use the approved HostedDbSyncFromPreview flow; resolve row conflicts with the owner. Never rebuild a live database just to add schema fields. No hosted resources have been created by this build.

## Image system

See `ASSETS.md` for sources and replacement guidance. The four local files cover cinematic stage, congregation, live performance and editorial artist roles. Real Deborah photos were not supplied. The portrait is clearly labeled **not Deborah**. Do not remove this label until replacing the image with an approved genuine portrait.

## Verification

- Automated browser test suite: **50 checks passed**.
- Tested 12 page routes, desktop overflow, script leakage, invalid/valid invitation states, sample creation, default status, listing, filtering, detail rendering, status saving, escaped internal notes, contact preview, mobile overflow and menu toggle.
- Tests operate on the real rendered application in a same-origin iframe; sample session data is restored afterward.
- Homepage console: no output/errors.
- Desktop hero and mobile homepage screenshots reviewed successfully.
- Desktop/mobile invitation form and dashboard screenshots reviewed successfully: readable fields and notices, responsive cards, no clipping or page-wide overflow. Initial screenshot-tool saturation was resolved by sequential retries.
- No claim of production backend/security or live-domain testing.

## Not yet implemented

- Next.js, TypeScript or server-rendered routes.
- Authentication, manager/admin roles, secure sessions, authorization and audit trail.
- Server-side invitation/contact handling, validation, rate limiting and spam protection.
- Live private dashboard, shared invitation data or team accounts.
- Event creation/editing/publishing inside management UI.
- Real email or WhatsApp notifications and automated responses.
- Calendar, engagement histories, logistics workflows, expenses, financial tracking and analytics.
- Secure document uploads/storage, file scanning and signed URLs.
- Payments, banking integration or donation receipts.
- Official portraits, biography, ministry history, music releases, event details and contact/social links.
- Approved production legal documents and data retention policies.

## Recommended next steps

1. Supply Deborah's approved photographs, biography, genuine music URLs, verified contact/social links and giving instructions.
2. Upgrade the project if platform-level Hosted access rules are desired. Define authorized management users, then configure and test path admission through the platform tools; saved rules are not live until approved deployment.
3. Implement a trusted intake backend with server validation, anti-abuse measures and append-only anonymous submission permissions; deny anonymous listing, reading, updating and deleting of private records. A static browser cannot supply these guarantees.
4. Migrate management to dedicated protected route paths and enforce authenticated roles and per-record permissions on **every** private API. UI visibility and a shared JS password are not security.
5. Add approved public events and implement protected event publishing and document storage.
6. Review legal policies, photography rights and retention/deletion procedures before handling real requests.
7. Perform a production security/accessibility review and end-to-end testing, including timezone and real mobile-device tests.
8. Publish through the Publish tab, or explicitly request Hosted Deploy. No deployment is automatic in this build.

## File structure

```
index.html, about.html, ministry.html, events.html, event.html
invite.html, give.html, contact.html, dashboard.html
css/style.css            shared responsive visual system
js/app.js               reusable view functions, routing, preview workflows, public-event adapter
images/                 locally stored replaceable editorial assets and favicon
tests.html, js/tests.js  real-page browser smoke tests
.tables/schema.json     platform-managed schema foundation
README.md, ASSETS.md     implementation, security and asset documentation
```
