# Primitive restyles (§8)

Done once per project, for the primitives in use.

## 8. Restyle shadcn primitives once

Edit `components/ui/*` once so every usage inherits the style. Do not patch the same classes at each call site.
Restyle only the primitives the project uses.

**Button** (cva)
- Base: `rounded-full` instead of `rounded-md`; keep the focus-visible ring.
- `default`: `bg-primary text-primary-foreground hover:bg-primary/85`
- `secondary`: `bg-card text-foreground ring-1 ring-hairline hover:bg-accent` (white pill on gray)
- `outline`: `bg-transparent ring-1 ring-border hover:bg-wash` (no border)
- `ghost`: `hover:bg-wash`
- `destructive`: `bg-card text-danger-strong ring-1 ring-hairline hover:bg-danger-soft` (solid red only inside a confirm dialog)
- Sizes (add any that are missing): `default h-10 px-4 text-sm`, `sm h-8 px-3 text-[13px]`, `lg h-11 px-5 text-sm`,
  `icon size-10`, `icon-sm size-8`, `icon-xs size-7`. SVG inside: `size-4` (`size-3.5` for xs).

**Dropdown menu, popover, select, command, context menu** (content / popup parts)
- Content: `rounded-card bg-popover p-1.5 shadow-float`, remove border/ring classes.
- Items: `rounded-md px-2.5 py-2 text-[13px]`, highlighted `bg-wash`.

**Tooltip:** dark pill: `bg-primary text-primary-foreground rounded-lg px-2.5 py-1.5 text-xs`.

**Badge:** `rounded-full h-6 px-2.5 text-xs font-medium gap-1.5`. Status looks in §9.10.

**Input, textarea, select trigger:** `rounded-inner bg-card ring-1 ring-hairline border-0 h-10 px-3 text-sm`,
focus `ring-2 ring-foreground/20`, invalid `ring-danger/60`.

**Switch, checkbox, radio:** checked `bg-primary`; unchecked track `bg-track`.

**Tabs / toggle group:** restyle to the segmented look (§9.5): pill container, black active item.

**Sidebar** (if used): set the sidebar tokens (§4); menu buttons `rounded-full h-9 px-3 gap-2.5 text-sm`; change the
active-state classes of the menu button to `bg-sidebar-primary text-sidebar-primary-foreground` (shadcn's default uses
the accent token for both hover and active).

**Dialog:** `rounded-panel bg-background p-6 shadow-float border-0`; actions right-aligned as pills.

**Sheet:** floating inset look:
`inset-y-3 right-3 h-auto w-[min(480px,calc(100vw-24px))] sm:max-w-[480px] rounded-panel bg-background shadow-float border-0`
(the `sm:max-w-*` override is needed because shadcn caps sheet width by default; mirror for left sheets).

**Toast (Sonner):** `rounded-card bg-card shadow-float border-0 text-[13px]`, leading status icon chip `sm`.

**Card:** shadcn's Card (border, shadow, large padding) does not match this style. Use the Surface look (§9.1)
or restyle Card to it.

**Chart, table:** leave the files; style through usage (§9.13, §9.14).

