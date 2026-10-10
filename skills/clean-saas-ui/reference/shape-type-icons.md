# Shape, type, icons (§5–§7)

Applies to everything. Read on every UI task.

## 5. Shape, space, elevation

### Radius

| Element | Class | px |
|---|---|---|
| Framed app shell | `rounded-shell` | 28 |
| Working well (panel), dialog, sheet | `rounded-panel` | 24 |
| Nested well (column), large section | `rounded-column` | 20 |
| Surface: card, tile, table container, menu, popover, toast | `rounded-card` | 14 |
| Inner block in a surface, form input | `rounded-inner` | 10 |
| Menu item | `rounded-md` | 8 |
| Buttons, nav items, filters, search, badges, avatars, icon chips, segmented controls | `rounded-full` | - |

When a container hugs its child (padding ≤ 8px), child radius ≈ parent radius − padding so corners stay concentric
(column 20 with `p-1.5` → card 14).

### Spacing (4px grid)

| Context | Classes |
|---|---|
| Around a framed shell | `sm:p-3 lg:p-5` (0 on mobile) |
| Page / shell padding | `p-4 lg:p-6` |
| Navigation → page title | `mt-8 lg:mt-10` (top nav) / `pt-6 lg:pt-8` (sidebar layout) |
| Page header → main content | `mt-6` |
| Well padding (panel) | `p-3` |
| Toolbar → content | `mt-4` |
| Group header → its content | `gap-3` |
| Between surfaces in a grid or row | `gap-3` |
| Nested well padding / gap between stacked cards | `p-1.5` / `gap-2` |
| Compact surface padding (cards in wells) | `p-3.5` |
| Roomy surface padding (tiles, charts, form sections) | `p-5` |
| Rows inside a surface | `mt-2` to `mt-3` |

Never invent one-off values (5px, 7px, 13px gaps).

### Elevation

- **In-flow surfaces:** no shadow. Tone difference + optional `ring-1 ring-hairline`.
- **Hover:** ring darkens (`hover:ring-foreground/15`) or fill appears (`hover:bg-wash`). No lift, no scale.
- **Selected:** `ring-[1.5px] ring-foreground`.
- **Floating** (menus, popovers, select, dialog, sheet, toast): `shadow-float`, no border.
- **Never:** `shadow-sm/md/lg` on cards, shadow and border together, colored shadows, glass blur, inner shadows.

---

## 6. Typography

Typeface: Geist (or Inter). Sentence case everywhere; never uppercase tracked labels.

| Role | Classes |
|---|---|
| Page title (one per page) | `text-3xl lg:text-[40px] font-medium leading-[1.05] tracking-[-0.035em]` |
| Section title | `text-[15px] font-medium tracking-tight` |
| Surface / card title | `text-sm font-semibold` (one line, truncate) |
| Body, navigation, buttons | `text-sm` (13-14px), buttons `font-medium` |
| Meta / secondary | `text-xs text-muted-foreground` |
| Micro label (inside meta blocks, sidebar sections) | `text-[11px] text-muted-foreground` |
| Lead number in a card | `text-[26px] font-medium leading-none tracking-tight tabular-nums` |
| KPI number | `text-[32px] font-medium leading-none tracking-tight tabular-nums` |
| IDs, codes, log timestamps | `font-mono text-[11px] text-muted-foreground` |

- All numbers use `tabular-nums`. Units (`%`, currency) stay the same size as the number.
- Separate meta items with a spaced middle dot: `First · Second`.
- Weights: 400 body, 500 titles / numbers / buttons, 600 card titles. Never 700+.
- Truncate rather than wrap in cards and table cells (`truncate`, `min-w-0` on flex children).

---

## 7. Iconography

Icons come in three treatments. Pick by role, not by taste.

