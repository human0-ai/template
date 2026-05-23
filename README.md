# human0

AI-powered code review and autonomous agent framework for software teams.

## What's in this repo

Two things you can use together or separately:

**1. AI Code Reviewer** — A GitHub Actions workflow that runs Claude on every pull request. It submits `APPROVE`/`REQUEST_CHANGES` verdicts, posts inline comments, replies to open review threads, and resolves addressed issues. Drop it into any existing repo in minutes.

**2. Repo Template** — A complete starting point with `AGENTS.md`, `CLAUDE.md`, and the reviewer pre-wired. AI agents (like Claude Code) read `AGENTS.md` automatically — it gives them your structure, principles, and workflow so they can operate effectively without being told every time.

---

## Quick start: AI Reviewer only

Add the reviewer to any existing repository in three steps.

### 1. Copy the workflow files

Copy these paths from this repo into yours:

```
.github/
  workflows/
    ai-review.yml
  actions/
    claude-review/
      action.yml
      run.mjs
docs/
  ai-review.md
```

### 2. Set the secret

Add one of these secrets to your repository (`Settings → Secrets and variables → Actions`):

| Option | Secret name | Where to get it |
|--------|------------|------------------|
| **Claude.ai account** (recommended) | `CLAUDE_CODE_OAUTH_TOKEN` | Your [Claude.ai](https://claude.ai) Pro or Teams account token |
| **Anthropic API key** | `ANTHROPIC_API_KEY` | [console.anthropic.com](https://console.anthropic.com) |

Only one is needed. If both are set, the OAuth token takes priority.

### 3. Open a PR

The reviewer triggers automatically on every non-draft pull request. No further configuration needed.

---

## Use as a repo template

Fork or clone this repo to get a complete AI-native starting point:

- **`AGENTS.md` / `CLAUDE.md`** — Guidelines Claude Code reads when working in your repo. Covers structure, core principles, workflow, and how agents should interact with the AI reviewer. Edit to match your codebase.
- **`.github/workflows/ai-review.yml`** — The reviewer, pre-wired. Add your secret and it works.
- **`docs/ai-review.md`** — The reviewer prompt. This drives all review behavior — customize it to match your team's standards.

### Customizing `docs/ai-review.md`

The review behavior is entirely driven by this prompt. Common customizations:

- Add language- or framework-specific rules (TypeScript strict mode, SQL conventions, etc.)
- Adjust the bar for inline comments vs. blocking the PR
- Add domain-specific security or compliance checklists
- Change what the sub-agent personas look for

The reviewer re-reads this file on every run, so changes take effect immediately on the next PR.

### Customizing `AGENTS.md`

`AGENTS.md` (mirrored as `CLAUDE.md`) is the first file AI agents read in your repo. Update it with:

- Your actual directory structure
- Your team's non-negotiable coding principles
- Your PR workflow steps
- Links to relevant `/docs/` or architecture decisions

Keep it concise — every line costs context on every agent run.

---

## How the reviewer works

On every pull request, the workflow:

1. Fetches the PR diff, title, description, open review threads, and recent commit history
2. Runs **Claude Opus** with the prompt from `docs/ai-review.md`
3. The reviewer spawns three sub-agents in parallel — `simpler-solution`, `goal-alignment`, and `architect` — to analyze the change from independent angles
4. Weighs sub-agent findings, verifies them against the diff, and writes a structured verdict to `/tmp/review.json`
5. Posts the review via GitHub API: inline comments, thread replies, and thread resolutions in one pass

**Incremental reviews:** When the bot has previously approved a PR, it only reviews the delta since that approval. No tokens wasted re-auditing settled code.

**Deduplication:** If the bot already approved the exact HEAD commit, it skips the run entirely.

---

## Skipping the reviewer

Add the `no-ai-review` label to a PR to skip the reviewer for that PR only.

The workflow also skips draft PRs automatically — convert to ready when you want a review.

---

## Requirements

- GitHub Actions enabled
- A [Claude.ai](https://claude.ai) Pro or Teams account **or** an [Anthropic API key](https://console.anthropic.com)

The reviewer uses the `opus` model. Claude.ai Pro/Teams accounts include API access via OAuth token. API key billing goes through your Anthropic account directly.

---

## Built by [human0](https://human0.ai)

human0 is building the platform for AI-operated companies — orchestrating agents, delegating tasks, and keeping humans in the loop at exactly the points that matter. This is the framework we run internally, open-sourced so any team can use it.
