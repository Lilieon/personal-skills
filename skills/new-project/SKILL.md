---
name: new-project
description: Scaffolds and initializes a new project — git init, stack bootstrap via its standard tooling, README, docs/ structure, AGENTS.md, and the first ADRs (stack choice + architecture decisions via the architecture-decision skill). Use when starting a new project from scratch.
---

# New Project

Initialize a new project: git repository, stack bootstrap, documentation skeleton, and the first recorded decisions. Keep the scaffold minimal — ask before creating anything, and use the stack's official tooling instead of hand-rolling structure.

## Principles

- Ask before creating anything.
- Minimal scaffold: no structure nobody asked for.
- Always prefer the stack's official tooling over manual setup.
- Granular, conventional commits (`chore:`, `feat:`, `docs:`, …).

## Process

### 1. Interview

Ask short questions and stop as soon as you have enough:

- Project name
- Type: application / API / library / CLI / other
- Language and stack (framework, package manager)
- Target directory: create `./<name>/` — unless the user is already inside the intended directory

### 2. Git

- `git init -b main` in the project directory.
- Check `git config user.name` and `user.email`; ask the user for values if missing.
- Write a minimal `.gitignore` adapted to the chosen stack — standard patterns only (build output, dependencies, editor/OS noise). Nothing speculative.

### 3. Stack bootstrap

If a stack is chosen, initialize it with its official tool inside the project directory:

- Node: `npm init -y`
- Rust: `cargo new` (or `cargo init` if the directory already exists)
- Go: `go mod init <module>`
- .NET: `dotnet new`
- PHP: `composer init`

Add nothing beyond what the tool generates.

### 4. Documentation

- `README.md` skeleton at root: title, one-line description, prerequisites, install, usage — placeholders to fill.
- `AGENTS.md` at root: copy from [references/agents-template.md](references/agents-template.md) and adapt it — fill the commands table with the stack's real build/test/lint commands and the actual project layout.
- `docs/adr/` is created in the next step, with the first ADR.

### 5. Architecture decisions

- If the `architecture-decision` skill is available, load it and follow its process. If not installed, say so and apply a minimal fallback: interview context, compare options with explicit trade-offs, record the outcome as a MADR-style ADR.
- Always record **ADR 0001 — choice of stack** in `docs/adr/0001-choice-of-stack.md` (MADR format): options considered, why this stack, revisit triggers.
- If other architecture decisions come up during initialization (e.g. monolith vs microservices, realtime pattern), record them as subsequent ADRs (0002, 0003, …). Those decisions also create/update `docs/architecture.md`, as defined by the architecture-decision skill.

### 6. Commits

Granular, conventional:

1. `chore: initialize project` — git artifacts, `.gitignore`, stack bootstrap
2. `docs: add README, AGENTS.md and ADRs` — documentation and recorded decisions
