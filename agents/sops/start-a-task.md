# SOP: Start a task

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Begin every task the same way, so any agent can pick up any task.

## Scope

Every task, before any file is changed.

## Who

The agent taking the task.

## Steps

1. Read [AGENTS.md](../../AGENTS.md) and the task's issue. Write the goal in one sentence.
2. Read the wiki pages the task touches: Decisions first, then Structure and the page for the app.
3. Pick skills from [SKILLS.md](../SKILLS.md), three at most, and read each one.
4. Decide whether the task is a leaf, using the test in [HARNESS.md](../HARNESS.md).
5. For a leaf, create a branch for the task and follow the matching procedure. For anything larger, follow
   [split-and-delegate](split-and-delegate.md).
6. Write the plan as a short list in the issue.

## Exceptions

| Situation | What to do |
|---|---|
| The task conflicts with a decision | Stop and report. Do not change what is decided |
| The task needs a decision nobody has made | Ask the owner, then record the answer on the Decisions page |
| Another agent already holds the issue or branch | Do not start. Ask for a hand-off |

## Done when

The goal, the skills, leaf or split, and the plan are written in the issue.
