# SOP: Reuse a function from a Ten98 app

**Owner:** Ten98 | **Last updated:** 15 November 2026 | **Review:** when development starts

## Purpose

Copy working code from the existing Ten98 apps when no library or API does the job, without depending on their
packages.

## Scope

Functions in [Campaign](https://github.com/Ten98-IO-Company/ten98-campaign),
[Discover](https://github.com/Ten98-IO-Company/ten98-discover),
[Books](https://github.com/Ten98-IO-Company/ten98-books) and the
[code-system](https://github.com/Ten98-IO-Company/ten98-code-system). They share the OS's stack, so their code
carries over.

Interface components are not copied from the design system. The OS uses shadcn/ui and daisyUI.

## Who

The agent building the module that needs the function.

## Steps

1. Confirm that the earlier steps of the reuse order in [STACK.md](../STACK.md) found nothing: the platform, a
   package already in the stack, and a public library or a provider's API.
2. Search those repositories for a function that already does the job.
3. Read it with its callers and its tests, at one commit.
4. Copy the smallest complete piece: the function, what it needs, and its tests.
5. Adapt it to the OS: its records, its organisation as the tenant, and its names.
6. Record the source in the pull request: the repository, the commit and the file path.
7. Run the copied tests in the OS, and add tests for what you changed.

## Exceptions

| Situation | What to do |
|---|---|
| The function only wraps a library | Do not copy it. Use the library directly |
| The function leans on a large part of its package | Copy it only if the whole piece is small. Otherwise write it new |
| The code uses something outside [STACK.md](../STACK.md) | Rewrite that part on the stack. Do not bring the other tool in |
| The source has a known defect | Fix it in the OS and say so in the pull request |
| The file carries someone else's copyright notice | Keep that notice with the copied code |
| The code is not Ten98's own | Treat it as a dependency, by [add-a-dependency](add-a-dependency.md) |
| The function handles sign-in, tenancy or money | Ask for a review by an agent that did not write it |

## Done when

The code and its tests are in the OS, the pull request names the source, and nothing imports `@ten98/runtime` or
`@ten98/ui`.
