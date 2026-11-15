# ten98-os

These instructions are for every coding agent, whichever tool runs it. Keep them tool-neutral. A tool's own
instruction file only points here.

ten98-os is one system for the whole business: a core (base, Groupware, Workspace) and four apps on it (Marketing,
Sales, Finance, Websites). Each app is a set of mini-apps, and each mini-app is made of modules.

Status: vision. Development has not started. It begins when the stack unification of Campaign, Discover and Books
is complete.

## Read first

1. [README.md](README.md)
2. The wiki: [Home](https://github.com/Ten98-IO-Company/ten98-os/wiki),
   [Decisions](https://github.com/Ten98-IO-Company/ten98-os/wiki/Decisions),
   [Structure](https://github.com/Ten98-IO-Company/ten98-os/wiki/Structure) and
   [Mini-apps](https://github.com/Ten98-IO-Company/ten98-os/wiki/Mini-Apps).
3. [agents/STACK.md](agents/STACK.md): the selected stack, the reuse order and the rules of good practice.
   Compliance is strict.
4. [agents/HARNESS.md](agents/HARNESS.md): how work is split, run in parallel, advised and checked.
5. [agents/SKILLS.md](agents/SKILLS.md): which skills and which procedure fit each kind of task.

## How you work

- Start every task by [agents/sops/start-a-task.md](agents/sops/start-a-task.md).
- Question the request before you plan. Find its crux, and carry out the best version of it. Say what you changed
  and why. A child agent keeps to its brief: it proposes a better version to its parent and waits.
- Do a task yourself only when it is a leaf. Otherwise split it by
  [agents/sops/split-and-delegate.md](agents/sops/split-and-delegate.md).
- Run independent parts at the same time, each in its own session on its own feature branch. There is no cap.
- Work as an autonomous loop: build, test end to end, fix, and test again. Ask the owner only for an environment
  setting, for a decision that is theirs, or when an issue survives two attempts.
- Pick at most three skills from the shortlist, and follow the procedure in [agents/sops/](agents/sops/) for the
  kind of work.
- Report what you verified and what you did not. Never describe an unchecked result as working.

## Rules

- The wiki's Decisions page is the record. A proposal is not a decision until it is listed there as decided. A
  decision is given once: do not ask the owner again for what the page already answers.
- Write documentation to the wiki, not to `docs/` or the README. The README stays short. Procedures that agents
  follow live in `agents/`.
- ten98-os is a clean slate. Rules written for the other Ten98 apps about reusing `@ten98/runtime` and `@ten98/ui`,
  moving shared code into them, or not copying from them do not apply here.
- Do not depend on `@ten98/runtime` (the code-system) or `@ten98/ui` (the design system).
- Do not reinvent the wheel. Follow the reuse order in [agents/STACK.md](agents/STACK.md): the platform, a package
  already in the stack, a public library or a provider's API, code copied from a codebase Ten98 owns, and new code
  only for the gap.
- Write once. Every idea and every piece of data has one home, and the rest is derived from it. Keep it DRY, and
  keep it simple (KISS).
- The interface is Tailwind CSS with shadcn/ui and daisyUI. Both are used everywhere, on one theme, with one shared
  component for each element.
- Comply strictly with the stack in [agents/STACK.md](agents/STACK.md). Nothing outside it enters the code base,
  and only the owner changes it.
- Install public packages by [agents/sops/add-a-dependency.md](agents/sops/add-a-dependency.md). Copy Ten98's own
  code by [agents/sops/reuse-a-ten98-function.md](agents/sops/reuse-a-ten98-function.md), and record the source
  in the pull request.
- The licence is PolyForm Strict 1.0.0: no redistribution, no changes by outside people, and no commercial use.
  Take an outside contribution only when its author has accepted [CONTRIBUTOR-AGREEMENT.md](CONTRIBUTOR-AGREEMENT.md)
  in the pull request. Do not copy AGPL or other copyleft code in, and do not open the source code of an AGPL
  reference: study its running product and its documents. Code copied from another project keeps that project's
  licence notice in the file.
- Each tenant has its own deployment. Inside it, data is separated strictly by organisation. The user who signs up
  owns the app or the organisation they create. "Workspace"
  means only the part of the core where work is done.
- A mini-app owns its tables. Reach another mini-app's data through the core or through that mini-app.
- Views work on all records: the OS's own records as well as custom tables. A view changes a record only through the
  mini-app that owns it.
- Every task has its own feature branch. Change the repository through a pull request, and never merge your own
  code change. Until code starts, pull requests go into `main`. Once it starts, they go into `dev` first and reach
  `main` when tested, as in the other Ten98 apps.
- The wiki is its own git repository in `wiki/` and is pushed directly to its `master` branch.
- A change merges only when the automated checks pass on its latest commit. The lockfile, schema changes and
  shared components change on one branch at a time.
- Deployments, and anything else that faces outward, need the owner's yes each time.
- Never open, print, copy or summarise a credentials file. Never put a secret in a brief, commit, issue, pull
  request or message. Scan for secrets before every push.
- Never report a security defect that no release has fixed in an issue, pull request, commit message or the wiki.
  Report it through the repository's private reporting, as [SECURITY.md](SECURITY.md) describes.
- This repository and its wiki are public and hold only ten98-os's own code. The app that manages SaaS deployments
  and the deployment set-up are private. Never put their code, server names or details of how deployments are run
  here.

## Handing work to another agent

Work must be easy to move between agents, so nothing needed to continue may live only in your session.

- Decisions go in the wiki, work items in GitHub issues, progress in pull requests.
- Keep to one task per branch and push often.
- When you stop mid-task, follow [agents/sops/finish-and-hand-off.md](agents/sops/finish-and-hand-off.md).
- Run the same checks every agent runs. A change is accepted on its checks and review, not on who wrote it.
