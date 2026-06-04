# GPT_PROPOSAL.md

## Status

Author: GPT
Phase: Independent architecture proposal
Role status: Candidate only, not assigned

This proposal is written after the repository protocol layer has been created.
It does not claim permanent leadership or execution ownership.

## 1. Project Understanding

`oracle-agent` should become a multi-agent coordination and execution system where different AI systems can cooperate through explicit repository state instead of relying on hidden chat memory.

The repository should serve as the shared external memory, negotiation surface, task board, architecture record, and eventually the implementation base.

The first goal is not to build code quickly.
The first goal is to prevent uncontrolled multi-agent drift.

## 2. Core Architecture Principle

The system should be protocol-first, repository-centered, and role-emergent.

Meaning:

1. Protocol comes before hierarchy.
2. GitHub files are the shared memory layer.
3. Agents must leave written artifacts.
4. Roles should emerge from demonstrated capability.
5. Execution begins only after written consensus.

## 3. Proposed System Layers

### Layer 0: Founder Authority

The founder keeps final control over strategy, credentials, deployment, irreversible actions, and final role assignment.

Agents can recommend and negotiate, but cannot override founder authority.

### Layer 1: Protocol Layer

Files:

- `AGENTS.md`
- `DISPATCH.md`
- `GOVERNANCE/HANDOFF_PROTOCOL.md`
- `GOVERNANCE/ROLE_NEGOTIATION.md`

Purpose:

- define entry rules,
- prevent silent overwrites,
- prevent premature hierarchy,
- require handoff notes,
- externalize memory.

### Layer 2: Proposal Layer

Files:

- `ARCHITECTURE/GPT_PROPOSAL.md`
- `ARCHITECTURE/CLAUDE_PROPOSAL.md`
- `ARCHITECTURE/GEMINI_REVIEW.md`
- `ARCHITECTURE/CODEX_EXECUTION_ANALYSIS.md`
- `ARCHITECTURE/COMPARISON.md`

Purpose:

- collect independent architecture views,
- expose disagreements,
- compare suitability,
- form consensus topology.

### Layer 3: Decision Memory Layer

Suggested files:

- `MEMORY/PROJECT_CONTEXT.md`
- `MEMORY/DECISIONS.md`
- `MEMORY/OPEN_QUESTIONS.md`

Purpose:

- preserve durable context,
- record final decisions,
- prevent repeated debates,
- make future agents self-orienting.

### Layer 4: Dispatch Layer

Suggested files:

- `TASKS/BACKLOG.md`
- `TASKS/ACTIVE.md`
- `TASKS/DONE.md`
- `TASKS/BLOCKED.md`

Purpose:

- convert architecture into concrete tasks,
- avoid duplicate work,
- expose blockers,
- define handoff points.

### Layer 5: Implementation Layer

Suggested directories:

- `src/`
- `tests/`
- `docs/`
- `scripts/`

Implementation should begin only after consensus.

## 4. Candidate Agent Roles

These are candidate roles, not final assignments.

### GPT Candidate Strengths

GPT may be strong at:

- system architecture,
- strategy framing,
- protocol design,
- synthesis across agents,
- translating founder intent into structured documents,
- maintaining high-level coherence.

GPT may be weaker at:

- long autonomous coding sessions,
- direct local environment execution,
- deeply persistent repo state without explicit reads,
- guaranteeing first-pass production code correctness.

### Claude Candidate Strengths

Claude may be strong at:

- long-form reasoning,
- critique,
- alternative architecture generation,
- catching implicit assumptions,
- writing clear design documents,
- cautious safety and maintainability review.

Claude may be weaker at:

- over-expanding conceptual scope,
- drifting into explanation instead of execution,
- assuming context not actually present,
- producing implementation without strict task boundaries.

### Gemini Candidate Strengths

Gemini may be useful for:

- external review,
- broad comparison,
- second-opinion validation,
- multimodal or ecosystem-level checks.

Gemini may be weaker as a primary coordinator unless its repository write behavior is proven stable.

### Codex Candidate Strengths

Codex may be strong at:

- implementation planning,
- code generation,
- refactoring,
- test creation,
- repository execution,
- turning specifications into working code.

Codex may be weaker at:

- high-level philosophical alignment,
- founder-intent interpretation,
- multi-agent governance design,
- resisting premature implementation without clear dispatch.

## 5. Proposed Collaboration Flow

### Phase 0: Protocol and Proposal

1. GPT writes protocol layer.
2. GPT writes independent proposal.
3. Claude writes independent proposal.
4. Gemini reviews both.
5. Codex analyzes execution feasibility.
6. Comparison document is created.
7. Founder reviews and approves topology.

### Phase 1: Consensus Topology

Output:

- `ARCHITECTURE/COMPARISON.md`
- `GOVERNANCE/ROLES.md`
- `SPEC/SYSTEM_SPEC.md`

### Phase 2: Task Decomposition

Output:

- `TASKS/BACKLOG.md`
- `TASKS/ACTIVE.md`
- `SPEC/TASK_BREAKDOWN.md`

### Phase 3: Implementation

Output:

- code under `src/`,
- tests under `tests/`,
- docs under `docs/`,
- changelog or decision records.

## 6. Suggested Governance Rules

1. Any agent may propose.
2. Any agent may critique.
3. No agent may silently overwrite another agent's proposal.
4. Implementation requires a dispatch item.
5. Major decisions require a decision record.
6. Credentials and deployment remain founder-controlled.
7. The repository is the memory source of truth.

## 7. Risks

### Risk 1: Premature Execution

Agents may begin coding before agreement.

Mitigation:

- keep `DISPATCH.md` explicit,
- block `src/` work until consensus.

### Risk 2: Role Ego Drift

Agents may assume status based on brand or initial contribution.

Mitigation:

- require role negotiation,
- evaluate based on artifact quality.

### Risk 3: Context Fragmentation

Different agents may rely on different chat histories.

Mitigation:

- repository files must be treated as shared memory,
- important reasoning must be written down.

### Risk 4: Over-Architecture

The system may spend too long designing and never execute.

Mitigation:

- after proposals and comparison, force a small MVP scope.

## 8. Recommended MVP Direction

After consensus, the first executable MVP should be small:

1. repository-based agent protocol,
2. task queue markdown files,
3. decision log,
4. one simple agent loop design,
5. testable CLI or script only after system specification is accepted.

Avoid building a complex platform too early.

## 9. Proposed Next Step

Claude should now write:

`ARCHITECTURE/CLAUDE_PROPOSAL.md`

Claude should directly challenge this proposal, especially on:

- whether repository-centered memory is sufficient,
- whether role emergence is practical,
- whether markdown dispatch is enough,
- where GPT's architecture may be too abstract,
- what execution topology would reduce drift fastest.

## 10. Closing Position

GPT's position is that `oracle-agent` should begin as a disciplined coordination substrate, not as an immediate coding project.

The correct first product is not code.
The correct first product is reliable multi-agent alignment.
