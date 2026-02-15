# AgentPreso Skill Repo

This is the **public distribution repo** for the AgentPreso agent skill and CLI install pointer. It lives at `github.com/agentpreso/agentpreso`.

The actual product source code is in a private monorepo. Do not look for application code here.

## Repo structure

- `skills/<name>/SKILL.md` — Agent skill files with YAML frontmatter (name, description). The SKILL.md is loaded into agent context when the skill is activated.
- `commands/` — Slash commands, one file per command. These are invoked by agents as `/<command-name>`.
- `references/` — Detailed reference docs loaded on demand by agents. Keep these thorough but not loaded by default.
- `examples/` — Valid AgentPreso markdown files that demonstrate themes, layouts, charts, and diagrams.

## Rules

- **Do not add binaries** to this repo. CLI binaries are built in CI and hosted on R2 at agentpreso.com.
- **Skill files must be concise.** SKILL.md is always loaded into context — use progressive disclosure to push detail into `references/`.
- **Examples must be valid.** Every `.md` file in `examples/` should be a renderable AgentPreso deck.
- **Keep the README user-facing.** It serves as the GitHub landing page for developers and AI agent users.
