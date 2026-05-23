# AI Development Guidelines

Keep this file concise — add only essential guidelines, not examples or edge cases.

## Structure

<!-- Update this to match your actual repo layout -->
- `/src/` - Application source code
- `/docs/` - Architecture decisions, guides, and references
- `/.plans/` - Temporary plan files for active work (date-prefixed, delete when done)

## Core Principles

- **Minimalism** - Only write what's necessary, less code = less maintenance
- **Code Quality** - Prioritize clarity over cleverness, meaningful names
- **No Duplicate Code** - Extract shared logic, refactor if repeated
- **Small Functions** - Under ~100 lines, single purpose
- **Testing** - Focus on critical paths and edge cases
- **Documentation** - Document "why", not "what"; keep docs near code
- **DX First** - Update documentation before implementing changes
- **Plain Language** - When talking to people, drop the jargon. Short sentences, friendly tone, easy to follow. Tell them **what** you did and **why** it matters — not **how** you did it. The code already shows the how.

## Ownership

Own the task end-to-end. Owning something means you're responsible for the outcome being right — not just for doing what you were told. Decide, act, push back when you should, and tell the user what you did.

- **Default to action.** If the next step is obvious, take it. Don't narrate intent and wait — just do it.
- **Pick a path.** When two options are close, choose one and note the reasoning in the PR. Don't stall on a coin flip.
- **Recover yourself.** Failing tests, lint errors, broken CI, missing files — fix them. Don't escalate things you can resolve.
- **Only ask when stuck for real.** Genuine ambiguity, scope changes, or destructive/irreversible actions warrant a question. Routine work doesn't.
- **Push back when you should.** Real ownership means saying so when a request is wrong, risky, or there's a clearly better path — not nodding along. Suggest the better path; if the user still wants the original, do it.
- **Close the loop.** Keep going until code is in, CI is green, review threads converge, and the PR is ready for merge — then report back.

## Workflow

1. **Read context first** — before editing any doc, plan, or file, read the root `README.md` and relevant `/docs/` or `/.plans/` files so changes are grounded in existing context.
2. **Implement the changes** — follow core principles above.
3. **Open a draft PR** — after your first meaningful commit, push and open a **draft** PR without asking. Skip only if a PR already exists. Call `subscribe_pr_activity` immediately to monitor CI and reviews.
4. **Fix CI failures** — when CI events come in, investigate and push fixes to the same branch. Don't wait to be told.
5. **Address review comments** — fix issues raised by the AI reviewer or humans, then reply on each thread explaining the fix or reasoning. The reviewer resolves threads automatically.
6. **Refresh PR docs** — before flipping ready, update the PR title and description to match the final changes, and update any plans/docs the work touched.
7. **Mark ready** — once CI is green and reviews converge, flip the PR from draft to ready and tell the user it's ready for merge.

## PR Descriptions

Write for a non-technical reader. Describe **what** changed and **why**, not **how** — the code shows the how. Keep it short; only add implementation details when a specific decision needs explaining.

## AI Reviewer

An automated AI reviewer (`github-actions[bot]`) runs on every PR and submits an `APPROVE` or `REQUEST_CHANGES` verdict. `REQUEST_CHANGES` must be addressed before merge.

**Aim for consensus on every open thread** — fix the issue, or reply with reasoning. Push back when you disagree; the reviewer isn't infallible. But don't merge through a stalemate: if the reviewer holds firm on a point you can't resolve in code, defer it to a follow-up plan in `/.plans/` and reply on the thread with the link.

Re-trigger a review after replying (or whenever you want a fresh pass) with an empty commit: `git commit --allow-empty`. Keep iterating until both sides converge.

## Plans & Docs

`/.plans/` and `/docs/` are **living documents** — update them in the same PR as related code changes, never leave them stale.

- `/.plans/` - date-prefixed (e.g., `2026-01-27-feature-name.md`), one feature per plan, delete when complete
- `/docs/` - general docs, architecture, guides; fix or remove when code invalidates them
