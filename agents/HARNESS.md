# Recursive harness

This is how the AI builds ten98-os. An agent that receives a task either does it, or splits it and hands each part
to a child agent that works the same way. The pattern is the
[Recursive Agent Harness](https://arxiv.org/abs/2606.13643): the unit that repeats is a full agent with its own
tools, not a bare model call. In ten98-os a child may split its work again, down to a fixed depth.

## The loop every agent runs

1. **Read.** `AGENTS.md`, the task's issue, and the wiki pages the task names.
2. **Size the task.** It is a leaf when all three are true:
   - it stays inside one mini-app or one piece of the core;
   - one agent can hold it in mind without losing track;
   - one run of the checks proves it.
3. **Leaf: do it.** Pick skills from [SKILLS.md](SKILLS.md), follow the matching procedure in [sops/](sops/), run
   the checks and report.
4. **Not a leaf: split it.** Follow [sops/split-and-delegate.md](sops/split-and-delegate.md).
5. **Verify the children.** Run their acceptance checks yourself. A child's report is not proof.
6. **Integrate and report up.** Say what changed, how it was checked and what is still open.

## Levels

The split follows the product, so each level has a natural owner.

| Level | An agent at this level | Splits into |
|---|---|---|
| App | Owns one app or one part of the core | Mini-apps |
| Mini-app | Owns one mini-app | Modules |
| Module | Builds one module | Nothing. This is a leaf |

There are at most three levels of agents. No agent splits below a module.

## The brief a parent writes

| Part | What it holds |
|---|---|
| Goal | One sentence saying what is true when the task is done |
| Base | The branch and commit to start from |
| Files it owns | The paths the child may change |
| Not to touch | Shared files, which stay with the parent |
| What to read | The decisions and pages that bind the task |
| Acceptance checks | The exact checks that must pass |
| Limits | When to stop and report without finishing |

A child gets this brief, not the parent's history.

## The report a child sends back

- The files it changed.
- The checks it ran and their results.
- What is not done.
- Anything the parent must decide.

## Rules

- Two agents never own the same file. One agent, the parent, integrates shared files.
- A parent accepts a child's work only on its own run of the checks.
- After two failed attempts at the same check, an agent stops and reports up.
- Work that touches money, access or tenancy gets a review by an agent that did not write it.
- Every level is a GitHub issue linked to its parent, and every leaf is a branch with a pull request. Any agent, on
  any tool or machine, can continue from there.
- A tool that cannot start child agents runs the children one after another, each from its written brief and in a
  fresh session.
