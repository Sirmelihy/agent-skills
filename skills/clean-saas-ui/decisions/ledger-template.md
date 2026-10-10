# Ledger template

Copy the first block to `design-decisions.md` at the root of the project being built. The second block shows a
filled ledger for reference; do not copy it.

- `choice` holds the option id from the decision's entry (`framed`, `sheet`) or, for content decisions, a short
  value (`amount`, `paid=success · overdue=danger`).
- `source`: `user` (answered a question) · `prompt` (stated in a request) · `default` (the user let the agent
  choose) · `inferred` (derived by the agent from the criteria).
- Dates are ISO (`YYYY-MM-DD`).

## Template

````markdown
# Design decisions

<!--
Managed by the clean-saas-ui skill. Agents: read this before building or changing UI, and do not ask again
about anything recorded here. Rows with source user, prompt or default change only when the user asks;
inferred rows may be re-derived when the content changes. Replaced values move to History.
-->

## Project

| id | choice | source | date | note |
|---|---|---|---|---|

## Entities

## Screens

## History
````

## Example

````markdown
# Design decisions

## Project

| id | choice | source | date | note |
|---|---|---|---|---|
| nav | sidebar | prompt | 2026-10-02 | "sidebar koy" |
| shell | framed | user | 2026-10-02 | |
| sidebar-placement | outside | user | 2026-10-02 | |
| sidebar-behavior | fixed | default | 2026-10-02 | |
| chrome | search, notifications | user | 2026-10-02 | |
| typeface | geist | default | 2026-10-02 | |
| density | comfortable | user | 2026-10-03 | |
| dark-mode | none | user | 2026-10-02 | |
| operation-colors | archive=neutral · approve=success | user | 2026-10-04 | |

## Entities

### invoice

| id | choice | source | date | note |
|---|---|---|---|---|
| lead | amount | user | 2026-10-02 | |
| status-map | paid=success · pending=info · overdue=danger · draft=neutral | user | 2026-10-02 | |
| detail-view | sheet | user | 2026-10-03 | |
| metric-direction | days-overdue=higher-worse | inferred | 2026-10-03 | |

## Screens

### /dashboard

| id | choice | source | date | note |
|---|---|---|---|---|
| constraints | no card grid; KPI tiles and chart surfaces allowed | user | 2026-10-02 | "card yok" |
| pattern | KPI row · revenue chart · recent invoices table | user | 2026-10-02 | |
| header | summary: outstanding, overdue · period control 7d/30d/90d · no primary | user | 2026-10-02 | |
| wells | none | inferred | 2026-10-02 | 3 surfaces |

## History

- 2026-10-03 · project.density: compact → comfortable (user)
````
