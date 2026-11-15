# SOP: Review a change

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Accept a change on evidence, not on the word of the agent that wrote it.

## Scope

Every pull request before it is merged. Work on money, access or tenancy always gets this review.

## Who

An agent that did not write the change.

## Steps

1. Read the task's brief and its acceptance checks.
2. Read the whole diff.
3. Run the checks yourself on the pull request's latest commit.
4. Check the rules in [AGENTS.md](../../AGENTS.md): only owned files changed, each mini-app keeps to its own
   tables, nothing falls outside [STACK.md](../STACK.md), every new package is pinned with its licence recorded,
   and no secret is in the diff.
5. Check the reuse order: nothing is hand-written that the platform or a package in the stack already does, and
   nothing is written twice.
6. For money, access or tenancy, try one case that should fail and confirm that it does.
7. Give a verdict in the pull request, naming the commit you reviewed: accept, or list each objection with the
   check or evidence behind it.
8. Merge an accepted change. The agent that wrote it does not merge it.

## Exceptions

| Situation | What to do |
|---|---|
| You cannot run the checks | Say so. Do not accept |
| The change comes from an outside contributor | Read the whole diff first. Run its checks only in a sandbox that holds no credentials |
| You would have written it differently | That is not an objection. Raise only what a check or a rule supports |
| The same objection comes back a second time | Stop the loop and report to the parent or the owner |

## Done when

The pull request holds a verdict with its evidence and the commit it covers.
