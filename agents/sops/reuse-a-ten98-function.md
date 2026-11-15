# SOP: Reuse a function from a Ten98 app

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Copy code from the existing Ten98 apps when no library or API does the job and the code is shown to work, without
depending on their packages.

## Scope

Functions in [Campaign](https://github.com/Ten98-IO-Company/ten98-campaign),
[Discover](https://github.com/Ten98-IO-Company/ten98-discover),
[Books](https://github.com/Ten98-IO-Company/ten98-books) and the
[code-system](https://github.com/Ten98-IO-Company/ten98-code-system). They share the OS's core stack, so much of
their server code can carry over.

These apps are pre-release. Many of their flows do not work yet, and they fall short of their reference apps in
features and quality. Their code is not trusted as it stands.

Screens are rebuilt, not copied: the OS uses shadcn/ui and daisyUI in place of the design system. Server code
carries over with changes. Expect to change its tenant keys to the organisation, and its hand-written SQL to typed
queries.

## Who

The agent building the module that needs the function.

## Steps

1. Confirm that the earlier steps of the reuse order in [STACK.md](../STACK.md) found nothing: the platform, a
   package already in the stack, and a public library or a provider's API.
2. Search those repositories for a function that does the job.
3. Read it with its callers and its tests, at one commit.
4. Prove that it works before you copy it. Run its tests, and run the flow it belongs to end to end. Compare the
   result with the mini-app's reference app.
5. Copy the smallest complete piece: the function, what it needs, and its tests.
6. Adapt it to the OS: its records, the organisation as the unit that data is separated by, and its names.
7. Record the source in the pull request: the repository, the commit and the file path.
8. Run the copied tests in the OS, and add tests for what you changed.

## Exceptions

| Situation | What to do |
|---|---|
| The flow it belongs to does not work | Do not copy it. Build the flow against the reference app |
| It works but falls short of the reference app | Copy it and finish it to that standard, or write it new if that is quicker |
| You cannot run it to check | Treat it as unproven. Do not copy it |
| The function only wraps a library | Do not copy it. Use the library directly |
| The function leans on a large part of its package | Copy it only if the whole piece is small. Otherwise write it new |
| The code uses something outside [STACK.md](../STACK.md) | Rewrite that part on the stack. Do not bring the other tool in |
| The source has a known defect | Fix it in the OS and say so in the pull request |
| The file carries someone else's copyright notice | Keep that notice with the copied code |
| The code is not Ten98's own | Treat a package as a dependency, by [add-a-dependency](add-a-dependency.md). Code copied from another project keeps its licence notice in the file and is listed in the repository's notices file |
| The function handles sign-in, tenancy or money | Ask for a review by an agent that did not write it |

## Done when

The code is shown to work, it and its tests are in the OS, the pull request names the source, and nothing imports
`@ten98/runtime` or `@ten98/ui`.
