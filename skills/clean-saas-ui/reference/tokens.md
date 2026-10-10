# Foundations and design tokens (§3–§4)

Read at project setup and for any color or token question.

## 3. Foundations

- **shadcn/ui** initialized per its installation guide for the project's framework. Base color Neutral or Stone;
  it does not change the result, because the §4 values replace the generated ones (not a decision, see
  `decisions/rules.md`). Add components only as screens need them.
- **Primitive library:** check which one the project uses (`npx shadcn info`, or `style` in `components.json`).
  Base UI composes triggers with `render={<Button />}`, Radix with `asChild`. Snippets below put classes directly on
  triggers so they work with either. Never mix the two APIs.
- **Typeface:** decision `typeface`: Geist + Geist Mono, or Inter. Loading differs per framework (§11); the
  token mapping in §4 works for all of them.
- **Icons:** the project's configured icon library (lucide by default). See §7.

---

## 4. Design tokens

Keep the CSS file shadcn generated (the one `components.json → tailwind.css` points to). Replace the light-theme values
in `:root` with these, add the extra tokens, and expose them in `@theme inline` (shadcn's convention: define in
`:root` / `.dark`, map in `@theme inline`). Hex is fine.

```css
:root {
  --radius: 0.625rem;              /* shadcn primitives; this style's own radii are named below */

  /* Surfaces, outermost -> innermost (use as many layers as a screen needs) */
  --canvas: #E5E5E1;               /* page behind a framed app shell */
  --background: #F4F4F2;           /* app background / shell */
  --panel: #EAEAE6;                /* working well that groups surfaces */
  --column: #F2F2EF;               /* nested well: columns, table header, grouped lists */
  --card: #FFFFFF;                 /* surfaces, pills, inputs */
  --subtle: #F8F8F6;               /* hovered rows, inner blocks */

  --foreground: #0A0A0A;
  --card-foreground: #0A0A0A;
  --popover: #FFFFFF;
  --popover-foreground: #0A0A0A;
  --primary: #0A0A0A;
  --primary-foreground: #FFFFFF;
  --secondary: #FFFFFF;
  --secondary-foreground: #0A0A0A;
  --muted: #EDEDEA;
  --muted-foreground: #6B6B66;     /* labels and meta; >= 4.5:1 on white and background */
  --faint: #A3A39E;                /* placeholder, disabled, decoration only */
  --accent: #F1F1EE;
  --accent-foreground: #0A0A0A;
  --destructive: #DC2626;
  --border: #E4E4E0;
  --input: #E4E4E0;
  --ring: #0A0A0A;

  /* Sidebar (only used if the product has one): match the tone it sits on */
  --sidebar: #F4F4F2;
  --sidebar-foreground: #0A0A0A;
  --sidebar-primary: #0A0A0A;
  --sidebar-primary-foreground: #FFFFFF;
  --sidebar-accent: rgb(0 0 0 / 0.05);
  --sidebar-accent-foreground: #0A0A0A;
  --sidebar-border: #E4E4E0;
  --sidebar-ring: #0A0A0A;

  /* Helpers (alpha-based so dark mode only needs new values) */
  --hairline: rgb(0 0 0 / 0.06);   /* 1px ring around white elements on gray */
  --wash: rgb(0 0 0 / 0.05);       /* hover fill for ghost controls */
  --track: rgb(0 0 0 / 0.10);      /* empty progress segments, connectors, timelines */

  /* Status: base = dots, bars, solid badges, icon chips | soft = tinted bg | strong = text/icon on soft */
  --success: #22C55E;  --success-soft: #DCFCE7;  --success-strong: #15803D;
  --warning: #EAB308;  --warning-soft: #FEF9C3;  --warning-strong: #A16207;
  --caution: #F97316;  --caution-soft: #FFEDD5;  --caution-strong: #C2410C;
  --danger:  #EF4444;  --danger-soft:  #FEE2E2;  --danger-strong:  #B91C1C;
  --info:    #3B82F6;  --info-soft:    #DBEAFE;  --info-strong:    #1D4ED8;

  /* Charts: monochrome first, then status hues */
  --chart-1: #0A0A0A;
  --chart-2: #8A8A85;
  --chart-3: #CFCFCA;
  --chart-4: #22C55E;
  --chart-5: #F97316;
}

@theme inline {
  /* add next to the shadcn-generated entries */
  --color-canvas: var(--canvas);
  --color-panel: var(--panel);
  --color-column: var(--column);
  --color-subtle: var(--subtle);
  --color-faint: var(--faint);
  --color-hairline: var(--hairline);
  --color-wash: var(--wash);
  --color-track: var(--track);

  --color-success: var(--success);
  --color-success-soft: var(--success-soft);
  --color-success-strong: var(--success-strong);
  --color-warning: var(--warning);
  --color-warning-soft: var(--warning-soft);
  --color-warning-strong: var(--warning-strong);
  --color-caution: var(--caution);
  --color-caution-soft: var(--caution-soft);
  --color-caution-strong: var(--caution-strong);
  --color-danger: var(--danger);
  --color-danger-soft: var(--danger-soft);
  --color-danger-strong: var(--danger-strong);
  --color-info: var(--info);
  --color-info-soft: var(--info-soft);
  --color-info-strong: var(--info-strong);

  /* Named radii for this style (independent of --radius) */
  --radius-shell: 28px;
  --radius-panel: 24px;
  --radius-column: 20px;
  --radius-card: 14px;
  --radius-inner: 10px;

  /* The only shadow: floating layers */
  --shadow-float: 0 12px 32px -8px rgb(0 0 0 / 0.18), 0 0 0 1px rgb(0 0 0 / 0.05);

  /* Works with next/font variables and with self-hosted / Google-hosted fonts */
  --font-sans: var(--font-geist-sans, "Geist Variable"), "Geist", ui-sans-serif, system-ui, sans-serif;
  --font-mono: var(--font-geist-mono, "Geist Mono Variable"), "Geist Mono", ui-monospace, monospace;
}

@utility no-scrollbar {
  scrollbar-width: none;
  &::-webkit-scrollbar { display: none; }
}

@layer base {
  body { @apply bg-background text-foreground antialiased; }
}
```

