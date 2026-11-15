# SOP: Add a dependency

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Add a public package without bringing in a licence problem or an unmaintained library.

## Scope

Any package installed into ten98-os.

## Who

The agent that needs the package.

## Steps

1. Confirm that no package already installed, and no core service, does the job.
2. Check [STACK.md](../STACK.md). The package must not do the job of a stack layer.
3. Check the licence. MIT, Apache-2.0 and BSD are fine. Anything else follows the exceptions below.
4. Check that the package is maintained.
5. Pin the exact version.
6. Record the package, its version, its licence and the reason in the pull request.
7. Keep the package's notice where its licence asks for one.

## Exceptions

| Situation | What to do |
|---|---|
| The package is a second choice for a stack layer | Do not install it. Only the owner changes the stack |
| The licence is GPL, AGPL or another copyleft licence | Do not install it. Study it as a reference only |
| The licence is commercial or source-available | Ask the owner. Univer's licensed version is already approved |
| The package calls an outside provider | Put it behind the core's connection for that kind of provider |
| The thing is a server, not a library | It runs as its own part of the deployment, not as a dependency |

## Done when

The version is pinned, the licence is recorded in the pull request, and the checks pass.
