---
name: clean-saas-ui
description: Decision-driven visual design language for clean, modern SaaS product UI on shadcn/ui + Tailwind v4, in any React setup (Vite, Next.js, React Router, TanStack). Before building, it asks the user the structural and product decisions the task needs (app shell, navigation, detail views, screen patterns, ...), records them in design-decisions.md at the project root and never asks a recorded one again. Look - tonal gray layers instead of shadows, white rounded surfaces, pill controls, black accents, color only for meaning, round tinted icon chips. Use when building or restyling any app interface, or when asked for a clean / minimal / shadcn-style / Linear-style look.
---

# Clean SaaS UI

A **decision-driven** design language. The look is fixed by rules. Every structural or product choice is made by
the user once, written to a ledger, and reused from then on.

Paths are relative to this file's directory, except `design-decisions.md` (the **ledger**), which lives at the root
of the project being built.

## 0. Decision gate (mandatory, before any UI code)

Run the gate every time a task creates or changes UI, before writing code.

1. **Read the ledger.** Open `design-decisions.md` at the project root. If it does not exist, create it from
   `decisions/ledger-template.md`. If the project already has UI but no ledger, adopt it first (below).
2. **Read the index.** `decisions/index.md` lists every decision with its scope, type (`ask` / `infer`) and trigger.
3. **Take what the request already says.** A decision the request states ("put a sidebar", "open invoices in a
   side panel") is recorded with source `prompt` and not asked. A stated constraint that can be read two ways
   ("no cards": KPI tiles too?) becomes the `constraints` question.
4. **Find the open decisions:** those whose trigger this task hits and whose condition holds, minus those already
   in the ledger. Rules (`decisions/rules.md`) are never decisions.
5. **Ask the open `ask` decisions** (see Asking). Take each one's options and recommendation logic from
   `decisions/project.md`, `entity.md` or `screen.md`. Wait for the answers.
6. **Infer the open `infer` decisions** from their criteria. Do not ask about them.
7. **Record everything** in the ledger: choice, source, date, a short note when useful.
8. **Show a short summary** (3–8 lines) of the decisions this task uses, marking inferred ones, then build.
   Do not wait for confirmation of inferred decisions; the user can override any of them later.

### Asking

- Use the host's structured question tool when there is one (Claude Code: `AskUserQuestion`, at most 4 questions
  per call, 2–4 options each). Otherwise ask in chat as a short numbered list and wait.
- Ask in the user's language. One decision per question. The recommended option comes first, marked
  "(Recommended)", and every option says in a few words what it changes on screen.
- Go in rounds, in the order given in `decisions/index.md`. Decisions unlocked by an answer (e.g.
  `sidebar-placement` after `shell = framed` and `nav = sidebar`) go into the next round.
- Never ask a decision that is in the ledger, that the request already answers, or that is a rule.
- If the user answers "you decide" for a question, or says up front not to ask, take the recommended options,
  record them with source `default`, and list them in the summary.

### Recording

- Sources: `user` (answered a question) · `prompt` (stated in a request) · `default` (the user let the agent
  choose) · `inferred` (derived by the agent from the criteria).
- `user`, `prompt` and `default` rows change only when the user asks. `inferred` rows may be re-derived when the
  content changes; say so in the summary.
- When a request contradicts a recorded decision, the request wins: update the row, move the old value to
  `## History`, name the existing screens that no longer match, and offer to update them.
- Entity decisions (an invoice's detail view, a customer's lead number) apply on every screen that shows the entity.

### Adopting an existing UI

When the project already has screens but no ledger, read the layout and a few screens and fill in the decisions the
code already shows (shell, navigation, typeface, detail views, lead elements, status mapping). Present them in one
question ("The code shows: framed shell, sidebar, Geist, invoices open in a sheet. Record these?"). Confirmed rows
get source `user`; the rest are asked as usual.

---

## 1. Character

Calm, neutral, tactile, precise. The interface steps back so the content and its meaning step forward.

- **Quiet base, loud meaning.** Nearly everything is off-white, light gray or near-black. Saturated color appears only
  where it tells the user something.