If `shell = framed`, put `bg-canvas` on the body and `bg-background` on the shell.

### Token usage map

| Token | Utility | Use for |
|---|---|---|
| canvas | `bg-canvas` | Page behind a framed shell |
| background | `bg-background` | App background, shell, sidebar |
| panel | `bg-panel` | Working well that groups many surfaces |
| column | `bg-column` | Nested wells, table header row, grouped lists |
| card | `bg-card` | Surfaces, pills, inputs, icon buttons |
| subtle | `bg-subtle` | Hovered rows, inner blocks |
| hairline | `ring-1 ring-hairline` | Edge of white elements on gray (instead of borders) |
| wash | `hover:bg-wash` | Hover on ghost controls and pills sitting on gray |
| track | `bg-track` | Empty progress segments, connectors, timelines, neutral icon chips |
| muted-foreground | `text-muted-foreground` | Labels, meta lines, axis ticks |
| faint | `text-faint` | Placeholder, disabled, decorative separators |
| primary | `bg-primary text-primary-foreground` | Primary action, active item, selection |
| status base | `bg-success` ... | Dots, progress bars, solid badges, icon chips |
| status soft + strong | `bg-success-soft text-success-strong` | Delta chips, soft badges, inline alerts |
| border | `border-border` | Dividers *inside* surfaces, tables and forms |

### Status tones

| Tone | Means |
|---|---|
| success | done, healthy, positive change, high score |
| warning | needs attention soon, medium score |
| caution | at risk, blocked, low score |
| danger | failed, rejected, overdue, negative change |
| info | in progress, waiting, neutral activity |
| neutral | draft, inactive, unknown |

Map the product's own statuses onto these six. Never introduce a seventh status color. Create, read, update and
delete chips reuse four of them (§7).

### Categorical palette

Category identity (types, groups, stages, teams, channels) is not status. Use the fixed sequence below, with a black
icon or text (`text-black`), the same in both themes. Its hues stay clear of the five status hues, so a category never
reads as a state or an operation; the mixed levels keep neighbors apart. Palette classes appear only here; everything
else uses tokens.

```ts
// palette.ts
export const CATEGORY = [
  "bg-violet-400 text-black",
  "bg-lime-400 text-black",
  "bg-pink-400 text-black",
  "bg-cyan-500 text-black",
  "bg-fuchsia-300 text-black",
  "bg-teal-300 text-black",
] as const

export const categoryColor = (index: number) => CATEGORY[index % CATEGORY.length]
```

- A category keeps the same hue everywhere in the app.
- Never give a category a status-family hue (`green`, `emerald`, `yellow`, `amber`, `orange`, `red`, `rose`, `blue`,
  `sky`, `indigo`): those read as a status or an operation.
- At most six categorical hues on one screen; beyond that, fall back to neutral chips.

