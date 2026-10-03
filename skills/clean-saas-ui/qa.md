# Anti-patterns and QA (§17, §19)

Read before calling a screen done.

## 17. Anti-patterns

- Writing UI code before the decision gate; asking again about a decision already in the ledger; asking about a
  rule; changing a `user`, `prompt` or `default` decision without being asked.
- Building elements the product does not need because they appear in this file; copying placeholder labels.
- Forcing a pattern the content does not fit (columns for unordered data, KPI tiles on a settings page).
- Shadows on in-flow surfaces; shadow and border on the same element.
- Colored or gradient primary buttons; more than one black primary per region; two black active states nested.
- A dark sidebar in a light theme (breaks the tonal layering).
- Default shadcn Card used as-is (border + shadow + large padding).
- Small radii (≤ 6px) on containers, or mixed radius languages.
- Tinted section backgrounds, colored table headers, rainbow charts, a seventh status color.
- Icon chips on actions or navigation, several chips per item, chips in every table row; emoji as icons.
- Uppercase tracked labels, weights 700+, more than ~8 text sizes.
- Centered text in surfaces and tables (empty states excepted).
- Borders between every row *and* column.
- Lorem ipsum, identical numbers, placeholder names, totals that do not add up.
- Non-deterministic values at render time.
- Whole-page horizontal scroll.

## 19. QA checklist

**Visual**
- [ ] Squint test: only black accents and meaningful colors stand out.
- [ ] Layers read by tone; no in-flow shadows.
- [ ] Containers follow the radius scale; controls are pills.
- [ ] One black primary action per region.
- [ ] Labels gray, values dark; numbers tabular.
- [ ] Spacing on the 4px grid, no one-off gaps.
- [ ] Icon chips mark identity only, at most one per item, hues consistent per category.
- [ ] The page title is the largest text; lead numbers come second.

**Decisions**
- [ ] Every decision this task used is in `design-decisions.md`, with source and date.
- [ ] The screen matches the ledger (shell, navigation, patterns, detail views, lead elements, status mapping).
- [ ] The summary shown before building listed every inferred decision.

**Structure and content**
- [ ] Every element on screen exists because the product needs it.
- [ ] Every label, metric and status comes from the product, none from this skill's placeholders.
- [ ] Counts and totals add up; values varied and realistic; no `undefined` or `NaN`.

**Technical**
- [ ] Build passes; no hydration warnings (SSR frameworks).
- [ ] Works at 375, 768, 1280 and 1536px; no page-level horizontal scroll.
- [ ] Keyboard: tab through navigation, controls, menus and dialogs; focus always visible.

