# Decision index

The control panel of this skill: every decision it knows, with scope, type and trigger. Read it on every UI task
(gate step 2). To make the agent ask more or less, change a row's **type** here; nothing else needs to change.

- **Scope:** `project` (once per app) · `entity` (once per kind of record: invoice, customer, ticket ...) ·
  `screen` (once per route or view).
- **Type:** `ask` (ask the user, then record) · `infer` (derive from the criteria, record, list in the summary).
- **Trigger:** when the decision becomes relevant. A decision is open only when the task hits its trigger, its
  condition holds, and it is not in the ledger yet.
- Options, recommendation logic and look-ups are in the file named in the last column.
- Anything not listed here is either a rule (`rules.md`, never asked) or content that comes from the user.

## Project

| id | type | trigger | condition | file |
|---|---|---|---|---|
| `shell` | ask | first UI task | – | project.md |
| `nav` | ask | first UI task | – | project.md |
| `sidebar-placement` | ask | first UI task | `shell = framed` and `nav` has a sidebar | project.md |
| `sidebar-behavior` | ask | first UI task | `nav` has a sidebar | project.md |
| `chrome` | ask | first UI task | – | project.md |
| `typeface` | ask | first UI task | – | project.md |
| `density` | ask | first UI task | – | project.md |
| `dark-mode` | ask | first UI task | – | project.md |
| `wayfinding` | ask | first detail or nested page | – | project.md |
| `content-domain` | ask | first UI task | no real product content in the request or the codebase | project.md |
| `state-location` | infer | first filter or view switch | – | project.md |

## Entity

| id | type | trigger | condition | file |
|---|---|---|---|---|
| `detail-view` | ask | the entity's details are first shown or opened | – | entity.md |
| `create-edit` | ask | the entity's first create or edit flow | – | entity.md |
| `lead` | ask | the entity is first shown as a card, row or tile | – | entity.md |
| `status-map` | ask | the entity's status is first shown | the entity has statuses | entity.md |
| `card-content` | ask | the entity is first shown as a card | – | entity.md |
| `metric-direction` | infer | a metric is first scored, charted or given a delta | – | entity.md |
| `category-hue` | infer | a category is first shown with color | – | entity.md |
| `icon` | infer | the entity first gets an icon or icon chip | – | entity.md |

## Screen

| id | type | trigger | condition | file |
|---|---|---|---|---|
| `constraints` | ask | the request states a constraint that can be read two ways | – | screen.md |
| `pattern` | ask | new screen | – | screen.md |
| `header` | ask | new screen | – | screen.md |
| `kpis` | ask | new screen | `pattern` has KPI tiles | screen.md |
| `chart` | ask | new screen | `pattern` has a chart | screen.md |
| `table` | ask | new screen | `pattern` has a table | screen.md |
| `events` | ask | new screen | `pattern` shows events over time | screen.md |
| `filters` | ask | new screen | the screen has a toolbar or filters | screen.md |
| `wells` | infer | new screen | – | screen.md |
| `screen-density` | infer | new screen | – | screen.md |
| `group-headers` | infer | new screen | the screen groups items into columns or sections | screen.md |

## Order of questions

1. `constraints`, if any (they can change everything else).
2. Project decisions, in table order.
3. Entity decisions, per entity in the order the screen shows them.
4. Screen decisions: `pattern` and `header` first, then the ones `pattern` unlocks.

Decisions unlocked by an answer go into the next round.
