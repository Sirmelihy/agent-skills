# Catalog: cards, status, progress (§9.7–§9.11)

Part of the element catalog (§9): how an element looks when a screen uses it. Look up only what the screen uses; never add an element because it is listed here. Interactive snippets carry `"use client"` (required by Next.js App Router, ignored elsewhere).

### 9.7 Cards

How a card looks, whatever it represents:

- White surface, `rounded-card`, hairline ring, no shadow. `p-3.5` in wells and columns, `p-5` standalone.
- Vertical order (every row optional except the title):
  1. **Header:** title (`text-sm font-semibold`) + one meta line (`text-xs text-muted-foreground`, `·` separated);
     corner action top-right.
  2. **Identity line:** organization, owner or category: a wordmark, an avatar or an `sm` icon chip + text.
  3. **Lead:** one number (26px) with its supporting visual (segmented bar, sparkline, delta chip) and a short
     qualitative label on the right (`text-xs text-muted-foreground`).
  4. **Status line:** colored dot + text (§9.10).
  5. **Meta block:** 2-3 label/value cells (§9.11).
- Five rows maximum. Rows separated by `mt-2`-`mt-3`, never by lines.
- Hover: `hover:ring-foreground/15`. Selected: `ring-[1.5px] ring-foreground`.
- Compact variant (dense lists, archives): title, meta line, one mono line (`font-mono text-[11px]`); `px-3.5 py-3`.
- Logos and avatars keep their own colors (they are content). For mocks, use fictional brands as text wordmarks.

Reference composition:

```tsx
<article className="rounded-card bg-card p-3.5 ring-1 ring-hairline transition-shadow hover:ring-foreground/15">
  <header className="flex items-start justify-between gap-2">
    <div className="min-w-0">
      <h3 className="truncate text-sm font-semibold">{title}</h3>
      <p className="truncate text-xs text-muted-foreground">{metaA} · {metaB}</p>
    </div>
    {cornerAction}
  </header>
  <div className="mt-2 flex items-center gap-2.5">
    <span className="text-[26px] font-medium leading-none tracking-tight tabular-nums">{leadValue}</span>
    <SegmentedProgress value={score} label={scoreName} />
    <span className="ml-auto text-xs text-muted-foreground">{qualitativeLabel}</span>
  </div>
  <StatusLine tone={tone} className="mt-3">{statusText}</StatusLine>
  <MetaGrid className="mt-3" items={metaItems} />
</article>
```

### 9.8 Group headers

For columns, sections and grouped lists: `md` icon chip + label (`text-[13px] font-semibold`) + meta
(`text-xs text-muted-foreground`, e.g. a count) in a `flex items-center gap-2.5 px-1` row. When the groups form a
sequence (steps, stages), a connector `h-px flex-1 bg-track` runs from each header toward the next. Outcome groups
can show a solid status badge with a count on the right instead of a chip. Inside a sheet, the chips take the
categorical palette in section order (§9.17).

### 9.9 Scores and progress

```ts
// tones.ts
export type StatusTone = "success" | "warning" | "caution" | "danger" | "info" | "neutral"
export type ScoreTone = "high" | "medium" | "low"

export function scoreTone(value: number, { high = 75, medium = 60 } = {}): ScoreTone {
  if (value >= high) return "high"
  if (value >= medium) return "medium"
  return "low"
}

export const SCORE_BAR: Record<ScoreTone, string> = { high: "bg-success", medium: "bg-warning", low: "bg-caution" }
```

```tsx
// segmented-progress.tsx
import { cn } from "@/lib/utils"
import { SCORE_BAR, scoreTone, type ScoreTone } from "./tones"

export function SegmentedProgress({ value, label, tone = scoreTone(value), segments = 10, className }: {
  value: number          // 0-100
  label: string          // accessible name
  tone?: ScoreTone       // override when higher is worse (risk, load, churn)
  segments?: number
  className?: string
}) {
  const filled = Math.round((value / 100) * segments)
  return (
    <div
      role="meter"
      aria-label={label}
      aria-valuenow={value}
      aria-valuemin={0}
      aria-valuemax={100}
      className={cn("flex items-center gap-[3px]", className)}
    >
      {Array.from({ length: segments }, (_, i) => (
        <span key={i} className={cn("h-4 w-1 rounded-full", i < filled ? SCORE_BAR[tone] : "bg-track")} />
      ))}
    </div>
  )
}
```

- Segmented bars are the default look for any 0-100 value (score, progress, capacity, confidence):
  10 segments in cards, 5 in tables.
- Always pair with the number and/or a qualitative label.
- Long continuous progress (uploads, multi-step completion): a `h-1.5 rounded-full bg-track` track with a
  `bg-primary` fill.

### 9.10 Status

```tsx
// status.tsx
import { cn } from "@/lib/utils"
import type { StatusTone } from "./tones"

const DOT: Record<StatusTone, string> = {
  success: "bg-success", warning: "bg-warning", caution: "bg-caution",
  danger: "bg-danger", info: "bg-info", neutral: "bg-faint",
}
const SOLID: Record<StatusTone, string> = {
  success: "bg-success text-black", warning: "bg-warning text-black", caution: "bg-caution text-black",
  danger: "bg-danger text-black", info: "bg-info text-black", neutral: "bg-wash text-foreground",
}
const SOFT: Record<StatusTone, string> = {
  success: "bg-success-soft text-success-strong", warning: "bg-warning-soft text-warning-strong",
  caution: "bg-caution-soft text-caution-strong", danger: "bg-danger-soft text-danger-strong",
  info: "bg-info-soft text-info-strong", neutral: "bg-wash text-muted-foreground",
}

export function StatusLine({ tone, children, className }: {
  tone: StatusTone
  children: React.ReactNode
  className?: string
}) {
  return (
    <p className={cn("flex items-center gap-2 text-xs text-foreground/80", className)}>
      <span aria-hidden className={cn("size-1.5 shrink-0 rounded-full", DOT[tone])} />
      <span className="truncate">{children}</span>
    </p>
  )
}

export function StatusBadge({ tone, soft = false, children }: {
  tone: StatusTone
  soft?: boolean
  children: React.ReactNode
}) {
  return (
    <span className={cn(
      "inline-flex h-6 items-center gap-1.5 rounded-full px-2.5 text-xs font-medium",
      soft ? SOFT[tone] : SOLID[tone]
    )}>
      <span aria-hidden className="size-1.5 rounded-full bg-current" />
      {children}
    </span>
  )
}
```

- **Dot + text** inside cards and dense rows.
- **Soft badge** in tables, lists and detail views.
- **Solid badge** for group headers and final outcomes (the loudest form; use sparingly).
- **Status icon chip** when the status is the identity of a list item (notifications, alerts, activity).

### 9.11 Meta blocks

```tsx
// meta-grid.tsx
import { cn } from "@/lib/utils"

export function MetaGrid({ items, className }: {
  items: { label: string; value: React.ReactNode }[]   // 2-3 items
  className?: string
}) {
  return (
    <dl className={cn("grid auto-cols-fr grid-flow-col divide-x divide-border rounded-inner ring-1 ring-border", className)}>
      {items.map((item) => (
        <div key={item.label} className="min-w-0 px-3 py-2">
          <dt className="text-[11px] text-muted-foreground">{item.label}</dt>
          <dd className="truncate text-[13px] font-medium tabular-nums">{item.value}</dd>
        </div>
      ))}
    </dl>
  )
}
```

Larger key-value sets (detail views): a two-column `dl` with `text-xs text-muted-foreground` terms and
`text-[13px] font-medium` values, rows `py-2.5` divided by `border-b border-border`.

