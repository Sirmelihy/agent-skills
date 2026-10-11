# Rules: never ask, never record

These look like choices but are fixed by the design language. Apply them silently. If something here should become
a question, move it into `index.md` as a decision and give it an entry; until then, it is not asked.

## Layering and shape

- At most four tones stacked: background → panel → column → card (§10.2).
- In-flow surfaces never cast shadows; only floating layers use `shadow-float`. Never shadow and border together (§5).
- Surface padding follows context: `p-3.5` inside wells and columns, `p-5` standalone (§5, §9.7).
- Radii follow the scale, controls are pills, nested corners stay concentric (§5).
- The gray values are the §4 tokens. shadcn's init base color (Neutral or Stone) does not change the result (§3).
- Hover darkens a ring or adds a wash; selected is `ring-[1.5px] ring-foreground`; no lift or scale (§5, §13).

## Color and status

- Six status tones, never a seventh (§4).
- Status form follows context: dot + text in cards and dense rows, soft badge in tables, lists and detail views,
  solid badge only in group headers and final outcomes, status icon chip when the status is the item's identity,
  never in a table row (§9.10, §9.14).
- Colored icon chips (status, operation, category) are one solid fill with a black icon, the same in both themes;
  neutral chips are `bg-track` with a `text-foreground` icon (§7).
- Create = success, read = info, update = warning, delete = danger on every chip in the app; other operations follow
  `operation-colors` (§7).
- A sheet's title is plain text; its section headers carry `md` chips in categorical palette order by position,
  neutral after the sixth (§9.17).
- A delta chip is green or red by whether the change is good, not by its direction; direction comes from
  `metric-direction` (§9.12).
- Every color signal also carries text, an icon or a shape (§2, §15).
- A category keeps one hue everywhere, never one from a status family; at most six hues on a screen (§4).
- Unread is a `bg-primary` dot, never a tinted row (§9.15).

## Actions and navigation

- One black primary action per region; secondary as white pills, tertiary as ghost (§9.4, §10.5).
- Destructive actions are red-text secondary pills; solid red only inside a confirmation dialog. A destructive zone
  is its own surface at the end of a form, with a confirmation dialog (§9.4, §9.16).
- Inside a region that already shows a black active state, the nested active item is a white pill (§9.2).
- 2–5 options → segmented control; more → a select or scrolling tabs (§9.5).
- More than 7 filters → the rest go behind a filters icon button (§9.6).
- The account pill sits at the right end of the top bar with `nav = top`, in the sidebar footer with a sidebar (§9.2).
- Below `lg` the top nav moves into a sheet; below `xl` the search pill becomes an icon button; below `sm` a framed
  shell goes edge-to-edge (§14).
- Table row actions appear on hover and stay focusable; long tables get a sticky header; pagination is small pills
  with a muted "1–20 of N" range (§9.14).

## Content and data

- Any 0–100 value is a segmented bar (10 segments in cards, 5 in tables); uploads and multi-step completion use the
  continuous bar. Always paired with the number or a label (§9.9).
- Meta blocks: `MetaGrid` with 2–3 cells in cards; a two-column `dl` in detail views (§9.11).
- Forms: single column, ~640px; two columns only for short paired fields; actions bottom-right; sticky footer on
  long forms (§9.16).
- Charts: horizontal dashed grid only; no legend for a single series; never a pie with more than 4 slices (§9.13).
- Empty: dashed outline, `xl` chip, two lines, optional pill. Loading: skeletons in the real shape, never a
  full-page spinner. Error: inline soft danger block with a retry pill (§9.18).
- Deterministic data, fixed locale and time zone, totals that add up (§12).
- Below `sm`, grids collapse to one column and rows of columns become snap carousels (§14).
