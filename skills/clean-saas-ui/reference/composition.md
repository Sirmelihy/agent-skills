# Composition (§10)

How to put elements together on a screen. It does not prescribe a layout; the screen decisions do.

## 10. Composition principles

These guide how to put elements together. They do not prescribe a layout.

1. **Structure comes from the decisions.** Navigation (`nav`), shell (`shell`) and the patterns on each screen
   (`pattern`) are in the ledger before anything is styled.
2. **Layer by tone.** Background → (optional well) → white surfaces. Use a `bg-panel` well when a region holds many
   surfaces; place a few surfaces directly on the background (decision `wells`). Framed or full-bleed is decision
   `shell`. Never stack more than four tones.
3. **Group with wells and space, not borders.** Related items share a well or sit closer together.
4. **One clear hierarchy per screen:** page title > lead numbers > surface titles > body > meta.
5. **One primary action per region.** Secondary actions as white pills, tertiary as ghost.
6. **Pick patterns by content shape.** This table computes the recommended option for decision `pattern`; the
   user's answer wins:

| Content | Usually fits |
|---|---|
| Items moving through ordered states | Columns in a well, group headers with chips and connectors |
| Many records with comparable fields | Table |
| A few key numbers | KPI tiles, optionally one chart |
| Trends and comparisons | Chart surface |
| One entity's details | Stacked surfaces in a sheet or page |
| Configuration | Form sections with setting rows |
| Events over time | List or timeline with icon chips |

7. **Rhythm and alignment.** One gutter value per level (§5), aligned surface edges, left-aligned text,
   right-aligned numbers in tables.
8. **Density** (decisions `density`, `screen-density`). Comfortable by default. For data-heavy screens, a compact
   mode reduces padding (surfaces `p-3`, table rows `h-12`) but never text sizes.

