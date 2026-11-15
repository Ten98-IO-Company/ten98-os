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

## Rules

- The wiki's Decisions page is the record. A proposal is not a decision until it is listed there as decided.
- Write documentation to the wiki, not to `docs/` or the README. The README stays short.
- The licence is non-commercial and not MIT. Do not copy AGPL or other copyleft code in. Pin the version and check
  the licence of every dependency you add.
- Install public packages directly. Keep in-house libraries small and only for what is unique to Ten98. The design
  system is a custom library.
- A mini-app owns its tables. Reach another mini-app's data through the core or through that mini-app.
- Change the repository through a branch and a pull request into `main`. The wiki is its own git repository in
  `wiki/` and is pushed directly to its `master` branch.
- Never report a security defect that no release has fixed in an issue, pull request, commit message or the wiki.

## Handing work to another agent

Work must be easy to move between agents, so nothing needed to continue may live only in your session.

- Decisions go in the wiki, work items in GitHub issues, progress in pull requests.
- Keep to one task per branch and push often.
- When you stop mid-task, write in the pull request what is done, what is left and how to check it.
- Run the same checks every agent runs. A change is accepted on its checks and review, not on who wrote it.
