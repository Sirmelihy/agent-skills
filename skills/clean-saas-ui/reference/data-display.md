# Catalog: KPI tiles, charts, tables, lists (§9.12–§9.15)

Part of the element catalog (§9): how an element looks when a screen uses it. Look up only what the screen uses; never add an element because it is listed here. Interactive snippets carry `"use client"` (required by Next.js App Router, ignored elsewhere).

### 9.12 KPI tiles

- Roomy surface (`p-5`). Top row: label (`text-[13px] text-muted-foreground`, optional `sm` icon chip before it) and a
  delta chip on the right. Then the number (32px), then an optional hint line or a 32px sparkline.
- Delta chip: `inline-flex h-6 items-center gap-0.5 rounded-full px-2 text-xs font-medium tabular-nums`, soft success
  or soft danger by whether the change is *good* (a rising error rate is red), with a 14px arrow.
- 3-5 tiles per row; one row maximum at the top of a view.

### 9.13 Charts

Use shadcn Chart (Recharts) and its `ChartConfig` so series colors come from tokens:

```tsx
const config = {
  current:  { label: "This period",     color: "var(--chart-1)" },
  previous: { label: "Previous period", color: "var(--chart-3)" },
} satisfies ChartConfig

<ChartContainer config={config} className="h-56 w-full">
  <BarChart data={data} barGap={4}>
    <CartesianGrid vertical={false} strokeDasharray="3 4" />
    <XAxis dataKey="label" tickLine={false} axisLine={false} tickMargin={8} />
    <YAxis tickLine={false} axisLine={false} width={32} />
    <ChartTooltip cursor={{ fill: "var(--subtle)" }} content={<ChartTooltipContent />} />
    <Bar dataKey="current" fill="var(--color-current)" radius={6} barSize={12} />
    <Bar dataKey="previous" fill="var(--color-previous)" radius={6} barSize={12} />
  </BarChart>
</ChartContainer>
```

- **Monochrome first:** black for the main series, grays for comparison. A status hue only when a series *is* that
  status (failures in danger). Categorical hues only for truly categorical series, from the §4 palette order.
- Horizontal dashed grid only; no axis lines, no tick lines, no chart border or background.
- Bars rounded (`radius={6}`) and thin (10-14px). Lines stroke 2, `type="monotone"`, no dots except the active one.
  Areas filled at 8-12% opacity.
- Legend as small dots + labels in the chart card's header, not Recharts' legend. No legend for a single series.
- Tooltips: white floating surface (`rounded-card shadow-float`), values tabular.
- Prefer a ranked list with segmented bars over pie/donut; never more than 4 slices.
- Chart card: roomy surface; header row = section title + legend + optional `sm` segmented control (period).

### 9.14 Tables

- Container: `Surface` with `overflow-hidden`. Header row `bg-column`, cells `h-10 px-4 text-xs font-medium
  text-muted-foreground`, no header borders.
- Rows `h-14`, `border-border/70` between rows, `hover:bg-subtle`. No zebra stripes, no vertical borders.
- First column two-line: primary (`text-[13px] font-medium`) + meta (`text-xs text-muted-foreground`), optionally led
  by an avatar or an `sm` category chip that says what kind the row is (`gap-3`). Never a status chip in a row.
- Numbers right-aligned and tabular. Status as soft badge or dot + text. Scores as number + 5-segment bar.
- Row actions appear on hover (`opacity-0 group-hover:opacity-100`), stay focusable.
- Sticky header for long tables; pagination as small pills with a muted "1-20 of N" range.

### 9.15 Lists and activity

- List: a surface with `px-4`; rows `flex items-center gap-3 py-3 border-b border-border last:border-0`;
  leading avatar or icon chip, title + meta in the middle, trailing value, badge or chevron.
- Activity / timeline: `sm` icon chips (status, operation or category) on a vertical `w-px bg-track` line; event
  text `text-[13px]` with the actor in `font-medium`; timestamp `text-xs text-muted-foreground`.
- Notifications: same as list rows; unread marked by a `size-2 rounded-full bg-primary` dot, not by a tinted row.

