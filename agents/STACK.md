# Stack

ten98-os uses one stack, the same as Campaign, Discover and Books. Compliance is strict: nothing outside this table
enters the code base.

| Layer | Choice | Version today |
|---|---|---|
| Language | TypeScript, with full checking on | 7.0.2 |
| Runtime | Node | 24.22.1 or later, below 25 |
| Package manager | pnpm | 11.19.0 |
| Interface | React | 19.2.8 |
| Framework and router | TanStack Start and TanStack Router | 1.168.61 and 1.170.42 |
| Server | Nitro | 3.0.260903-beta |
| Build | Vite | 8.3.4 |
| Database | PostgreSQL, with row-level security forced | 18 |
| Data access | Drizzle, over `pg` | 0.45.2 and 8.23.0 |
| Sign-in | Better Auth | 1.7.7 |
| Validation | zod | 4.6.6 |
| Background jobs | pg-boss | 12.37.1 |
| Deployment | k3s | Not set yet |

The versions are the ones the existing apps pin on 15 November 2026. ten98-os moves with them.

## Rules

- There is one choice per layer. No second framework, router, data-access library, database, sign-in library,
  validation library, job queue or package manager.
- Every source file is checked TypeScript. Checking is never switched off for a file.
- Every table has row-level security forced, and the app connects as a role that does not own the tables.
- Every version is pinned exactly.
- An automated check enforces this table from the first commit of code. It fails the build when anything falls
  outside it.
- Only the owner changes this table, and the change is recorded on the wiki's Decisions page first.

## What still needs no change here

A package that is not a layer, such as a date library, a chart library or the sheet editor, comes in by
[sops/add-a-dependency.md](sops/add-a-dependency.md). It must not do the job of a layer.

## Examples of a breach

- A second framework or server, such as Next.js or Express.
- A second data-access library or database, such as Prisma, MongoDB or SQLite.
- A lockfile from npm, Yarn or Bun.
- A second validation or sign-in library.
- A JavaScript file, or a TypeScript file with checking disabled.
