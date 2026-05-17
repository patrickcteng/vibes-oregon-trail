# `.agents/`

Project-level agent and Claude Code config: commands, hooks, settings, scripts.

`.claude/` at the repo root is a symlink to this directory so tools expecting the conventional `.claude/...` path still resolve correctly. Write new config here directly (e.g. `.agents/commands/foo.md`, `.agents/settings.json`) — do not write through the `.claude` symlink as if it were the source of truth.

See [`AGENTS.md`](../AGENTS.md) for repo-wide agent guidance.
