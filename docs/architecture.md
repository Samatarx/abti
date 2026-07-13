# Architecture

Abti is intentionally small. It is not an application, service, dashboard, or data pipeline. It is a coding-assistant skill that adds a learning debrief at the right moment.

```text
Developer
↓
Coding assistant
↓
Abti
↓
Learning debrief
```

## Where Abti sits

Abti sits after implementation, close to PR time.

During implementation, the developer needs momentum: code changes, debugging help, tests, refactors, and explanations that directly support the task. A learning debrief during that phase can become noise.

At PR time, the developer is already switching from building to explaining. That is the right moment to ask:

- What changed?
- What did I practise?
- What did the AI assistant solve?
- What should I be able to explain before merging?

## Why after implementation

AI-assisted coding can blur the line between work the developer actively reasoned through and work the assistant generated. Abti does not try to measure that. Instead, it creates a short pause after the work is done so the developer can inspect the implementation and leave with clearer understanding.

This keeps the coding assistant focused during active work and makes the learning debrief feel useful rather than intrusive.

## What Abti uses

Abti uses only the current session context available to the coding assistant. That may include:

- The current conversation.
- A visible diff or summary.
- Files discussed in the session.
- Tests, errors, or debugging steps mentioned in the session.
- The PR summary or commit message the developer is preparing.

Abti should not invent context. If there is not enough information, it should ask for a diff, PR summary, files changed, or a short task summary.

## What Abti produces

Abti produces a concise markdown learning debrief with:

- What the developer practised.
- What the AI assistant helped with.
- What the developer should understand before merging.
- A few quick questions.
- Things to double-check.
- One follow-up exercise.
- Learning tags.

The learning debrief is meant to be read in about a minute.
