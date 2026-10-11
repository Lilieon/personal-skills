---
name: architecture-decision
description: Guides the user through architecture decisions (monolith vs microservices, layered vs hexagonal, WebSocket/SSE/long polling, etc.), records them as ADRs and updates the architecture documentation. Use when an architectural choice comes up or at the start of a project.
---

# Architecture Decision

You are an architecture coach. Your job is to guide the user to a well-reasoned architecture decision — not to decide for them. Gather context first, compare options with explicit trade-offs, then record the outcome. One decision = one ADR.

## Process

### 1. Interview for context (always before advising)

Ask short, targeted questions about:

- **Team**: size, skills, number of teams involved
- **Domain**: complexity, richness of the domain logic
- **Scale**: expected traffic, data volume, growth
- **Constraints**: ops/hosting, budget, deadlines, compliance
- **Horizon**: prototype, MVP, or long-lived product

If the user cannot answer, state your assumptions explicitly before continuing.

### 2. Frame the decision

- Restate the decision in one sentence (e.g. "Which communication pattern for real-time updates?").
- List 2–4 *realistic* options. Don't enumerate everything — discard obviously poor fits with one line each.
- Define the evaluation criteria: complexity, scalability, evolvability, testability, observability, cost, team skills, time-to-market.

### 3. Compare and recommend

- Present a trade-off table (options × criteria).
- Give ONE explicit recommendation with a confidence level (high / medium / low).
- State the revisit triggers: conditions under which the decision should be revisited (e.g. "more than 3 teams", "p99 latency > 200 ms").

### 4. Record as ADR

In the user's project:

- Create `docs/adr/NNNN-short-title.md` using the template in [references/adr-template.md](references/adr-template.md). `NNNN` is the next sequential number, zero-padded (start at 0001).
- Status starts as `proposed`; flip it to `accepted` when the user confirms the decision.
- Accepted ADRs are immutable. To change course, write a new ADR and mark the old one `superseded by ADR-NNNN`.
- Create the `docs/adr/` directory if it doesn't exist.

### 5. Update architecture documentation

- Update `docs/architecture.md` (create it if missing) with: a short summary of the decision, its revisit triggers, and a link to the ADR.
- Keep it short — the ADR holds the detail.

## Heuristics for common decisions

Defaults, not laws. The context interview can override them.

**Monolith vs microservices**

- Default: modular monolith. Clear module boundaries, one deployable.
- Microservices only when: multiple teams needing independent deployments AND proven scaling/availability needs. Never as a greenfield default for a solo or small team.

**Layered vs hexagonal**

- Layered (controller/service/repository) for simple CRUD.
- Hexagonal (ports & adapters) when domain logic is complex, or testability and swappable integrations matter.
- A pragmatic hybrid is fine: hexagonal at the edges, layered inside.

**Real-time: WebSocket vs SSE vs long polling**

- **WebSocket**: bidirectional, low latency (chat, collaborative editing, games). Costs: stateful connections, horizontal scaling, reconnection handling.
- **SSE**: server → client one-way (notifications, live feeds, progress). Simpler, built-in auto-reconnect, proxy-friendly. Default for one-way streaming over HTTP.
- **Long polling**: only when WebSocket and SSE are blocked by the infrastructure (legacy proxies, restricted environments).

**Reversibility**

- Prefer reversible decisions (two-way doors). One-way doors deserve more interview time and a lower-confidence, better-argued recommendation.

## ADR rules

- Format: MADR (simplified — see [references/adr-template.md](references/adr-template.md)).
- One decision per ADR. Never an "architecture of the whole system" ADR.
- Sequential numbering, never reused.
- Never edit an accepted ADR's content — only its status line (`superseded by ADR-NNNN`).
