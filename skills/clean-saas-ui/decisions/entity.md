# Entity decisions

An entity is a kind of record the product shows: invoice, customer, ticket, candidate. Its decisions are made once
and apply on every screen that shows it. Record them under `### <entity>` in the ledger's `## Entities` section.

When a question needs a concrete proposal (a card spec, a status mapping), write that proposal from the entity's
real fields as the recommended option, and offer one or two genuine alternatives.

---

## `detail-view` · Where an entity's details open

- `sheet`: floating inset sheet on the right; the list stays visible behind it.
- `page`: its own route (e.g. `/invoices/[id]`), with a page header and `wayfinding`.
- `both`: a sheet for a quick look, with an "Open" action to the full page.

**Recommend:** `sheet` when the details fit in ~3–5 stacked surfaces and users work through a list; `page` when the
entity has its own sub-lists or tabs, or needs a shareable URL. **Look:** §8 (sheet), §9.3, §9.17.

## `create-edit` · Where create and edit forms open

- `dialog`: up to ~5 fields.
- `sheet`: ~6–15 fields; the user keeps the list in view.
- `page`: long or multi-step forms, with a sticky footer.

**Recommend:** by field count, as above. **Look:** §9.16, §9.17.

## `lead` · The element that wins

The one value a user scans for on this entity's cards, rows and tiles: its title, or one number.

Offer 2–3 candidates from the entity's fields plus `title`. **Recommend:** the field that answers the user's main
question about the entity (an invoice → its amount; a customer → health score or revenue; a ticket → its title).
Record the field name. **Look:** §2.5, §9.7 (lead row), §9.14 (first column, right-aligned value).

## `status-map` · Product statuses → tones

Map every status of the entity to one of the six tones: success, warning, caution, danger, info, neutral.

Propose a full mapping as the recommended option, e.g. `paid=success · pending=info · overdue=danger ·
draft=neutral`. Offer an alternative only where a status can honestly go two ways ("on hold": warning or neutral).
Never a seventh color. **Look:** §4 (status tones).

## `card-content` · What the entity's card shows

Only when the entity is shown as cards.

- `full`: up to five rows: header (title + meta line), identity line, lead (number + visual + label), status line,
  meta block (2–3 cells).
- `compact`: title, meta line, one mono line. For dense lists and archives.

Propose a concrete spec from the entity's fields as the recommended option, for example:
"Full: title + client · due date; amount with delta chip; status line; meta: issued, items, owner". Name the
identity line (wordmark, avatar, `sm` icon chip or none) and the lead visual (segmented bar, sparkline, delta chip
or none). Offer one leaner and one richer alternative. **Look:** §9.7, §9.9, §9.11.

## `metric-direction` · Is higher better? (infer)

For every metric of the entity that gets a score bar, chart or delta: `higher-better` or `higher-worse` (risk,
churn, load, error rate, time to resolve). Drives the `SegmentedProgress` tone override (§9.9) and the delta chip
color (§9.12). **Infer** from the metric's meaning; ask only if it is genuinely unclear.

## `category-hue` · Category colors (infer)

Assign categorical hues in palette order (§4), one per category, fixed everywhere in the app. At most six per
screen; beyond that, neutral chips. Record the mapping, e.g. `design=0 · engineering=1 · sales=2`.

## `icon` · Entity icon (infer)

One icon from the project's icon library for the entity (and one per category when categories get chips). The chip
color follows §7: categorical for kind, status for state, the operation color for create / read / update / delete,
neutral otherwise.