| Treatment | Role | Look |
|---|---|---|
| **Plain icon** | Actions, controls, navigation, inline hints | Monochrome `currentColor`, 14 / 16 / 18px, default stroke |
| **Icon button** | Icon-only actions | Plain icon centered in a circle: `size-10 rounded-full bg-card ring-1 ring-hairline hover:bg-accent` (`size-8`, `size-7` for smaller) |
| **Icon chip** | Identity: what kind of thing, state or operation this is | Solid colored circle with a black icon (below) |

### Icon chip (signature element)

A circle filled with one solid, vivid color and a black icon on it. It gives an item an identity at a glance and is
one of the most recognizable details of this style.

- **Fill:** one flat, opaque color. No soft tint, no transparency, no gradient, no ring in the same hue.
- **Icon:** black (`text-black`) on every colored chip, in both themes, unless the user asks otherwise. Never an icon
  in the chip's own hue.
- **Neutral chip:** no hue. `bg-track` with a `text-foreground` icon, so it follows the theme.

```tsx
// icon-chip.tsx
import { cn } from "@/lib/utils"
import type { StatusTone } from "./tones"

const SIZE = {
  sm: "size-6 [&_svg]:size-3.5",
  md: "size-8 [&_svg]:size-4",
  lg: "size-10 [&_svg]:size-5",
  xl: "size-14 [&_svg]:size-6",
} as const

export const STATUS_CHIP: Record<StatusTone, string> = {
  success: "bg-success text-black",
  warning: "bg-warning text-black",
  caution: "bg-caution text-black",
  danger: "bg-danger text-black",
  info: "bg-info text-black",
  neutral: "bg-track text-foreground",
}

export type Operation = "create" | "read" | "update" | "delete"

export const OPERATION_CHIP: Record<Operation, string> = {
  create: STATUS_CHIP.success,
  read: STATUS_CHIP.info,
  update: STATUS_CHIP.warning,
  delete: STATUS_CHIP.danger,
}

export function IconChip({ icon: Icon, color, size = "md", className }: {
  icon: React.ElementType                 // any icon component
  color?: string                          // STATUS_CHIP[tone], OPERATION_CHIP[op], categoryColor(i); neutral if omitted
  size?: keyof typeof SIZE
  className?: string
}) {
  return (
    <span className={cn(
      "grid shrink-0 place-items-center rounded-full",
      SIZE[size],
      color ?? STATUS_CHIP.neutral,
      className
    )}>
      <Icon aria-hidden />
    </span>
  )
}
```

Color, by what the chip says: a **categorical** hue for *what kind* (§4 palette); a **status** chip for *what state*;
an **operation** chip for *which operation* (below); **neutral** when color would mean nothing.

### Operation colors

Create, read, update and delete have one color each, everywhere in the app. Anything that stands for one of them
takes that color: dialog and sheet headers (lg), cards that represent the operation, activity and audit entries
(sm-md).

| Operation | Also called | Tone | Color | Icon (lucide) |
|---|---|---|---|---|
| create | add, new | success | green | `plus` |
| read | get, view, details | info | blue | `eye` |
| update | edit, rename | warning | yellow-amber | `pencil` |
| delete | remove | danger | red | `trash-2` |

- The chip marks the dialog, card or event, never the button that runs the operation. Buttons keep §9.4: black
  primary, red-text destructive, solid red only inside a confirmation dialog.
- Any other operation (archive, export, duplicate, approve ...) has no fixed color. It is decision
  `operation-colors`: ask the user once and record it. Never pick its hue on your own.

Where chips shine: group / section / column headers (md), dialog and sheet headers (lg), leading element of list
rows, notifications, search results and activity items (sm-md), timeline nodes (sm), identity line of a card (sm),
settings section headers (md), empty states (xl). Paired outcomes or participants can overlap: `flex -space-x-2`,
each chip with `ring-2 ring-<surface tone>` (e.g. `ring-card`, `ring-panel`).

Not for: buttons and actions, navigation items, every row of a dense table (use a status dot there), decoration
without meaning. At most one chip per item.

