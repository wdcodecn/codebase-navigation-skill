---
name: codebase-navigation
description: Set up or improve reusable codebase navigation when coding agents repeatedly rediscover files, ownership, and logic in large or multi-repository projects. Use for code maps, retrieval routing, and lightweight context/index maintenance.
---

# Codebase Navigation

Make the next task start near the right implementation, with enough context to
understand ownership and change impact. A successful result lets an agent connect
a user's symptom or feature request to the relevant repository, entry point,
state owner, callers, and constraints without repeating a broad investigation.

This skill works with a single repository, a monorepo, or several checkouts. It
does not require a particular editor, language, search product, or agent platform.

## Start from the actual bottleneck

Use the user's examples and existing navigation to distinguish:

- **Location:** the agent cannot connect product terminology to implementation.
- **Relationships:** it finds a symbol but misses callers, dispatch, or consumers.
- **Meaning:** it finds code but repeats work to establish state ownership,
  compatibility, or the reason a constraint exists.
- **Continuity:** useful knowledge or indexes stop matching later source changes.

Several can apply. Inspect the relevant existing map, rules, and tool capability
before choosing a remedy. Prefer improving a working source of truth over adding
a second one. A tool mentioned by the user is a candidate, not a mandatory center
of the design unless they explicitly require it.

Confirm the intended checkout for each affected repository. Do not infer it from
a similar directory name or mix an active worktree with another copy. Preserve
unrelated work. Distinguish setup authorization from publishing, installing new
services, uploading code, or modifying production systems.

## Connect the smallest useful set of facts

Extend the existing code map where one exists; otherwise use
[the map template](assets/CODE_MAP.template.md) selectively. Each useful entry
connects:

`user wording / symptom → repository → entry → owner → relevant boundary`

Include a short responsibility or distinction when it saves investigation: who
decides the state, which implementation is historical, which client consumes an
API, or where authorization is enforced. Link the current source or maintained
contract that supports it. Search aliases can bridge product vocabulary and code
identifiers, including across languages.

For cross-repository behavior, record the actual boundary identifier, such as an
HTTP method/path, message name, bridge action, or package API. Trace both sides
where the task requires it. A source graph inside one repository does not prove
that a runtime request reaches the expected consumer.

Keep the map selective. Do not generate a second copy of the whole source tree,
API specification, or business logic. Stable ownership and constraints belong
near their owner; environment state belongs in current configuration or runtime
evidence. Use history or an existing decision record when the question needs the
reason for a behavior, not as a mandatory preflight for every edit.

## Route retrieval by the question

| Evidence available | Useful next move |
| --- | --- |
| Exact path or known owner | Open the relevant current source. |
| URL, error text, event, or exact identifier | Scoped lexical search, such as `rg -n -F`, then inspect the match in context. |
| Product terminology without a code identifier | Map aliases first; use existing semantic search if it can narrow the candidates. |
| Unknown callers, dependencies, or change impact | A current structural index or language service. |
| Overloaded symbol, interface, generated type, or ambiguous reference | Type-aware language tooling where supported. |
| Behavior contradicts static code | The appropriate existing runtime evidence, within authorized access. |
| A regression depends on an earlier change | Focused history for the identified owner, such as `git log -S`. |

Read [tool adapters](references/tool-adapters.md) only when selecting or repairing
a retrieval tool. Inspect installed schemas/help: similarly named graph tools and
different versions do not share one API. Read current source before editing when
an index may be stale or omit a required detail. Empty results are not proof that
there are no callers, routes, or consumers.

Stop expanding once the entry, owner, required neighbors, and constraints are
clear enough for the task. Return focused paths, symbols, and reasons instead of
whole-file dumps. Do not route every request through an expensive investigation.

## Make new sessions benefit

Add a short pointer in each affected repository's agent entrypoint to its useful
navigation and owning references. Check discovery from the directories people
actually use, including repository roots and supported worktrees. Keep the
default context small; load topic details only when relevant.

If automatic maintenance is requested, follow
[event-driven maintenance](references/event-driven-maintenance.md). Distinguish
deterministic source-index refresh from semantic navigation updates:

- An index can track changed source automatically using a verified tool.
- The implementing agent updates a map or contract when it changes a recorded
  entry, owner, boundary, or invariant. An indexer cannot infer product meaning
  reliably merely from a file change.

Do not claim that a rule saying “remember to update” is executable automation.
Use supported lifecycle integration when needed, explain its coverage, and verify
it. A shell command, skill install, or hook file existing on disk does not prove
that a future session will run it.

## Check useful behavior, then finish

Use a small sample of real navigation questions that includes a simple lookup,
a dispersed flow, and a failure or ambiguous reference where applicable. With
read-only probes, check whether the approach finds the correct checkout, owner,
required consumers, and relevant constraint. Record missed edges or stale entries
and fix those within scope. This is a navigation check, not a requirement to add
CI or a product test suite.

Measure latency or memory only when making those claims. Separate retrieval
quality, task completion, and cost; an upstream benchmark does not establish
local results. For a script or hook, verify its operational behavior and failure
handling as described in the maintenance reference.

Report the useful entrypoint, changed setup, verification, and any remaining
activation or coverage limits. Preserve the distinction between configured,
manually exercised, automatically observed, committed, and published.

When preparing this skill's outputs for public sharing, read
[publishing safely](references/publishing-safely.md). For the research behind the
approach, consult [selected sources](references/sources.md), not a mandatory
reading list for each task.
