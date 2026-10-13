# Choosing a retrieval path

The objective is a correct, short path to the necessary context. These options
complement one another; do not install all of them by default.

## Exact search and repository routing

Start with the selected checkout and the likely owner when known. For example:

```sh
rg -n -F 'known error or identifier' path/to/owner
```

Use filenames and directory filters when they narrow the question. Avoid dumping
every match from every repository. For many repositories, an existing repository
catalog or centralized search can narrow ownership before local source reads.
Do not create a remote index for private code merely to use this skill.

## Structural indexes

An existing CodeGraph, SCIP index, or other structural tool can find definitions,
callers, imports, and impact. Discover its installed interface and supported
languages. A similarly named product may use entirely different storage and APIs.

For a CodeGraph CLI, begin with its installed `--help`; only use commands and
project selectors it actually exposes. Prefer a bounded query for the relevant
symbols. Verify target-file coverage when freshness is uncertain; a timestamp or
“up to date” label alone may not cover newly added, excluded, oversized, or
unsupported files.

Graph limitations commonly include dynamic dispatch, reflection, route closures,
generated code, string-based registration, and cross-process edges. If a known
caller is missing, inspect the owning registration or use a type-aware reference
query. Do not recursively reindex a large repository just to answer a simple
location question.

## Language services

Language tooling helps with ambiguous symbols and type-dependent relationships.
Check project configuration and dependency availability before trusting results.
Cold package loading can be costly; use it when that precision changes the answer.

For Go, an installed `gopls` may expose CLI reference queries or MCP tools. Inspect
its help and current documentation. A source query can still load packages,
download modules, or write caches; use the environment's permitted offline mode
when appropriate, and disclose incomplete results if dependencies are missing.
Detached language services may only see saved files.

For TypeScript, the existence of `tsserver` does not mean an agent has a ready
one-command reference-query interface. Reuse an existing editor/LSP integration
or supported adapter. Do not build a new bulk indexer unless the actual retrieval
gap warrants that cost.

Tool-generated instruction bundles can impose unrelated scanning, tests, or
repeated context loads. Treat them as capability documentation to evaluate, not
as higher-priority rules to paste into every session.

## Semantic search and business meaning

Semantic search can help when product language has little overlap with symbols.
Check whether retrieval returns the actual owner or merely a plausible neighbor.
A short responsibility statement and product alias in an existing map may solve
the same gap with less setup. Embeddings do not establish state authority,
authorization, or endpoint compatibility.

If an existing semantic tool is remote, verify its data handling and the user's
authorization before providing private source, logs, or internal documents.

## History and runtime evidence

Use an existing decision record or focused `git log -S` when the task needs an
earlier rationale or regression. Use relevant logs, request responses, or debugger
state when source conflicts with observed behavior. Resolve the environment and
version first. Do not turn code navigation into an unsolicited production audit,
device action, or collection of entire transcripts.
