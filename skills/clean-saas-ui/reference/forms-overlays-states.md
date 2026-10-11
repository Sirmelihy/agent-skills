# Catalog: forms, overlays, states (§9.16–§9.18)

Part of the element catalog (§9): how an element looks when a screen uses it. Look up only what the screen uses; never add an element because it is listed here. Interactive snippets carry `"use client"` (required by Next.js App Router, ignored elsewhere).

### 9.16 Forms and settings

- Section: roomy surface; header = section title + one-line `text-xs text-muted-foreground` description.
- Setting row: label (`text-[13px] font-medium`) + description (`text-xs text-muted-foreground`) on the left,
  control on the right; rows `py-4 border-b border-border last:border-0`.
- Field: label above the input (`mb-1.5`), helper text below, error text (`text-xs text-danger-strong`) replaces
  the helper and the input gets `ring-danger/60`. Use shadcn `Field` parts when available.
- Single column, ~640px max width; two columns only for short paired fields.
- Actions bottom-right: secondary "Cancel" pill + black primary pill; a sticky footer bar for long forms.
- Destructive zone: its own surface at the end, title in `text-danger-strong`, destructive pill, confirmation dialog.

### 9.17 Overlays

- **Menus, popovers, selects, command palette:** `rounded-card bg-popover p-1.5 shadow-float`; items `rounded-md`,
  highlighted `bg-wash`; shortcuts as muted `Kbd`.
- **Dialog:** `rounded-panel bg-background p-6 shadow-float`; title `text-lg font-medium tracking-tight`; content in
  surfaces if grouped; pill actions right-aligned. A create, read, update or delete dialog puts its `lg` operation
  chip (§7) and the title on one row (`flex items-center gap-3`), not above it; the description goes below both,
  left-aligned with the chip.
- **Sheet:** floating inset panel (§8), content on `bg-background` in stacked surfaces, sticky footer with pill actions.
  The title is always plain text, never led by a chip. Each section is a group header (§9.8) above its surface; the
  header's `md` chip takes the categorical palette by position (first section `CATEGORY[0]`, second `CATEGORY[1]`,
  and so on; neutral after the sixth). The same holds for detail, create and edit sheets.
- **Tooltip:** dark pill, one short line.
- **Toast:** white floating surface, leading `sm` status icon chip, one line + optional action as a ghost pill.

### 9.18 Empty, loading, error

- **Empty:** `rounded-card border border-dashed border-track py-8 text-center`; an `xl` neutral or category icon chip,
  one `text-[13px] font-medium` line, one `text-xs text-muted-foreground` line, optionally one secondary pill.
- **Loading:** skeletons mirror the real element's shape (radius, padding, row heights); text lines `rounded-full`;
  `Skeleton` with `bg-wash`. No full-page spinners.
- **Error:** inline soft danger block (`rounded-inner bg-danger-soft text-danger-strong px-3 py-2 text-xs`) with a
  retry pill. Never a full red page.

