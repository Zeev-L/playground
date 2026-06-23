# skills-marketplace — personal Claude Code skill marketplace

### 🔎 Browse the interactive catalog → **https://zeev-l.github.io/skills-marketplace/**
_Filter 221 skills by role, search, and copy install commands — including “Copy all install commands.”_

---

A personal [Claude Code](https://claude.com/claude-code) marketplace that **references** skills
living in curated open-source repos. Most plugins point at **my own Zeev-L clones** of the upstream
repos (for backup + stability); each clone auto-syncs from its upstream daily via a GitHub Action.

## Install

```bash
# 1. Add this marketplace
claude plugin marketplace add Zeev-L/skills-marketplace

# 2. Install any plugin (see table below for names)
claude plugin install gstack@skills-marketplace
claude plugin install pm-product-discovery@skills-marketplace
claude plugin install marketing-skills@skills-marketplace
```

In an interactive session you can use the slash-command equivalents:
`/plugin marketplace add Zeev-L/skills-marketplace` then `/plugin install <name>@skills-marketplace`.
Update everything later with `claude plugin marketplace update skills-marketplace`.

> **HTTPS install note.** 14 of the plugins install with no setup — the 13 `git-subdir` plugins
> (everything from `pm-skills` and `omri-a.-cc-stuff`) plus local `text-tools`, because they use explicit
> HTTPS URLs. The **4 whole-repo plugins** — **`agent-skills`, `gstack`, `awesome-pm-skills`,
> `marketing-skills`** — are `github` sources that Claude Code clones over **SSH**. On a machine without a
> GitHub SSH key that will fail with `Host key verification failed`. Fix it once, either:
>
> ```bash
> # Option A — make git use HTTPS for GitHub (recommended; matches a gh-token setup)
> git config --global url."https://github.com/".insteadOf "git@github.com:"
> ```
>
> Option B — set up a GitHub SSH key (https://docs.github.com/authentication/connecting-to-github-with-ssh).

## Plugins (18)

| Plugin | What it is | Upstream source / attribution | Backup clone |
|---|---|---|---|
| `text-tools` | My own text-manipulation skills (e.g. `bulletize`) | Zeev-L (original) | n/a — local to this repo |
| `agent-skills` | Production-grade software-engineering skills (spec, plan, TDD, review, ship) | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) · Addy Osmani · MIT | `Zeev-L/addyosmani-agent-skills` |
| `gstack` | 60+ engineering skills: code review, debugging, QA, deploy, security | [garrytan/gstack](https://github.com/garrytan/gstack) · Garry Tan · MIT | `Zeev-L/gstack` |
| `awesome-pm-skills` | 28+ AI-powered PM skills from Lenny's Podcast | [menkesu/awesome-pm-skills](https://github.com/menkesu/awesome-pm-skills) · menkesu · MIT | `Zeev-L/awesome-pm-skills` |
| `pm-product-discovery` | Teresa Torres discovery: opportunity-solution trees, assumption tests, interview scripts | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-product-strategy` | Strategy canvases: Lean/Business-Model, Porter's, SWOT, Ansoff | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-toolkit` | Core PM toolkit skills | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-execution` | Delivery / project management: sprint planning, retros, OKRs, stakeholder maps | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-market-research` | Market and user research skills | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-ai-shipping` | Shipping AI features: intended-vs-implemented, shipping artifacts | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `pm-data-analytics` | A/B test analysis, cohort analysis, SQL queries | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) · Paweł Huryn · MIT | `Zeev-L/pm-skills` |
| `marketing-skills` | SaaS PMM + biz-dev: GTM/launch, positioning, pricing, sales-enablement, CRO | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) · Corey Haines · MIT | `Zeev-L/marketingskills` |
| `x` | Post and read tweets on X (Twitter) from Claude Code | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |
| `gdoc-math` | Markdown + LaTeX → native Google Doc with editable equations | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |
| `find-session` | Search past Claude Code conversations by keyword; get session IDs | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |
| `setup-pulse` | Install the claude-pulse statusline for token-usage monitoring | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |
| `claude-reviewer` | Review a project's `.claude/` setup against best practices | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |
| `skill-reviewer` | Evaluate any skill's design quality and flag anti-patterns | [omriariav/omri-cc-stuff](https://github.com/omriariav/omri-cc-stuff) · Omri Ariav | `Zeev-L/omri-a.-cc-stuff` |

## How the backup / sync works

Each external plugin is referenced from a **clone under my own `Zeev-L` account**, not the original
repo, so the marketplace keeps working even if an upstream is renamed or deleted. Every clone carries
a `.github/workflows/sync-upstream.yml` Action that runs daily (and on demand) to merge the latest
from upstream and push, so the clones stay current. `text-tools` is my own original content and lives
directly in this repo.

All referenced upstreams are **MIT-licensed**. Attribution to each original author is preserved above
and in each clone's retained `LICENSE`.

## Notes

- `gstack` includes skills that execute commands / automate a browser (`browse`, `scrape`,
  deploy skills). It's a popular MIT repo by Garry Tan — treat those skills like any code that
  runs locally.
