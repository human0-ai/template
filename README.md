# human0 Repository Template

> **AI agents that own your codebase end-to-end.** This template wires a fully autonomous development loop into any GitHub repository — agents build, an AI reviewer approves, and approved PRs merge themselves.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

---

## What is this?

This is a starter template for **AI-agent-driven development**. Fork it, add your API key, and your repository gains:

- **Automated AI code review** — every pull request gets reviewed by Claude, which posts inline comments and renders a verdict (`APPROVE` or `REQUEST_CHANGES`)
- **Auto-merge on approval** — when the AI reviewer approves and CI is green, the PR merges itself, no human click needed
- **Agent guidelines** — an `AGENTS.md` file that tells every AI agent working in this repo exactly how to operate: your structure, principles, and workflow

It's the same setup [human0.ai](https://human0.ai) uses internally to run autonomous companies with AI agents.

---

## 5-Minute Quickstart

**Fork, configure, and run your first AI-reviewed PR in under 5 minutes.**

### 1. Fork this repo

Click **Use this template** (or fork) to create your own copy.

### 2. Add your API credential

Go to **Settings → Secrets and variables → Actions → New repository secret** and add one of:

| Secret name | Value |
|---|---|
| `ANTHROPIC_API_KEY` | Your [Anthropic API key](https://console.anthropic.com/) |
| `CLAUDE_CODE_OAUTH_TOKEN` | Your Claude.ai OAuth token (alternative) |

### 3. Enable workflow permissions

Go to **Settings → Actions → General → Workflow permissions** and select:
- ✅ **Read and write permissions**
- ✅ **Allow GitHub Actions to create and approve pull requests**

### 4. Customize your agent guidelines

Edit `AGENTS.md` to reflect your project:
- Replace the `## Structure` section with your actual directory layout
- Add any project-specific conventions your agents should follow
- The `## Workflow` and `## AI Reviewer` sections are ready to use as-is

### 5. Open a pull request

Create any PR — the AI reviewer runs automatically. On approval, enable auto-merge and the PR lands itself.

---

## How it Works

```
Developer or AI agent opens a PR
         │
         ▼
GitHub Actions triggers ai-review.yml
         │
         ▼
human0-ai/code-review action runs
  ├── Three parallel sub-reviewers analyze the diff
  │     ├── Simpler-solution: is there a simpler approach?
  │     ├── Goal-alignment: does this serve the stated purpose?
  │     └── Architect: is the structure sound?
  ├── Findings consolidated into a single review
  └── Verdict: APPROVE or REQUEST_CHANGES
         │
    APPROVE + CI green
         │
         ▼
    Auto-merge fires → PR lands
```

**Agent loop:** AI agents in this repo follow the workflow in `AGENTS.md` — they open draft PRs early, address reviewer threads autonomously, and drive each PR to merge without requiring human intervention for routine changes.

---

## What's Included

| File | Purpose |
|---|---|
| `AGENTS.md` | Agent guidelines — every AI agent reads this on every run |
| `CLAUDE.md` | Symlink to `AGENTS.md` (for tools that look for either name) |
| `docs/ai-review.md` | Reviewer instructions — customize to set your review bar |
| `.github/workflows/ai-review.yml` | The automation trigger |

---

## Integrating into an Existing Repo

You don't have to fork this template. To add AI code review to an existing project:

1. Copy `.github/workflows/ai-review.yml` into your repo
2. Copy `docs/ai-review.md` (or write your own review standards)
3. Add the `ANTHROPIC_API_KEY` or `CLAUDE_CODE_OAUTH_TOKEN` secret
4. Enable workflow write permissions (step 3 above)
5. Optionally add `AGENTS.md` with your project guidelines

---

## Customizing Review Behavior

Edit `docs/ai-review.md` to change how the AI reviewer evaluates PRs. The default standard is:
- Correctness over cleverness
- Simplicity over abstractions
- Security and edge case coverage
- Stale plan file cleanup

Add domain-specific rules — "never use `any` in TypeScript," "all DB queries must go through the repository layer," etc.

---

## Requirements

- A GitHub repository (public or private)
- An Anthropic API key **or** a Claude.ai OAuth token
- GitHub Actions enabled (free for public repos; free tier minutes for private)

**Estimated cost:** A typical code review consumes ~10,000–50,000 tokens. At Anthropic API prices, this is roughly $0.01–$0.15 per review depending on PR size and the model tier used.

---

## FAQ

**Does this work with private repositories?**  
Yes. The action runs inside GitHub Actions and never sends your code to an external server beyond Anthropic's API. Anthropic's [data usage policy](https://www.anthropic.com/legal/aup) applies.

**Can I use a different AI model?**  
The action uses Claude (via Anthropic). Model selection is handled inside the `human0-ai/code-review` action — see that repo for configuration options.

**What if the AI reviewer is wrong?**  
Push back in the PR thread. The reviewer isn't infallible — if you disagree, reply with reasoning. The reviewer is designed to consider counter-arguments. If you can't reach consensus, defer the point to a `/.plans/` follow-up and link it in the thread, then the reviewer will approve.

**How do I disable AI review for a specific PR?**  
Add the `no-ai-review` label to the PR. The workflow skips labeled PRs.

**Does auto-merge merge immediately?**  
Auto-merge fires when: (1) the AI reviewer approves, and (2) all required status checks pass. If you have branch protection rules requiring human approval, those still apply.

**Can multiple AI agents work in the same repo simultaneously?**  
Yes. The `concurrency` group in the workflow ensures only one review runs per PR at a time, preventing conflicts.

---

## Related

- **[human0-ai/code-review](https://github.com/human0-ai/code-review)** — The AI reviewer action powering this template
- **[human0.ai](https://human0.ai)** — The platform for running fully autonomous AI companies

---

## License

Apache 2.0 — see [LICENSE](LICENSE).
