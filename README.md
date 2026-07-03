# Punta

**Short links, event pages, and check-in — built for orgs, not spreadsheets.**

Campus organizations run on posters, group chats, and registration links that don't talk to each other. Punta connects the full chain: branded short URL → event landing page → signup → door check-in → exportable report — in one dashboard.

> Status: **early planning** — see [docs/IMPLEMENTATION_PLAN.md](docs/IMPLEMENTATION_PLAN.md).

## Why orgs need more than a form builder or link tool

Generic tools solve one slice well. Orgs actually juggle five jobs every event:

| Job | What usually happens | Punta |
| --- | -------------------- | ----- |
| Share the link | Paste a long URL in FB caption | Branded short link + QR on the poster |
| Explain the event | Duplicate info in Canva + form description | One **event page** (time, venue, map link, agenda) |
| Collect signups | Separate form; no tie to who clicked which poster | **Registration** tied to campaign link + waitlist |
| Track channels | Guess which post worked | Per-link analytics: clicks → signups → check-ins |
| Prove attendance | Sign-in sheet photo | **QR check-in** + CSV for org reports |

Punta is **org-first**: teams, roles, reusable branding, and exports designed for student council audits — not ad-tech click farms.

## Core flows

### Organizer

```text
Create org → New event → Publish landing page
     ↓
Generate links (poster QR, IG bio, partner org)
     ↓
Watch funnel: clicks → registrations → check-ins
     ↓
Export attendance + download QR for door
```

### Attendee

```text
Scan QR / tap link → Event page → Register (minimal fields)
     ↓
Email or on-screen ticket with check-in QR
     ↓
Show QR at venue → marked present
```

## What makes Punta different

- **Link + event + registration are one object** — not three tabs in three products.
- **Campaign links** — `punta.example/uplb-es/gbm-poster` vs `.../gbm-messenger` share one event but attribute signups.
- **Check-in closes the loop** — analytics mean "who actually came," not just "who clicked."
- **Org branding** — logo, colors, custom slug prefix; pages look like *your* org.
- **Campus-aware fields** — college, year level, org affiliation, dietary (common in PH org events).
- **Venue handoff** — deep link to [Room TBA](https://room-tba.uplbtools.me) when the room is on campus.
- **Discord / webhook hooks** — signup and check-in pings for org moderators (pairs with [uplbtools/discord-bot](https://github.com/uplbtools/discord-bot)).
- **Privacy-respecting** — no third-party ad pixels; org owns registrant data; export/delete on request.
- **Free tier for campus orgs** — paid features (custom domain, SSO) only if demand appears.

## Planned modules

| Module | Description |
| ------ | ------------- |
| **Links** | Short URLs, QR PNG/SVG, optional password, expiry |
| **Events** | Schedule, capacity, waitlist, rich description |
| **Pages** | Public landing (mobile-first), embeddable registration widget |
| **Registrations** | Custom fields, confirmation ticket, edit/cancel policy |
| **Check-in** | Scanner mode for volunteers, offline queue (later) |
| **Analytics** | Funnel per campaign link; export CSV |
| **Orgs & roles** | Owner, editor, door staff (check-in only) |

## Repo layout (planned)

```text
punta/
├── apps/
│   ├── web/           # org dashboard + public event pages
│   └── scanner/       # lightweight check-in PWA (optional split)
├── packages/
│   ├── db/            # Drizzle schema
│   ├── link-core/     # slug generation, redirect rules
│   └── analytics/     # funnel aggregation
└── docs/
    ├── IMPLEMENTATION_PLAN.md
    └── ORG_ROLES.md
```

## Relationship to UPLB Tools

Optional integrations, not hard dependencies:

- Room TBA for venue map links
- Discord bot for `registration.created` / `checkin.completed` events
- Shared auth patterns with other uplbtools apps (future)

## Contributing

Planning phase — org pain stories and field requirements welcome via issues.

## License

MIT — see [LICENSE](LICENSE).
