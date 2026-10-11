# Catalog: layout and navigation (§9.1–§9.6)

Part of the element catalog (§9): how an element looks when a screen uses it. Look up only what the screen uses; never add an element because it is listed here. Interactive snippets carry `"use client"` (required by Next.js App Router, ignored elsewhere).

### 9.1 Surfaces and wells

```tsx
// surface.tsx
import { cn } from "@/lib/utils"

export function Surface({ className, ...props }: React.ComponentProps<"div">) {
  return <div className={cn("rounded-card bg-card ring-1 ring-hairline", className)} {...props} />
}
```

- **Surface:** white, `rounded-card`, hairline ring, no shadow. Compact `p-3.5`, roomy `p-5`.
- **Well:** a gray container that groups surfaces without a border: `rounded-panel bg-panel p-3`; nested well
  `rounded-column bg-column p-1.5`. Wells replace boxes-with-borders as the grouping device.
- **Shell** (decision `shell`): *framed* puts the whole app on `bg-background` inside a `rounded-shell` frame on
  `bg-canvas` (`sm:p-3 lg:p-5` around it, edge-to-edge below `sm`); *full-bleed* puts it directly on `bg-background`.

### 9.2 Navigation

The navigation model is decision `nav` (sidebar details: `sidebar-placement`, `sidebar-behavior`; global
utilities: `chrome`). Whichever it is, it looks like this.

**Top navigation** (fits ≤ 7 top-level sections)
- Container: `flex items-center gap-0.5 rounded-full bg-card p-1 ring-1 ring-hairline`
- Item: `rounded-full px-4 py-2 text-sm text-foreground/75 transition-colors hover:bg-wash hover:text-foreground`
- Active item: `bg-primary text-primary-foreground`, `aria-current="page"`
- Logo mark: `size-11 rounded-full bg-primary` with a white mark, left of the nav.
- Right side: search pill, icon buttons, account pill (below).

**Sidebar** (fits many sections, hierarchy, or frequent switching)
- Width 240-264px; collapsed icon rail 64px with tooltips.
- Background: same tone as what it sits on (`bg-background`), or `bg-canvas` when the content floats beside it as a
  framed shell. Use `border-r border-border` only if the tones are identical and a seam is needed.
- Item: `flex h-9 items-center gap-2.5 rounded-full px-3 text-sm text-foreground/75 hover:bg-wash hover:text-foreground`
  with a plain 16px icon (not an icon chip).
- Active item: `bg-primary text-primary-foreground`.
- Count: `ml-auto text-xs tabular-nums text-muted-foreground` (on the active item `text-primary-foreground/60`).
- Section label: `px-3 pb-1 pt-4 text-[11px] font-medium text-muted-foreground`.
- Header: logo mark + product name (`text-sm font-semibold`). Footer: account pill or workspace switcher.

**Secondary navigation** (views, tabs inside a page): segmented control (§9.5). When nested inside a region that
already shows a black active state, step down: active item becomes a white pill on gray
(`bg-card ring-1 ring-hairline`) instead of black.

**Breadcrumbs:** `text-[13px] text-muted-foreground`, separators `/` in `text-faint`, current item
`font-medium text-foreground`.

**Search pill:** `flex h-11 items-center gap-2 rounded-full bg-card px-4 ring-1 ring-hairline
focus-within:ring-foreground/20`, 16px search icon in `text-muted-foreground`, borderless transparent input.
A ⌘K hint as `Kbd` on the right is a nice touch.

**Account pill:** `flex h-11 items-center gap-2 rounded-full bg-card pl-1 pr-3 ring-1 ring-hairline hover:bg-accent`
with a `size-9` avatar, name `text-sm font-medium`, 16px chevron.

**Icon buttons in bars:** `size-11 rounded-full bg-card ring-1 ring-hairline hover:bg-accent`, 18px icon,
`aria-label`. A notification dot: `size-2 rounded-full bg-danger ring-2 ring-card` at the top-right.

