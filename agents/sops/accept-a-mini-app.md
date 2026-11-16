# SOP: Accept a mini-app

**Owner:** Ten98 | **Last updated:** 16 November 2026 | **Review:** when development starts

## Purpose

Decide that a mini-app is done by testing it end to end, without waiting for the owner.

## Scope

Every mini-app, after its modules are merged. The same loop runs for everything built so far at each checkpoint of
the roadmap.

## Who

A tester agent that did not write the mini-app. The parent agent runs the loop.

## Steps

1. Before the mini-app is built, the parent writes its acceptance list in the issue: what a person can do when it is
   done, and what must be refused. The list is drawn from the mini-app's reference app, which sets the bar for
   features and quality.
2. Build the release image from the merged code and start a fresh deployment from it. Do not test a working copy.
3. Test every item on the list end to end, through the screens and through the API, as a person would use it.
4. Test what must fail: another organisation's records, a missing permission, a repeated request and wrong input.
   For money, check the figures to the minor unit.
5. Write a report in the issue: each item, pass or fail, with the evidence, and anything that looked wrong but was
   not on the list.
6. Send each failure to the agent that owns the files. When it is fixed, test the whole list again, not only the
   item that failed.
7. The mini-app is done when the whole list passes on a fresh deployment.

## Exceptions

| Situation | What to do |
|---|---|
| A test needs an environment setting, a key, an account or a domain | Ask the owner for it. Carry on with the items that do not need it |
| The same item fails twice after a fix | Stop the loop and report to the owner, with both reports |
| An item cannot be tested | Say so. The mini-app is not done |
| A test would spend money, send a real message or use live credentials | Do not run it. Use the provider's test mode, or ask the owner |
| The list is wrong or incomplete | Propose the change to the parent. Do not change the list yourself |

## Done when

The whole list passes on a fresh deployment, and the report is in the issue.
