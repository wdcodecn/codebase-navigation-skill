# Code navigation

Use this as a starting shape, not a required section list. Replace the illustrative
rows with verified entries for this workspace; omit sections that add no value.

## Checkout and ownership

| Repository / component | Role | Actual checkout or resolution rule |
| --- | --- | --- |
| `<repository>` | `<responsibility>` | `<how to select the intended checkout>` |

## Frequent questions

| User wording / aliases | Entry → implementation owner | State authority / relevant constraint |
| --- | --- | --- |
| `<feature or symptom>` | `<repo>:<path>#<symbol> → <owner>` | `<short distinction and owning source>` |

## Cross-component boundaries

| Flow | Producer / caller | Boundary identifier | Consumer / state owner |
| --- | --- | --- | --- |
| `<flow>` | `<repo>:<path>#<symbol>` | `<method + path, event, bridge action, or API>` | `<repo>:<path>#<symbol>` |

## Retrieval and freshness

Document only the tools actually available here, their project-selection rules,
and the fallback for missing or stale results. Keep normal lookups direct.

When an implementation changes a listed entry, owner, boundary, or constraint,
update that entry with the change. Use source symbols and maintained contracts;
avoid copying volatile runtime state or relying only on line numbers.