### 9.3 Page header

- Left: page title (§6) and an optional one-line summary (1-3 key figures, `text-sm text-muted-foreground`,
  separated by `·`).
- Right: optional segmented control (view or period) and at most one black primary action.
- Detail pages: a ghost `icon-sm` back button or breadcrumbs above the title.
- Layout: `flex flex-wrap items-end justify-between gap-4`; actions wrap under the title on small screens.

### 9.4 Buttons and actions

- Hierarchy per region: one **primary** (black pill), any number of **secondary** (white pills), **ghost** for
  low-emphasis and toolbar actions, **destructive** as a red-text secondary pill. Solid red only for the confirm
  button of a confirmation dialog: `destructive-solid` (`bg-danger-solid text-white`, §8).
- Icon + label: 16px icon left of the label, gap 6-8px. Icon-only: circle with `aria-label`.
- Corner action on a surface (open, expand): `size-7 rounded-full ring-1 ring-hairline hover:bg-wash` with a 14px
  arrow-up-right icon, top-right of the surface.
- Labels are verbs or verb + noun in sentence case ("Export", "New report").

### 9.5 Segmented control

```tsx
// segmented-control.tsx
"use client"

import { cn } from "@/lib/utils"

export function SegmentedControl<T extends string>({ options, value, onChange, label, size = "md" }: {
  options: readonly T[]
  value: T
  onChange: (value: T) => void
  label: string
  size?: "sm" | "md"
}) {
  return (
    <div role="radiogroup" aria-label={label} className="flex rounded-full bg-card p-1 ring-1 ring-hairline">
      {options.map((option) => (
        <button
          key={option}
          role="radio"
          aria-checked={option === value}
          onClick={() => onChange(option)}
          className={cn(
            "rounded-full font-medium transition-colors",
            size === "sm" ? "h-7 px-3 text-xs" : "h-9 px-4 text-[13px]",
            option === value ? "bg-primary text-primary-foreground" : "text-foreground/70 hover:text-foreground"
          )}
        >
          {option}
        </button>
      ))}
    </div>
  )
}
```

2-5 options. More than five → a select or tabs that scroll.

### 9.6 Filters and toolbars

```tsx
// filter-pill.tsx
"use client"

import { ChevronDown } from "lucide-react"
import {
  DropdownMenu, DropdownMenuContent, DropdownMenuRadioGroup, DropdownMenuRadioItem, DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"

export function FilterPill({ label, value, options, onChange }: {
  label: string
  value: string
  options: string[]
  onChange: (value: string) => void
}) {
  return (
    <DropdownMenu>
      <DropdownMenuTrigger className="inline-flex h-9 shrink-0 items-center gap-1.5 rounded-full bg-card px-3.5 text-[13px] ring-1 ring-hairline outline-none transition-colors hover:bg-accent focus-visible:ring-2 focus-visible:ring-foreground/20 aria-expanded:ring-foreground/20">
        <span className="text-muted-foreground">{label}</span>
        <span className="font-medium">{value}</span>
        <ChevronDown aria-hidden className="size-3.5 text-muted-foreground" />
      </DropdownMenuTrigger>
      <DropdownMenuContent align="start" className="min-w-48">
        <DropdownMenuRadioGroup value={value} onValueChange={onChange}>
          {options.map((option) => (
            <DropdownMenuRadioItem key={option} value={option}>{option}</DropdownMenuRadioItem>
          ))}
        </DropdownMenuRadioGroup>
      </DropdownMenuContent>
    </DropdownMenu>
  )
}
```

- Filter pill = gray label + dark value + chevron. The first option is the neutral default ("All", "Any").
- Toolbar: filters in a `no-scrollbar` horizontally scrolling row (`flex min-w-0 flex-1 gap-2 overflow-x-auto`);
  sort and view options pinned right as secondary pills / icon buttons.
- 3-7 visible filters; more go behind a "filters" icon button. Active (non-default) filters may get a small
  clear button inside the pill.

