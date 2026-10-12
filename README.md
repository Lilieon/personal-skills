# personal-skills

A collection of reusable agent skills — versioned, and easy to share across tools (Kilo, Claude Code, and any Agent Skills–compatible assistant).

## Skills

| Name | Description |
|------|-------------|
| [architecture-decision](skills/architecture-decision/) | Guides through architecture decisions (monolith vs microservices, layered vs hexagonal, WebSocket/SSE/long polling…), records them as ADRs and keeps the architecture documentation up to date. |
| [new-project](skills/new-project/) | Scaffolds and initializes a new project: git init, stack bootstrap via its standard tooling, README, docs/, AGENTS.md, and the first ADRs (stack choice + architecture decisions). |

## Conventions

- Each skill lives in `skills/<name>/SKILL.md` with YAML frontmatter: `name` and a one-line `description`.
- Supporting files sit next to the skill (e.g. `references/`).

## Install

Copy or symlink the skill folder into your tool's skills directory:

- **Kilo** (global): `~/.config/kilo/skills/<name>` — or per project: `<project>/.kilo/skills/<name>`
- **Claude Code**: `~/.claude/skills/<name>` — or per project: `<project>/.claude/skills/<name>`
- Any other Agent Skills–compatible tool: its equivalent skills folder.

## License

[MIT](LICENSE)
