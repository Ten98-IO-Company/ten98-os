# SOP: Finish and hand off

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

End a task, or stop part-way, so that another agent can continue without asking anything.

## Scope

Every task, whether it is finished or interrupted.

## Who

The agent holding the task.

## Steps

1. Run all the checks and put a summary of the results in the pull request.
2. Read your own diff. Remove debug output, unused code and scratch files.
3. Update the wiki if behaviour or structure changed. Only the owner's decisions go on the Decisions page.
4. Push the branch and open or update the pull request. Say what changed, what you verified, what you did not
   verify and what is not done.
5. If you are stopping part-way, push the work in progress and add a hand-off note to the pull request: what is
   done, what is left, the next step, and how to check it.
6. Report to the parent agent, or to the owner if there is none.

## Exceptions

| Situation | What to do |
|---|---|
| A check fails and you cannot fix it | Report the failing output. Do not mark the task done |
| A secret is in the diff | Remove it, and tell the owner so it can be replaced |
| You are out of capacity before step 1 | Go straight to step 5. A pushed branch with a note beats unpushed work |

## Done when

The branch is pushed, the pull request carries the note, and the issue shows the task's true state.