- **Soft geometry.** Controls are pills and circles; containers have generous, concentric rounded corners. Nothing is sharp.
- **Depth by tone.** Layers are distinguished by slightly different grays, not by shadows or heavy borders.
- **Black as accent.** The strongest emphasis is solid near-black: the primary action, the active item, the selection.
- **Dense but breathable.** A lot of information per screen, organized by spacing and grouping rather than lines.
- **Small delights.** Round tinted icon chips, segmented progress bars, overlapping chips, mono IDs, tabular numbers.

## 2. Principles

1. **Depth from tone, not shadow.** Each layer is a few percent lighter than the one beneath it. Shadows exist only on
   floating layers (menus, popovers, dialogs, sheets, toasts).
2. **Neutral by default; color = meaning.** If removing a color loses no information, remove it. No decorative
   gradients, tinted section backgrounds or colored headers.
3. **Black is the accent.** Primary action, active navigation item, active segment, selected outline: near-black.
4. **Soft geometry.** Interactive controls are `rounded-full`; containers follow the radius scale (§5).
5. **Lead with one thing.** Every card, tile or row has one element that wins (a title or a number). Everything else
   supports it.
6. **Quiet labels, loud values.** Labels small and gray; values dark and medium/semibold. Never the reverse.
7. **Space over lines.** Group with spacing and tone before reaching for borders. When in doubt, add space.
8. **Few sizes, few weights.** About eight text sizes in total; weights 400 / 500 / 600 only.
9. **Never color alone.** Every color signal also carries text, an icon or a shape.
10. **Believable content.** Real-feeling data and copy are part of the design (§12).

---

## 3. Where things are

| File | Read when |
|---|---|
| `decisions/index.md` | Every UI task (gate step 2) |
| `decisions/project.md` · `entity.md` · `screen.md` | A decision of that scope is open |
| `decisions/rules.md` | Unsure whether something is a decision |
| `decisions/ledger-template.md` | Creating the ledger |
| `reference/tokens.md` (§3–§4) | Project setup; any color or token question |
| `reference/shape-type-icons.md` (§5–§7) | Every UI task |
| `reference/primitives.md` (§8) | Project setup; adding a shadcn component |
| `reference/layout-navigation.md` (§9.1–§9.6) | Shell, wells, navigation, page header, buttons, segmented controls, filters |
| `reference/cards-status.md` (§9.7–§9.11) | Cards, group headers, scores and progress, status, meta blocks |
| `reference/data-display.md` (§9.12–§9.15) | KPI tiles, charts, tables, lists and activity |
| `reference/forms-overlays-states.md` (§9.16–§9.18) | Forms and settings, overlays, empty / loading / error |
| `reference/composition.md` (§10) | Planning a screen |
| `reference/framework-data.md` (§11–§12) | Framework specifics, mock data, formatting |
| `reference/motion-responsive-a11y.md` (§13–§15) | Motion, the responsive pass, the accessibility pass |
| `reference/dark-mode.md` (§16) | Only when `dark-mode` is not `none` |
| `qa.md` (§17, §19) | Before calling a screen done |

Section numbers (§) are stable across files: "§9.10" means the file that holds section 9.10.

- The catalog (§9) says how an element looks when a screen uses it. Never add an element because it is listed there.
- Code snippets are reference implementations of a look. Adapt names, structure and props to the project; their
  placeholder text is never content.
- Stack: shadcn/ui + Tailwind v4 in any React setup; framework specifics are in §11. For component APIs and CLI
  usage, follow the installed shadcn components (and the official shadcn skill, `npx skills add shadcn/ui`, if
  present). For visual decisions, this skill wins.

## 4. Workflow

1. **Decision gate** (§0).
2. **Foundations once per project:** tokens (§4), fonts per `typeface` (§11), primitive restyles (§8) for the
   primitives in use, `dark-mode` (§16) if not `none`.
3. **Data and types** (§12), following the entity decisions: `lead`, `status-map`, `category-hue`.
4. **Build screens** per the screen decisions, looking up each element's look in the reference as you use it.
5. **Responsive pass** (§14), **accessibility pass** (§15).
6. **Build and lint**; fix type and rendering errors.
7. **QA** (`qa.md`) in the browser at several widths; fix and re-check. The ledger matches what was built.
