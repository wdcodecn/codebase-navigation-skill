# Codebase Navigation Skill

A reusable agent skill for finding the right code and retaining useful project
context across tasks, from one repository to a multi-repository workspace.

[中文说明](README.zh-CN.md) · [Skill instructions](skills/codebase-navigation/SKILL.md)

## What it helps with

- Connect product language and symptoms to repositories, entry points, and owners.
- Trace cross-component boundaries and identify who decides a state.
- Choose exact search, structural indexes, language services, history, or runtime
  evidence according to the question.
- Reuse concise navigation in new sessions without loading an entire codebase.
- Design incremental, event-driven index maintenance that exits when finished.

The skill is tool-agnostic. CodeGraph and language services are optional adapters,
not prerequisites. It ships instructions and a map template, **not an installer,
indexing daemon, or preconfigured automatic updater**. When asked to set up
maintenance, the agent adapts it to the user's tools and verifies the behavior.

## Install

Copy `skills/codebase-navigation/` into a skill directory supported by your agent.
For Codex, one supported user location is `~/.codex/skills/`:

```sh
git clone https://github.com/wdcodecn/codebase-navigation-skill.git
mkdir -p ~/.codex/skills
cp -R codebase-navigation-skill/skills/codebase-navigation ~/.codex/skills/
```

If that skill already exists, compare versions before copying; do not overwrite
local adaptations blindly. Start a new session if your agent does not discover
new skills dynamically. Other agents may use a different skill directory or
metadata convention; follow their documented installation method. Agents without
skill discovery can be given the `SKILL.md` file directly.

## Use

Example request:

> Use $codebase-navigation to improve this workspace. Agents keep rediscovering
> the same code. Find the actual navigation gaps, reuse existing documentation,
> and make relevant context easy to find in future sessions. If indexing needs
> maintenance, use supported events and avoid an idle background service.

Narrower requests also work:

> Improve our cross-repository code map. Include responsibility and API boundaries,
> not just filenames. Keep this documentation-only.

> Our code index becomes stale after new features. Check the current tooling and
> configure bounded, incremental refresh if supported. Preserve unrelated projects.

Explicit task constraints take precedence. Using the skill does not authorize
publishing, production access, remote code uploads, new services, or CI changes.

## Contents

- `SKILL.md`: problem-driven navigation and setup workflow.
- `assets/CODE_MAP.template.md`: a selective map shape for verified project facts.
- `references/tool-adapters.md`: when different retrieval methods help.
- `references/event-driven-maintenance.md`: freshness, resource, and lifecycle requirements.
- `references/publishing-safely.md`: adapting private experience into public material.
- `references/sources.md`: selected 2026 practices and current tool documentation.

Paths above are relative to `skills/codebase-navigation/`. Supporting references
are loaded only when relevant. No private source, project index, execution log,
machine configuration, or personal filesystem path is distributed here.

## Limits

A map or graph cannot prove runtime behavior. Index coverage varies by language,
framework, generated code, and version. Semantic navigation still needs the agent
making a relevant change to maintain it. Hooks may need explicit host trust; their
presence does not mean they are active. No speed, accuracy, or memory improvement
is guaranteed without measurement in the target workspace.

This repository does not install packages, change an agent's configuration,
upload source, or start a service merely by being cloned or read.

## License

[MIT](LICENSE). External sources are linked for reference and retain their own licenses.
