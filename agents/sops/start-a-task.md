# SOP: Start a task

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Begin every task the same way, so any agent can pick up any task.

## Scope

Every task, before any file is changed.

## Who

The agent taking the task.

## Steps

1. Read [AGENTS.md](../../AGENTS.md) and the task's issue.
2. Read the wiki pages the task touches: Decisions first, then Structure and the page for the app.
3. Question the request. Write its crux in one sentence: what it is really for. If a better version would serve
   that crux, plan that version, and say what you changed and why.
4. Pick skills from [SKILLS.md](../SKILLS.md), three at most, and read each one.
5. Decide whether the task is a leaf, using the test in [HARNESS.md](../HARNESS.md).
6. For a leaf, create a feature branch for the task and follow the matching procedure. For anything larger, follow
   [split-and-delegate](split-and-delegate.md).
7. Write the plan as a short list in the issue.

## Exceptions

| Situation | What to do |
|---|---|
| The task conflicts with a decision | Stop and report. Do not change what is decided |
| The best version differs a lot from what was asked | Do it, and put the difference first in your report, so it is easy to reverse |
| The task needs a decision nobody has made | Ask the owner, then record the answer on the Decisions page |
| The Decisions page already answers the question | Do not ask again. A decision is given once |
| Another agent already holds the issue or branch | Do not start. Ask for a hand-off |

## Done when

The crux, the skills, leaf or split, and the plan are written in the issue.
