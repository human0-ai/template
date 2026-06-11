<h1 align="center">human0</h1>

<p align="center">
  Describe a change. Claude Code ships it. You barely touch it.
</p>

<p align="center">
  <a href="https://human0.ai/open-source">human0.ai</a> ·
  <a href="https://github.com/human0-ai/code-review">the reviewer action</a>
</p>

---

Fork this template and your repo runs on a self-driving loop.

You say what you want — in plain language, from your laptop or your phone. Claude
Code does the rest. It researches the code. It makes the change. It writes the
docs. It opens a pull request.

Then an AI reviewer checks the work. If something's off, the agent fixes it and
tries again. It loops on its own until the review passes. Then it merges.

You step in twice: to say what you want, and to say "go."

What you get out of the box:

- **`AGENTS.md` / `CLAUDE.md`** — your rules, read by every agent on every run.
  Write them once.
- **An AI reviewer** — checks every PR, comments inline, gives one verdict:
  **APPROVE** or **REQUEST_CHANGES**.
- **An autonomous workflow** — open a draft PR, watch the preview, say "go." The
  agent clears the review and the PR merges itself.

Built for Claude Code, including Claude Code on the web. The reviewer and rules
work with Codex or any agent too. It's the same setup that runs
[human0](https://human0.ai) itself — every commit reviewed and merged by AI.

## Before you start: one prerequisite

The template is free (Apache 2.0) and runs entirely in your own GitHub Actions,
but the reviewer runs on **your own Anthropic key** — bring an
[Anthropic API key](https://console.anthropic.com/) or a Claude.ai OAuth token
(`claude setup-token`). It's bring-your-own on purpose: **no per-seat fee, and
your code never leaves your repo.** Anthropic bills you directly for usage —
each review typically costs about **$0.01–0.15**. You add this key as a GitHub
secret in step 1 below.

## Two ways to use it

### 1. Drop the reviewer into an existing repo

If you just want the AI reviewer on your current project, you don't need to fork
anything. Add a credential and one workflow file — full steps in the
[code-review action README](https://github.com/human0-ai/code-review#set-it-up).

### 2. Start a new repo from this template

Use this repo as a template (the green **Use this template** button), then:

1. **Add a credential.** In **Settings → Secrets and variables → Actions**, add
   one of:
   - `ANTHROPIC_API_KEY` — an [Anthropic API key](https://console.anthropic.com/), or
   - `CLAUDE_CODE_OAUTH_TOKEN` — a Claude.ai OAuth token (`claude setup-token`).
2. **Edit `AGENTS.md`** to describe your project — its structure and rules.
3. **Review `docs/ai-review.md`** — this is your reviewer's instructions. Tailor
   it to your project before you start relying on it.
4. **Open a pull request.** The reviewer runs on the next push.

To let an approval merge on its own, enable **auto-merge** and require the AI
review in your branch protection settings.

## Repository settings

For the reviewer to **approve** PRs (which is what lets an approval auto-merge),
GitHub must allow Actions to approve pull requests:

**Settings → Actions → General → Workflow permissions** → enable
**"Allow GitHub Actions to create and approve pull requests."**

In an organization this is often locked at the org level — set it under
**Organization → Settings → Actions → General** instead. You don't need the
"Read and write" default token permission; the workflow already requests the
write scopes it needs.

## What's in here

| Path | What it's for |
| --- | --- |
| `AGENTS.md` | Guidelines agents read every run. `CLAUDE.md` is a symlink to it. |
| `docs/ai-review.md` | The reviewer's prompt — edit it to change how the reviewer behaves. |
| `.github/workflows/ai-review.yml` | Runs the reviewer on every PR. |

## Customizing the reviewer

The reviewer is just a prompt plus your `AGENTS.md`. To change the bar, tone, or
project-specific rules, edit `docs/ai-review.md`. To teach it your conventions
without touching the prompt, write them in `AGENTS.md` — it reads that on every
run.

## License

Apache 2.0 — see [LICENSE](./LICENSE).
