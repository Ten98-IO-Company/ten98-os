# Stack

ten98-os uses one stack: TypeScript end to end, run as long-running services on k3s. Compliance is strict. Nothing
outside this file enters the code base.

- It does not use a serverless platform, a Python back end or Next.js.
- Every part is the latest stable release, pinned exactly.
- There is one package for each job.
- A library or an API that already does the job comes before our own code.

Versions were checked on 15 November 2026 and resolve together without a conflict. They are checked again when
development starts.

## Layers

| Layer | Choice | Version |
|---|---|---|
| Language | TypeScript, with full checking on | 7.0.2 |
| Runtime | Node, on its long-term-support line | 26.13.1 |
| Package manager | pnpm | 12.21.0 |
| Framework and router | TanStack Start and TanStack Router | 1.169.5 and 1.170.46 |
| Server | Nitro, built as a Node server | 3.0.261103-rc |
| Build | Vite, with `@vitejs/plugin-react` | 8.3.8 and 6.3.0 |
| Interface | React | 19.3.1 |
| Styling | Tailwind CSS, with `@tailwindcss/vite` | 4.3.5 |
| Components | shadcn/ui on Base UI, and daisyUI | `shadcn` 4.23.0, `@base-ui/react` 1.9.0 and `daisyui` 5.8.1 |
| Database | PostgreSQL, with row-level security forced | 18.7 |
| Data access | Drizzle over `pg` | 0.45.4 and 8.23.1 |
| Schema changes | drizzle-kit | 0.31.11 |
| Sign-in, organisations and roles | Better Auth | 1.7.25 |
| Validation | zod, with drizzle-zod | 4.6.7 and 0.8.3 |
| Background jobs | pg-boss | 12.38.2 |
| Mail | nodemailer, through a mail provider | 10.5.0 |
| Logs | pino | 10.4.0 |
| MCP server | `@modelcontextprotocol/server` | 2.4.0 |
| Tests | Node's built-in test runner | Part of Node |
| Browser tests and browser containers | Playwright | 1.65.1 |
| Deployment | k3s | v1.37.2+k3s1 |

- **Nitro** is the one part with no stable release. Version 3 is at release candidate, and TanStack Start's
  documented way to host a Vite build on Node uses it. It moves to 3.0 when that is published. No other pre-release
  is allowed.
- **Type packages** follow their library: `@types/node` 26.6.6, `@types/react` 19.3.0, `@types/react-dom` 19.3.0
  and `@types/pg` 8.23.1.
- **shadcn/ui** can generate its components on Base UI, Radix UI or React Aria. ten98-os uses Base UI only, which
  shadcn/ui's changelog names as the default since July 2026. The small helper packages its command line adds are
  pinned like any other, and its icon set is the one icon set.

## Interface

Tailwind CSS, shadcn/ui and daisyUI are used everywhere: on the OS's own screens and on the sites, stores and
portals the builder publishes.

| Set | What it gives |
|---|---|
| shadcn/ui | Working components with keyboard and screen-reader behaviour: dialogs, menus, forms and tables |
| daisyUI | Ready styles and themes, with no script: buttons, cards, navigation and page sections |

- **One theme.** The theme is written once, as a daisyUI theme. shadcn/ui's colour names point at it, so both sets
  share the same colours, and a site or an organisation changes them in one place.
- **One component for each element.** Where both sets have the same element, such as a button, the OS's shared
  components pick one. The same element then looks the same everywhere.
- Look in the two sets first. Write a component only when neither has one, and add it to the OS's shared
  components, not inside a mini-app.
- A common feature looks and works the same in every mini-app: one component and one layout.
- Colours, spacing and type sizes come from the theme, never from a literal value.
- The custom design system, `@ten98/ui`, is not used.

## Reuse order

Follow this order for every feature, and stop at the first that fits.

1. What the platform already gives: Node, the browser, PostgreSQL and the framework.
2. A feature of a package already in this file, such as a Better Auth plugin.
3. A maintained public library or a provider's API, by [sops/add-a-dependency.md](sops/add-a-dependency.md).
4. Code copied from a codebase Ten98 owns, by
   [sops/reuse-a-ten98-function.md](sops/reuse-a-ten98-function.md).
5. New code, for the gap only.

Do not wrap a library in functions that only rename it.

## One package per job

