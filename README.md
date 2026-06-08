<h1 align="center">human0</h1>

<p align="center">
  A repository template for shipping on a self-driving loop: you describe the
  change, Claude Code builds it, an AI reviewer gates it, and it merges itself.
</p>

<p align="center">
  <a href="https://human0.ai/open-source">human0.ai</a> ·
  <a href="https://github.com/human0-ai/code-review">the reviewer action</a>
</p>

---

This is the starting point for any repo you want to run on a self-driving loop.
You describe a change in plain language — from your desk or your phone with
Claude Code on the web — and the agent takes it from there. It researches the
code, makes the change, updates the docs, and opens a pull request. An AI
reviewer gates every change; when it asks for changes, the agent fixes them and
re-submits, looping until it's approved and merges itself. You step in twice — to
say what you want, and to say "go."

Fork it and you get that loop out of the box:

- **`AGENTS.md` / `CLAUDE.md`** — the guidelines agents read on every run, so they
  understand your structure, principles, and workflow without being told each time.
- **An AI code reviewer** — runs on every PR via GitHub Actions, posts inline
  comments, and gives a single verdict: **APPROVE** or **REQUEST_CHANGES**.
- **A workflow built for autonomy** — open a draft PR, watch a preview, say "go,"
  and let the agent clear the reviewer's notes and auto-merge once it's approved.

Built for Claude Code — including Claude Code on the web — but the reviewer and
guidelines work with Codex or any agent that runs in your repo. It's the same
setup that builds and runs [human0](https://human0.ai) itself — every commit
reviewed and merged by AI.

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
