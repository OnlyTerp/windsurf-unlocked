# Windsurf Unlocked

> Audited against Windsurf docs, pricing, and changelog on **2026-04-24**. This rewrite cuts the guide down to the highest-leverage setup and workflow advice for Windsurf in 2026.

*By Terp — [Terp AI Labs](https://x.com/OnlyTerp)*

<p>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/stargazers"><img alt="Stars" src="https://img.shields.io/github/stars/OnlyTerp/windsurf-unlocked?style=social"></a>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/network/members"><img alt="Forks" src="https://img.shields.io/github/forks/OnlyTerp/windsurf-unlocked?style=social"></a>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/blob/main/LICENSE"><img alt="MIT" src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
  <img alt="Audited April 2026" src="https://img.shields.io/badge/audited-April%202026-0ea5e9">
  <img alt="Windsurf 2.x" src="https://img.shields.io/badge/Windsurf-2.x-22c55e">
</p>

**📖 [Main guide](#why-this-guide-exists) · 🚀 [Starter kit](./starter/README.md) · 💬 [Prompts](./PROMPTS.md) · 📊 [Benchmarks](./BENCHMARKS.md) · 🧠 [Vault protocol](./VAULT_PROTOCOL.md) · 🗣️ [SOUL](./SOUL.md) · 🤝 [Contribute](./CONTRIBUTING.md)**

> 🎁 **New to Windsurf? Get $10 in extra usage** with this referral link: **[windsurf.com/refer?referral_code=kowwopt506rq1907](https://windsurf.com/refer?referral_code=kowwopt506rq1907)**. You get $10, I get $10. The guide stays free.

---

## Why This Guide Exists

Old Windsurf advice aged badly.

Three things changed:

1. **Pricing changed.** In March 2026, Windsurf moved self-serve users from monthly credits to **daily + weekly quota budgets** with optional extra usage. Read the official quota explainer before you buy: [Quota-Based Usage](https://docs.windsurf.com/windsurf/accounts/quota), [Pricing](https://windsurf.com/pricing).
2. **Windsurf 2.0 changed the workflow.** Agent Command Center, Spaces, Devin delegation, updated model picker, and better browser/MCP flows matter more than older “prompt trick” content. Source: [changelog](https://windsurf.com/changelog).
3. **The model landscape changed.** You now have fast, free, adaptive, frontier, and battle-group options inside one product. Source: [Cascade Models](https://docs.windsurf.com/plugins/cascade/models.md), [Arena Mode](https://docs.windsurf.com/windsurf/cascade/arena).

This version is intentionally shorter:

- less feature tourism
- more “use this when X”
- more links to focused companion docs
- fewer claims that go stale in two weeks

If you only read three sections, read [§2](#2-agent-command-center--spaces), [§4](#4-model-optimization--swe-16), and [§7](#7-directory-scoped-instructions-agentsmd).

---

## 60-Second Quickstart

If you want the fastest route to a strong Windsurf setup in any repo:

```bash
curl -fsSL https://raw.githubusercontent.com/OnlyTerp/windsurf-unlocked/main/starter/install.sh | bash
```

That installs:

- an [8-role subagent team](./starter/.windsurf/agents)
- reusable [skills](./starter/.windsurf/skills)
- opt-in [hooks](./starter/.windsurf/hooks.json)
- a `plans/` directory for persistent planning
- a `vault/` wiki scaffold for durable context
- an `AGENTS.md` constitution template
- curated [workflows](./starter/.windsurf/workflows)
- a curated [MCP config](./starter/.windsurf/mcp_config.json)

First five minutes after install:

1. Fill in `AGENTS.md`.
2. Turn on only the hooks you actually want.
3. Keep routine work on a cheap/free model.
4. Use Plan mode before any non-trivial feature.
5. Put one task per Space.

Details: [starter/README.md](./starter/README.md).

---

## What Changed Since Older Guides

### The important changes

| Change | Why it matters | Source |
|---|---|---|
| Quotas replaced credits for self-serve | You now manage **daily + weekly allowance**, not one monthly credit pool | [Quota docs](https://docs.windsurf.com/windsurf/accounts/quota) |
| Pro / Max / Teams pricing changed | Current self-serve pricing is **Free / $20 Pro / $200 Max / $40 Teams seat** | [Pricing](https://windsurf.com/pricing) |
| Adaptive model router landed | Good default when you want model selection help and visible per-token pricing | [Changelog](https://windsurf.com/changelog) |
| Windsurf 2.0 shipped | Agent Command Center, Spaces, Devin in Windsurf, browser improvements | [Changelog](https://windsurf.com/changelog) |
| Arena mode matured | Model comparison now has real workflow value if you use worktrees correctly | [Arena docs](https://docs.windsurf.com/windsurf/cascade/arena) |
| Plan mode writes external plan files | Better continuity than in-chat planning | [Modes docs](https://docs.windsurf.com/windsurf/cascade/modes) |
| MCP transports are broader now | Windsurf supports stdio, Streamable HTTP, and SSE; pick the maintained transport for each server | [MCP docs](https://docs.windsurf.com/windsurf/cascade/mcp) |

### The practical implication

The best Windsurf users in 2026 are not the ones with the fanciest prompts.

They are the ones who:

- keep project rules short
- use Plan mode before Code mode
- spend frontier quota only on hard tasks
- isolate parallel work with worktrees or Spaces
- store durable context in files, not just auto-memories

---

## Best-Value Setup in 10 Minutes

Use this order:

1. **Install the starter kit** into the repo you care about.
2. **Write a real `AGENTS.md`** with commands, invariants, and “never do” rules.
3. **Keep routine work on SWE-1.5 or another low-cost/free model.**
4. **Use Plan mode** for anything that spans multiple files.
5. **Use one Space per task** in Agent Command Center.
6. **Use MCP only for systems you actually need**: GitHub, docs, issue tracker, database, browser/devtools.
7. **Only delegate to Devin** when background execution is genuinely better than staying local.

That gets most of the value without turning Windsurf into a toy box.

---

## Table of Contents

- [1. Cascade Modes: Code / Plan / Ask](#1-cascade-modes-code--plan--ask)
- [2. Agent Command Center & Spaces](#2-agent-command-center--spaces)
- [3. Devin in Windsurf — Cloud Delegation](#3-devin-in-windsurf--cloud-delegation)
- [4. Model Optimization — SWE 1.6](#4-model-optimization--swe-16)
- [5. Skills System](#5-skills-system)
- [6. MCP Server Integration](#6-mcp-server-integration)
- [7. Directory-Scoped Instructions (AGENTS.md)](#7-directory-scoped-instructions-agentsmd)
- [8. Hooks](#8-hooks)
- [9. Memories & Rules](#9-memories--rules)
- [10. Workflows](#10-workflows)
- [11. Worktrees — Parallel Cascade](#11-worktrees--parallel-cascade)
- [12. Arena Mode](#12-arena-mode)
- [13. Browser, Docs, and Web Search](#13-browser-docs-and-web-search)
- [14. App Deploys](#14-app-deploys)
- [15. Starter Kit](#15-starter-kit)
- [16. Prompt Library](#16-prompt-library)
- [17. Custom Subagents](#17-custom-subagents)
- [18. Benchmarks](#18-benchmarks)
- [19. Security and Hygiene](#19-security-and-hygiene)
- [20. Context Engineering — The Agentic Wiki](#20-context-engineering--the-agentic-wiki)
- [21. Spec-Driven Development with Cascade](#21-spec-driven-development-with-cascade)
- [22. Skills Ecosystem — `gh skill`, AgentSkills.io, and Viral Skills](#22-skills-ecosystem--gh-skill-agentskillsio-and-viral-skills)
- [23. Observability — Evals for Cascade](#23-observability--evals-for-cascade)

---

## 1. Cascade Modes: Code / Plan / Ask

Source: [Cascade Modes](https://docs.windsurf.com/windsurf/cascade/modes)

Use the modes correctly:

| Mode | Use it for | Don’t use it for |
|---|---|---|
| **Ask** | learning, explaining code, reading docs, investigating | implementation |
| **Plan** | any task where scope is still fuzzy | tiny edits |
| **Code** | implementation once intent is clear | first-pass design on messy tasks |

My rule:

- **Ask** when the goal is understanding.
- **Plan** when the goal is deciding.
- **Code** when the goal is shipping.

Why Plan mode matters now:

- it can produce an external markdown plan file
- that file survives long sessions better than chat-only planning
- it reduces “agent wandered off” failures

If a task touches more than one file, Plan mode is usually the right first move.

---

## 2. Agent Command Center & Spaces

Source: [Windsurf 2.0 changelog](https://windsurf.com/changelog)

Windsurf 2.0 made this the real home screen.

What matters:

- **Agent Command Center** gives you one view of local + cloud agent sessions.
- **Spaces** group sessions, PRs, files, and context around one task.

Best practice:

- one bug = one Space
- one feature = one Space
- one cleanup campaign = one Space

Don’t mix unrelated work in one Space just because it’s the same repo. That defeats the entire point.

Use Spaces for:

- parallel implementation tracks
- one feature with one planning session plus one coding session
- comparing model or subagent approaches without losing context

---

## 3. Devin in Windsurf — Cloud Delegation

Source: [Devin in Windsurf](https://docs.windsurf.com/windsurf/devin)

Windsurf now exposes Devin Cloud directly in the IDE.

What it is good for:

- long-running refactors
- background bugfix work
- tasks that benefit from a separate VM and independent iteration
- work you want to review asynchronously

What it is not good for:

- a 2-line edit
- simple navigation or Q&A
- tasks where you still don’t understand the requirements

Important caveats:

- it is included with self-serve Pro, Max, and Teams plans, but **billing consumes shared quota and extra usage**
- access is rolling out gradually; if you don’t see Devin Cloud, the docs say to log out and back in
- Enterprise users should ask their admin for access

Delegate when you want **parallelism**, not when you want **faster typing**.

---

## 4. Model Optimization — SWE 1.6

Sources: [Cascade models](https://docs.windsurf.com/plugins/cascade/models.md), [quota docs](https://docs.windsurf.com/windsurf/accounts/quota), [pricing](https://windsurf.com/pricing), [Arena docs](https://docs.windsurf.com/windsurf/cascade/arena), [changelog](https://windsurf.com/changelog)

This is where most people waste money and context.

### Current pricing snapshot

| Plan | Price | Included allowance | Extra usage |
|---|---|---|---|
| Free | $0 | Light | No |
| Pro | $20/mo | Standard | Yes |
| Max | $200/mo | Heavy | Yes |
| Teams | $40/user/mo | Standard | Yes |
| Enterprise | Contact sales | Custom | Custom |

### What changed

Self-serve Windsurf no longer works like “500 monthly credits.” It is now:

- **daily allowance**
- **weekly allowance**
- optional **extra usage** after you hit quota

### Practical model rules

1. **Use free or cheap models for routine edits.**
   - The quota docs explicitly recommend free models like **SWE-1.5** for routine tasks.
2. **Use one frontier model consistently per task.**
   - Repeated requests to the same model improve caching and reduce waste.
3. **Use Adaptive when you want a strong default and don’t want to micromanage.**
4. **Use Arena only when comparison is worth the cost.**
   - Arena charges for each model separately.

### Simple model strategy

| Task shape | Recommended starting point |
|---|---|
| quick fix, grep, small refactor | SWE-1.5 or another low-cost/free option |
| medium feature with some ambiguity | Adaptive or your preferred mid-cost model |
| hard design problem / difficult refactor | a frontier model |
| “I want two competing approaches” | Arena with worktrees |

The point is not “always use the smartest model.” The point is “spend intelligence where it changes the outcome.”

---

## 5. Skills System

Skills are where Windsurf stops being “chat in an editor” and starts becoming a reusable operating system.

Use a **skill** when you want:

- a multi-step procedure
- bundled files/scripts/templates
- something Cascade should be able to trigger based on intent

Use a **workflow** when you want:

- a manual slash command
- a repeatable trajectory you explicitly invoke yourself

The starter kit already includes the right foundation:

- `wiki-query`
- `wiki-update`
- `planning-with-files`
- `pr-ready`
- `secret-scrubber`
- `test-backfill`
- `ast-grep`
- `compact-hygiene`

If you only add one custom skill to your own repo, add the task that your team repeats every week.

---

## 6. MCP Server Integration

Source: [MCP docs](https://docs.windsurf.com/windsurf/cascade/mcp)

MCP is worth it when the tool unlocks a real workflow:

- GitHub / GitLab
- docs or internal knowledge
- issue tracker
- browser/devtools
- database
- deployment platform

Rules:

1. Prefer **official or maintained** servers.
2. Prefer the transport the server actively maintains: **stdio**, **Streamable HTTP**, or **SSE**.
3. Avoid stale setup guides that reference old config shapes.
4. Install only the servers you actually use.

Bad MCP setups create tool spam.
Good MCP setups remove tab-switching.

### Curated MCP list

Additions to this list should follow [CONTRIBUTING.md](./CONTRIBUTING.md): maintained server, docs, Streamable HTTP or stdio preferred, usable without proprietary paid infra, and >30 days without known critical bugs.

| Server | Use it for | Transport | Source |
|---|---|---|---|
| GitHub MCP | issues, PRs, repo automation | stdio or remote HTTP | [GitHub MCP server](https://github.com/github/github-mcp-server) |
| Filesystem MCP | scoped local file access outside the workspace | stdio | [Model Context Protocol servers](https://github.com/modelcontextprotocol/servers) |
| Memory MCP | small local knowledge graph | stdio | [Model Context Protocol servers](https://github.com/modelcontextprotocol/servers) |
| PostgreSQL MCP | read-only database inspection | stdio | [Model Context Protocol servers](https://github.com/modelcontextprotocol/servers) |
| Fetch MCP | fetch web content through an MCP tool | stdio | [Model Context Protocol servers](https://github.com/modelcontextprotocol/servers) |

Keep the list short. If a server exposes too many tools, disable the ones you do not use so you stay under Cascade’s 100-tool limit.

---

## 7. Directory-Scoped Instructions (AGENTS.md)

Source: [Memories & Rules docs](https://docs.windsurf.com/windsurf/cascade/memories)

This is still the highest-ROI file in the whole repo.

What `AGENTS.md` should contain:

- real commands
- project invariants
- testing expectations
- forbidden moves
- ownership/context pointers

Why it beats long prompts:

- it is committed
- it is reusable
- it scopes naturally by directory
- it is more reliable than hoping auto-memories fire

Keep it short.

If the file is full of vibes, Cascade will ignore the important parts.

Use subdirectory `AGENTS.md` files only when that folder genuinely needs different rules.

---

## 8. Hooks

Hooks are where you enforce discipline without remembering to ask for it every time.

Good hook candidates:

- secret scan before writes/commits
- auto-format
- telemetry/logging
- worktree setup

Bad hook candidates:

- expensive or flaky network calls
- anything that blocks normal work too often

The starter kit ships hooks **disabled by default**. That is the right default. Turn on only what you trust.

---

## 9. Memories & Rules

Source: [Memories & Rules docs](https://docs.windsurf.com/windsurf/cascade/memories)

Use the right persistence layer:

| Mechanism | Best for | Shared? |
|---|---|---|
| **Memories** | one-off local facts | No |
| **Rules** | repeatable behavior constraints | Yes, if committed |
| **AGENTS.md** | repo or folder operating instructions | Yes |
| **Skills** | reusable procedures with assets | Yes |
| **Workflows** | manual slash-command trajectories | Yes |

Key rule from the docs:

> If you want durable, team-visible knowledge, prefer **Rules** or **AGENTS.md** over auto-generated Memories.

That is why this repo leans so hard on files.

---

## 10. Workflows

Source: [Workflows docs](https://docs.windsurf.com/windsurf/cascade/workflows)

Workflows are markdown playbooks invoked manually with `/name`.

Use them for:

- PR review routines
- release steps
- test/fix loops
- rollout checklists
- deployment sequences

Do **not** use workflows as a substitute for project rules.

Rule of thumb:

- **Rules** shape behavior.
- **Skills** automate reusable procedures.
- **Workflows** give you named trajectories you explicitly start.

---

## 11. Worktrees — Parallel Cascade

Worktrees are how you do parallel agent work without contaminating one branch or one file tree.

Use them when:

- comparing model outputs
- running multiple subagents
- splitting one large feature into isolated branches
- using Arena seriously

Do not run every experiment in your main working tree and call it “parallel.”

That just creates merge anxiety.

---

## 12. Arena Mode

Source: [Arena docs](https://docs.windsurf.com/windsurf/cascade/arena)

Arena is for **comparison**, not daily driving.

Good uses:

- compare two models on the same hard task
- test whether a frontier model is actually worth it
- explore two designs before choosing one

Important details:

- each model gets its **own worktree**
- you pay the cost of **each** model used
- battle groups can reduce decision fatigue, but still cost twice the displayed per-model amount because two models run

If you are not going to compare outputs carefully, don’t use Arena.

---

## 13. Browser, Docs, and Web Search

Source: [Web and Docs Search](https://docs.windsurf.com/windsurf/cascade/web-search)

This is underrated because people use it sloppily.

Use:

- `@docs` for official docs
- `@web` when recency matters
- pasted URLs when you want a specific page parsed

The docs note that page reads happen locally on your device/network. That matters if you are behind VPN or reading private/internal docs through your own browser context.

Best use:

- dependency upgrade research
- “what changed in X?”
- official API docs lookup during implementation

Worst use:

- vague broad searches that balloon context

---

## 14. App Deploys

Source: [App Deploys docs](https://docs.windsurf.com/windsurf/cascade/app-deploys)

Useful for quick previews. Not a substitute for real production deployment discipline.

What it does today:

- deploys supported JS/static apps
- currently targets Netlify
- gives you a public preview URL
- can create a `windsurf_deployment.yaml` for redeploy flow

What to remember:

- preview deployments are public
- your code is uploaded
- docs explicitly frame this as preview-oriented, not sensitive-production-oriented

Good for demos. Be cautious for anything private.

---

## 15. Starter Kit

The [starter kit](./starter/README.md) is the practical core of this repo.

Install it if you want:

- a ready-made `.windsurf/` layout
- role-based subagents
- a real planning system
- wiki scaffolding
- reusable skills and workflows

Skip it only if you already have a better house style in your repo.

---

## 16. Prompt Library

Use [PROMPTS.md](./PROMPTS.md) as a cookbook, not a religion.

The right prompt library should:

- shorten ramp time
- give you reliable starter phrasing
- not replace project-specific rules

If you are copying giant prompts into every conversation, your repo instructions are probably too weak.

---

## 17. Custom Subagents

This is still one of the most useful patterns in the repo.

The starter kit ships:

- `@architect`
- `@implementer`
- `@reviewer`
- `@tester`
- `@security`
- `@docs`
- `@perf`
- `@shipper`

This works because each role has:

- narrower responsibility
- less context bloat
- clearer success criteria

Do not create 20 subagents because it looks cool.
Create only the ones that map to real recurring roles in your workflow.

---

## 18. Benchmarks

Use [BENCHMARKS.md](./BENCHMARKS.md) for one thing:

**task-shaped decision making**.

Good benchmark questions:

- which model is faster on multi-file features?
- which model is cheaper for debug traces?
- which setup has lower harness overhead?

Bad benchmark question:

- “which model is best?”

There is no universal best. Only best for a workload.

---

## 19. Security and Hygiene

Minimum bar:

- never paste secrets into prompts if you can avoid scoped auth instead
- use `.codeiumignore` / repo ignore rules to exclude junk and sensitive paths
- enable secret scanning if your team is going to lean on agent automation
- avoid giant noisy sessions that pack unrelated sensitive context together

The more autonomous your setup gets, the more important boring hygiene becomes.

---

## 20. Context Engineering — The Agentic Wiki

Companion doc: [VAULT_PROTOCOL.md](./VAULT_PROTOCOL.md)

This is the best long-term memory pattern in the repo.

Use `vault/` for:

- decisions
- services
- incidents
- glossary
- maps of content

Why it works:

- markdown is reviewable
- context compounds across sessions
- it is better for durable team memory than hoping retrieval guesses right

Use the wiki for **facts and decisions**, not essay writing.

---

## 21. Spec-Driven Development with Cascade

This is the anti-scope-drift layer.

Use a spec/plan/PRD file when:

- the task is expensive to undo
- multiple files or people are involved
- the request is under-specified

Simple pattern:

1. write the plan
2. agree on the constraints
3. implement from the file
4. review against the file

This is boring.
That is why it works.

---

## 22. Skills Ecosystem — `gh skill`, AgentSkills.io, and Viral Skills

Portable skill formats are getting more important across coding tools.

That matters for Windsurf because good skills are increasingly:

- reusable across tools
- auditable as files
- easier to share and version

My advice:

- import carefully
- audit every external skill before trusting it
- prefer a smaller number of battle-tested skills over a giant graveyard of half-working ones

The ecosystem is real.
The hype is also real.
Be selective.

---

## 23. Observability — Evals for Cascade

If you care about serious team usage, you need more than “felt good.”

Use some combination of:

- benchmark tasks
- PR review outcomes
- failure pattern notes
- logging via hooks
- Windsurf analytics where available

The starter kit includes observability patterns, but they should stay **opt-in**.

The point of observability is not surveillance.
It is faster feedback on what actually helps.

---

## Companion Files

- [**`starter/`**](./starter/) — the installable working setup
- [**`PROMPTS.md`**](./PROMPTS.md) — copy-paste prompt library by task phase
- [**`BENCHMARKS.md`**](./BENCHMARKS.md) — workload-shaped performance and cost comparisons
- [**`VAULT_PROTOCOL.md`**](./VAULT_PROTOCOL.md) — how to run the wiki pattern well
- [**`SOUL.md`**](./SOUL.md) — global rules/personality layer
- [**`CONTRIBUTING.md`**](./CONTRIBUTING.md) — how to improve this repo without adding noise

---

## If You Only Steal 7 Ideas From This Repo

1. Put real rules in `AGENTS.md`.
2. Use Plan mode before Code mode on multi-file work.
3. Store durable knowledge in files, not just memories.
4. Keep one task per Space.
5. Use cheap/free models for routine work.
6. Use worktrees when comparing approaches.
7. Keep your setup boring enough that you will actually maintain it.

---

## Final Take

Windsurf in 2026 is no longer just “Cursor but different.”

The real advantage is the stack around the model:

- planning
- rules
- skills
- worktrees
- Spaces
- browser/docs access
- MCP
- optional cloud delegation

Most people do not need more tricks.
They need a cleaner operating model.

That is what this repo should help with.
