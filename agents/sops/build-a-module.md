# SOP: Build a module

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Build one module inside one mini-app, to the rules of the OS.

## Scope

Leaf tasks only. Nothing imports the code-system or design-system packages.

## Who

The agent that owns the module's files.

## Steps

1. Find the module on the wiki's Structure page and read its mini-app's page.
2. Do not reinvent the wheel. Follow the reuse order in [STACK.md](../STACK.md): the platform, a package already
   in the stack, a public library or a provider's API by [add-a-dependency](add-a-dependency.md), then code from a
   Ten98 app by [reuse-a-ten98-function](reuse-a-ten98-function.md). Write new code only for what is left.
3. Keep the module's data in its own mini-app's tables. Reach any other data through the core or the mini-app that
   owns it.
4. Declare what the module adds, once: its records for views, the events it emits, the actions it offers, and its
   permissions. Derive the rest from that declaration.
5. Build the screen from the OS's shared components, which come from shadcn/ui and daisyUI. Add a missing one to the
   OS's shared components, not inside the mini-app.
6. Ask the core for anything outside: a browser, a provider, an AI model, files, mail.
7. Write the tests with the code and run the checks.
8. Finish by [finish-and-hand-off](finish-and-hand-off.md).

## Exceptions

| Situation | What to do |
|---|---|
| The work needs a change in another mini-app | Do not edit it. Open a task for its owner |
| A rule in `AGENTS.md` blocks the obvious build | Stop and ask. Do not work around the rule |
| The module touches money, access or tenancy | Ask for a review by an agent that did not write it |

## Done when

The checks pass, the mini-app's declaration lists the module, and nothing outside the owned files has changed.
