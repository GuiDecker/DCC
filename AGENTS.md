# DCC: how to work with this plugin

DCC gives you engineering skills (`skills/`) and specialist subagents (`agents/`, named `dcc:<name>`).

- Before non-trivial work, check whether a DCC skill fits the task and follow it. Useful defaults:
  - planning a feature or refactor: `plan-orchestrate`, subagent `dcc:planner`
  - writing code: `tdd-workflow` (tests first), `coding-standards`
  - finishing a change: `verification-loop`, subagent `dcc:code-reviewer`
  - anything touching auth, secrets, input handling or PII: `security-review`, subagent `dcc:security-reviewer`
  - splitting work across several agents or sessions: `team-agent-orchestration`, `dev-team`, `parallel-execution-optimizer`
  - ambiguous decisions and tradeoffs: `council`
- The `orch-*` skills (`orch-add-feature`, `orch-fix-defect`, `orch-change-feature`, `orch-refine-code`) run an end-to-end pipeline for one task.
- Subagents load only in local Devin (CLI and Desktop). In cloud sessions, apply the matching skill yourself.
- Skills were written for Claude Code. When a skill mentions Claude-only tools (`Agent(...)`, `~/.claude/...`, slash commands, hooks), use the closest Devin equivalent and keep the method.
- Prefer the user's project rules over DCC defaults when they conflict.
