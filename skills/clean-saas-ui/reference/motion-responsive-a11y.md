# Motion, responsive, accessibility (§13–§15)

Read for the responsive pass and the accessibility pass.

## 13. Motion

- `transition-colors` (rings: `transition-shadow`), 150ms. Never `transition-all` on layout.
- Hover: white pills → `bg-accent`; ghost/gray contexts → `bg-wash`; surfaces → ring darkens; rows → `bg-subtle`.
  No translate, lift or scale on hover. Buttons may use `active:scale-[0.98]`.
- Menus and popovers ≈150ms (shadcn defaults). Sheets slide ≈250ms ease-out.
- Respect reduced motion (`motion-reduce:transition-none`, `motion-reduce:animate-none`).
- Drag and drop: the dragged item gets `shadow-float rotate-1`; the drop slot is a dashed outline with its radius.

## 14. Responsive behavior

- **Top nav < lg:** items move into a sheet opened by a menu icon button (full-width pills, black active).
- **Sidebar:** icon rail on medium screens, off-canvas sheet on mobile (shadcn `Sidebar` supports both).
- **< sm:** framed shell becomes edge-to-edge (no canvas padding, no shell radius), page padding `p-4`, title `text-3xl`,
  grids collapse to one column, wide rows of columns become `snap-x snap-mandatory` with `w-[85vw]` items,
  toolbars scroll with `no-scrollbar`.
- Search pill collapses to an icon button below `xl`.
- The page itself never scrolls horizontally; only wide content scrolls inside its own container.
- Touch targets ≥ 40px on touch layouts (`h-10` pills).

## 15. Accessibility

- `muted-foreground` is the lightest color allowed for readable text; `faint` only for placeholders and decoration.
- Every color signal has words, an icon or a shape.
- Icon-only buttons have `aria-label`; decorative icons and chips are `aria-hidden` when a text label is present.
- `aria-current="page"` on the active nav item; segmented controls use radiogroup semantics (or shadcn ToggleGroup).
- Progress uses `role="meter"` with value and label.
- One `h1` per page; group titles `h2`; surface titles `h3`. Landmarks: `header`, `nav`, `main`, `aside`.
- Focus always visible on keyboard: `focus-visible:ring-2 focus-visible:ring-foreground/20` (or shadcn's outline).
- Tables are real tables; menus, dialogs and sheets use shadcn primitives for keyboard support.

