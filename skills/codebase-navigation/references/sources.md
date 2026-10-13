# Selected sources

These are optional background for design decisions, checked on 2026-10-14.
They are not a required reading list or evidence of performance in another
project. Enterprise implementations, vendor evaluations, and research studies
have different scopes and limitations.

- **Stripe, 2026-02-19:** [Minions, part 2](https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents-part-2).
  Relevant practice: scope guidance to directories and task needs; share maintained
  rules rather than duplicate them across agent products. Its cloud/CI design is
  not a prerequisite for this skill.
- **Uber, 2026-08-27:** [Running a Software Factory Efficiently at Uber Scale](https://www.uber.com/gb/en/blog/efficient-software-factory/).
  Relevant practice: connect code with engineering ownership and existing context;
  measure wasted retrieval work. Do not copy its infrastructure scale or model
  selection policy into a small workspace.
- **Sourcegraph, 2026-07-31:** [How to evaluate Sourcegraph on your own codebase](https://sourcegraph.com/blog/how-to-evaluate-sourcegraph-on-your-own-codebase).
  Relevant distinction: retrieval, completion, and cost are separate outcomes;
  dispersed tasks differ from easy lookups. This is a vendor's own evaluation.
- **Gloaguen et al., 2026-09-29 revision:** [Evaluating AGENTS.md](https://arxiv.org/abs/2602.11988).
  Relevant caution: repository instructions do not universally improve task
  success; evaluate additional context rather than maximizing its size.
- **Qin and Xie, 2026-07-27:** [Agent Retrieval Bench](https://arxiv.org/abs/2607.24882).
  Relevant caution: no single evaluated retrieval family dominated all tasks.

Current tool references (version-dependent, not all introduced in 2026):

- [CodeGraph upstream](https://github.com/colbymchenry/codegraph)
- [Go gopls MCP](https://go.dev/gopls/features/mcp)
- [Codex hooks](https://learn.chatgpt.com/docs/hooks)
