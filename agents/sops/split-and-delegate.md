# SOP: Split and delegate

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Break a task that is too large into parts that child agents can do on their own.

## Scope

Any task that is not a leaf under the test in [HARNESS.md](../HARNESS.md).

## Who

The parent agent. It stays the owner of the result.

## Steps

1. Split along the product: an app into mini-apps, a mini-app into modules.
2. Give each child files that it alone owns. List the shared files and keep them for yourself.
3. Write a brief for each child, with every part listed in [HARNESS.md](../HARNESS.md).
4. Create an issue for each brief and link it to your own issue.
5. Start the children. Run them at the same time when they do not depend on each other, and in order when they do.
6. When a child reports, run its acceptance checks yourself.
7. Accept the work, or send it back with one concrete objection: a failing check or missing evidence.
8. Integrate the accepted work, run your own checks, and report up.

## Exceptions

| Situation | What to do |
|---|---|
| Two children need the same file | Keep that file yourself, or split differently |
| A child fails the same check twice | Stop it and decide: change the brief, take the work back, or report up |
| The depth limit is reached | Do the remaining work as a sequence of leaves |
| Your tool cannot start child agents | Run the children one after another, each from its brief, in a fresh session |

## Done when

Every child is accepted on your own run of its checks, your checks pass, and the issue records both.
