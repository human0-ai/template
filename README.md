<h1 align="center">human0</h1>

<p align="center">
  A repository template for working with AI agents — and an AI reviewer that
  holds the quality bar on every pull request.
</p>

<p align="center">
  <a href="https://human0.ai">human0.ai</a> ·
  <a href="https://github.com/human0-ai/code-review">the reviewer action</a>
</p>

---

This is the starting point for any repo you want AI agents to operate in. Fork
it and you get, out of the box:

- **`AGENTS.md` / `CLAUDE.md`** — the guidelines agents read on every run, so they
  understand your structure, principles, and workflow without being told each time.
- **An AI code reviewer** — runs on every PR via GitHub Actions, posts inline
  comments, and gives a single verdict: **APPROVE** or **REQUEST_CHANGES**.
- **A workflow built for autonomy** — draft a PR, watch a preview, say "go", and
  let the reviewer's approval auto-merge it.

It's the same setup that builds and runs [human0](https://human0.ai) itself —
every commit reviewed and merged by AI.

## Two ways to use it

### 1. Drop the reviewer into an existing repo

If you just want the AI reviewer on your current project, you don't need to fork
anything. Add a credential and one workflow file — full steps in the
[code-review action README](https://github.com/human0-ai/code-review#quick-start).

### 2. Start a new repo from this template

Use this repo as a template (the green **Use this template** button), then:

1. **Add a credential.** In **Settings → Secrets and variables → Actions**, add
   one of:
   - `ANTHROPIC_API_KEY` — an [Anthropic API key](https://console.anthropic.com/), or
   - `CLAUDE_CODE_OAUTH_TOKEN` — a Claude.ai OAuth token (`claude setup-token`).
2. **Edit `AGENTS.md`** to describe your project — its structure and rules.
3. **Open a pull request.** The reviewer runs on the next push.

To let an approval merge on its own, enable **auto-merge** and require the AI
review in your branch protection settings.

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