| Job | The one choice | Not used |
|---|---|---|
| Pages, routes and loading data | TanStack Start and Router | A second router, a data-fetching library, a global state library |
| Serving the app | Nitro, as a Node server | Express, Fastify, Hono or any second server |
| Styling | Tailwind CSS | CSS-in-JS, a second CSS framework |
| Components | shadcn/ui and daisyUI, on one theme | A third component set, or two versions of the same element |
| Reading and writing the database | Drizzle over `pg` | A second ORM, query builder or driver |
| Checking input | zod | Any other validation library |
| Sign-in, organisations, roles and invitations | Better Auth and its plugins | `openid-client`, hand-written sessions, tokens or invitations |
| Background and scheduled work | pg-boss | A second queue, a cron library, Redis, RabbitMQ |
| Sending mail | nodemailer | A provider's own sending library |
| Logs | pino | `console` in server code, a second logger |
| Requests to outside services | The built-in `fetch` | A request library |
| Tests | Node's test runner and Playwright | Jest, Vitest, Cypress, Puppeteer |
| Building | Vite | A second bundler |

## Carried over from the existing apps

These are installed when the mini-app that needs them is built.

| Package in the existing apps | In ten98-os | Why |
|---|---|---|
| `@ten98/runtime` | Dropped | Libraries and APIs do its jobs. See the wiki's Build approach page |
| `@ten98/ui` | Dropped | Tailwind CSS, shadcn/ui and daisyUI replace it |
| `openid-client` | Dropped | Better Auth does sign-in |
| `detect-browser` | Dropped | `ua-parser-js` does the same job |
| `ua-parser-js` | Kept at 1.0.41 | Reads the visitor's browser. The 1.x line is MIT. Version 2 is AGPL and must not be installed |
| `parse5` 8.1.1 and `saxes` 6.0.0 | Kept | One reads HTML and the other reads XML |
| `mmdb-lib` 3.0.5 | Kept | Finds a visitor's country |
| `qrcode-generator` 2.0.4 | Kept | Makes QR codes |

## Not chosen yet

No package for these jobs is installed before the owner chooses one.

| Job | Settled at |
|---|---|
| Forms and data grids | The core's review. shadcn/ui's guides use TanStack Form and TanStack Table |
| Charts | The Workspace review |
| Live sync | The Workspace review |
| Univer's licensed packages and its server | Decided. Versions are set at the Workspace review |
| File storage, with an S3-compatible API | The Groupware review |
| The mail provider | The Groupware review |
| Access to AI models | The core's review |
| Site builder, editor, whiteboard and flow canvas | Each app's review |
| Search beyond PostgreSQL's own | When PostgreSQL's search is not enough |
| Linter and formatter | None for now |
| Cluster add-ons: certificates, a PostgreSQL operator, metrics | The deployment design |

## Rules of good practice

### Write once

ten98-os follows Django's rule: every idea and every piece of data lives in one place, and the rest is derived
from it. Keep it DRY, and keep it simple (KISS).

- A record's shape is written once, as its Drizzle table. Its zod schema comes from drizzle-zod, and its TypeScript
  type comes from the schema.
- A mini-app describes its records, events, actions and permissions once. Views, forms, the API, MCP, automations
  and the AI all read that description.
- A setting, a constant or a piece of text has one home.
- Choose the simplest design that works. Do not add a layer, an option or an abstraction for a need nobody has yet.

### Versions and packages

- Every version is exact, with no `^` or `~`. pnpm saves exact versions (`saveExact`) and the lockfile is committed.
- One version of each package in the whole workspace, defined once in pnpm's `catalog`.
- `package.json` names the Node and pnpm versions, and an install with any other version fails (`engineStrict`).
- A release must be stable and at least three days old before it is installed (`minimumReleaseAge`).
- Install scripts of dependencies stay blocked, except for packages on the allow list (`allowBuilds`).
- A version changes by a pull request that updates this file and the lockfile together.

### TypeScript

- The compiler settings match the existing apps: `strict`, no unused locals or parameters, and
  `erasableSyntaxOnly`. Copied code then checks without edits.
- Use only syntax that can be erased: no `enum`, no `namespace` and no constructor parameter properties. Node runs
  the TypeScript files directly.
- No `any`, `@ts-ignore` or `@ts-nocheck`. Data from outside is `unknown` until zod has checked it.
- Modules are ES modules.

### Screens

- A route's loader fetches its data. A component does not fetch in an effect.
- State lives in the URL first, as search parameters checked by zod, and then in the component.
- Every control works from the keyboard and has a label.
- React code follows the skill named in [SKILLS.md](SKILLS.md).

### Routes and server functions

- Every server function and server route checks sign-in and permission itself.
- zod checks every input before use: server function input, route and search parameters, form data and webhook
  bodies.
