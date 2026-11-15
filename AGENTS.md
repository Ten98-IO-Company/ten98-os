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
3. [agents/STACK.md](agents/STACK.md): the selected stack. Compliance is strict.
4. [agents/HARNESS.md](agents/HARNESS.md): how work is split between agents and checked.
5. [agents/SKILLS.md](agents/SKILLS.md): which skills and which procedure fit each kind of task.

## How you work

- Start every task by [agents/sops/start-a-task.md](agents/sops/start-a-task.md).
- Do a task yourself only when it is a leaf. Otherwise split it by
  [agents/sops/split-and-delegate.md](agents/sops/split-and-delegate.md).
- Pick at most three skills from the shortlist, and follow the procedure in [agents/sops/](agents/sops/) for the
  kind of work.

## Rules

- The wiki's Decisions page is the record. A proposal is not a decision until it is listed there as decided.
- Write documentation to the wiki, not to `docs/` or the README. The README stays short. Procedures that agents
  follow live in `agents/`.
- Write the interface and the code new in ten98-os. Do not depend on `@ten98/runtime` (the code-system) or
  `@ten98/ui` (the design system).
- Copy code from codebases Ten98 owns instead of rewriting it: Campaign, Discover, Books, the code-system and the
  design system. Record the source in the pull request. See
  [agents/sops/reuse-a-ten98-function.md](agents/sops/reuse-a-ten98-function.md).
- Comply strictly with the stack in [agents/STACK.md](agents/STACK.md). Nothing outside it enters the code base,
  and only the owner changes it.
- Install public packages directly, by [agents/sops/add-a-dependency.md](agents/sops/add-a-dependency.md).
- The licence is PolyForm Strict 1.0.0: no redistribution, no changes by outside people, and no commercial use.
  Take an outside contribution only when its author has accepted [CONTRIBUTOR-AGREEMENT.md](CONTRIBUTOR-AGREEMENT.md)
  in the pull request. Do not copy AGPL or other copyleft code in.
- The tenant is the organisation. The user who signs up owns the app or the organisation they create. "Workspace"
  means only the part of the core where work is done.
- A mini-app owns its tables. Reach another mini-app's data through the core or through that mini-app.
- Views work on all records: the OS's own records as well as custom tables. A view changes a record only through the
  mini-app that owns it.
- Change the repository through a branch and a pull request into `main`. The wiki is its own git repository in
  `wiki/` and is pushed directly to its `master` branch.
- Never report a security defect that no release has fixed in an issue, pull request, commit message or the wiki.

## Handing work to another agent

Work must be easy to move between agents, so nothing needed to continue may live only in your session.

- Decisions go in the wiki, work items in GitHub issues, progress in pull requests.
- Keep to one task per branch and push often.
- When you stop mid-task, follow [agents/sops/finish-and-hand-off.md](agents/sops/finish-and-hand-off.md).
- Run the same checks every agent runs. A change is accepted on its checks and review, not on who wrote it.
