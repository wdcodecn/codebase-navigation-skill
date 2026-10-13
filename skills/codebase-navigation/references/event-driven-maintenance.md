# Keeping context current without an idle service

Use this reference when the user asks for automatic freshness, particularly on
resource-constrained machines. It describes an implementation contract, not a
universal installer. Generate only the adapter the actual environment needs.

## Separate source facts from semantic knowledge

Source indexes can be updated deterministically. Navigation entries contain
meaning: product aliases, ownership, state authority, and important boundaries.
The agent changing those concepts should update their existing map/contract in
the same task. Do not regenerate every document or summarize every chat on each
turn. Do not claim semantic maintenance is guaranteed by source indexing.

## Choose supported events

Possible events include starting or resuming a task, finishing a task, switching
a checkout, or explicitly querying a stale index. Choose a small set supported by
the actual host. A low-cost fingerprint check at turn end is often sufficient;
syncing after every file read or tool call is usually unnecessary.

If no suitable lifecycle integration exists, provide an explicit on-demand
command and state that freshness is manual. Do not silently substitute a daemon,
timer, login service, or recurring agent task.

## A bounded foreground design

The following is pseudocode, not an executable hook:

```text
on an allowed lifecycle event:
    resolve the configured checkout roots
    return immediately if the current task is outside their scope
    acquire one nonblocking maintenance lock
    for each relevant checkout, within the event's time budget:
        verify its actual Git root and source-index location
        compute a cheap source-change fingerprint
        skip if it matches the last successfully indexed fingerprint
        run the installed tool's supported incremental refresh
        verify refresh completed rather than merely skipped a busy index
        compare the source fingerprint again
        save success atomically only if source did not change during refresh
    release the lock and exit
```

Configure roots; do not hard-code a username, repository count, operating-system
install prefix, or one developer's package bundle. Resolve the executable from a
verified configured path or the environment. Prefer a supported CLI or public
API; isolate version-sensitive code behind a small adapter with a clear failure.

### Fingerprints and invalidation

Account for changed revision/checkout, tracked modifications, deletions, renames,
and relevant untracked files. A design based only on `HEAD` misses uncommitted
work; a design based only on the names in `git status` misses repeated edits to
an already-dirty file. Include suitable file metadata or content fingerprints
for candidate source files, and include index/parser configuration changes.

Use the indexer's actual supported inputs/exclusions instead of assuming every
extension is indexed. Consider index replacement/version changes. Avoid hashing
every source file on every event. If source changes while refreshing, leave it
pending for a later event instead of recording a false clean state.

### Resource and failure behavior

- Serialize refreshes across simultaneous sessions that share an index. Use a
  platform-appropriate lock that releases on process exit; a lock file's mere
  existence must not permanently block maintenance after a crash.
- Bound event time and child-process time. Terminate only children owned by the
  maintenance invocation on timeout, never every process with the tool's name.
- Keep logs bounded and limited to status/diagnostics; do not store raw source,
  credentials, chat text, or full tool payloads by default.
- Avoid implicit downloads, tool upgrades, telemetry, or remote indexing. Check
  the tool's actual options rather than inventing environment variables.
- Do not report a skipped or failed update as successful. Keep stale state
  visible and retain a direct-source fallback; avoid endless retry loops.
- Reuse an existing index. Treat a missing index or expensive initial rebuild as
  a separate setup decision instead of doing it on every session start.
- A runtime heap limit is not a cap on total process RSS, native allocations,
  child processes, or filesystem cache. Measure the quantity being claimed.

When replacing persistent indexing, verify configuration scope and inherited
settings. Disabling a watcher may still leave an MCP server per session. An
on-demand CLI can avoid that residency where it offers the needed queries.
Do not break unrelated projects or terminate other active sessions. State whether
existing sessions need to restart for a configuration change to take effect.

## Codex adapter, when applicable

Consult the [current hook documentation](https://learn.chatgpt.com/docs/hooks)
and the installed host before generating configuration. As documented when this
skill was authored, Codex supports command hooks such as `SessionStart` and
`Stop`, with JSON input on stdin. `Stop` requires JSON output on success.
Synchronous execution avoids adding an asynchronous maintenance worker.

Discover hooks from the directories people actually open. Project configuration
inheritance and nested Git roots matter. Verify effective settings rather than
assuming a workspace-level file applies identically to every child repository.

New or changed unmanaged hooks require host trust. Do not fabricate trust hashes,
disable trust checks, or claim a hook is active merely because its definition is
present. Prepare and manually validate the artifact first, then use the supported
trust flow. Report each relevant source's actual configured/trusted/observed
state; trust in one source may not cover another.

Agent/editor products use different events and output contracts. Adapt to their
documented lifecycle rather than copying a Codex hook into another product and
promising equivalent behavior.

## Verification proportional to the change

For a new helper, exercise useful operational cases in an isolated fixture or
another explicitly suitable scope: no changes, source change, added/deleted
source, repeated edit of a dirty file, concurrent invocation, missing tool/index,
out-of-scope checkout, and failure/timeout as relevant. Do not modify real
business code just to create a freshness probe. Follow the user's validation
constraints; this does not require a product regression suite or CI integration.

Then inspect the host's effective configuration and hook discovery/trust state.
Where possible, observe a real lifecycle invocation and confirm child processes
exit. Keep manual invocation and automatically observed execution distinct.
