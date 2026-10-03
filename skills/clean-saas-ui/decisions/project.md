# Project decisions

Made once per app, recorded under `## Project` in the ledger. Every entry lists the options (the ids are what the
ledger records), how to compute the recommended option, and where the look is defined.

---

## `shell` · App shell

How the app sits on the page.

- `framed`: body on `bg-canvas`; the app on `bg-background` inside a `rounded-shell` frame with `sm:p-3 lg:p-5`
  around it. Edge-to-edge below `sm`.
- `full-bleed`: body on `bg-background`, no frame.

**Recommend:** `framed` when `nav = top` (the pill nav reads best inside a frame); `full-bleed` otherwise.
**Unlocks:** `sidebar-placement`. **Look:** §9.1, §4 (note under the token block), §14.

## `nav` · Navigation model

- `top`: pill top navigation. Fits up to ~7 flat sections. Moves into a sheet below `lg`.
- `sidebar`: 240–264px sidebar. Fits many sections, hierarchy or frequent switching. Icon rail at `md`, off-canvas
  sheet on mobile.
- `both`: sidebar for the sections, plus a top bar for global utilities (`chrome`) or a second navigation level.

**Recommend:** count the top-level sections: ≤ 7 and flat → `top`; otherwise `sidebar`.
**Unlocks:** `sidebar-placement`, `sidebar-behavior`. **Look:** §9.2, §5 (navigation → title spacing), §14.

## `sidebar-placement` · Sidebar and the frame

Only when `shell = framed` and `nav` has a sidebar.

- `outside`: the sidebar sits on `bg-canvas` (sidebar tokens set to the canvas tone); only the content area is
  framed and floats beside it.
- `inside`: the frame holds sidebar and content; the sidebar takes the shell tone (`bg-background`), with a
  `border-r` only if a seam is needed.

**Recommend:** `outside`. **Look:** §9.2 (sidebar background), §4 (sidebar tokens).

## `sidebar-behavior` · Sidebar collapsing

Only when `nav` has a sidebar.

- `fixed`: expanded from `lg`, icon rail at `md`, off-canvas below. No user toggle.
- `collapsible`: the same, plus a toggle that collapses it to the 64px icon rail on desktop (remembered per viewer).

**Recommend:** `fixed` for up to ~10 items; `collapsible` beyond. **Look:** §9.2, §14.

## `chrome` · Global utilities

Which app-wide utilities the frame carries. Multi-select; record the selected ids, or `none`.

- `search`: search pill (`h-11`) with a ⌘K hint; becomes an icon button below `xl`.
- `notifications`: icon button with an unread dot; the list follows §9.15.
- `workspace-switcher`: in the sidebar header or footer; left of the account pill with `nav = top`.
- `help`: icon button.

**Recommend:** `search` + `notifications`; add `workspace-switcher` only for multi-tenant products.
Where the account pill goes is a rule, not part of this decision (`rules.md`). **Look:** §9.2, §9.15, §14.

## `typeface` · Typeface

- `geist`: Geist + Geist Mono.
- `inter`: Inter, with Geist Mono for IDs and codes.

**Recommend:** `geist`. **Look:** §3, §6, §11 (font loading).

## `density` · Default density

- `comfortable`: the spacing in §5.
- `compact`: surfaces `p-3`, table rows `h-12`. Text sizes never shrink.

**Recommend:** `comfortable`; `compact` for tools where users scan many rows all day (operations, monitoring,
finance back office). Single screens can still differ (`screen-density`). **Look:** §10.8.

## `dark-mode` · Dark mode

- `none`: light theme only.
- `system`: follows the operating system.
- `toggle`: follows the system by default, with a light / dark / system switch in the account menu.

**Recommend:** `none`, unless the request or the product calls for it. **Look:** §16.

## `wayfinding` · Getting back from detail pages

- `back`: a ghost `icon-sm` back button above the page title.
- `breadcrumbs`: breadcrumbs above the title.

**Recommend:** `back` when detail pages are one level deep; `breadcrumbs` from two levels on. **Look:** §9.2, §9.3.

## `content-domain` · Domain for mock content

Only when neither the request nor the codebase gives product content.

Offer 2–3 coherent domains that fit the request's wording (for example: B2B invoicing, support desk, hiring
pipeline), each in a few words. **Recommend:** the one closest to the request. **Look:** §12.

## `state-location` · Where filter and view state lives (infer)

- `url`: search params, when the router supports it and the screen is meant to be real.
- `local`: component state, for mocks.

**Infer:** `url` for real apps with a router, `local` for mocks. **Look:** §11.
