# HANDOFF_PROTOCOL.md

## Purpose

This document defines how agents transfer work between each other.

The goal is continuity without hidden context loss.

## Handoff Requirements

Every handoff must contain:

1. current objective,
2. completed work,
3. unresolved uncertainty,
4. next recommended action,
5. known risks,
6. affected files.

## Handoff Rules

- Never assume another agent has hidden memory.
- Never rely on chat history outside the repository.
- Important reasoning must be written into files.
- Long-term context must be externalized into markdown.

## Principle

The repository is the shared memory layer.
Not the chat window.