- Database access and secrets stay in server-only files, which no component imports.
- A change to a record goes through an action of the mini-app that owns it. The interface, automations, the AI, the
  API and MCP all call the same action.
- Every action takes an idempotency key, so a retry cannot repeat it.
- An event is written in the same transaction as the change it reports.
- An automation stops at a fixed depth, so rules cannot set each other off without end.

### Database

- Every table that holds an organisation's data carries the organisation's id and has row-level security forced.
  The app connects as a role that does not own the tables and cannot create them.
- All work runs in one of three contexts: an organisation, a portal customer, or the system. Each sets itself
  inside a transaction. Work with no context fails. It does not quietly return nothing.
- One resolver in the core finds the organisation for incoming mail, visits, webhooks and jobs. It returns only the
  organisation's id, and it is the only code that reads without a context.
- Queries are typed Drizzle queries. Hand-written SQL is for schema changes, security rules and database functions.
- Schema changes are generated by drizzle-kit and checked in. A merged change is never edited: a new one corrects
  it.
- Tables are created by schema changes at release, never while the app runs.
- After each schema change, the database's functions, triggers, security rules and grants are compared with the
  expected list, so a generated change cannot drop a guard.
- Money is whole minor units in `bigint`, as in Books. Quantities and rates are `numeric`, and times are
  `timestamptz`. Never a floating-point number or a local time.
- Every foreign key has an index.
- A write that touches several tables is one transaction.

### Sign-in and access

- Sign-in, sessions, two-factor sign-in, organisations, roles and invitations come from Better Auth and its
  plugins. No hand-written password, session or token code.
- Staff and customers sign in separately.
- Secrets come from the environment. They never reach the browser, the logs or the repository.

### Background jobs

- Work that outlasts a request, runs on a schedule or calls a provider in bulk is a pg-boss job in the worker role.
- A job can run twice without harm.
- A job's payload is checked by zod and carries ids, not copies of records.
- A failed job retries with a growing delay, and then stops where a person will see it.

### Running on k3s

- One deployment serves one tenant. It takes its database, file storage, mail, AI and shared-service settings from
  the environment, so the same image runs for every tenant.
- One image is started in different roles: web, worker, visit collector, live sync, and sites and portals.
- Every deployment runs the latest release. A schema change runs unattended, starting from the previous release.
- A deployment reports its version and its health, so the app that manages deployments can upgrade and watch it.
- Univer's server and the browser containers are services shared by all deployments. A deployment reaches them
  through its settings.
- A deployment runs on its own. It never needs the app that manages SaaS deployments, and without a shared service
  the mini-apps that need it stay off.
- A role keeps nothing on its own disk.
- Settings come from the environment and are checked by zod at start-up. A missing setting stops the start.
- Every role answers a health check, and finishes the work in hand before it exits.
- The image runs as a non-root user, from a base image pinned by digest.
- Schema changes run as their own step before the new version takes traffic.
- The database has point-in-time recovery. A restore is rehearsed before any real data is stored, and again after
  every change to the backup set-up.
- Logs are JSON lines on standard output, with secrets and personal data redacted.
- The OS's own code uses PostgreSQL for data, jobs and messages. The Redis and RabbitMQ that Univer's server needs
  serve Univer only.

### Tests

- Unit and integration tests use Node's test runner. Integration tests run against a real PostgreSQL.
- Every table with row-level security has a test proving that one organisation cannot read or change another's
  rows.
- The two-organisation test also covers jobs, files and documents kept on Univer's server.
- Browser flows are tested with Playwright.
- Tests run on the local machine. A test never spends money, sends a real message, uses a provider's live
  credentials or types a real password.
- One command runs every check: types, the stack check, tests and the build.

## The automated check

An automated check enforces this file from the first commit of code. It fails the build when a package, a version
or a file falls outside it. The existing apps' `check:architecture` script is the starting point. A change merges
only when the checks pass on its latest commit.

## Changing the stack

Only the owner changes a choice in this file, and the change is recorded on the wiki's Decisions page first. A
version moves by a pull request.

## Examples of a breach

- A second framework or server, such as Next.js or Express.
- A second data-access library or database, such as Prisma, MongoDB or SQLite.
- A lockfile from npm, Yarn or Bun.
- A second validation or sign-in library.
- Two versions of the same element, such as a daisyUI button on one screen and a shadcn/ui button on another.
- A second theme, or a colour set outside the theme.
- A hand-written component, helper or wrapper for something a package in this file already does.
- A JavaScript file, or a TypeScript file with checking disabled.
- A version range, a pre-release other than Nitro, or `ua-parser-js` 2.
