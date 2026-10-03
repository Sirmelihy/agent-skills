# Screen decisions

A screen is one route or view. Record its decisions under `### <route>` in the ledger's `## Screens` section.
Ask `pattern` and `header` first; the others open only when `pattern` includes their element.

---

## `constraints` · What the user's constraint covers

When the request states a constraint that can be read two ways, ask what it covers before anything else.
Example: "no cards" → only the card grid, or KPI tiles and chart surfaces too? "Simple" → fewer sections, or the
compact density? Record the clarified wording. It overrides every recommendation below for this screen.

## `pattern` · What the screen is made of

The patterns on the screen, top to bottom. Recommend from the content shape (§10.6):

| Content | Usually fits |
|---|---|
| Items moving through ordered states | Columns in a well, group headers with chips and connectors |
| Many records with comparable fields | Table |
| A few key numbers | KPI tiles, optionally one chart |
| Trends and comparisons | Chart surface |
| One entity's details | Stacked surfaces in a sheet or page |
| Configuration | Form sections with setting rows |
| Events over time | List or timeline with icon chips |

Offer the recommended composition (e.g. "KPI row · revenue chart · recent invoices table") plus one or two real
alternatives, such as board vs. table for records that move through states. Respect `constraints`.
**Look:** §10.

## `header` · Page header

- Summary line: which 1–3 figures, or none.
- Right side: a view or period segmented control (with which options), or none; the single primary action (which
  verb), or none.

**Recommend from the screen's job:** list screens get "New <entity>" as the primary action; analytics screens get a
period control and no primary action; settings screens get neither. **Look:** §9.3, §9.4, §9.5.

## `kpis` · KPI tiles

Which 3–5 metrics, in one row at the top. Per tile: a hint line, a 32px sparkline or nothing; an `sm` icon chip
before the label or not.

**Recommend:** the metrics that summarize the screen's main table or chart; sparklines on metrics whose trend
matters. **Look:** §9.12.

## `chart` · Chart

- Form: `bar` (compare periods or categories), `line` (trend over time), `area` (volume over time), `ranked-list`
  (shares, with segmented bars; used instead of a pie).
- Color: monochrome (default), a status hue when a series *is* that status, categorical for truly categorical series.
- A period segmented control in the chart header, or not.

**Recommend:** from the question the chart answers. **Look:** §9.13.

## `table` · Table

- Columns and their order.
- First column: two-line text, or led by an avatar or an `sm` icon chip.
- Page size.

**Recommend:** first column = the entity's title with a meta line; the `lead` number right-aligned; 20 rows per
page. **Look:** §9.14.

## `events` · Events over time

- `list`: rows with leading icon chips, title + meta, trailing timestamp.
- `timeline`: `sm` chips on a vertical track line.

**Recommend:** `timeline` for one entity's history; `list` for a feed across entities. **Look:** §9.15.

## `filters` · Filters and sort

Which filters (3–7 visible), their default values ("All", "Any"), and the sort options.

**Recommend:** filters on the fields users narrow by most (status, owner, date range). **Look:** §9.6.

## `wells` · Grouping wells (infer)

A `bg-panel` well when a region holds ~4 or more surfaces, or a board of columns; surfaces directly on the
background otherwise. Never more than four tones. **Look:** §9.1, §10.2.

## `screen-density` · Density of this screen (infer)

Follows `density`. A data-heavy screen in a comfortable app may go compact (surfaces `p-3`, rows `h-12`); text
sizes never shrink. **Look:** §10.8.

## `group-headers` · Group headers (infer)

`md` icon chip + label + count by default; a solid status badge with a count for outcome groups; `bg-track`
connectors when the groups form a sequence. **Look:** §9.8.
