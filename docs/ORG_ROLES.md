# Org roles & permissions

How teams access Punta without everyone being an admin.

**Status:** draft — refine during auth implementation.

---

## Roles

| Role | Links | Events | Registrations | Check-in | Billing | Org settings |
| ---- | ----- | ------ | ------------- | -------- | ------- | ------------ |
| **Owner** | CRUD | CRUD | view/export/delete | scan | manage | CRUD |
| **Editor** | CRUD | CRUD | view/export | scan | — | — |
| **Door staff** | — | view | view (name only) | scan | — | — |
| **Analyst** | view | view | view/export | — | — | — |

- One **owner** per org minimum; ownership transfer supported.
- **Door staff** see attendee name + ticket QR, not full registration answers (unless org enables for small events).
- Invite via email magic link or org code (campus-friendly).

---

## Org model

```ts
type Org = {
  id: string;
  slug: string; // punta.example/o/{slug}
  name: string;
  logoUrl: string | null;
  brandColor: string | null;
  plan: "free" | "pro"; // pro deferred
};

type OrgMember = {
  orgId: string;
  userId: string;
  role: "owner" | "editor" | "door" | "analyst";
};
```

Public URLs:

- Org hub: `/o/{orgSlug}`
- Event: `/o/{orgSlug}/{eventSlug}` or short `/e/{code}`

---

## Audit

Owners can view **audit log**: who exported data, changed capacity, deleted registrations (last 90 days on free tier).
