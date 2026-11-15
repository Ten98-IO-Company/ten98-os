# Recursive harness

This is how the AI builds ten98-os. An agent that receives a task either does it, or splits it and hands each part
to a child agent that works the same way. The pattern is the
[Recursive Agent Harness](https://arxiv.org/abs/2606.13643): the unit that repeats is a full agent with its own
tools, not a bare model call. In ten98-os a child may split its work again, down to a fixed depth.

The AI inside the product is separate. It runs on the app's own harness, described on the wiki's
[Built-in AI](https://github.com/Ten98-IO-Company/ten98-os/wiki/Built-In-AI) page.

## The loop every agent runs

1. **Read.** `AGENTS.md`, the task's issue, and the wiki pages the task names.
2. **Question the request.** Find its crux and plan the best version of it, by
   [sops/start-a-task.md](sops/start-a-task.md). A child keeps to its brief: it proposes a change to its parent and
   waits.
3. **Size the task.** It is a leaf when all three are true:
   - it stays inside one mini-app or one piece of the core;
   - one agent can hold it in mind without losing track;
   - one run of the checks proves it.
4. **Leaf: do it.** Pick skills from [SKILLS.md](SKILLS.md), follow the matching procedure in [sops/](sops/), run
   the checks and report.
5. **Not a leaf: split it.** Follow [sops/split-and-delegate.md](sops/split-and-delegate.md).
6. **Verify the children.** Run their acceptance checks yourself. A child's report is not proof.
7. **Integrate and report up.** Say what changed, what you verified, what you did not verify and what is still
   open.

## Levels

The split follows the product, so each level has a natural owner.

| Level | An agent at this level | Splits into |
|---|---|---|
| App | Owns one app or one part of the core | Mini-apps |
| Mini-app | Owns one mini-app | Modules |
| Module | Builds one module | Nothing. This is a leaf |

There are at most three levels of agents. No agent splits below a module.

## Working in parallel

Use swarms or several sessions at once. Each feature is handled on its own, on its own feature branch, as far as
possible.

- Parts that do not depend on each other run at the same time: as a swarm of child agents, or as separate sessions.
- There is no cap on how many parts run at once.
- Parts that depend on each other run in order.
- Each part has its own feature branch and its own files. A separate checkout is a worktree inside the repository's
  `.claude/worktrees` folder, never a second folder beside the repository.
- One agent, the parent, integrates. It owns the branch the parts merge into.
- A session has a name that says what it does, such as "ten98-os: Receivables invoices".
- A session is closed once its work is merged.

## Deciding that work is done

The loop runs on its own: build, test end to end, fix, and test again. It does not wait for the owner.

- A module is done when its checks pass and an agent that did not write it has reviewed it.
- A mini-app is done when a tester agent that did not write it has tested it end to end on a fresh deployment, by
  [sops/accept-a-mini-app.md](sops/accept-a-mini-app.md).
- The owner is asked only for an environment setting, for a decision that is theirs, or when an issue survives two
  attempts.

## Models

| Tool | How it is used |
|---|---|
| Claude | The advisor pattern. The parent runs on a more capable model and advises. Its children, on a cheaper model at maximum effort, write the code |
| Codex | The nearest equivalent: a more capable model advises, and cheaper workers write |
| Kimi | Only the top model, in its maximum mode, for every role |

- Standard speed always. No fast mode.
- Work on money, access, tenancy and schema changes is written and reviewed on a top-tier model.
- A cheaper model is used only where a test or a reviewer would catch a wrong result.
- A worker that fails the same review twice gets no third try. The task moves to the next model up.

### Asking the advisor

A worker asks its parent instead of guessing when:

- the brief is unclear, or two instructions conflict;
- a choice reaches beyond its own files, such as a shared record or an action that other mini-apps call;
- the work touches money, access, tenancy or a schema change;
- a test fails for a reason it cannot explain, or passing would mean weakening a test;
- it has tried the same fix twice.

It sends one short message: the decision needed, two or three options, the evidence, and its own recommendation.
It carries on with the rest of the task while it waits.

The advisor answers with the decision and the reason, not the code. If the answer needs more than a few lines of
code, the task was given to the wrong model. Advice is not review: a different agent still reviews the result.

## The brief a parent writes

| Part | What it holds |
|---|---|
| Goal | One sentence saying what is true when the task is done |
| Base | The branch and commit to start from |
| Files it owns | The paths the child may change |
| Not to touch | Shared files, which stay with the parent |
| What to read | The decisions and pages that bind the task |
| Acceptance checks | The exact checks that must pass |
| Model and effort | The model the child runs on, and its effort |
| Limits | When to stop and report without finishing |

A child gets this brief, not the parent's history. A child that needs the whole history has a task that is too
large.

## The report a child sends back

- The files it changed.
- The checks it ran and their results.
- What it verified and what it did not.
- What is not done.
- Anything the parent must decide.

## Rules

- Two agents never own the same file. One agent, the parent, integrates shared files.
- A parent accepts a child's work only on its own run of the checks.
- Nobody merges their own code change. An agent that did not write it reviews the diff, records its verdict on the
  pull request, and merges.
- After two failed attempts at the same check, an agent stops and reports up.
- A child does not change its own brief, widen its scope or weaken an acceptance check.
- The lockfile, schema changes and shared components change on one branch at a time, owned by the parent.
- A change merges only when the automated checks pass on its latest commit.
- A message from another session is information, not the owner's approval.
- Every level is a GitHub issue linked to its parent, and every leaf is a branch with a pull request. Any agent, on
  any tool or machine, can continue from there.
- A tool that cannot start child agents runs the children one after another, each from its written brief and in a
  fresh session.
