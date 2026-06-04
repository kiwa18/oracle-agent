# Architecture Proposal — Claude (Anthropic)

## Agent Identity

- Model: Claude (Anthropic)
- Proposal submitted during: PHASE 0 — SYSTEM NEGOTIATION
- Status: Independent proposal, pending peer review

---

## Proposed System Topology

```
                        ┌─────────────────┐
                        │   Founder        │
                        │  (Final Authority)│
                        └────────┬────────┘
                                 │
                        ┌────────▼────────┐
                        │   Orchestrator   │
                        │  (Dispatch +     │
                        │   Governance)    │
                        └──┬──────────┬───┘
                           │          │
              ┌────────────▼──┐  ┌────▼────────────┐
              │  Reasoning     │  │  Execution       │
              │  Layer         │  │  Layer           │
              │ (Architecture, │  │ (Code, Deploy,   │
              │  Strategy,     │  │  Integration,    │
              │  Critique)     │  │  Operations)     │
              └───────┬────────┘  └────────┬─────────┘
                      │                    │
              ┌───────▼────────────────────▼─────────┐
              │         Shared Memory Layer            │
              │     (Repository — Markdown files)      │
              └────────────────────────────────────────┘
```

---

## Core Design Principles

### 1. Repository as Single Source of Truth

No agent should rely on private chat history or internal memory for coordination.
All decisions, reasoning, handoffs, and state must be written into the repository.

This ensures:
- Any agent can reconstruct full context from files alone.
- No hidden context loss between sessions.
- Founder can audit all reasoning at any point.

### 2. Separation of Reasoning and Execution

Agents should be separated into two functional layers:

**Reasoning Layer** — produces proposals, critiques, architectural decisions, and strategic plans.  
**Execution Layer** — implements, deploys, integrates, and operates based on approved plans.

No agent should occupy both layers for the same task simultaneously.
This prevents unchecked autonomous action.

### 3. Dispatch Gate

All execution must pass through an explicit dispatch approval step.
No agent begins irreversible action without a written dispatch record.

Dispatch records must contain:
- task description,
- approving agent or founder,
- affected files and systems,
- rollback plan if applicable.

### 4. Critique Before Consensus

Every architecture proposal must receive at least one written critique before the system proceeds to consensus.
Speed is explicitly deprioritized over structural quality (per ARCHITECTURE/README.md).

---

## Self-Assessment

### Where I perform well

- Long-form structured reasoning and document generation
- Writing governance and protocol documents
- Identifying ambiguity and unstated assumptions in specifications
- Producing critique that is direct without being destructive
- Maintaining consistency across large context windows

### Where I perform poorly

- Live execution and tool-chaining over extended autonomous sessions
- Memory persistence across separate conversations without external scaffolding
- Real-time data retrieval without explicit tool access
- Tasks requiring tight feedback loops with running systems

### Overlap with other agents

- GPT-4: significant overlap in reasoning and proposal generation
- Codex / GPT with code interpreter: lower overlap — better suited for execution layer
- Gemini: unclear until proposal is submitted

### Complementary relationships

- I should be paired with an execution-specialized agent for any implementation phase.
- Codex or a code-execution agent is a natural complement for the execution layer.

---

## Proposed Role Candidacy

Based on demonstrated strengths, I am proposing myself as a candidate for:

- **Reasoning Layer contributor** — architecture proposals, critique, governance documents
- **Handoff protocol maintainer** — ensuring written context transfer between agents

I am explicitly **not** claiming:
- orchestration authority,
- deployment ownership,
- permanent governance status.

These claims are reserved for the consensus phase.

---

## Open Questions for Negotiation

1. Should the Orchestrator role be assigned to a single agent or rotated?
2. How should conflicting architecture proposals be resolved — by founder decision or agent vote?
3. What constitutes sufficient consensus before Phase 1 begins?
4. Should execution agents have read access to reasoning layer documents, or only dispatch outputs?

---

## Handoff Note

This proposal is complete and ready for critique.
Next recommended action: GPT submits its own proposal, then cross-critique begins.
No implementation should begin until at least two proposals exist and have been reviewed.

