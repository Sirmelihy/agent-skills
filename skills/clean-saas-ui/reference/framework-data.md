# Framework and data (§11–§12)

Framework specifics, mock data and formatting.

## 11. Framework notes

The design language is framework-independent; only these details change.

| Concern | Vite / SPA | Next.js App Router | Other (React Router framework mode, Remix, Astro islands) |
|---|---|---|---|
| CSS entry | `src/index.css` (per `components.json`) | `app/globals.css` | per `components.json` |
| Fonts | `@fontsource-variable/geist` + `@fontsource-variable/geist-mono` imported in the entry, or Google Fonts | `next/font` (exposes `--font-geist-sans` / `--font-geist-mono`) | self-host or Google Fonts |
| Links | router's `Link` / `NavLink` | `next/link` | router's link |
| Active nav state | `NavLink` `isActive` (React Router), `activeProps` (TanStack Router) | `usePathname()` | router's match API |
| Rendering | client only | server components by default | SSR + hydration |

- The `--font-sans` / `--font-mono` tokens (§4) fall back from the Next.js font variables to the self-hosted family
  names, so the same CSS works everywhere.
- Navigation items take the router's link component and the classes from §9.2; always set `aria-current="page"` on
  the active item.
- **SSR frameworks:** rendering must be deterministic (§12) to avoid hydration mismatches.
- **Next.js App Router:** keep client components as leaves; pass only serializable props across the server → client
  boundary (no functions, no icon components; import such config inside the client component); page `searchParams`
  is a Promise (`await searchParams`); wrap components using `useSearchParams` in `<Suspense>`.
- Filter and view state belongs in the URL when the router supports it; local state is fine for mocks
  (decision `state-location`).

---

## 12. Data and content

The design only looks finished with believable content, whatever the domain.

- **The lead element** of each entity (decision `lead`): the one number or title a user scans for.
- **Statuses mapped** onto the six tones (§4) before writing UI (decision `status-map`).
- **Deterministic data.** No `Math.random()`, `Date.now()` or argument-less `new Date()` during render. Write literal
  data, or generate it at module level with a seeded PRNG:

```ts
// seed.ts
export function mulberry32(seed: number) {
  return () => {
    seed = (seed + 0x6d2b79f5) | 0
    let t = Math.imul(seed ^ (seed >>> 15), 1 | seed)
    t = (t + Math.imul(t ^ (t >>> 7), 61 | t)) ^ t
    return ((t ^ (t >>> 14)) >>> 0) / 4294967296
  }
}
```

- **A fixed reference date** (`export const TODAY = "YYYY-MM-DD"`) for every relative state in mock data.
- **Fixed locale and time zone** in formatters (stable output across server, client and screenshots):

```ts
// format.ts
const day = new Intl.DateTimeFormat("en-US", { month: "short", day: "numeric", timeZone: "UTC" })
const compact = new Intl.NumberFormat("en-US", { notation: "compact", maximumFractionDigits: 2 })

export const formatDay = (iso: string) => day.format(new Date(`${iso}T00:00:00Z`))
export const formatCompact = (n: number) => compact.format(n)
export const formatMoney = (n: number, currency = "USD") =>
  new Intl.NumberFormat("en-US", { style: "currency", currency, notation: "compact", maximumFractionDigits: 2 }).format(n)
```

- **Totals add up.** Summaries equal the sum of what they summarize; group counts ≥ visible items.
- **Varied, unround values.** Spread scores and amounts, mix tones, make one group visibly busier than the others.
- **Coherent copy.** Status texts fit their state; names are diverse and realistic; IDs follow one pattern.
- **Fictional organizations**, no real logos, no lorem ipsum, no "John Doe" / "Test", never `undefined` / `NaN` on screen.
- **Demo states:** one selected item, one empty state, one long title that truncates.

