# Windsurf Unlocked

> **Tested on Windsurf 2.0.50 — April 2026** · The community power-user bible for Cascade, Agent Command Center, and Devin-in-Windsurf

### Every feature Cascade ships that most people aren't using — configured properly

*By Terp — [Terp AI Labs](https://x.com/OnlyTerp)*

<p>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/stargazers"><img alt="Stars" src="https://img.shields.io/github/stars/OnlyTerp/windsurf-unlocked?style=social"></a>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/network/members"><img alt="Forks" src="https://img.shields.io/github/forks/OnlyTerp/windsurf-unlocked?style=social"></a>
  <a href="https://github.com/OnlyTerp/windsurf-unlocked/blob/main/LICENSE"><img alt="MIT" src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
  <img alt="Windsurf 2.0.50" src="https://img.shields.io/badge/Windsurf-2.0.50-0ea5e9">
  <img alt="SWE 1.6 Fast" src="https://img.shields.io/badge/SWE%201.6%20Fast-950%20tok%2Fs-22c55e">
  <img alt="PRs welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen">
</p>

**📖 [Main guide](#what-this-guide-covers) · 🚀 [Starter kit](./starter/README.md) · 💬 [Prompts](./PROMPTS.md) · 📊 [Benchmarks](./BENCHMARKS.md) · 🤝 [Contribute](./CONTRIBUTING.md)**

> 🎁 **New to Windsurf? Get $10 in free credits** with this referral link: **[windsurf.com/refer?referral_code=kowwopt506rq1907](https://windsurf.com/refer?referral_code=kowwopt506rq1907)** — you get $10, I get $10. The whole guide is free; this is the only ask.

---

## 60-Second Quickstart

If you want to install the full power-user setup into one of your repos right now:

```bash
# In the root of the repo you want to upgrade
curl -fsSL https://raw.githubusercontent.com/OnlyTerp/windsurf-unlocked/main/starter/install.sh | bash
```

That drops in:

- An [**8-role subagent team**](./starter/.windsurf/agents) (architect / implementer / reviewer / tester / security / docs / perf / shipper) — pattern popularized by Claude Code, covered in [§17](#17-custom-subagents)
- Pre-wired [**hooks**](./starter/.windsurf/hooks) (secret scanner, Langfuse observability, auto-formatter, worktree seeder) — all **disabled by default**, flip on what you want
- [**Curated skills**](./starter/.windsurf/skills) (wiki-update, wiki-query, pr-ready, test-backfill, secret-scrubber)
- A [**`vault/` scaffold**](./starter/vault) for the agentic-wiki pattern from [§20](#20-context-engineering--the-agentic-wiki)
- An [**`AGENTS.md` template**](./starter/AGENTS.md) constitution to fill in for your project
- A [**curated MCP config**](./starter/.windsurf/mcp_config.json) using Streamable HTTP (not deprecated SSE)
- [**Spec-Driven workflows**](./starter/.windsurf/workflows) (`plan-then-implement`, `speckit-specify`, `speckit-plan`, `megaplan`)

First 5 minutes after install: edit `AGENTS.md`, flip on the hooks you want, verify with `@reviewer Read AGENTS.md and list invariants that need filling in`. Done.

Details and customization: [**starter/README.md**](./starter/README.md).

---

## Companion Files

- [**`starter/`**](./starter/) — the actual working `.windsurf/` setup. Clone it, install it, fork it.
- [**`PROMPTS.md`**](./PROMPTS.md) — 60+ battle-tested Cascade prompts organized by phase (plan / implement / refactor / debug / test / review / security / perf / docs / ship / teach / meta / edge cases).
- [**`BENCHMARKS.md`**](./BENCHMARKS.md) — open-source benchmark methodology + published vendor numbers + community-contributed real-world data. PR your numbers.
- [**`VAULT_PROTOCOL.md`**](./VAULT_PROTOCOL.md) — drop-in AGENTS.md block for the Karpathy-style Agentic Wiki (compounding markdown memory that beats RAG for internal docs).
- [**`SOUL.md`**](./SOUL.md) — the global-rules personality layer that turns Cascade from a polite assistant into an actual collaborator. Install via the one-liner in [§9 SOUL](#soul--the-global-rules-personality-layer) or paste the five rule pillars into `~/.codeium/windsurf/memories/global_rules.md`.
- [**`CONTRIBUTING.md`**](./CONTRIBUTING.md) — how to add prompts, skills, subagents, hooks, benchmarks, MCP servers, and translations.

**Jump straight to the new stuff: [⚡ Unlocked Power Moves](#unlocked-power-moves)** — 16 viral techniques with copy-paste recipes, led by the Apr 16 [Opus 4.7 + Thinking Levels](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026) drop and the free-tier [Kimi K2 Swarm](#15-the-kimi-k2-free-swarm--6-parallel-agents-for-0).

If you only have 10 minutes, read [§17 Custom Subagents](#17-custom-subagents) and [§20 Context Engineering](#20-context-engineering--the-agentic-wiki), then install the starter kit. That's the 80% of the value.

**⭐ If this saves you even one hour, star the repo — it makes the work worth doing.**


---

## What This Guide Covers

Windsurf 2.0 shipped on **April 15, 2026** — hours after the first draft of this guide went up. It's the biggest single release Cascade has ever had: a full Agent Command Center, Spaces, and Devin delegation straight from the editor, layered on top of the already-deep autonomous feature set (skills, MCP, hooks, worktrees, Arena Mode, hooks, memories).

Cascade now has most of the "harness" capabilities that tools like **Hermes**, **OpenClaw**, and **Claude Code** charge you to assemble yourself — graph-aware memory, persistent plans, parallel agents, cloud delegation, observability hooks, multi-provider model selection — and with **SWE 1.6 Fast** on Cerebras at 950 tok/s it runs at a speed that makes those harnesses feel slow and expensive.

This guide shows you how to configure every surface properly, wire them into real tools, and build production workflows that rival anything you'd get from a bespoke harness.

**Not a guide to build features Windsurf lacks. A guide to unlock what's already there.**

---

## What's New in Windsurf 2.0 (April 2026)

If the last time you looked at Windsurf was 1.9 or earlier, the big changes are:

| New in 2.0 | Why it matters |
|------------|----------------|
| **Agent Command Center** | Kanban-style view of every agent you have running — local Cascade and cloud Devin — in one place. |
| **Spaces** | Group agent sessions, PRs, files, and shared context under a single task. Agents spawned inside a Space inherit the Space's context automatically. |
| **Devin in Windsurf** | Cloud agent, full VM, desktop + browser + computer-use, included with every self-serve plan. Up to **$50 in extra usage** credits on first GitHub connect. |
| **Windsurf Browser** | Chromium-based browser integrated into the editor with a Cascade tool that reads page contents (replaces the old browser-preview-only flow). |
| **Refreshed Cascade sidebar** | Faster initial load, better `.gitignore` / `.codeiumignore` handling. |
| **SWE 1.6 + SWE 1.6 Fast** | New default SWE model, 10%+ better on SWE-Bench Pro, parallel-tool-call happy. 950 tok/s on Cerebras via SWE 1.6 Fast. **Free for everyone for 3 months.** |
| **Adaptive model router** | One slot in the model picker that picks the right model per-task at a fixed per-token rate. Promo: 0.50 USD / 1M input, 2 USD / 1M output, 0.10 USD / 1M cache read. |
| **Pricing-aware model picker** | Per-model input/output/cache-read rates visible inline. Prompt cache timer in the context-window indicator. Token counts on every response card. |

Bumping to 2.0 is worth it for the Agent Command Center alone, but the sleeper feature is that **Cascade now streams into the Agent Command Center in real time and Devin sessions live alongside local sessions in the same Kanban** — no more context-switching between browser tabs and editor.

---

## What's Hot Right Now (April 14–17, 2026)

Even in the 72 hours since Windsurf 2.0 dropped, the broader agent/coding ecosystem moved. Here's what's trending *this week* and where it lands in this guide:

| Drop / trend | Date | What it is | Where it lands |
|---|---|---|---|
| [**Claude Opus 4.7 + Windsurf thinking-level picker**](https://www.anthropic.com/news/claude-opus-4-7) | **Apr 16** | Anthropic's most capable GA model — 1M context, 128K output, high-res vision (2576px), better agentic coding. Windsurf added it to Cascade the same day with promo credit pricing and each thinking tier exposed as a separate, credit-priced entry in the model picker — up to a MAX tier you can pick per-message without typing a keyword. Claude Code CLI exposes tiers via [`/effort` + `ultrathink` keywords](https://claudelog.com/faqs/what-is-ultrathink/); Anthropic's Cowork / Chat surfaces dropped the manual picker for [adaptive thinking](https://platform.claude.com/docs/en/build-with-claude/adaptive-thinking). Cascade is the only harness that puts every tier in the picker with visible per-message credit cost. | [Power Move #0](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026), [§16 Model Optimization](#16-model-optimization--swe-16-adaptive-battle-groups) |
| [**Kimi K2 in the Cascade picker — free/promo tier**](https://www.windsurf.com/changelog) | Jul 2025 → ongoing | Windsurf has shipped successive [low-credit](https://www.threads.com/@pahud/post/DMeZLopuyhb) and [free](https://www.theblockbeats.info/flash/337382) Kimi K2 entries since v1.11.1 (K2 at 0.5x credits) and [K2.5's 7-day free-to-all promo in March 2026](https://www.theblockbeats.info/flash/337382). [Kimi K2.6](https://aitoolsrecap.com/Blog/moonshot-ai-kimi-k2-6-release-coding-agent-benchmarks-2026) (Apr 20) tops SWE-Bench Pro at 58.6%, beating Opus 4.6 and GPT-5.4 at roughly [5× cheaper API list price](https://openrouter.ai/moonshotai/kimi-k2.6). Pairs with Windsurf 2.0's split-pane Spaces into the **Kimi Swarm** — 6 parallel agents on one workspace for near-$0. Check your picker for the current multiplier. | [Power Move #15](#15-the-kimi-k2-free-swarm--6-parallel-agents-for-0), [§16 Model Optimization](#16-model-optimization--swe-16-adaptive-battle-groups) |
| [**`gh skill` CLI**](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli) | **Apr 16** | New GitHub CLI command to discover / install / update / publish [`SKILL.md`](https://agentskills.io) skills across Copilot, Claude Code, Cursor, Codex, Gemini CLI — version-pinned, content-addressed, portable provenance. Drop into Windsurf's `.windsurf/skills/` with one flag. | [§22 Skills Ecosystem](#22-skills-ecosystem--gh-skill-agentskillsio-and-viral-skills) |
| [**mvanhorn/last30days-skill**](https://github.com/mvanhorn/last30days-skill) | GitHub Trending #1 Apr 16, 22k⭐ | Viral agent skill that searches Reddit / X / YouTube / HN / TikTok / Polymarket / GitHub in parallel and has an AI judge synthesize one brief. Ships installers for Claude Code, OpenClaw, Hermes. Works in Cascade with a two-line change. | [§22](#22-skills-ecosystem--gh-skill-agentskillsio-and-viral-skills) |
| [**Claude Code Subagents**](https://docs.anthropic.com/en/docs/claude-code/sub-agents) pattern | Exploded Apr 12–14 | `.claude/agents/*.md` per-role specialists with isolated context windows. Every competing tool is copying it. Cascade emulates via `.windsurf/agents/` + worktrees. | [§17 Custom Subagents](#17-custom-subagents) |
| [**Karpathy's LLM Wiki**](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) + [Context Engineering](https://towardsdatascience.com/deep-dive-into-context-engineering-for-ai-agents/) | Apr 4–9 | New discipline: *offload, retrieve, compress, isolate*. "RAG is dead, long live the Agentic Wiki." Claude Code's 3-tier compaction engine reverse-engineered publicly. | [§20 Context Engineering & the Agentic Wiki](#20-context-engineering--the-agentic-wiki) |
| [**Spec Kit v0.5.0**](https://github.com/github/spec-kit) / SDD | Apr 4–11 | GitHub's `specify init` + seven `/speckit.*` slash commands. Spec-Driven Development went mainstream this month, with AWS Kiro, Tessl, and IBM all shipping adaptations. | [§21 Spec-Driven Development](#21-spec-driven-development-with-cascade) |
| [**MCP SSE → Streamable HTTP**](https://www.channel.tel/blog/mcp-sse-to-streamable-http-migration) migration | Keboola dropped Apr 1, Atlassian Jun 30 | Every remote MCP server needs to migrate. Affects your `mcp_config.json` *today*. | [§6 MCP](#6-mcp-server-integration), [§24 Gotchas](#24-gotchas--known-issues-april-2026) |
| [**GitHub MCP Server 0.33.0**](https://github.com/github/github-mcp-server/releases/tag/v0.33.0) | Apr 14 | Resolve review threads, `path` / `since` / `until` filters on `list_commits`, OSS logging adapter for HTTP. | [§6 MCP](#6-mcp-server-integration) |
| [**Azure MCP Server 2.0 GA**](https://devblogs.microsoft.com/azure-sdk/announcing-azure-mcp-server-2-0-stable-release) | Apr 10 | 276 tools across 57 Azure services, self-hosted remote MCP. | [§6 MCP](#6-mcp-server-integration) |
| [**Instruction-file hierarchy**](https://amitray.com/claude-md-vs-agents-md-memory-md-skills-md-context-md-guide-2026/) (CLAUDE.md / AGENTS.md / MEMORY.md / SKILLS.md / CONTEXT.md) | Apr 14 | The pattern going around the agent-coding Twitter/X — distinct jobs for each file. Cascade already supports all of them; the docs just hadn't caught up. | [§7 AGENTS.md hierarchy](#the-instruction-file-hierarchy-apr-2026) |
| [**Cognition SWE 1.6 post-mortem**](https://cognition.ai/blog/swe-1-6) | Apr 7 | Cognition explicitly trained SWE 1.6 to *prefer parallel tool calls, avoid looping, use its own tools over shell*. The behaviors you want to reinforce in your rules. | [§16 Model Optimization](#16-model-optimization--swe-16-adaptive-battle-groups) |
| [**GPT-5.3-Codex-Spark**](https://codex.danielvaughan.com/2026/03/31/codex-spark-cerebras-real-time-coding/) @ 1000 tok/s | Feb 12 (blew up Mar/Apr) | OpenAI's Cerebras-hosted speed model. Direct competitor to SWE 1.6 Fast. Context for why the SWE 1.6 Fast promo matters *right now*. | [§16](#16-model-optimization--swe-16-adaptive-battle-groups) |
| [**Parallel / racing agents**](https://agent-wars.com/news/2026-04-10-twill-races-coding-agents-best-pr) (Twill.ai, AgentBox, ctx) | Apr 10 | Running N agents on one task in parallel and picking the winning PR is going mainstream. Cascade's [Arena Mode](#12-arena-mode--side-by-side-models) + [Worktrees](#11-worktrees--parallel-cascade) already do this. | [§12](#12-arena-mode--side-by-side-models), [§17](#17-custom-subagents) |
| [**Observability stack**](https://agenticcareers.co/blog/ai-agent-observability-stack-2026) (LangSmith / Langfuse / Arize / Helicone / Braintrust) | Late Mar – Apr | 67% of AI-engineer listings now require agent observability experience. Cascade hooks can feed any of them. | [§23 Observability & Evals](#23-observability--evals-for-cascade) |

**Bottom line:** if your AI-coding guide was written before April 14, 2026, it's already missing at least three viral primitives (`gh skill`, the subagents pattern, the SSE deprecation). This one is current.

---

## Unlocked Power Moves

> The 16 techniques actually going viral on X / Reddit / YouTube right now that make people say **"wait, Cascade can do that?"** — each with evidence of real adoption and a copy-paste recipe. Every one is reproducible in Windsurf 2.0.50 today.

If you only do three of these, do **[#0 Opus 4.7 + Thinking Levels](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026)**, **#1 Planning with Files**, and **#2 Chrome DevTools MCP**. They compound faster than anything else in this guide.

### 0. Opus 4.7 + Thinking Levels in the Cascade Picker (Apr 16, 2026)

**What it is:** Claude [**Opus 4.7**](https://www.anthropic.com/news/claude-opus-4-7) dropped Apr 16, 2026 — Anthropic's most capable generally available model, with stronger agentic coding, 1M-token context, 128K max output, high-resolution vision (2576px / 3.75MP, up from 1568px), and [**adaptive thinking**](https://platform.claude.com/docs/en/build-with-claude/adaptive-thinking) support. Windsurf added it to the Cascade model picker **the same day**, with **promo credit pricing** for self-serve and — the part most Claude subscribers never see — **each thinking tier as a separate, credit-priced entry in the picker**, up to a MAX tier.

**Why it's a wow (how each Anthropic surface compares):**

| Surface | How you pick a thinking tier |
|---|---|
| **Cascade in Windsurf** | Each tier is a **separate entry in the model picker** (base / Think Low / Medium / High / MAX). Per-message selection, visible credit cost per tier, pinnable. |
| **Claude Code CLI** | Set persistent tier with [`/effort` low/medium/high](https://claudelog.com/faqs/what-is-slash-effort-command/) or trigger a single-turn max with the [`ultrathink` keyword](https://claudelog.com/faqs/what-is-ultrathink/) (re-introduced in v2.1.68 after the brief [Jan 16 deprecation](https://decodeclaude.com/ultrathink-deprecated/)). No visual picker — you have to remember the keyword. |
| **Anthropic Cowork / Chat** | Adaptive thinking toggle only — the model decides how deep to think. No manual tier selection. |

Cascade's advantage isn't that thinking tiers *exist* — Claude Code CLI power users have had `/effort` + `ultrathink` for a while. It's that Cascade puts every tier in the **same picker you already use for model selection**, with the **credit multiplier printed next to each one**. You pick the tier visually, per message, and you see the cost before you send. That pattern matches what Windsurf already does for [GPT-5.4's Low / Medium / High / **Extra High Reasoning**](https://www.windsurf.com/changelog) (1x / 1x / 2x / 3x / **8x** credits) and for Opus 4.6 / 4.6 Think (2x / 8x). It's the friction-free version of the dial — the one a Cowork/Chat user will read this section and immediately want.

MAX thinking is the tier most people never notice exists. On a hard debugging session or an architecture decision, it feels closer to a human senior engineer chewing on the problem than a chatbot guessing. The trade-off is cost (highest credit multiplier) and latency (tens of seconds to first token), so you pick it deliberately.

**When to pick which level** (Cascade "Think" variants follow the same tiering Windsurf established for GPT-5.4; exact names and multipliers live in the in-IDE picker since [Feb 2026](https://www.windsurf.com/changelog)):

| Level | Use when | Skip when |
|---|---|---|
| **Opus 4.7** (base) | Agentic coding, multi-file refactors, long-horizon sessions | SWE 1.6 Fast handles it; you're on free tier; it's a 3-line change |
| **Opus 4.7 Think — Low / Medium** | Tricky but bounded — a gnarly regex, a race condition, a subtle test failure | The problem is search-shaped, not reasoning-shaped — a wiki lookup would've answered it |
| **Opus 4.7 Think — High** | Cross-system architecture, migration planning, security review, spec drafting | The task has <200 tokens of actual ambiguity — you're paying for thinking you won't use |
| **Opus 4.7 Think — MAX** | Hardest 5% of your work: novel algorithms, distributed-systems bug hunts, gnarly data-model decisions | Anything the tier below can solve. MAX is for the problem you'd escalate to your most senior engineer. |

**30-second setup:**

1. Update Windsurf to **2.0.50+** (Apr 16, 2026 or later).
2. In Cascade, open the model picker under the input box.
3. **Pin** `Opus 4.7` and `Opus 4.7 Think` (and the MAX variant if surfaced separately in your plan) so they float to the top — see [§16 Pin Your Favorites](#pin-your-favorites).
4. Check the in-picker **token-rate display** and **prompt-cache timer** ([Adaptive release notes](https://www.windsurf.com/changelog)) so you always see the live credit cost before you send.
5. Optionally, create a one-file slash command for MAX mode (below).

**Cascade prompt that demonstrates it:**

```
@reviewer + @architect, switch to Opus 4.7 Think — MAX.

Read the last 48 hours of commits on this branch, the open plan in
plans/, and the failing CI job. Produce a single-page root-cause
analysis with (a) the top two hypotheses ranked by likelihood, (b)
the smallest experiment that disambiguates them, and (c) the
rollback plan if we ship the wrong fix.

Take your time. I want the MAX-tier chain-of-thought, not a fast guess.
```

**Optional slash command** — `starter/.windsurf/workflows/max-think.md`:

```yaml
---
name: max-think
description: Route the next task to Opus 4.7 Think — MAX for deepest reasoning
---

# MAX Think Mode

Use Opus 4.7 Think at the MAX tier for this task.

- This is a high-stakes reasoning task — prefer correctness over speed
- Produce 2–3 hypotheses before converging on one
- Cite specific files/lines for every claim
- If uncertainty is unresolvable, say so and stop — don't guess
- Acceptable latency: up to 60s to first token
```

**Gotchas worth knowing:**

- **New tokenizer = 35% more tokens per prompt.** Opus 4.7 ships with a new tokenizer that can tokenize the same English text into [up to ~35% more tokens](https://dev.to/devtorres_/opus-47-uses-35-more-tokens-than-46-heres-what-im-doing-about-it-2del) than Opus 4.6. Anthropic didn't raise the per-token sticker price ($5 / $25 per 1M), but your effective bill per prompt can go up even on identical work. Prompt caching claws most of that back — see [Power Move #12](#12-prompt-caching-breakpoints--engineer-for-90-token-savings).
- **MAX isn't always better.** More thinking tokens = more cost and latency. On simple refactors, base Opus 4.7 (or SWE 1.6 Fast) often matches MAX at 1/8 the credits. Reserve MAX for genuinely hard reasoning.
- **The promo window is short.** Windsurf's promo pricing on new models historically lasts 2–4 weeks. Check the in-picker rate display before assuming today's price is tomorrow's.
- **Cybersecurity guardrails.** Opus 4.7 ships with Anthropic's new auto-detected cybersecurity safeguards (fallout from [Project Glasswing](https://www.anthropic.com/glasswing)). Legitimate pentest / red-team work may need the [Cyber Verification Program](https://www.anthropic.com/news/claude-opus-4-7).

**How the Anthropic surfaces differ (quick reference):**

- **Cowork / Chat** — adaptive thinking only, no manual tier selection. This is the surface most Claude subscribers know.
- **Claude Code CLI** — persistent tier via [`/effort`](https://claudelog.com/faqs/what-is-slash-effort-command/), single-turn max via `ultrathink` keyword, per-process override via the [`MAX_THINKING_TOKENS` env var](https://docs.anthropic.com/en/docs/claude-code/settings). Real, but keyword-driven — no visual picker.
- **Cascade in Windsurf** — every tier as its own picker entry, visible credit multiplier, per-message selection, pinnable. Same dial, way less friction.

---


### 1. Planning with Files (Manus-Style) — The $2B Acquisition Pattern

**What it is:** Persistent markdown plans in `plans/` that Cascade reads *and updates* as it works. The skill behind Meta's $2B Manus acquisition and the reason the [planning-with-files](https://github.com/OthmanAdi/planning-with-files) skill hit **18.4k⭐ in ~90 days**.

**Why it beats Cascade's built-in Plan mode:** Plan-mode plans live in-session. File-based plans survive `/compact`, session restarts, and context resets. The agent comes back two days later, reads the exact same plan, and resumes from checkbox #7.

**30-second setup:**

```bash
# From your repo root
mkdir -p plans
```

Add this to the top of your `AGENTS.md`:

```markdown
## Planning Protocol

For any task > 20 lines of code:

1. Create `plans/<slug>.md` with: Goal / Non-goals / Constraints / Task breakdown (checkboxes) / Risks / Rollback
2. Work one checkbox at a time, running tests after each
3. Update the plan file with `[x]` and a 1-line note as each checkbox completes
4. When resuming a session, read the plan file FIRST before touching code

Never proceed to step N+1 if step N's tests are red. Always update the plan before you update code.
```

**Cascade prompt to kick it off:**

```
Plan this in plans/add-stripe-webhooks.md before touching code.
Use Plan Mode. When the plan is written, stop and hand it to @reviewer.
```

**Drop-in skill:** We've packaged this as [`starter/.windsurf/skills/planning-with-files`](./starter/.windsurf/skills) — auto-runs when intent matches.

### 2. Chrome DevTools MCP — Give Your Agent Eyes

**What it is:** Google's [chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) server (35k⭐, official) exposes Chrome's full debugging surface to Cascade. Live DOM, console errors with source-mapped stack traces, network waterfall, screenshots, performance traces.

**Why it's a wow:** Most frontend AI bugs are "the agent can't see what it built." This fixes that in one config line. You describe a bug, Cascade *takes a screenshot*, reads the console, and iterates.

**30-second setup:**

```json
// starter/.windsurf/mcp_config.json  (we've added this for you)
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

**Cascade prompt that shows the magic:**

```
Open http://localhost:3000 in the chrome-devtools MCP.
Click "Sign up", fill in a test email, submit.
Take a screenshot, read the console, and fix whichever error prevents the redirect.
```

**Pair with** [Playwright MCP](https://playwright.dev/docs/getting-started-mcp) (driving) while DevTools MCP handles debugging — Steve Kinney's ["driving vs. debugging"](https://stevekinney.com/writing/driving-vs-debugging-the-browser) framing.

### 3. Ralph Wiggum Loop — Persistent Until Green

**What it is:** A `while` loop that calls Cascade repeatedly until tests pass. Named after the Simpsons character because it keeps trying, keeps helping, never gives up. [Steve Kinney's breakdown](https://stevekinney.com/writing/the-ralph-loop) and the viral [r/ClaudeCode thread](https://www.reddit.com/r/ClaudeCode/comments/1q2qvta/share_your_honest_and_thoughtful_review_of_ralph/) are the reference.

**Why it's a wow:** Watched a dev fix 47 failing tests in 23 minutes not by typing — by kicking off a loop and walking away. Controversial (see the skeptics in that thread), but devastating when the checkable outcome is well-defined.

**Windsurf-safe variant** (in [`starter/.windsurf/workflows/ralph-safe.md`](./starter/.windsurf/workflows)):

```bash
# ralph-safe.sh — kill-switch + max-iterations + cost cap
MAX_ITERS=${MAX_ITERS:-20}
COST_CAP_USD=${COST_CAP_USD:-5.00}
KILLSWITCH="${HOME}/.ralph-stop"

for i in $(seq 1 $MAX_ITERS); do
  [ -f "$KILLSWITCH" ] && { echo "Killswitch tripped"; break; }
  pnpm test --silent && { echo "Green at iter $i"; exit 0; }
  windsurf cascade "The test suite is red. Read the latest failures, fix the code (never the tests unless they're wrong), and stop. Don't try to validate — I'll run tests."
done
```

**When NOT to use it:** UI flows that need human judgment. Anything involving money or destructive data. Features that aren't auto-verifiable.

### 4. ast-grep Skill — Structural Code Search

**What it is:** [ast-grep](https://ast-grep.github.io) understands your code's AST, not just text. Ask things like *"find all async functions that don't have error handling"* or *"find all React components using `useEffect` with an empty deps array"*. The [official skill](https://github.com/ast-grep/claude-skill) drops into any `.windsurf/skills/` directory.

**Why it's a wow:** Your refactors stop missing edge cases. Text-based `grep` misses `asyncFunction()` vs `async function name()` vs `const x = async () => {}` — ast-grep catches all three structurally.

**30-second setup:**

```bash
brew install ast-grep   # or: cargo install ast-grep
gh skill install ast-grep/claude-skill --to .windsurf/skills/
```

Add to `AGENTS.md`:

```markdown
For any code search that requires understanding syntax (not plain text),
use `ast-grep` instead of `grep` / `ripgrep`. For plain text in comments
or non-code files, `rg` is still preferred.
```

Covered in the [ast-grep AI docs](https://ast-grep.github.io/advanced/prompting.html) with an example prompt [originally from Kieran Klaassen on X](https://x.com/kieranklaassen/status/1938453871086682232).

### 5. `/compact` Proactively, With Preservation Instructions

**What it is:** The `/compact` command in Cascade (also in Claude Code) compresses session history once context is about to blow out. The mistake everyone makes: running it when the bar hits 90%. By then the oldest (= most foundational) decisions are already being dropped. [MindStudio's Apr 2 writeup](https://www.mindstudio.ai/blog/claude-code-compact-command-context-management/) is the reference.

**The unlock:** Run `/compact` *with an instruction*, proactively, at the 50–60% mark:

```
/compact Preserve verbatim: the current plan file path, the AGENTS.md
invariants I've already cited this session, the 3 design decisions we
just made about auth, and anything under "Gotchas" in vault/.
Discard: exploration logs, test runs, tool outputs from rejected paths.
```

Cascade keeps what matters, drops what doesn't. Your session stays sharp through the full workday instead of degrading after hour 2.

### 6. Linear Agent API — Assignable AI Teammate

**What it is:** Linear's Agent API lets Cascade register as an actual teammate. You assign an issue to it like any human. A webhook fires, Cascade picks up the issue, runs in Plan Mode, posts the plan back to the Linear comment, then implements and opens a PR. Reference implementation in the [viral r/Linear post](https://www.reddit.com/r/Linear/comments/1s4gqdy/linearnative_ai_dev_agent_using_claude_code_mcp/).

**Why it's a wow:** Ticket → PR with zero IDE interaction. Your team sees "Cascade" in the assignee list like any other engineer, with an Agent Session panel showing its work.

**Recipe** (30 lines, [see §19.12](#1912-linear-agent-api--cascade-as-an-assignable-teammate)):

```typescript
// webhooks/linear.ts
import { LinearClient } from "@linear/sdk";

app.post("/webhooks/linear", async (req, res) => {
  const { action, data } = req.body;
  if (action !== "assigned" || data.assignee?.id !== process.env.CASCADE_USER_ID) {
    return res.json({ ok: true });
  }
  res.json({ ok: true }); // ACK immediately — plan/implement below can take minutes
  try {
    const issue = await linear.issue(data.id);
    const plan = await cascade.plan(issue.description, { mode: "plan" });
    await issue.createComment({ body: `## Plan\n${plan}` });
    await cascade.implement(plan, { issueId: issue.id });
  } catch (err) {
    console.error("cascade failed for issue", data.id, err); // never rethrow — retries spawn duplicates
  }
});
```

Scope the OAuth app with `actor=app`, `app:assignable`, `app:mentionable`.

### 7. LLM Wiki Vault — Persistent, Compounding Memory

**What it is:** The [llm-wiki-vault protocol](https://github.com/MirkoSon/llm-wiki-vault) — Karpathy-advocated alternative to embeddings-based RAG. Plain markdown, git-tracked, agents read/write via explicit workflows defined in `AGENTS.md`. Every session compounds the knowledge base instead of re-discovering it.

**Why it's a wow:** Your third session on a codebase is faster than your first, not slower. Unlike RAG, you can *read* the vault yourself, diff it, version it, grep it. Unlike in-memory, it survives.

**Drop-in vault protocol:** We've packaged this as [`VAULT_PROTOCOL.md`](./VAULT_PROTOCOL.md) — paste it into your `AGENTS.md` and you're done. See §20 for the full pattern.

### 8. prd.md / spec.md — One File Kills Scope Drift

**What it is:** Before any feature, write a `prd.md` (product requirements) or `spec.md` (technical spec) at the repo root or in `plans/`. Cascade reads it at the start of every session. The [anti-drift workflows post](https://vibecoding.app/blog/anti-drift-workflows-vibe-coders-guide) covers it alongside Spec Kit, Planning with Files, and the Ralph Loop.

**Why it's a wow:** The #1 reason AI-coded features end up wrong is the requirements drifted mid-session. A PRD checked into git is the cheapest drift-prevention device ever invented.

**Drop-in template:** [`starter/templates/PRD.template.md`](./starter/templates/PRD.template.md) — 111 lines, 9 sections, skip what doesn't apply.

**Cascade prompt:**

```
Read plans/prd-checkout-flow.md. If anything is ambiguous, list the
ambiguities — don't guess. Only once I confirm do we move to the plan.
```

### 9. Reflection Pattern — Generate → Evaluate → Revise

**What it is:** Make Cascade grade its own output before handing it back. [Research shows](https://toolhalla.ai/blog/reflection-pattern-ai-agents-2026) reflection boosts HumanEval coding accuracy from 80% → 91%. But **naive self-correction makes GSM8K math worse** — use it where there's an external signal (tests, lints, types), not where the model has to judge itself.

**Three variants to pick from:**

| Variant | When | How |
|---|---|---|
| **External-signal retry** | Tests, lints, types, compile errors | Loop: generate → run signal → retry with error |
| **Critic-model review** | Code reviews, security scans | Second agent (different model) critiques the first |
| **Self-critique** | Drafts, plans, docs | Same agent rewrites with checklist — use sparingly |

Dedicated workflow: [`starter/.windsurf/workflows/reflection-loop.md`](./starter/.windsurf/workflows).

### 10. Playwright MCP — Browser as a First-Class Tool

**What it is:** [Playwright MCP](https://playwright.dev/docs/getting-started-mcp) is the official Microsoft server that exposes Playwright's automation API to Cascade. Unlike Chrome DevTools MCP (debugging), Playwright is for *driving* — scripted clicks, form fills, assertions.

**The combo:** Chrome DevTools MCP + Playwright MCP in the same config = Cascade can drive the browser *and* debug what goes wrong.

**Already wired into the starter kit** — both `chrome-devtools` and `playwright` are enabled by default in `starter/.windsurf/mcp_config.json`.

### 11. VoltAgent Subagents — 100+ Specialist Recipes

**What it is:** [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) (16k⭐) — 100+ YAML-frontmatter specialists covering every corner of engineering: `architect-reviewer`, `database-optimizer`, `security-auditor`, `terraform-engineer`, `kubernetes-specialist`, and 95 more. Every file drops straight into `.windsurf/agents/` as a new `@role` subagent.

**Why it's a wow:** You don't have to design your subagent team. You pick five from a list of 100 that's actively maintained. Stellar starting point for specialist teams.

**Recipe:**

```bash
# Port the top 5 most-useful ones into your Cascade setup
for agent in architect-reviewer code-reviewer security-auditor performance-engineer test-automator; do
  curl -sL "https://raw.githubusercontent.com/VoltAgent/awesome-claude-code-subagents/main/categories/04-quality-security/${agent}.md" \
    -o ".windsurf/agents/${agent}/AGENT.md"
done
```

Tweak the `tools:` frontmatter to match Cascade's tool names, change `model: opus` to whatever you pin.

### 12. Prompt-Caching Breakpoints — Engineer for 90% Token Savings

**What it is:** Every long system prompt, AGENTS.md, or sticky context block should hit Anthropic's [prompt cache](https://prompt-caching.ai). Cascade handles caching automatically, but you can *engineer* your setup to maximize hit rate. [Claude Lab's Apr 8 writeup](https://claudelab.net/en/blog/claude-prompt-caching-practical-guide) covers the pattern.

**The unlock — cache-friendly ordering:**

```
[STATIC — cache hit]        AGENTS.md, invariants, commands
[STATIC — cache hit]        Per-role AGENT.md
[STATIC — cache hit]        Relevant vault/ pages
[SEMI-STATIC — partial]     Current plan file
[DYNAMIC — fresh every turn] User message, recent tool results
```

Put stable things first, volatile things last. 90% cheaper on turn 2+. One `AGENTS.md` edit resets the cache, so batch your invariant changes.

### 13. Screenshot-Feedback Visual Iteration

**What it is:** For any UI work, make screenshot-take → AI-describe → AI-fix the loop. Two MCP servers make this trivial: Chrome DevTools MCP (`take_screenshot`) + vision-capable model (Claude Opus 4.6, GPT-5.4, SWE 1.6 can all ingest images).

**Why it's a wow:** The agent *literally sees* the misaligned button. No more "change `mt-4` to `mt-6` and pray."

**Cascade prompt (works today):**

```
Take a screenshot of localhost:3000/dashboard. Compare it to
design/dashboard-spec.png. Describe every discrepancy (spacing,
color, copy, alignment). Fix the top 3 most impactful ones.
```

Recipe file: [`starter/.windsurf/workflows/visual-iteration.md`](./starter/.windsurf/workflows).

### 14. Markdown Plan Files > Built-in Planners

**What it is:** Andrew Shu's [viral post](https://www.ashu.co/markdown-plan-files-vibe-coding/) — an AGENTS.md block that forces every non-trivial task through a file-based plan instead of Cursor's Plan panel or Claude's in-memory tasks.

**Why it's a wow:** Same reason as #1, but broader — it's a one-paragraph change to AGENTS.md that transforms how Cascade approaches multi-step work across every repo you own.

**The block to paste:**

```markdown
## How You Plan

Before changing more than one file:

1. Create `plans/<YYYY-MM-DD>-<slug>.md` with numbered subtasks
2. Each subtask: one verb, one file-or-directory scope, one acceptance criterion
3. Commit the empty plan before any code change — the plan is the contract
4. Work one subtask at a time; do not batch
5. When blocked or uncertain, add a "Questions" section to the plan and stop

Never skip the plan. If you think a task is too small for a plan, ask.
```

Source: [0xandrewshu/ai-utils/rule-markdown-plan](https://github.com/0xandrewshu/ai-utils/tree/main/rule-markdown-plan).

---

### 15. The Kimi K2 Free Swarm — 6 Parallel Agents for $0

**What it is:** Open 6 Cascade sessions side-by-side in a single Windsurf workspace (Space), split your task into 6 disjoint subtasks, run all six on the [**Kimi K2**](https://aitoolsrecap.com/Blog/moonshot-ai-kimi-k2-6-release-coding-agent-benchmarks-2026) entry in the model picker — which Windsurf has shipped [at 0.5× credits since v1.11.1](https://www.threads.com/@pahud/post/DMeZLopuyhb) (July 2025) and [free-to-all during promo windows](https://www.theblockbeats.info/flash/337382) (e.g. K2.5's 7-day all-plans promo in March 2026). Six parallel trajectories finish in the time one would have taken — for near-zero incremental credits.

**Why it's a wow:** Every other "N agents in parallel" pattern — Arena Mode (§12), Twill.ai, AgentBox, worktree fan-out — multiplies credits by N. This one is the only pattern where N costs roughly the same as 1. And [Kimi K2.6](https://kimi-k2.org/blog/24-kimi-k2-6-release) (Apr 20, 2026) isn't a toy model: it tops SWE-Bench Pro at [58.6%](https://aitoolsrecap.com/Blog/moonshot-ai-kimi-k2-6-release-coding-agent-benchmarks-2026), beating Opus 4.6 (53.4%) and GPT-5.4 (57.7%) on the benchmark closest to real GitHub issues, with open MIT-licensed weights and API list price roughly 5× cheaper than Claude Sonnet 4.6 ([Kimi K2.6: $0.60 input / $2.80 output per 1M tokens](https://openrouter.ai/moonshotai/kimi-k2.6) vs [Sonnet 4.6: $3.00 / $15.00](https://pricepertoken.com/pricing-page/model/anthropic-claude-sonnet-4.6)). The swarm pattern turns that into a compounding free-tier advantage inside Windsurf specifically — because only Windsurf 2.0's Spaces + split-pane UI lets you operate six sessions visually on one screen with shared project context.

**30-second setup:**

1. Open (or create) a Space for the task in the Agent Command Center — the six agents will inherit the Space's context automatically (see [§2](#2-agent-command-center--spaces))
2. `Cmd/Ctrl+\` to split the Cascade pane; repeat until you have 6 panes (a 3×2 grid works best on a 27"+ display)
3. In each pane, click **New Session** → select **Kimi K2** from the model picker (look for the free/promo entry — the multiplier is printed next to the model name)
4. In pane 1, run the **swarm-split prompt** below to decompose your task into 6 disjoint subtasks (or use the `swarm-split` workflow that ships in the starter kit)
5. Paste subtask 1 into pane 1, subtask 2 into pane 2, … — launch all six. Watch the grid.

**The swarm-split prompt:**

```
Decompose the following task into exactly 6 independent, parallelizable subtasks.
Each subtask must be runnable in isolation — no shared mutable state, no blocking
dependencies, no overlapping file paths.

Output format (one block per subtask):

### Subtask N — <title>
- Scope: <one file or directory, absolute path from repo root>
- Acceptance: <one sentence; how to verify it's done>
- Model hint: kimi-k2   # override only if a subtask genuinely needs deeper reasoning

Rules:
1. Each subtask touches a DISTINCT file path — no two subtasks modify the same file
2. If two subtasks would conflict, collapse them into one or sequence them and reduce the count
3. If the task genuinely cannot be split 6 ways, output fewer (3/4/5) and explain why in one line
4. Do NOT invent subtasks to reach 6 — padding produces merge hell

Task: <paste task here>
```

**Why it works:**

- **Kimi K2 is strong at well-scoped, medium-complexity subtasks** — exactly what the split produces. The weakness most community reports flag (instruction-following on long multi-step prompts) goes away when each subtask is narrow. ([Kimi K2.6 release notes](https://kimi-k2.org/blog/24-kimi-k2-6-release))
- **Path-disjoint subtasks mean zero merge conflicts** — you can accept all 6 diffs in sequence with no rebase drama
- **A single Space means each session sees the same project-level context** without re-paying tokens for the setup
- **The 3×2 pane grid is a live dashboard** — a stuck agent is visible in 2 seconds, faster than any scheduler you could write

**When NOT to swarm:**

- **Single-file refactors** — no split benefit; one agent is cheaper and cleaner
- **Tightly-coupled subtasks** — schema + migration + services touching the same models is a sequential problem, not a parallel one
- **Exploration / debugging** — one focused agent beats six parallel guesses
- **Integration work** — you want context coherence end-to-end, not six parallel forks of it

**Guardrails (community-reported, learned the hard way):**

- **Prefer [Worktrees](#11-worktrees--parallel-cascade)** if there's any chance of path overlap — each agent in its own worktree, converge via normal git merge flow. Path disjointness via prompt is a rule, worktrees are a safety net.
- **Name each session** after its subtask slug before you launch — six untitled Cascade sessions in the Command Center is unreadable within 3 minutes
- **Review the split manifest** before launching. If the architect gives you overlapping scopes, re-prompt; don't paper over it by "being careful"
- **Keep one human pane empty** as a spotter — use it to `@` the stuck agents, accept diffs, rescue failing ones. Seven panes, six working, one driving.
- **Don't swarm on Opus 4.7 MAX or GPT-5.4 Extra High Reasoning** — the whole point is leveraging a free/low-credit tier. If every subtask genuinely needs MAX, you have the wrong task shape (see [Power Move #0](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026)).

**Cost math (community-reported):**

For a sprint-sized task split 6 ways (say: 6 new parallel endpoints, 6 test files, 6 small refactors across modules):

| Model choice | Incremental credit cost |
|---|---|
| Opus 4.7 base × 6 | ~6× mid-tier credits |
| SWE 1.6 Fast × 6 | ~6× low-credit (still drains quota) |
| **Kimi K2 on current free/promo × 6** | **~$0** |

Promo rates shift — check the multiplier printed next to the model in your picker before you launch. The pattern still works at 0.5× or 0.25×; the "free" variant is what makes it go viral.

**Starter kit:** `starter/.windsurf/workflows/swarm-split.md` — a runnable workflow that generates the 6-way split, writes a `plans/<YYYY-MM-DD>-<slug>-swarm.md` manifest, and prints the per-pane launch order so you can paste subtasks in sequence without losing your place.

**Cross-links:** [§2 Agent Command Center & Spaces](#2-agent-command-center--spaces), [§11 Worktrees & Parallel Cascade](#11-worktrees--parallel-cascade), [§12 Arena Mode](#12-arena-mode--side-by-side-models), [§16 Model Optimization](#16-model-optimization--swe-16-adaptive-battle-groups).

---

**All 16 are wired into the starter kit** — if you installed `starter/` already, most of the infrastructure is already there. The individual sections below go deeper on the features each move builds on.

---

## Get Started

### Install Windsurf

Download at [windsurf.com](https://windsurf.com) — available for Windows, Mac, and Linux. Linux ARM64 is now a first-class client as of Feb 2026 (deb + rpm).

> Referral link (mutual Flex Credit bonus per [Windsurf's referral terms](https://windsurf.com/refer/terms-of-service); current amount published on [windsurf.com/refer](https://windsurf.com/refer)): [windsurf.com/refer?referral_code=kowwopt506rq1907](https://windsurf.com/refer?referral_code=kowwopt506rq1907)

### Plans & Pricing

Current plans: **Free** / **Pro** / **Teams** / **Max** — see [windsurf.com/pricing](https://windsurf.com/pricing) for latest details.

Key things to know right now:
- **SWE 1.6 is free for everyone** for the next 3 months (Fireworks, 200 tok/s)
- **SWE 1.6 Fast** is free for paying users (Cerebras, 950 tok/s) — use it freely without thinking about tokens
- **Adaptive** model is available to every self-serve plan; it draws down quota at a fixed per-token rate regardless of which underlying model it picks
- **Devin in Windsurf** is included in Pro/Max/Teams, drawing from the same Windsurf quota
- New GitHub → Devin connection grants up to **$50 in extra usage** credits

---

## Table of Contents

0. [**Unlocked Power Moves**](#unlocked-power-moves) — The 16 techniques actually going viral right now, led by Opus 4.7 + MAX thinking (Apr 16, 2026) and the free-tier Kimi K2 Swarm — each with a copy-paste recipe
1. [Cascade Modes: Code / Plan / Ask](#1-cascade-modes-code--plan--ask) — When to use each, plan files, implement handoff
2. [Agent Command Center & Spaces](#2-agent-command-center--spaces) — Multi-agent Kanban, task-level grouping, context inheritance
3. [Devin in Windsurf — Cloud Delegation](#3-devin-in-windsurf--cloud-delegation) — When to hand off, planning workflow, pricing model
4. [Terminal Command Execution](#4-terminal-command-execution) — Auto-execution, allow/deny lists, enterprise policies
5. [Skills System](#5-skills-system) — Progressive disclosure, bundled resources, system-level skills
6. [MCP Server Integration](#6-mcp-server-integration) — Marketplace, OAuth, tool toggling, custom registries, whitelist regex
7. [Directory-Scoped Instructions (AGENTS.md)](#7-directory-scoped-instructions-agentsmd) — Context per directory
8. [Hooks](#8-hooks) — Every hook point including `post_cascade_response_with_transcript` and `post_setup_worktree`
9. [Memories & Rules](#9-memories--rules) — Persistent context + the `rules_applied` telemetry trick
10. [Workflows](#10-workflows) — Slash-command automations
11. [Worktrees — Parallel Cascade](#11-worktrees--parallel-cascade) — Isolated sessions, post-setup hook, cleanup
12. [Arena Mode — Side-by-Side Models](#12-arena-mode--side-by-side-models) — Battle Groups, worktree isolation, converge workflow
13. [Web Search & Windsurf Browser](#13-web-search--windsurf-browser) — `@web`, `@docs`, URL parsing, the 2.0 in-editor browser
14. [App Deploys — One-Click Netlify](#14-app-deploys--one-click-netlify) — Public URLs, team deploys, claiming
15. [Editor-Layer AI: DeepWiki, Codemaps, Vibe and Replace](#15-editor-layer-ai-deepwiki-codemaps-vibe-and-replace) — Hover explanations, shareable code maps, AI find-replace
16. [Model Optimization — SWE 1.6, Adaptive, Battle Groups](#16-model-optimization--swe-16-adaptive-battle-groups) — Which model, when, and how to route
17. [Custom Subagents](#17-custom-subagents) — Personality profiles for specialized tasks
18. [Real-World Configurations](#18-real-world-configurations) — Production MCP servers and patterns
19. [Harness Parity: Hermes/OpenClaw Features in Cascade](#19-harness-parity-hermesopenclaw-features-in-cascade) — Graph RAG, vault memory, auto-capture, multi-provider, Telegram, observability — all inside Windsurf
20. [Context Engineering & the Agentic Wiki](#20-context-engineering--the-agentic-wiki) — The four moves, Karpathy's wiki pattern, Claude Code's 3-tier compaction
21. [Spec-Driven Development with Cascade](#21-spec-driven-development-with-cascade) — Spec Kit v0.5.0, `/speckit.*` commands, native Cascade SDD flow
22. [Skills Ecosystem — `gh skill`, agentskills.io, Viral Skills](#22-skills-ecosystem--gh-skill-agentskillsio-and-viral-skills) — Skills you should install *today*
23. [Observability & Evals for Cascade](#23-observability--evals-for-cascade) — Langfuse, Braintrust, `rules_applied` telemetry
24. [Gotchas & Known Issues (April 2026)](#24-gotchas--known-issues-april-2026) — Current quirks worth knowing
25. [Troubleshooting](#25-troubleshooting) — Common issues and fixes
26. [Feature Matrix](#feature-matrix) — Everything at a glance

---

## 1. Cascade Modes: Code / Plan / Ask

Cascade has three **modes**, toggled with `⌘+.` / `Ctrl+.` or the dropdown under the input box. Most people only ever use one. Using all three correctly is the single biggest productivity unlock in Cascade.

| Mode | Use case | Tools |
|------|----------|-------|
| **Code** | Features, refactors, bug fixes | All tools enabled — writes files, runs commands, installs deps |
| **Plan** | Any non-trivial task | All tools enabled, but produces a markdown plan instead of code |
| **Ask** | Learning, questions, code explanations | Search tools only — will not modify anything |

### Plan Mode — The Underused Superpower

Plan Mode doesn't just "plan", it:
- Explores your codebase first to understand current state
- Asks clarifying questions (use `megaplan` in the input for a more aggressive version that asks many more)
- Offers multiple implementation options with an interactive picker
- Writes the final plan to `~/.windsurf/plans/<name>.md`

Why the on-disk plan matters:
- **It persists across sessions.** If implementation goes sideways, open a fresh session, `@`-mention the plan, and continue from scratch — no re-explaining.
- **It's shareable.** Commit the plan file to PRs for review before code lands.
- **Devin can pick it up.** Hand the plan to Devin (see [Section 3](#3-devin-in-windsurf--cloud-delegation)) for long-running execution.

### Implement Handoff

When a plan is ready, click **Implement** on the plan file. Cascade automatically switches to Code Mode and begins executing against the plan. You don't lose the markdown — it stays at `~/.windsurf/plans/` so you can revisit.

### Pro Pattern

```
User: /plan Implement a rate limiter for /api/auth/* that survives process restarts
Cascade (Plan Mode): <asks 3-4 clarifying questions>
Cascade: <writes ~/.windsurf/plans/auth-rate-limiter.md with 3 options>
User: <picks option 2, clicks Implement>
Cascade (Code Mode): <executes the plan, checkpoints after each step>
```

Type `megaplan` to trigger the advanced form that asks *more* clarifying questions — use it for architecture-level work where getting the design wrong is expensive.

---

## 2. Agent Command Center & Spaces

### The New Home Screen for Cascade

The Agent Command Center (introduced in 2.0) is a Kanban-style surface inside Windsurf showing every agent you have running — local Cascade sessions and cloud Devin sessions — organized by status.

**What's on the board:**
- **Local agents** — Cascade sessions running in your editor
- **Cloud agents** — Devin sessions running on their own VMs
- Columns are grouped by status: in-flight, needs review, blocked, done

You open it from the sidebar without leaving the editor. It doesn't replace the editor pane — you can always jump back into any session and take over manually for last-mile edits.

### Spaces: Task-Level Context Grouping

A **Space** bundles everything for a single task or project:
- Agent sessions (Cascade + Devin)
- Pull requests
- Files
- Project-level context shared across sessions

**Why Spaces matter:** when you create a new agent inside a Space, it **inherits everything the Space already knows**. No re-explaining the project. No re-attaching files. A new Devin session inside an "Auth Rewrite" Space knows about all the PRs, files, and prior agent trajectories in that Space.

### Creating a Space

Three ways:
- **Drag-drop** — drag a session onto another session in the sidebar to group them
- **Split pane** — `Cmd/Ctrl+\` splits the current pane, click **New Session** in the empty half; new session inherits Space context
- **`Cmd/Ctrl+T`** — opens a new session inside the current Space

Every session is technically its own Space by default, even if you don't see it that way. You can promote single sessions into shared Spaces whenever it's useful.

### Recommended Workflow

```
1. New Space: "Payments V2 Migration"
   - Drop the RFC, architecture doc, and current payments folder in as context
2. Plan Mode session (local Cascade) → writes plan.md
3. Hand the plan to Devin Cloud → handles migration over ~30 min on its own VM
4. Review Devin's PR from the Kanban without leaving the editor
5. Local Cascade in the same Space handles follow-up bugfixes — inherits everything
```

Switching between Spaces is identical to switching tasks — except every task now has a **team of agents** inside it.

> **🎯 The $0 Swarm pattern:** open 6 Cascade panes inside a single Space, point them all at the current free/promo [Kimi K2](#15-the-kimi-k2-free-swarm--6-parallel-agents-for-0) entry in the picker, hand each one a disjoint subtask. Six parallel trajectories, shared Space context, near-zero incremental credits. Full recipe in [Power Move #15](#15-the-kimi-k2-free-swarm--6-parallel-agents-for-0).

---

## 3. Devin in Windsurf — Cloud Delegation

Windsurf 2.0 integrates **[Devin](https://devin.ai)** directly into the editor. Devin is a fully autonomous cloud agent that runs on its own VM with desktop, browser, and computer-use. You delegate work with one click, walk away, close your laptop, come back later to a PR.

### What Devin Handles Well

Tasks that are either *long-running* or *best done outside your local environment*:
- Test migrations across dozens of files
- Deployments that require live external systems
- Framework upgrades (Next 14 → 15, React 18 → 19, etc.)
- CI/CD debugging where Devin can replay the failing job on its VM
- Browser-driven testing and scraping tasks (computer-use)
- Anything involving overnight runs or long compile/build loops

### Pricing

Devin is included with every self-serve Windsurf plan (Pro / Max / Teams). It draws from your **existing Windsurf quota** rather than being billed separately. New GitHub connections get up to **$50 in extra usage** credits for first-time Devin Cloud use.

Enterprise accounts have Devin Cloud **disabled by default** — admins need to enable it in org settings if the org has also purchased Cognition Platform.

### The Delegate Flow

```
1. Start a local Cascade session in Plan Mode
2. Cascade writes a plan to ~/.windsurf/plans/feature.md
3. Click "Delegate to Devin" on the plan file
4. Devin spins up its VM, picks up the plan, starts executing
5. Devin session appears as a new card in the Agent Command Center
6. You keep coding locally OR close your laptop
7. Devin opens a PR when done; review it from inside Windsurf
```

This is the workflow that actually reaches harness-parity with things like Hermes' orchestrator/worker pattern or OpenClaw's sub-agent model — but without running the infrastructure yourself.

### When NOT to delegate

- The task is small (< 15 min locally with Cascade)
- You want tight iteration — Cascade's local feedback loop is faster
- Sensitive / regulated code that shouldn't leave your environment (though Devin runs on isolated VMs, check your org's policy)
- Pure-frontend tasks where visual iteration matters

For everything else, delegate and let Devin grind while you sleep.

---

## 4. Terminal Command Execution

### The UI Controls (Start Here)

Cascade's terminal controls are primarily **UI-driven**, not JSON config. This is where most users should start.

**Settings → Cascade → Terminal:**

| Setting | Options | What It Does |
|---------|---------|-------------|
| Auto-execution level | Disabled / Allowlist Only / Auto / Turbo | How aggressively Cascade runs commands without asking |
| Allow list | Regex patterns | Commands that auto-execute when level is "Allowlist Only" |
| Deny list | Regex patterns | Commands that always require confirmation |

These controls appear in the Cascade panel under the three-dots menu. Most users configure command execution here — hooks add additional guardrails on top.

### Enterprise Allow/Deny Lists

As of Jan 2026, **enterprise admins** can set organization-wide allow and deny lists that override user-level settings. If you're on Teams/Enterprise, check the admin dashboard — you may already have inherited policies you can layer personal rules on top of. On Windows, admins can enforce restrictions via Group Policy.

### Editor Settings

These VS Code-level settings reduce friction:

```json
{
  "terminal.integrated.allowChords": false,
  "terminal.integrated.confirmOnExit": "never",
  "terminal.integrated.enableConfirmation": false,
  "security.workspace.trust.enabled": false
}
```

`security.workspace.trust.enabled: false` is important — workspace trust blocks terminal commands in untrusted folders.

### Pre-Run Command Hook

For audit logging or command blocking, use the `pre_run_command` hook (see [Section 8](#8-hooks)).

---

## 5. Skills System

### How Skills Work

Windsurf auto-discovers skills from multiple locations:

| Path | Scope | Use Case |
|------|-------|----------|
| `.windsurf/skills/<name>/SKILL.md` | Workspace | Project-specific skills |
| `~/.codeium/windsurf/skills/<name>/SKILL.md` | User (global) | Skills across all projects |
| `.agents/skills/<name>/SKILL.md` | Workspace (alias) | Cross-tool compatibility |
| `.claude/skills/<name>/SKILL.md` | Workspace (alias) | Cross-tool compatibility |

### Progressive Disclosure — Why Skill Scaling Works

Cascade uses **progressive disclosure**: only the skill's `name` and `description` are in context by default. The full `SKILL.md` body and any supporting files are loaded **only when Cascade decides to invoke the skill** (or when you `@mention` it).

This means you can define **hundreds of skills** without blowing up your context window. The only thing the model sees upfront is a compact index of `{name, description}` pairs.

**Consequence:** your `description` field is doing the work of a full tool spec. Treat it as advertising copy the model reads when deciding whether to pull the skill in. Be specific, action-oriented, and mention the trigger conditions.

### Skill Directory Layout with Bundled Resources

Skills aren't just a single markdown file — you can bundle scripts, templates, and checklists alongside `SKILL.md` and reference them in the body. Cascade gets access to everything in the skill folder when the skill is invoked.

```
.windsurf/skills/deploy-to-production/
├── SKILL.md
├── deployment-checklist.md
├── rollback-procedure.md
├── scripts/
│   └── health-check.sh
└── config-template.yaml
```

### Creating a Skill

**`.windsurf/skills/run-tests/SKILL.md`:**

```yaml
---
name: run-tests
description: Run the project test suite, parse failures, suggest fixes. Use when the user says "run tests", "check tests", or after any implementation change.
---

# Run Tests

1. Detect the project type:
   - `package.json` → run `npm test`
   - `pyproject.toml` → run `pytest`
   - `Cargo.toml` → run `cargo test`
2. Capture stdout and stderr
3. If tests fail:
   - Parse the failure output
   - Identify the failing test name and assertion
   - Suggest a fix based on the error message
4. Return a summary: passed, failed, skipped counts
```

**`.windsurf/skills/deploy-check/SKILL.md`:**

```yaml
---
name: deploy-check
description: Pre-deployment validation checklist. Runs tests, secret scan, import resolution, and .env.example coverage. Use before any deploy, merge-to-main, or release.
---

# Deploy Check

1. Run the run-tests skill
2. Search for TODO, FIXME, HACK, XXX comments
3. Check for hardcoded secrets: API keys, passwords, tokens
4. Verify all imports resolve (no missing modules)
5. Check that environment variables are documented in .env.example
6. Report: READY or list of blockers with file:line references
```

### Invoking Skills

- **Auto-invocation:** Cascade matches your request to skill descriptions automatically
- **Manual:** Type `@skill-name` in the Cascade chat
- **UI:** Cascade panel → three-dots menu → Skills to browse, create, and edit
- **In workflows:** Reference skills by name in workflow steps

### System-Level Skills (Enterprise / MDM)

As of March 2026, enterprise admins can ship system-level `SKILL.md` definitions through MDM-managed configs. Teams get a baseline skill library without needing each developer to check files into their repo.

### Tips

- Keep descriptions specific and action-oriented ("Run tests and report failures" not "Testing stuff")
- Include trigger phrases in the description — Cascade uses it for matching
- One skill = one atomic task. Chain skills via workflows for complex tasks
- Use the global path (`~/.codeium/windsurf/skills/`) for skills you want in every project

---

## 6. MCP Server Integration

### The Easiest Way

Cascade panel → **MCPs** icon in the top right menu → browse the Marketplace → **Install**. No JSON needed. Official MCPs show a blue checkmark indicating they're maintained by the parent service.

### Manual Configuration

For custom servers or env-specific setups, edit `mcp_config.json`:

| Location | Scope |
|----------|-------|
| `~/.codeium/windsurf/mcp_config.json` | User (global) |
| `.windsurf/mcp_config.json` | Workspace |

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/workspace"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@github/github-mcp-server"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_xxxxxxxxxxxx"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost/db"
      }
    }
  }
}
```

Windsurf supports three MCP transports: **stdio** (most common), **Streamable HTTP**, and **SSE**. For HTTP servers the URL should point at the MCP endpoint, e.g. `https://your-server.com/mcp`.

### OAuth — Auto-Trigger for HTTP/SSE

When you add an HTTP or SSE MCP server that requires OAuth, Windsurf automatically opens the login flow instead of failing silently. Added in Feb 2026 — this was a huge source of friction before.

### The 100-Tool Limit

Cascade enforces a ceiling of **100 total tools** at any given time across all enabled MCP servers. If you install a bunch of servers and hit the ceiling, you can toggle individual tools on/off from each MCP's settings page (Cascade panel → MCPs icon → click the server → toggle specific tools).

This matters a lot with fat servers like GitHub, Linear, Slack, Notion — each can expose 30+ tools individually. Disable the ones you don't need; keep your tool budget for the high-leverage stuff.

### MCP Whitelist (Auto-Approval Regex)

For MCP tools you use constantly (and trust), configure auto-approval via regex so Cascade doesn't stop and ask each call. Matches against the full tool call string. Use anchored, narrow patterns — don't blanket-allow write tools.

### Building a Custom MCP Server

If you need to connect Cascade to a tool without an existing MCP server (CRM, email, custom API), build one with Python and the MCP SDK:

**Install:**

```bash
pip install mcp requests
```

**`my_mcp_server.py`:**

```python
#!/usr/bin/env python3
"""Custom MCP server — stdio transport."""

import os
import json
import asyncio
import requests
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp.types import Tool, TextContent

API_KEY = os.getenv("API_KEY", "")
BASE_URL = "https://api.example.com"
TIMEOUT = 10

server = Server("my-server")

@server.list_tools()
async def list_tools():
    return [
        Tool(
            name="get_record",
            description="Fetch a record by ID",
            inputSchema={
                "type": "object",
                "properties": {
                    "record_id": {"type": "string", "description": "The record ID"}
                },
                "required": ["record_id"]
            }
        ),
        Tool(
            name="search_records",
            description="Search records by query",
            inputSchema={
                "type": "object",
                "properties": {
                    "query": {"type": "string", "description": "Search query"},
                    "limit": {"type": "integer", "description": "Max results", "default": 10}
                },
                "required": ["query"]
            }
        )
    ]

@server.call_tool()
async def call_tool(name: str, arguments: dict):
    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    }

    try:
        if name == "get_record":
            resp = requests.get(
                f"{BASE_URL}/records/{arguments['record_id']}",
                headers=headers,
                timeout=TIMEOUT
            )
            resp.raise_for_status()
            return [TextContent(type="text", text=json.dumps(resp.json(), indent=2))]

        elif name == "search_records":
            resp = requests.get(
                f"{BASE_URL}/search",
                headers=headers,
                params={"q": arguments["query"], "limit": arguments.get("limit", 10)},
                timeout=TIMEOUT
            )
            resp.raise_for_status()
            return [TextContent(type="text", text=json.dumps(resp.json(), indent=2))]

    except requests.exceptions.Timeout:
        return [TextContent(type="text", text="Error: Request timed out")]
    except requests.exceptions.HTTPError as e:
        return [TextContent(type="text", text=f"Error: HTTP {e.response.status_code}")]
    except Exception as e:
        return [TextContent(type="text", text=f"Error: {str(e)}")]

if __name__ == "__main__":
    asyncio.run(stdio_server(server))
```

**Register it in `mcp_config.json`:**

```json
{
  "mcpServers": {
    "my-server": {
      "command": "python",
      "args": ["my_mcp_server.py"],
      "env": {
        "API_KEY": "your_key_here"
      }
    }
  }
}
```

### Admin Controls & Custom Registries

Teams/Enterprise admins can:
- Point Cascade at a **custom MCP registry** instead of the public Marketplace
- Configure org-wide MCP whitelists and defaults via the cloud dashboard
- Pre-install MCP servers for every user in the org

See the admin docs in your Teams settings for details.

### SSE Is Deprecated — Migrate to Streamable HTTP (April 2026)

The MCP transport layer is consolidating fast. If your `mcp_config.json` has `"transport": "sse"` on any remote server, that integration is on borrowed time:

- **Keboola** dropped SSE support April 1, 2026
- **Atlassian** deadline is June 30, 2026
- Every new MCP server shipped in 2026 only supports **Streamable HTTP** (single endpoint, stateful sessions via `Mcp-Session-Id` header, optional server-initiated streaming)
- [The MCP spec formally deprecated HTTP+SSE transport](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports) in the 2025-06-18 revision

Cascade supports both. Update your remote configs:

```jsonc
// OLD — deprecated
{
  "mcpServers": {
    "some-saas": {
      "transport": "sse",
      "url": "https://api.example.com/mcp/sse"
    }
  }
}

// NEW — Streamable HTTP
{
  "mcpServers": {
    "some-saas": {
      "transport": "streamable-http",
      "url": "https://api.example.com/mcp"
    }
  }
}
```

For **your own servers**: the [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) ships `StreamableHTTPServerTransport` — one route instead of two, proper proxy behavior, no load-balancer stickiness required. Known gotcha: SDK 1.25–1.27 has a regression where sessions die on TCP keepalive timeout; pin to 1.24.x until it's patched, or keep an SSE GET stream open during idle. Python: `mcp.server.streamable_http` since SDK 1.9.

**Why this matters for Cascade specifically:** several MCPs in the public Marketplace still list SSE transport. When they go dark, your workflows silently lose tools. Audit your active servers at the start of every sprint until Q3 2026.

### New MCP Servers Worth Adding (April 2026)

These landed in the last two weeks and are worth a slot in your config:

| Server | Ships | Why it's worth adding |
|---|---|---|
| [GitHub MCP Server 0.33.0](https://github.com/github/github-mcp-server/releases/tag/v0.33.0) | Apr 14 | Resolves review threads, `path` / `since` / `until` filters on `list_commits`, OAuth auto-trigger, OSS logging adapter for HTTP. Replaces any hand-rolled `gh` wrapper you had. |
| [Azure MCP Server 2.0 GA](https://devblogs.microsoft.com/azure-sdk/announcing-azure-mcp-server-2-0-stable-release) | Apr 10 | **276 tools across 57 Azure services.** Self-hosted remote MCP — deploy it where your team is. Kills every bespoke Azure wrapper script. |
| [Keboola MCP](https://github.com/keboola/mcp-server) | Streamable HTTP only as of Apr 1 | Data pipelines, warehouses, flows. Good reference implementation of the new transport. |
| [Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp) | Updated Apr 2026 | Browser automation for Cascade beyond the built-in [Windsurf Browser](#13-web-search--windsurf-browser) — real Chrome, not Chromium-embedded. |
| [AWS MCP Suite](https://github.com/awslabs/mcp) | Ongoing | Official AWS MCP servers for Bedrock, Cost Explorer, Lambda, ECS. Streamable HTTP. |
| [Playwright MCP](https://github.com/microsoft/playwright-mcp) | v1.1.0 Apr 2026 | E2E browser tests scripted by Cascade. Plays nicer than the Windsurf Browser for repeatable flows. |
| [fastmcp](https://github.com/jlowin/fastmcp) | 2.x stable | Not a server — the best Python SDK for *writing* MCP servers. Faster than the official SDK and Streamable-HTTP-first. |

**Dynamic tool loading.** GPT-5.4 added first-class `search_tools`. If your custom MCP has >30 tools, implement a `list_tools` endpoint that returns only relevant tools per query instead of dumping everything into Cascade's context. This alone frees up 5–15k tokens per turn. The [Azure MCP Server](https://github.com/Azure/azure-mcp) is the canonical example — 276 tools, but Cascade only ever sees the handful relevant to the current prompt.

### MCP Server Quality Rules

| Rule | Why |
|------|-----|
| Always set `timeout` on HTTP calls | Prevents Cascade from hanging on dead endpoints |
| Never hardcode API keys | Use `env` in mcp_config.json |
| Return clear error messages | Cascade shows them to the user |
| Keep tool descriptions specific | Cascade uses them to decide which tool to call |
| Use `inputSchema` with required fields | Prevents ambiguous tool calls |
| Keep total tool count per server low | Cascade's 100-tool ceiling is shared across all servers |

---

### Official MCP Server Setup Guides

Step-by-step setup for popular official MCP servers in Windsurf.

#### GitHub MCP Server

**1. Get a GitHub Personal Access Token:**
- Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
- Generate new token with scopes: `repo`, `read:org`, `read:user`, `issues:write`, `pull_requests:write`
- Copy the token (starts with `ghp_`)

**2. Install the server:**

**Via Marketplace (easiest):**
- Cascade panel → MCPs icon → search "GitHub" → Install

**Via Manual Config:**
Add to `~/.codeium/windsurf/mcp_config.json` (global) or `.windsurf/mcp_config.json` (project):

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@github/github-mcp-server"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_YOUR_TOKEN_HERE"
      }
    }
  }
}
```

**3. Restart Windsurf** to load the new MCP server.

**4. Test it:**
Type in Cascade: "List my recent GitHub issues" or "Create an issue in this repo titled 'Test from Windsurf'"

**Available tools:** `search_repositories`, `create_issue`, `update_issue`, `list_issues`, `create_pull_request`, `list_commits`, `get_file_contents`, `create_branch`, `push_files`

---

#### Notion MCP Server

**1. Get a Notion Integration Token:**
- Go to [notion.so/my-integrations](https://www.notion.so/my-integrations)
- Create new integration → Name it "Windsurf" → Copy "Internal Integration Token"
- Share specific Notion pages/databases with this integration (required!)

**2. Install the server:**

**Via Marketplace:**
- Cascade panel → MCPs icon → search "Notion" → Install

**Via Manual Config:**
```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notion/mcp-server"],
      "env": {
        "NOTION_TOKEN": "secret_YOUR_TOKEN_HERE"
      }
    }
  }
}
```

**3. Share pages with the integration:**
- In Notion, go to the page/database you want to access
- Click "..." → Add connections → Select your "Windsurf" integration
- Repeat for all pages you need access to

**4. Restart Windsurf** and test: "Search my Notion pages for 'project roadmap'"

**Available tools:** `search_pages`, `get_page`, `create_page`, `update_page`, `query_database`, `create_database_item`

---

#### Slack MCP Server

**1. Create a Slack App:**
- Go to [api.slack.com/apps](https://api.slack.com/apps)
- Create New App → From scratch → Name it "Windsurf" → Select your workspace
- Go to OAuth & Permissions → Add scopes: `chat:write`, `channels:read`, `groups:read`, `im:read`, `mpim:read`, `users:read`, `search:read`
- Install to Workspace → Copy "Bot User OAuth Token" (starts with `xoxb-`)

**2. Install the server:**

**Via Marketplace:**
- Cascade panel → MCPs icon → search "Slack" → Install

**Via Manual Config:**
```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@slack/mcp-server"],
      "env": {
        "SLACK_TOKEN": "xoxb-YOUR_TOKEN_HERE"
      }
    }
  }
}
```

**3. Invite the bot to channels:**
- In Slack, type `/invite @Windsurf` in each channel you want it to access

**4. Restart Windsurf** and test: "Send a message to #general saying 'Hello from Windsurf'"

**Available tools:** `post_message`, `get_channel_history`, `search_messages`, `list_channels`, `get_user_info`

---

### Multi-Platform Workflows

Combine MCP servers for cross-platform automation:

**Example workflow:**
```
"Find all GitHub issues labeled 'urgent' in my repo,
summarize them, and post the summary to Slack #engineering"
```

**Requirements:**
- GitHub MCP server configured
- Slack MCP server configured
- Both have appropriate permissions

**Another example:**
```
"Create a Notion page documenting the architecture decisions
from the last 5 GitHub PRs in this repo"
```

---

## 7. Directory-Scoped Instructions (AGENTS.md)

### How It Works

Place an `AGENTS.md` file in any directory. Cascade reads it automatically when working on files in that directory. Root-level AGENTS.md applies globally; subdirectory versions supplement it for files within.

**Project Root (`AGENTS.md`):**

```markdown
# Project Guidelines

## Architecture
- Use MCP servers for all external API integrations
- Shared types live in src/types.py
- Configuration via environment variables, never hardcoded

## Code Style
- TypeScript strict mode — no `any` types
- All functions have return type annotations
- Imports sorted: stdlib → third-party → local

## Testing
- Every new feature gets a test file
- Use vitest for unit tests
- Integration tests use MSW for API mocking
```

**`src/api/AGENTS.md`:**

```markdown
# API Layer Guidelines

- All API calls go through MCP servers, never direct HTTP
- Error responses include: error code, message, request ID
- Rate limiting: always respect Retry-After headers
- Never log full request bodies (may contain PII)
```

**`src/components/AGENTS.md`:**

```markdown
# Component Guidelines

- Functional components with TypeScript interfaces for props
- CSS modules or Tailwind — no inline styles
- Accessibility: all interactive elements need aria-labels
- Storybook stories for complex components
```

### Tips

- Keep AGENTS.md files short and specific to the directory
- Use them for rules that would be repetitive to state in every prompt
- Subdirectory AGENTS.md supplements (doesn't replace) the root file

### The Instruction File Hierarchy (Apr 2026)

A file-hierarchy convention is going around the agent-coding space — cross-agent guides now reference **five** different Markdown files with distinct jobs. Most people are only using one. Cascade supports all of them today; the docs just hadn't caught up. Here's the map:

| File | Scope | Cascade reads it? | Use it for |
|---|---|---|---|
| `AGENTS.md` | Directory-scoped rules, committed to repo | **Yes** — native, reads the whole tree | Project conventions, guardrails, stack info, commands to run |
| `CLAUDE.md` | Anthropic/Claude Code convention for the same thing | **Yes** — Cascade picks it up as a fallback when `AGENTS.md` is absent | Keep in sync with `AGENTS.md` if you also work in Claude Code |
| `.windsurfrules` | Legacy Windsurf project rules file | **Yes** — still supported | Free-form prose rules. Commit to repo. |
| `SKILL.md` (inside `.windsurf/skills/<name>/`) | Per-skill instructions + bundled resources | **Yes** — via the [Skills system](#5-skills-system) | Reusable multi-step procedures, scripts, resources |
| `MEMORY.md` (convention, not required) | Long-running learned facts | Via `@mention` + rules | Pin key decisions you want the agent to always recall — Cascade's built-in [Memories](#9-memories--rules) is the preferred way, but a repo-committed `MEMORY.md` works if you want team-shared memory |
| `CONTEXT.md` (convention) | Current-session snapshot | Via `@mention` | "Here's what's happening right now" — swap per session, don't commit |

**The rule of thumb that's going viral:** `AGENTS.md` is the *what not to do* (rules), `SKILL.md` is the *how to do it* (procedures), `MEMORY.md` is *what we already decided* (facts), `CONTEXT.md` is *where we are now* (state). Cascade's built-in [Memories & Rules](#9-memories--rules) handles personal preferences that shouldn't be in the repo at all.

**One-shot cross-agent compatibility.** If you also work in Claude Code, Cursor, Codex, or Gemini CLI, symlink a single file so every agent reads the same rules:

```bash
# From your repo root
ln -s AGENTS.md CLAUDE.md
ln -s AGENTS.md .cursorrules
ln -s AGENTS.md GEMINI.md
ln -s AGENTS.md .windsurfrules
```

Change one file, every agent in every tool updates. This is what the [`@include` directive proposal for Codex](https://github.com/openai/codex/issues/17401) is trying to solve more cleanly — until it ships, symlinks are the answer.

**Gotcha** ([#305](https://github.com/Exafunction/codeium/issues/305)): opening a workspace with nested git repos causes Cascade to load the rules file 2×–9× per response, burning tokens. Either flatten the layout or add `"codeium.rulesFile": "<single-path>"` to workspace settings until this is patched. See [§24 Gotchas](#24-gotchas--known-issues-april-2026).

---

## 8. Hooks

### Configuration

Hooks are defined at three levels (system → user → workspace), merged in priority order — workspace overrides user, user overrides system.

| Location | Scope |
|----------|-------|
| `~/.codeium/windsurf/hooks.json` | User (global — personal defaults for all projects) |
| `.windsurf/hooks.json` | Workspace (project-specific) |

Enterprise admins can distribute hooks through the cloud dashboard; those hooks take effect org-wide and workspace hooks stack on top.

**Official format:**

```json
{
  "hooks": {
    "pre_write_code": [
      {
        "command": "python .windsurf/hooks/check_secrets.py",
        "show_output": true,
        "working_directory": "."
      }
    ],
    "post_write_code": [
      {
        "command": "npx eslint --stdin-filename $FILE",
        "show_output": true
      }
    ],
    "pre_run_command": [
      {
        "command": "python .windsurf/hooks/command_audit.py",
        "show_output": false
      }
    ]
  }
}
```

**Key details:**
- Hooks are nested under a `"hooks"` key
- Each event is an **array** — you can stack multiple hooks per event
- No `"enabled"` flag — omit or remove the entry to disable
- Extra keys: `powershell` (for Windows cross-compat), `working_directory`
- On Windows, use `"powershell"` key or ensure `command` works cross-shell

### Available Hook Points

| Hook | When It Fires | Input (stdin JSON) |
|------|---------------|---------------------|
| `pre_read_code` / `post_read_code` | Before/after reading a file | `tool_info` with file path, agent action, trajectory ID |
| `pre_write_code` / `post_write_code` | Before/after writing to a file | `tool_info` with file path, agent action, trajectory ID |
| `pre_run_command` / `post_run_command` | Before/after terminal command | `tool_info` with command string |
| `pre_mcp_tool_use` / `post_mcp_tool_use` | Before/after MCP tool call | `tool_info` with tool name, args |
| `pre_user_prompt` | Before user's message is sent | prompt contents |
| `post_cascade_response` | After each assistant response | response metadata + `rules_applied` array |
| `post_cascade_response_with_transcript` | After each response, with full transcript | full conversation transcript |
| `post_setup_worktree` | After a new worktree is created | runs inside the worktree dir, `$ROOT_WORKSPACE_PATH` available |

### Hook Contract

- Receives context via **stdin** (JSON — the `tool_info` schema includes `agent_action_name`, `trajectory_id`, and action-specific fields)
- Exit code `0` = allow, exit code `2` = block (for pre-hooks)
- stdout is shown to the user if the hook blocks

### Secret Detection Hook

```python
#!/usr/bin/env python3
"""Block file writes that contain hardcoded secrets."""

import sys
import re
import json

SECRET_PATTERNS = [
    r'(?i)api[_-]?key\s*[=:]\s*["\'][a-zA-Z0-9]{20,}',
    r'(?i)secret\s*[=:]\s*["\'][a-zA-Z0-9]{20,}',
    r'(?i)password\s*[=:]\s*["\'][^"\']{8,}',
    r'sk-[a-zA-Z0-9]{48}',       # OpenAI
    r'ghp_[a-zA-Z0-9]{36}',       # GitHub
    r'sk-ant-[a-zA-Z0-9-]{90,}',  # Anthropic
    r'AIza[a-zA-Z0-9_-]{35}',     # Google
]

def main():
    try:
        tool_info = json.loads(sys.stdin.read())
        filepath = tool_info.get("file_path") or tool_info.get("file") or tool_info.get("path", "")
    except (json.JSONDecodeError, KeyError):
        sys.exit(0)  # Allow on parse failure — don't block on hook bugs

    if not filepath:
        sys.exit(0)

    try:
        with open(filepath, 'r') as f:
            content = f.read()
    except (FileNotFoundError, PermissionError):
        sys.exit(0)

    for pattern in SECRET_PATTERNS:
        match = re.search(pattern, content)
        if match:
            print(f"BLOCKED: Potential secret detected in {filepath}")
            print(f"  Pattern: {pattern}")
            print(f"  Match: {match.group()[:20]}...")
            sys.exit(2)  # Exit code 2 = block

    sys.exit(0)  # Allow

if __name__ == "__main__":
    main()
```

### Observability Hook: Log Every Response + Rules Applied

Use `post_cascade_response` to ship Cascade's behavior to your observability stack. The `rules_applied` field (added Feb 2026) lists which memories/rules were actually triggered for each response — invaluable for tuning rules over time.

```python
#!/usr/bin/env python3
"""Ship every Cascade response + applied rules to a JSONL log."""
import sys, json, time, pathlib

LOG = pathlib.Path.home() / ".codeium" / "windsurf" / "responses.jsonl"
LOG.parent.mkdir(parents=True, exist_ok=True)

try:
    data = json.loads(sys.stdin.read())
except json.JSONDecodeError:
    sys.exit(0)

entry = {
    "ts": time.time(),
    "trajectory_id": data.get("trajectory_id"),
    "rules_applied": data.get("rules_applied", []),
    "response_summary": (data.get("content") or "")[:200],
}

with LOG.open("a") as f:
    f.write(json.dumps(entry) + "\n")

sys.exit(0)
```

Pipe this file into LangFuse or Datadog for a Cascade-native analog of what LangFuse gives Hermes/OpenClaw out of the box (see [Section 19](#19-harness-parity-hermesopenclaw-features-in-cascade)).

### Auto-Format on Write

Runs your formatter after Cascade modifies code — the Cascade analog of a git pre-commit hook but agent-side.

```json
{
  "hooks": {
    "post_write_code": [
      { "command": "npx prettier --write $FILE", "show_output": false },
      { "command": "npx eslint --fix $FILE", "show_output": false }
    ]
  }
}
```

### Block Dangerous Commands

```python
#!/usr/bin/env python3
"""Block rm -rf /, dd to /dev/sd*, force pushes to main, etc."""
import sys, re, json

BLOCKED = [
    r"rm\s+-rf\s+/(\s|$)",
    r"dd\s+.*of=/dev/sd",
    r"git\s+push\s+.*--force\s+.*\b(main|master)\b",
    r":\(\)\s*\{\s*:\|\:&\s*\}",  # fork bomb
]

data = json.loads(sys.stdin.read())
cmd = data.get("command") or data.get("tool_info", {}).get("command", "")

for pattern in BLOCKED:
    if re.search(pattern, cmd):
        print(f"BLOCKED: Dangerous pattern matched: {pattern}")
        sys.exit(2)

sys.exit(0)
```

Full list of hook events at [docs.windsurf.com/windsurf/cascade/hooks](https://docs.windsurf.com/windsurf/cascade/hooks).

### Hook Merge Order

Hooks merge in priority order: **system → user → workspace → cloud dashboard (Enterprise)**. Workspace hooks override user hooks, which override system defaults.

---

## 9. Memories & Rules

### The Built-In Memory System

Windsurf has a native **Memories & Rules** system that persists context across sessions. This is the primary way to give Cascade long-term memory.

**How to access:** Cascade panel → Memories & Rules icon (or Settings → Cascade → Memories)

**Two types:**

| Type | Scope | Use For |
|------|-------|---------|
| **Memories** | Auto-captured | Things Cascade learns during conversation (preferences, patterns, decisions) |
| **Rules** | User-defined | Explicit instructions that always apply (coding style, naming conventions, architecture) |

### Setting Up Rules

Add rules through the Cascade UI (Memories & Rules → Rules tab):

```
Always use TypeScript strict mode.
Never use `any` — use proper interfaces or `unknown`.
All API calls must have a 10-second timeout.
Use named exports, not default exports.
```

### Trace Which Rules Actually Fire (`rules_applied`)

The `post_cascade_response` hook includes a `rules_applied` field — a list of memory/rule IDs that actually matched and shaped that response. Log it to see which rules are earning their keep and which are dead weight.

If you have 40 rules and only 3 ever fire, the other 37 are burning context for no reason. Delete them.

### SOUL — The Global-Rules Personality Layer

The highest-leverage use of Rules is a **personality file** — a set of rules that tell Cascade *how to behave*, not just *what the project is*. Default Cascade is RLHF-polished toward "helpful assistant": it hedges, pads, asks permission, opens with "Great question!" A good personality file overrides all of that.

We ship a community-safe version as **[`SOUL.md`](./SOUL.md)** at the root of this repo. Five sections:

| Pillar | What it fixes |
|---|---|
| **1. Core Identity & Vibe** | No throat-clearing, no HR-speak, no "I'd be happy to help". Direct, opinionated, terse. |
| **2. Execution & Autonomy** | Fix-and-retry instead of report-and-wait. Push back on bad premises. Surface gaps proactively. |
| **3. Engineering Rigor & Validation** | "Looks good" banned. Round-trip diffs on real input. Per-stage metric breakdowns. |
| **4. Speed, Context & Orchestration** | Parallelize by default. Batch reads. Timeouts on every network call. |
| **5. Workflows, Memory & Code** | Every non-trivial task becomes a reusable workflow. One learning saved to memory per task. |

**Install** (applies to every Windsurf project, forever):

```bash
# awk filter strips the wrapper doc and keeps only the 5 rule pillars.
# Temp file + mv pattern preserves existing rules if curl fails.
mkdir -p ~/.codeium/windsurf/memories
tmp=$(mktemp) && \
  curl -fsSL https://raw.githubusercontent.com/OnlyTerp/windsurf-unlocked/main/SOUL.md \
  | awk '/^## 1\. Core Identity/{p=1} /^## How to Install/{p=0} p' > "$tmp" \
  && [ -s "$tmp" ] && mv "$tmp" ~/.codeium/windsurf/memories/global_rules.md \
  || { rm -f "$tmp"; echo "Install failed — existing rules preserved."; }
```

Or paste into **Cascade Settings → Rules → Global Rules** via the UI. Full file and customization notes: **[`SOUL.md`](./SOUL.md)**.

One file, zero per-project setup, measurable change in Cascade output within the first prompt. If you only install one thing from this guide, install this.

### Memories & Rules vs AGENTS.md

| Feature | Memories & Rules | AGENTS.md |
|---------|-----------------|-----------|
| Scope | Global (all projects) | Per-directory |
| Persistence | Session-to-session | File-based |
| Best for | Personal preferences, coding style | Project architecture, conventions |
| Discovery | Cascade UI | Automatic by file location |

Use both. AGENTS.md for project context, Memories & Rules for personal preferences.

---

## 10. Workflows

### Slash-Command Automations

Workflows are reusable multi-step automations stored as markdown in `.windsurf/workflows/`. They use YAML frontmatter for metadata and markdown body for steps.

**`.windsurf/workflows/new-feature.md`:**

```yaml
---
name: new-feature
description: Scaffold a new feature with tests, types, and docs
---

# New Feature: {{feature_name}}

1. Create directory structure:
   - src/features/{{feature_name}}/
   - src/features/{{feature_name}}/index.ts
   - src/features/{{feature_name}}/{{feature_name}}.test.ts
   - src/features/{{feature_name}}/{{feature_name}}.types.ts

2. Generate boilerplate with correct naming

3. Run the deploy-check skill to validate the scaffold

4. Open the main file for editing
```

**`.windsurf/workflows/refactor-module.md`:**

```yaml
---
name: refactor-module
description: Safely refactor a module with tests and git tracking
---

# Refactor: {{module_path}}

1. Run tests and capture baseline (must all pass)
2. Create a git branch: refactor/{{module_name}}
3. Make the requested changes
4. Re-run tests — must match baseline
5. If tests break, revert and report what went wrong
6. If clean, stage changes and suggest a commit message
```

Workflows use the same YAML frontmatter format as skills (`name` + `description`) but support multi-step orchestration with `{{variable}}` substitution.

### Tips

- Use `{{variable}}` syntax for workflow parameters
- Reference skills in workflow steps by name
- Workflows are multi-step orchestrations; skills are atomic tasks — chain skills via workflows for complex automation

---

## 11. Worktrees — Parallel Cascade

Git worktrees let you run Cascade tasks in parallel without interfering with your main workspace. Each Cascade conversation gets its own checkout, so it can edit, build, and test independently of whatever you're doing in the main checkout.

### Starting a Worktree Session

In the Cascade input box, open the mode toggle (bottom right) and switch to **Worktree** before sending the first message. You can only switch into a worktree **at the start** of a session — not mid-conversation.

When Cascade finishes, click **Merge** to integrate the changes back into your main workspace.

### Where Worktrees Live

```
~/.windsurf/worktrees/<repo_name>/<random_id>/
```

Run `git worktree list` in your repo to see them. Windsurf cleans up older worktrees automatically.

**Gotcha:** if your project uses relative paths outside the repo root (symlinked deps, `../shared-lib`, monorepo source deps), they'll break inside a worktree because the worktree lives in a different directory. Use a `post_setup_worktree` hook to recreate the links.

### `post_setup_worktree` Hook

This hook runs inside the **new worktree directory** after it's created, with `$ROOT_WORKSPACE_PATH` pointing back at the original repo. Use it to copy `.env` files, install deps, symlink shared folders.

**`.windsurf/hooks.json`:**
```json
{
  "hooks": {
    "post_setup_worktree": [
      {
        "command": "bash $ROOT_WORKSPACE_PATH/hooks/setup_worktree.sh",
        "show_output": true
      }
    ]
  }
}
```

**`hooks/setup_worktree.sh`:**
```bash
#!/bin/bash

# Copy environment files from the original workspace
for f in .env .env.local .env.development; do
  if [ -f "$ROOT_WORKSPACE_PATH/$f" ]; then
    cp "$ROOT_WORKSPACE_PATH/$f" "$f"
    echo "Copied $f"
  fi
done

# Install dependencies
if [ -f "package.json" ]; then
  npm install
fi
if [ -f "pyproject.toml" ]; then
  uv sync || pip install -e .
fi

# Symlink monorepo siblings if your repo expects them
if [ -d "$ROOT_WORKSPACE_PATH/../shared-lib" ]; then
  ln -sfn "$ROOT_WORKSPACE_PATH/../shared-lib" "../shared-lib"
fi

exit 0
```

### When to Use Worktrees

- **Risky refactors** — let Cascade go wild in a worktree, review the diff before merging
- **Long-running tasks** — keep typing in main while Cascade works
- **Arena Mode** — each model in Arena Mode gets its own worktree automatically (see next section)
- **Trying multiple approaches** — spin up 3 worktree sessions with different strategies, keep the best one

---

## 12. Arena Mode — Side-by-Side Models

Arena Mode runs multiple Cascade instances in parallel with different models and lets you pick the best output. Each model gets its own worktree, so they don't step on each other.

### How to Enter Arena

Open the model picker and click the **Arena** tab. Either pick specific models or use a **Battle Group** (Windsurf randomizes the two models for you).

| Mode | Use Case |
|------|----------|
| **Single** | Run Cascade with a single chosen model |
| **Arena** | Compare responses from two models on the same prompt |

### Battle Groups

| Group | Contents | Best for |
|-------|----------|----------|
| **Frontier** | GPT 5.4, Claude Opus/Sonnet 4.6, Gemini 3.1 Pro, etc. | Intelligence-heavy design / architecture work |
| **Fast** | SWE 1.6, SWE 1.6 Fast, Claude Haiku, GPT-5.3-Codex-Spark | Speed, simple edits, refactors |
| **Hybrid** | Mix of frontier + fast | Balanced comparison |

Names are hidden until you click **"X is better"** to converge. Then identities are revealed and the two conversations are reshuffled. Your votes feed both a personal leaderboard and a global one at [windsurf.com/leaderboard](https://windsurf.com/leaderboard).

### Converge Workflow

1. Send prompt → both models run in parallel, each in its own worktree
2. Evaluate both outputs — code, test results, diff size
3. Click **"Left is better"** or **"Right is better"** to discard the loser
4. Subsequent messages go to both models simultaneously (so you can keep comparing) or stay single-track — your choice

### Cost

Arena charges the sum of the individual model costs for each turn. A 6x model + 4x model = 10x credits per request. For Battle Groups the displayed cost is the **maximum** of the two possible models so you can't be surprised.

### Pro Pattern

Use Arena + Battle Groups as a live benchmark. Over 20-30 tasks you'll develop calibrated intuition about which model actually wins on *your* codebase — independent of benchmarks and hype.

---

## 13. Web Search & Windsurf Browser

### `@web` and `@docs`

Cascade can browse the internet like a human: skim a page, find the relevant section, pull only the chunks it needs. This keeps credit usage low.

Four ways to trigger it:

| Trigger | What happens |
|---------|-------------|
| Natural phrasing ("what's new in the latest React?") | Cascade auto-decides to web search |
| `@web <query>` | Force a general web search |
| `@docs <query>` | Search over a curated docs set that Cascade reads with high quality |
| Paste a URL into your message | Cascade reads that specific page |

The **Enable Web Search** admin setting controls open-internet search. Even if it's disabled, Cascade can still read specific URLs you paste in — URL reads happen **locally on your machine**, inside your network (so a VPN is fine).

### Windsurf Browser (2.0)

Windsurf 2.0 ships a refined **in-editor Chromium browser** with a Cascade tool for reading page contents. Practical uses:

- Cascade can pull logs, dashboards, admin pages from inside Windsurf without leaving the editor
- Run your dev server and inspect it without opening Chrome
- Let Cascade iterate on visual UI changes by reloading and reading the rendered page
- Authenticate once to internal tools; the session persists for future reads

### Reading GitHub / Blog Posts / Docs

Paste the URL and Cascade breaks the page into chunks similar to how you'd skim it. For long pages it jumps to the section that matches your question. Most mainstream doc sites parse cleanly; some JS-heavy SPAs are hit-or-miss — file a feature request if a site you rely on is broken.

### Tip

Combine with Skills: wrap `@docs` calls for your specific stack into named skills (e.g. `@django-docs`, `@stripe-docs`) so Cascade reaches for the right reference automatically.

---

## 14. App Deploys — One-Click Netlify

Cascade can deploy a web app to a public URL in one step. Useful for shipping previews fast.

### What's Supported

- **Provider:** Netlify
- **Frameworks:** Next.js, React, Vue, Svelte (more coming)
- **Output URL format:** `<your-subdomain>.windsurf.build`

### Deploying

Just ask Cascade:

```
"Deploy this project to Netlify"
"Update my deployment"
```

Cascade analyzes your project, picks the framework, uploads files, creates the deployment, and hands you:
- A public URL
- A claim link (to move the project into your own Netlify account for custom domains, env vars, etc.)

It writes a `windsurf_deployment.yaml` at the repo root storing the project ID and framework so re-deploys hit the same URL.

### Claim Your Deploy

App Deploys are intended as previews. For production, **claim the deployment** (click the claim link) and point your own Netlify account at it — that's where you add custom domains, secret env vars, and production-grade security.

### Team Deploys

Teams/Enterprise admins can connect a Netlify Team account so deploys go to your org's Netlify instead of the Windsurf umbrella account. Toggle in Team Settings.

### Pairing with Devin

Ask Devin (see [Section 3](#3-devin-in-windsurf--cloud-delegation)) to handle longer deploy workflows — it has full VM access, a browser, and can complete interactive flows (DNS cutovers, secret rotation, etc.) that need a human-like touch.

---

## 15. Editor-Layer AI: DeepWiki, Codemaps, Vibe and Replace

These are Windsurf features outside the Cascade chat that most users never touch.

### DeepWiki

The same DeepWiki feature from Devin — brought into the editor as hover explanations.

- Hover a symbol → `Cmd+Shift+Click` → DeepWiki opens a detailed explanation in the Primary Side Bar
- Works on functions, classes, variables — explains what the code actually does, not just its type signature
- Click **⋮ → Add to Cascade** to push the DeepWiki explanation into the current Cascade session as an `@mention`

Use it for onboarding into an unfamiliar codebase. Pair with Codemaps (below) for the macro view.

### Codemaps

Shareable hierarchical maps of how your code executes. Generated by a specialized agent.

- Open from the Activity Bar or via Command Palette → "Focus on Codemaps View"
- Create from a suggested topic, a custom prompt, or from the bottom of a Cascade conversation
- Each node links to a file + function — click to jump
- Share links with teammates; viewable in any browser
- `@mention` a Codemap in Cascade to give it macro structural context

**Codemap vs DeepWiki:** DeepWiki is per-symbol. Codemaps are per-flow (e.g. "what happens when a user signs up").

### Vibe and Replace

AI-powered find-and-replace. Instead of a literal string swap, you describe what you want done to each match in natural language.

- **Smart mode** — slow, careful, uses a more capable model
- **Fast mode** — quick, uses SWE 1.6 Fast or similar

Example:
```
Find: fetch(
Vibe prompt: "Add a 10-second timeout and consistent error handling"
```

Every `fetch(` call gets rewritten with your pattern. Much cleaner than a regex sweep for anything context-dependent.

### Productivity Tips

- DeepWiki while reading → Codemaps while planning → Cascade while building → Vibe and Replace for systematic touch-ups
- Use `@mention` to chain artifacts: a Codemap + a plan + a skill + a rule in a single Cascade prompt

---

## 16. Model Optimization — SWE 1.6, Adaptive, Battle Groups

### The Model Landscape (as of April 2026)

| Model | Speed | Cost | Best For |
|-------|-------|------|----------|
| **SWE 1.6** | ~200 tok/s (Fireworks) | **Free for 3 months** | New default for most agentic coding |
| **SWE 1.6 Fast** | ~950 tok/s (Cerebras) | Paying plans, very low cost | Speed-sensitive tasks — most of them, honestly |
| **SWE 1.5** | ~950 tok/s | Low | Previous-gen, still great; pin if you depend on its behavior |
| **swe-grep** | ~fast | Very low | Powers [Fast Context](https://docs.windsurf.com/context-awareness/fast-context); not manually selectable |
| **SWE-1-mini** | Real-time | — | Powers passive suggestions in Windsurf Tab |
| **Adaptive** | Varies | Fixed per-token rate | Let Windsurf route to the right model per-task |
| **GPT-5.4** / **5.4 Mini** | Medium | Promo 1x / 2x / 3x / 8x | General purpose, big context |
| **GPT-5.2-Codex** | Medium | — | Long sessions in huge codebases |
| **Claude Sonnet 4.6** | Medium | 2x / 3x | Complex logic, debugging, sharp refactors |
| **Claude Opus 4.7** (base) | Medium | Promo (check picker) | **New Apr 16, 2026** — Anthropic's most capable GA model; 1M context, 128K output, high-res vision. Default Opus choice for agentic coding. |
| **Claude Opus 4.7 Think (Low / Medium / High / MAX)** | Slow→Very slow | Tiered credits (high multiplier at MAX) | Explicit thinking-level picker — pick the deepest tier only for the hardest 5% of work. See [Power Move #0](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026). |
| **Claude Opus 4.6 (Fast)** | ~2.5x Opus speed | 10x / 12x | Heavy-duty reasoning, architecture |
| **Claude Opus 4.6** | Slow | 2x / 3x | Same intelligence as fast mode, cheaper, slower |
| **Claude Opus 4.6 Think** | Slow | 8x | Prior-gen thinking Opus — still great; pin if you need stable behavior while 4.7 is new |
| **Gemini 3.1 Pro** (Low/High Thinking) | Fast | 0.5x / 1x | Strong on structured tasks, multimodal |
| **Gemini 3 Flash** | Very fast | — | Pro-grade reasoning at Flash speed |
| **Kimi K2 / K2.5 / [K2.6](https://aitoolsrecap.com/Blog/moonshot-ai-kimi-k2-6-release-coding-agent-benchmarks-2026)** | Fast | **Free / low-credit promo** (check picker) | Open-weights frontier from Moonshot — [58.6% SWE-Bench Pro](https://aitoolsrecap.com/Blog/moonshot-ai-kimi-k2-6-release-coding-agent-benchmarks-2026) on K2.6, beats Opus 4.6 and GPT-5.4 on coding at roughly 5× cheaper list price ([$0.60 / $2.80](https://openrouter.ai/moonshotai/kimi-k2.6) vs Sonnet 4.6's [$3.00 / $15.00](https://pricepertoken.com/pricing-page/model/anthropic-claude-sonnet-4.6) per 1M input/output tokens). Windsurf has kept Kimi K2 in the picker [at low or zero credits](https://www.threads.com/@pahud/post/DMeZLopuyhb) since v1.11.1 (July 2025) and periodically runs [free-to-all promos](https://www.theblockbeats.info/flash/337382). Ideal swarm model — see [Power Move #15](#15-the-kimi-k2-free-swarm--6-parallel-agents-for-0). |
| **GLM-5**, **Minimax M2.5** | Fast | 0.75x / 0.25x | Alternative frontier models for Arena comparison |

Cascade's model picker now shows **per-model input / output / cache-read token rates inline** and a **prompt cache timer** in the context-window indicator. Use both to cost-optimize live.

### SWE 1.6 — The New Default

SWE 1.6 (April 7, 2026) is the new in-house frontier agentic coding model. Highlights from the [release notes](https://cognition.ai/blog/swe-1-6):

- **10%+ better on SWE-Bench Pro** than SWE 1.5
- **Parallel tool calls more often** — dramatically fewer round trips
- **Less looping** — length penalty during training keeps it from going in circles
- **Prefers its own tools over shelling out** — fewer interactive command prompts
- **Up to 950 tok/s** on Cerebras via SWE 1.6 Fast
- **Free tier for 3 months** (via Fireworks at ~200 tok/s)

Translation: **default to SWE 1.6 Fast** for everything except deep reasoning. The speed advantage compounds — one trajectory that used to take 30 seconds now takes 8, and Cascade makes fewer wasteful calls to boot.

### Opus 4.7 Thinking Levels — The Windsurf Picker Advantage

[Claude Opus 4.7](https://www.anthropic.com/news/claude-opus-4-7) (Apr 16, 2026) ships in Cascade with the same tiered picker Windsurf uses for other reasoning models: base + a thinking variant with **Low / Medium / High / MAX** levels. The base model is for agentic coding; the Think variants route more of the response budget through [adaptive thinking](https://platform.claude.com/docs/en/build-with-claude/adaptive-thinking), at a higher credit multiplier.

Where the Windsurf picker wins: every tier is a **separate, credit-priced entry in the model picker** — visible cost per tier, per-message selection, pinnable. Claude Code CLI exposes the same dial through the [`/effort` slash command](https://claudelog.com/faqs/what-is-slash-effort-command/) and the [`ultrathink` keyword](https://claudelog.com/faqs/what-is-ultrathink/) (which returned in v2.1.68 after the [brief Jan 16 deprecation](https://decodeclaude.com/ultrathink-deprecated/)), but it's keyword-driven — no picker, no visible cost before you send. Anthropic's Cowork and Chat surfaces dropped the manual picker entirely for adaptive thinking; you get no tier control at all. Only Cascade puts every tier in the picker with the credit multiplier printed next to each one, so on Windsurf you can:

- **Route most work to base Opus 4.7** or SWE 1.6 Fast (cheap, fast),
- **Escalate tricky-but-bounded problems to Think Low/Medium**,
- **Reserve MAX for the genuinely hard 5%** — architecture, security review, novel algorithms, gnarly debugging — where the 8×+ credit cost buys you reasoning you'd otherwise burn a senior engineer on.

Full recipe with when-to-use-which table and an optional `/max-think` slash command: see [**Power Move #0**](#0-opus-47--thinking-levels-in-the-cascade-picker-apr-16-2026).

**Tokenizer caveat:** Opus 4.7's new tokenizer can tokenize the same English text into [up to ~35% more tokens](https://dev.to/devtorres_/opus-47-uses-35-more-tokens-than-46-heres-what-im-doing-about-it-2del) than Opus 4.6. Sticker price is unchanged ($5 / $25 per 1M), but effective bill per prompt can rise. Prompt caching claws most of that back — use it aggressively ([Power Move #12](#12-prompt-caching-breakpoints--engineer-for-90-token-savings)).

### Adaptive Model Router

The **Adaptive** option in the model picker dynamically selects the right underlying model for each task and draws down quota at a **fixed per-token rate** regardless of which model it picks.

Extra usage promo (as of April 2026):
- **$0.50 / 1M input tokens**
- **$2.00 / 1M output tokens**
- **$0.10 / 1M cache read tokens**

Use Adaptive when:
- You're doing mixed work in a single session and don't want to keep switching
- You want predictable billing
- You've hit quota on a premium model but don't want to context-switch

Don't use Adaptive when you specifically need a certain model's behavior (e.g. Opus for deep debugging, SWE 1.6 Fast for raw speed).

### Routing Prompts with Natural Language

```
/fast  Refactor this util file to use TypeScript
/deep  Design a distributed caching strategy for our API
```

Cascade interprets:
- Short, specific requests → SWE 1.6 / SWE 1.6 Fast
- Complex, open-ended requests → Opus / Sonnet 4.6 / GPT-5.4

### Custom Model Selector Workflow

Create `.windsurf/workflows/fast.md`:

```yaml
---
name: fast
description: Use SWE 1.6 Fast for quick edits and refactors. Optimize for speed.
---

# Fast Mode (SWE 1.6 Fast)

Use the SWE 1.6 Fast model for this task:
- Make minimal changes
- Don't over-explain
- Just show the code
- Skip validation phrases
- Prefer parallel tool calls
```

Then type `/fast` in Cascade to trigger it.

### Pin Your Favorites

The new model picker (Feb 2026) lets you **pin** specific models so they float to the top. Pin SWE 1.6 Fast + Adaptive + Sonnet 4.6 and you've covered 95% of your work with three clicks.

### Prompt Cache Timer

The context-window indicator shows a **prompt cache timer** — how long until the current prompt falls out of the cache. When it's close to expiring, sending a follow-up *before* it expires is much cheaper than after. Useful for back-to-back related queries.

---

## 17. Custom Subagents

### Beyond Directory-Scoped Instructions

AGENTS.md files can define **subagent personalities** — specialized modes that Cascade switches into for specific tasks.

### Example: Terse Mode Profile

Create `.windsurf/agents/terse/AGENT.md`:

```markdown
---
name: terse
description: Ultra-direct coding mode. No validation phrases. Immediate execution.
---

# Terse Agent Profile

## Personality
- Skip throat-clearing ("That's a great idea!", "I'll help you with that")
- Execute immediately without asking permission
- Speed is #1 priority
- Keep responses under 3 sentences when possible

## Execution Rules
- Never re-read files already in context
- Batch tool calls for parallel execution
- If ambiguous, pick the most likely interpretation and proceed
- Show code changes directly, don't describe them

## Communication Style
- Direct statements only
- No bullet point summaries of what you'll do
- No apologies for brevity

## Use When
- The user says "quick fix", "just do it", "make it happen"
- Task is straightforward (refactor, rename, move)
- User seems frustrated with verbosity
```

### Activating Subagents

Type `@terse` in Cascade to switch to that personality.

**Pro tip:** Combine with model selector for `@terse /fast` — fastest possible execution mode. SWE 1.6 Fast + terse personality + Adaptive fallback = a workflow that makes Hermes' `@Molty` style feel clunky.

### Other Useful Profiles

| Profile | Use Case |
|---------|----------|
| `security` | Code review focused on vulnerabilities |
| `docs` | Writing documentation, comments, READMEs |
| `test` | Generating comprehensive test coverage |
| `optimize` | Performance-focused refactoring |
| `reviewer` | PR-style review comments, no code changes |
| `architect` | Plan Mode bias, asks many clarifying questions |

### Bringing the `.claude/agents/` Subagent Pattern to Cascade

The pattern that went viral this week (Apr 12–14, 2026) is Claude Code's **subagents** — per-role specialists in `.claude/agents/*.md` with their own system prompts, tool allow-lists, and **isolated context windows**. Cursor, VS Code Copilot (`runSubagent`), and Gemini CLI have all shipped clones. Cascade doesn't have native delegation, but the *outcome* is achievable today with three building blocks you already have:

1. **`.windsurf/agents/<role>/AGENT.md`** — the personality + tool/model pinning (above)
2. **[Worktrees](#11-worktrees--parallel-cascade)** — isolated filesystem + session per subagent so context doesn't bleed
3. **[Agent Command Center](#2-agent-command-center--spaces)** — the Kanban view that shows all of them running in parallel

**Recipe: an 8-subagent "team" for a real project.**

```
.windsurf/
└── agents/
    ├── architect/AGENT.md   # Plan Mode only, SWE 1.6, asks many clarifying Qs
    ├── implementer/AGENT.md # Code Mode, SWE 1.6 Fast, terse, parallel tool calls
    ├── reviewer/AGENT.md    # Read-only, PR-style comments, Claude Opus 4.6 pin
    ├── tester/AGENT.md      # Generates + runs test suite, blocks on coverage <80%
    ├── security/AGENT.md    # Threat model + vuln scan, read-only
    ├── docs/AGENT.md        # Updates README/AGENTS.md/CHANGELOG, no code
    ├── perf/AGENT.md        # Benchmarks + regressions, runs profiler, reports only
    └── shipper/AGENT.md     # PR description, release notes, deploy checklist
```

Each `AGENT.md` follows the same YAML frontmatter convention as Claude's subagents:

```markdown
---
name: reviewer
description: Read-only PR-style reviewer. Focus on correctness, security, testing gaps, and code smell. Never edits files. Invoke after any non-trivial diff.
model: claude-opus-4.6
tools: [read_file, grep, search_code, web_search]
---

# Reviewer Agent

## Review Checklist
1. Correctness: does the change do what the PR claims?
2. Security: injection, auth, secrets, PII logging
3. Tests: what's missing? What edge cases aren't covered?
4. Code smell: dead code, duplication, unclear names, overly clever constructs
5. Performance: N+1s, unbounded loops, sync calls on hot paths

## Output Format
- One inline comment per issue, grouped by severity (BLOCKER / MAJOR / MINOR / NIT)
- End with a summary and an explicit "LGTM" or "CHANGES REQUESTED"

## Never
- Edit files
- Approve your own work (if invoked on your own diff, say so)
- Rubber-stamp — if you have nothing to say, say that and stop
```

**Running them in parallel.** Kick off 3–4 at once via [Worktrees](#11-worktrees--parallel-cascade) inside a single [Space](#2-agent-command-center--spaces) — architect plans in worktree A, implementer codes in worktree B against the plan, reviewer reviews the PR in worktree C, tester runs the suite in worktree D. The Agent Command Center shows all of them streaming live.

**Why this beats `.claude/agents/`:**
- You keep SWE 1.6 Fast's 950 tok/s for the implementer while pinning the reviewer to Claude Opus 4.6 (the current SWE-Bench leader)
- Worktrees give you true filesystem isolation, not just context isolation
- You can delegate the *whole team* to a single Devin Cloud session via [§3](#3-devin-in-windsurf--cloud-delegation) when you log off

**Pro move:** commit the `.windsurf/agents/` folder to your repo so the whole team inherits the same specialist roster. Then symlink it to `.claude/agents/` so Claude Code users on your team get the same personalities for free.

### Racing Agents (Arena × Subagents)

The "parallel agent racing" pattern (Twill.ai, AgentBox, ctx, April 2026) — running N agents on the same task and picking the winner — is just [Arena Mode](#12-arena-mode--side-by-side-models) with different subagent profiles instead of different models. Combine them:

```
# Same prompt, same model, four different personalities, one Space
@architect /plan Add a rate limiter
@implementer /plan Add a rate limiter
@terse /plan Add a rate limiter
@security /plan Add a rate limiter
```

Let them all produce plans, then hand the best one to the implementer. Costs 4× the plan tokens but you pick from four angles instead of one — invaluable for architecture work where getting the plan wrong costs days.

---

## 18. Real-World Configurations

### Production MCP Server: Attio CRM

```json
{
  "mcpServers": {
    "attio-crm": {
      "command": "python",
      "args": ["attio_mcp_server.py"],
      "env": {
        "ATTIO_API_KEY": "your_attio_key"
      }
    }
  }
}
```

### Production MCP Server: Resend Email

```json
{
  "mcpServers": {
    "resend-email": {
      "command": "python",
      "args": ["resend_mcp_server.py"],
      "env": {
        "RESEND_API_KEY": "re_your_key"
      }
    }
  }
}
```

### Production MCP Server: Airtable

```json
{
  "mcpServers": {
    "airtable-ops": {
      "command": "python",
      "args": ["airtable_mcp_server.py"],
      "env": {
        "AIRTABLE_TOKEN": "pat_your_token",
        "AIRTABLE_BASE_ID": "app_your_base"
      }
    }
  }
}
```

### Combined Setup

Full `.windsurf/` directory for a production project:

```
.windsurf/
├── mcp_config.json          # MCP servers (workspace-level)
├── hooks.json               # Governance hooks
├── skills/
│   ├── run-tests/
│   │   └── SKILL.md
│   ├── deploy-check/
│   │   └── SKILL.md
│   └── api-migration/
│       └── SKILL.md
├── workflows/
│   ├── new-feature.md
│   └── refactor-module.md
├── hooks/
│   ├── check_secrets.py
│   ├── command_audit.py
│   ├── setup_worktree.sh
│   └── response_logger.py
├── agents/
│   └── terse/
│       └── AGENT.md
└── memories/                # Auto-managed by Windsurf
```

Global MCP servers go in `~/.codeium/windsurf/mcp_config.json`. Global skills go in `~/.codeium/windsurf/skills/`.

---

## 19. Harness Parity: Hermes/OpenClaw Features in Cascade

This is the section that triggered this whole guide: **people are paying for standalone AI harnesses (Hermes, OpenClaw, Claude Code wrappers) to get capabilities Cascade already has — or can trivially have through MCP + hooks + skills.** Below is how to reach rough parity with each high-value harness feature, using stock Windsurf.

If you're building a harness, stop. Use this instead.

### 19.1 Graph RAG / LightRAG-Style Memory

**What Hermes/OpenClaw do:** Run a LightRAG server that indexes your notes/code into an entity + relationship graph. Queries return facts like "who decided X and why" instead of just "text similar to X".

**Cascade equivalent:** Stand up LightRAG (or any graph-RAG service) as an MCP server with tools like `query_graph`, `add_fact`, `get_related`. Point a skill at it.

**`.windsurf/skills/deep-recall/SKILL.md`:**
```yaml
---
name: deep-recall
description: Query the project knowledge graph for decisions, entities, and relationships. Use when the user asks "why did we", "who decided", "what's the history of X".
---

# Deep Recall

1. Call lightrag.query_graph with the user's question
2. Present the returned entities + relationships
3. For each relationship, link to the source file/PR
4. If nothing matches, fall back to file search
```

**`.windsurf/mcp_config.json`:**
```json
{
  "mcpServers": {
    "lightrag": {
      "command": "python",
      "args": ["/path/to/lightrag_mcp_server.py"],
      "env": {
        "LIGHTRAG_URL": "http://localhost:9621"
      }
    }
  }
}
```

Now Cascade has exactly what Hermes has — without running Hermes.

### 19.2 Vault / MOC-Style Persistent Knowledge

**What OpenClaw does:** Maintains a vault of markdown files with Maps of Content (MOCs), wiki-links between entities, and auto-captured "Agent Notes" per session.

**Cascade equivalent:** A combination of:
- **AGENTS.md** files per directory for project context
- **Memories & Rules** for preferences that persist across sessions
- **Plan files** at `~/.windsurf/plans/` — `@mention`-able from any future session
- A `vault/` folder in your repo with MOCs, linked via relative paths, that Cascade treats as context

Add this to root `AGENTS.md`:
```markdown
## Project Vault
- All architectural decisions live in `vault/decisions/ADR-NNN.md`
- Subsystem maps live in `vault/mocs/<name>.md` — start here for any cross-cutting task
- When making a big decision, write an ADR *first*, then implement
```

### 19.3 Auto-Capture Hook — Extract Knowledge After Every Session

**What OpenClaw does:** Runs a hook after every session that extracts key facts, decisions, and TODOs into the vault.

**Cascade equivalent:** `post_cascade_response_with_transcript` hook.

**`.windsurf/hooks.json`:**
```json
{
  "hooks": {
    "post_cascade_response_with_transcript": [
      {
        "command": "python .windsurf/hooks/auto_capture.py",
        "show_output": false
      }
    ]
  }
}
```

**`.windsurf/hooks/auto_capture.py`:**
```python
#!/usr/bin/env python3
"""After each Cascade turn, extract decisions/TODOs into vault/agent-notes/."""
import sys, json, datetime, pathlib, re

VAULT = pathlib.Path("vault/agent-notes")
VAULT.mkdir(parents=True, exist_ok=True)

data = json.loads(sys.stdin.read())
transcript = data.get("transcript", "")
trajectory_id = data.get("trajectory_id", "unknown")

# Cheap local extraction — swap in an LLM call if you want more
decisions = re.findall(r"(?im)^(?:decision|decided|we'll|we will):\s*(.+)$", transcript)
todos = re.findall(r"(?im)^(?:todo|next step|next):\s*(.+)$", transcript)

if not decisions and not todos:
    sys.exit(0)

out = VAULT / f"{datetime.date.today()}-{trajectory_id[:8]}.md"
with out.open("a") as f:
    f.write(f"\n## Session {trajectory_id}\n")
    for d in decisions:
        f.write(f"- **Decision:** {d.strip()}\n")
    for t in todos:
        f.write(f"- **TODO:** {t.strip()}\n")

sys.exit(0)
```

For an LLM-powered version, shell out to a local model or an inference API from inside the hook.

### 19.4 Memory Bridge — Share Memory Across Tools

**What OpenClaw does:** CLI bridge so Codex/Claude Code can read your vault.

**Cascade equivalent:** Expose the vault over MCP. Point a local filesystem MCP server at the vault directory, and Cascade (plus any other MCP client) can query it.

```json
{
  "mcpServers": {
    "vault": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/vault"]
    }
  }
}
```

### 19.5 Multi-Provider Fallback Chains

**What Hermes does:** Cerebras → Fireworks → Ollama fallback if upstream is down.

**Cascade equivalent:** Windsurf already handles this internally for SWE 1.6 Fast (Cerebras → Fireworks fallback). For custom providers, use **BYOK** (Bring Your Own Key) in the model picker for Claude 4 Sonnet / Opus. If you want full provider control, wrap your own models as an OpenAI-compatible MCP server.

### 19.6 Orchestrator / Worker / Sub-Agent Pattern

**What OpenClaw does:** CEO/COO/Worker model — cheap model orchestrates, expensive model executes key tasks.

**Cascade equivalent:** Same pattern, built in:
- **Plan Mode** = CEO (uses a lightweight model for planning)
- **Code Mode with SWE 1.6 Fast** = Worker (fast, cheap execution)
- **Devin delegation** = specialized long-running sub-agent
- **Arena Mode** for when you can't decide = a secondary "second opinion" model
- **Spaces** = the coordination surface

For more structured orchestration, chain Skills + Workflows:

```yaml
# .windsurf/workflows/orchestrated-feature.md
---
name: orchestrated-feature
description: Plan with SWE 1.6, execute with SWE 1.6 Fast, review with Sonnet 4.6
---

1. Switch to Plan Mode, draft a plan for {{feature}}
2. Save plan to ~/.windsurf/plans/{{feature}}.md
3. Switch to Code Mode with SWE 1.6 Fast; implement plan
4. Switch model to Sonnet 4.6; run @code-review skill
5. If review clean → open PR; else iterate
```

### 19.7 Telegram / Mobile Access

**What Hermes does:** Telegram bot for mobile chat with your agent.

**Cascade equivalent:** Two options:
1. **Delegate to Devin from mobile** — once you've handed tasks to Devin from Windsurf, you can monitor + comment on Devin sessions from any device at [devin.ai](https://devin.ai)
2. **Telegram MCP server** — run a Telegram bot that proxies into Cascade-compatible webhooks; there are open-source MCP servers for this

For truly on-the-go Cascade, the Devin handoff is the right answer — you plan on desktop, Devin executes in the cloud, you monitor from phone.

### 19.8 Self-Improving System / Micro-Learning

**What OpenClaw does:** Micro-learning loop that compounds forever, $0/day.

**Cascade equivalent:** Memories & Rules + the stuck-diagnosis pattern from [Troubleshooting](#20-troubleshooting). When Cascade hits a recurring failure, force it to write a memory about the fix. Next time it won't repeat the mistake.

Automate it with a rule:

```
When you hit the same error twice in a session, stop and write a
memory capturing: (1) the trigger, (2) what failed, (3) the fix.
Future sessions must read and avoid the documented failure mode.
```

Combined with the auto-capture hook above, your agent gets smarter every day.

### 19.9 Observability (LangFuse / n8n)

**What OpenClaw does:** LangFuse traces every agent call; n8n automates workflows.

**Cascade equivalent:**
- **LangFuse parity** — use `post_cascade_response_with_transcript` + `pre_mcp_tool_use` hooks to ship every trajectory to LangFuse. Example in [Section 8](#8-hooks).
- **n8n parity** — n8n has an MCP server; add it and Cascade can fire n8n workflows directly.

```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": ["-y", "@n8n/mcp-server"],
      "env": {
        "N8N_API_KEY": "your_key",
        "N8N_BASE_URL": "https://your-n8n.example.com"
      }
    }
  }
}
```

### 19.10 Reranker / Better Search Quality

**What OpenClaw does:** Adds a reranker on top of vector search.

**Cascade equivalent:** Windsurf's [Fast Context](https://docs.windsurf.com/context-awareness/fast-context) + **swe-grep** already does RL-trained multi-turn context retrieval. You almost never need a custom reranker for code. For docs/notes, stack a reranker inside your LightRAG MCP server (see 19.1).

### 19.11 Real-Time Knowledge Sync

**What OpenClaw does:** File watcher syncs vault changes to LightRAG in <6s.

**Cascade equivalent:** Run a watcher (`chokidar`/`watchexec`) alongside your LightRAG server that reindexes on change — no Cascade-side config needed. Or use the LightRAG REST API and fire off updates from `post_write_code` hooks when vault files change.

### 19.12 Linear Agent API — Cascade as an Assignable Teammate

**What the big harnesses do:** Hermes/OpenClaw expose a webhook-triggered queue so Linear/Jira issues route to the agent automatically. No IDE interaction.

**Cascade equivalent:** Linear's official [Agent API](https://linear.app/docs/agents) (GA April 2026) lets you register Cascade as a first-class teammate. Webhook → orchestrator → `windsurf cascade` in plan mode → plan posted as a Linear comment → implement → PR. Reference setup described in the viral [r/Linear writeup](https://www.reddit.com/r/Linear/comments/1s4gqdy/linearnative_ai_dev_agent_using_claude_code_mcp/).

**Minimal orchestrator (Node, ~30 lines):**

```typescript
// apps/linear-orchestrator/src/webhook.ts
import express from "express";
import { LinearClient } from "@linear/sdk";
import { spawn } from "node:child_process";

const app = express();
app.use(express.json());

const linear = new LinearClient({ apiKey: process.env.LINEAR_API_KEY! });
const CASCADE_USER_ID = process.env.CASCADE_USER_ID!;

app.post("/webhooks/linear", async (req, res) => {
  const { action, data } = req.body;
  if (action !== "assigned" || data.assignee?.id !== CASCADE_USER_ID) {
    return res.json({ ok: true });
  }

  // ACK immediately so Linear doesn't retry while Cascade runs (plans can take
  // minutes). Webhook errors must NEVER propagate to Linear — retries spawn
  // new cascade subprocesses and cause runaway loops.
  res.json({ ok: true });

  try {
    const issue = await linear.issue(data.id);

    // Plan phase — Plan Mode, post plan back to Linear
    const plan = await runCascade([
      "windsurf", "cascade", "--mode=plan",
      `Plan this Linear issue in plans/${issue.identifier}.md. Post plan to stdout.`,
      "--context", `${issue.title}\n\n${issue.description}`,
    ]);
    await issue.createComment({
      body: `## Plan\n${plan}\n\nReply with changes or mention me to start implementation.`,
    });
    // (Optional) Implement phase — kicks off on explicit mention/comment
  } catch (err) {
    console.error("cascade failed for issue", data.id, err);
    // Optional: post a failure comment back to the issue so humans notice.
  }
});

function runCascade(args: string[]): Promise<string> {
  return new Promise((resolve, reject) => {
    const ps = spawn(args[0], args.slice(1), { cwd: process.env.REPO_ROOT });
    let out = "";
    ps.stdout.on("data", d => out += d);
    ps.stderr.on("data", d => process.stderr.write(d));   // drain stderr so the child doesn't deadlock on a full pipe
    ps.on("error", reject);                               // fires when the binary is missing or unspawnable
    ps.on("close", code => code === 0 ? resolve(out) : reject(new Error(`exit ${code}`))); // 'close' (not 'exit') waits for stdout/stderr to fully flush
  });
}

app.listen(8787);
```

**Setup:**

1. Register a Linear OAuth app with scopes `actor=app`, `app:assignable`, `app:mentionable`
2. Expose the webhook with Cloudflare Tunnel (`cloudflared tunnel run`) — no static IP needed
3. Set `CASCADE_USER_ID` to the app user id Linear returns
4. Install the [Linear MCP](https://linear.app/docs/mcp) server in `.windsurf/mcp_config.json` so Cascade can read/update issues during implementation too

Cascade now shows up in the Linear assignee dropdown like any teammate. Assign → plan → comment → PR, without opening the IDE.

---

### Bottom Line

Every harness feature you'd pay for or build yourself has a stock-Windsurf equivalent once you combine:

```
Skills + Hooks + MCP + Memories + Plans + Worktrees + Spaces + Devin
```

And you get it at **SWE 1.6 Fast speed** (950 tok/s on Cerebras), which is already 3-4x faster than most of those harnesses on Claude Sonnet.

---

## 20. Context Engineering & the Agentic Wiki

This is the discipline everyone's talking about in April 2026. [Andrej Karpathy's "LLM Wiki" gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (Apr 4) crystallized what power users already felt: **RAG is stateless and amnesiac. Every query re-discovers knowledge from scratch. The future is a persistent, compounding Agentic Wiki.** Three major blog posts and a dozen YouTube videos followed in the next week, including [Supermemory's context engineering guide](https://supermemory.ai/blog/what-is-context-engineering-complete-guide/) (Apr 9) and IBM's treatment on enterprise memory (Apr 7).

You don't need a harness for this. You need to apply the four context-engineering moves inside Cascade.

### The Four Moves

| Move | What it means | Cascade surfaces |
|---|---|---|
| **Offload** | Push rarely-needed info out of the context window to disk/DB | Plan files (`~/.windsurf/plans/`), AGENTS.md, `.windsurf/skills/`, Memories |
| **Retrieve** | Pull the right context back in at the right time | `@mention` (file/plan/skill), MCP tools (vector DB, graph DB), `@web`/`@docs` |
| **Compress** | Summarize or evict stale turns so the window stays cheap and sharp | Prompt cache timer (2.0), `megaplan` → fresh session, Devin handoff |
| **Isolate** | Prevent context bleed across different concerns | Worktrees, Spaces, [subagents](#17-custom-subagents) |

If your Cascade session is slow or stupid, it's almost always because you're failing one of the four. Diagnose: *am I carrying dead context, or am I missing a piece I need?*

### The Agentic Wiki Pattern (Cascade Edition)

Karpathy's version: a `vault/` folder of markdown files that the agent *maintains* over time — reading new sources, extracting entities, updating topic pages, linking cross-references. Works beautifully in Cascade with zero new infrastructure:

```
<repo>/
├── AGENTS.md                 # "Start every task by reading vault/INDEX.md"
├── vault/
│   ├── INDEX.md              # Map of contents — what lives where
│   ├── decisions/            # ADR-NNN — architectural decisions
│   ├── people/               # Who owns what
│   ├── services/             # Per-service runbooks & invariants
│   ├── incidents/            # Post-mortems, extracted lessons
│   ├── glossary.md           # Terms of art
│   └── moc/                  # Maps of Content — curated reading lists
└── .windsurf/
    ├── skills/
    │   ├── wiki-update/SKILL.md     # Update the wiki after every session
    │   └── wiki-query/SKILL.md      # Query the wiki before starting work
    └── hooks.json                    # post_cascade_response → wiki-update
```

**`.windsurf/skills/wiki-update/SKILL.md`:**

```yaml
---
name: wiki-update
description: Maintain the project wiki in vault/. Run at the end of any session that produced a decision, fact, or change of state. Extracts entities, updates pages, adds cross-links, never deletes.
---

# Wiki Update Skill

After a session that did any of the following, update the wiki:
- Made an architectural decision → `vault/decisions/ADR-NNN.md`
- Learned who owns a system → `vault/people/<name>.md` + link from `vault/services/<svc>.md`
- Fixed an incident → `vault/incidents/<date>-<short>.md` with root cause + fix + invariant to add
- Added a term of art → `vault/glossary.md`

Process:
1. Read `vault/INDEX.md` to understand the current shape of the wiki.
2. For each new fact, **prefer updating an existing page** over creating a new one.
3. Use `[[wikilinks]]` between entities. If you reference a page that doesn't exist, create a stub.
4. Append to `vault/INDEX.md` if you created a new page.
5. Never delete or rewrite existing content — append and mark stale sections with `> **Stale as of YYYY-MM-DD:** ...`.

Output a one-line summary of what you updated.
```

Bind it to the [`post_cascade_response_with_transcript` hook](#8-hooks) so it runs automatically after every session. Over weeks, your repo accumulates exactly the kind of compounding knowledge layer Karpathy describes — without running a vector database or a bespoke harness.

### Claude Code's Compaction Engine (And How to Do It in Cascade)

In early April, Claude Code's [3-tier compaction strategy leaked from internal telemetry](https://stachu.dev/claude-code-best-practices/): **recent turns in full, mid-range turns as abstractive summaries, distant turns as bullet-point-only skeletons**. Cascade doesn't expose a knob for this, but you can get most of the benefit manually:

- **Short tasks (<30 min):** let Cascade run the default context window. Trust the prompt cache.
- **Medium tasks (30 min – 2h):** every ~10 turns, say `summarize what we've done in one paragraph and continue from that summary`. This is Cascade's abstractive layer.
- **Long tasks (2h+):** do a [Plan Mode](#1-cascade-modes-code--plan--ask) writeup to `~/.windsurf/plans/`, close the session, open a fresh one, `@mention` the plan. This is the skeleton layer — you kept the decisions and dropped the turns.

The prompt cache timer in the 2.0 context-window indicator tells you when you're about to pay full rate again. If it drops to zero mid-task, do the summary move *now*.

### Anti-Patterns to Kill

| Anti-pattern | Why it hurts | Fix |
|---|---|---|
| Re-explaining project context in every prompt | Wastes cache, drowns the real question | `AGENTS.md` + Rules, let Cascade load it once |
| `@mention`-ing giant files "for context" | Burns 10k+ tokens on stuff Cascade doesn't need | `@mention` the directory, let it search |
| Pasting terminal output without cleaning | Stack traces inflate context; most lines are noise | Use `cascade > log 2>&1 | tail -50` and paste that |
| Running everything in one session for days | Context bloats, prompt cache invalidates | Plan → close → reopen with plan |
| Using one model for everything | Reviewer and implementer want different things | [Subagents](#17-custom-subagents) with pinned models |

---

## 21. Spec-Driven Development with Cascade

Spec-Driven Development (SDD) went mainstream in April 2026. [GitHub Spec Kit v0.5.0](https://github.com/github/spec-kit) shipped on April 11 with seven `/speckit.*` slash commands; AWS's Kiro, Tessl's Spec Studio, and IBM's watsonx Code Assistant all rolled out SDD features in the same two weeks; [the Cognition writeup on SWE 1.6](https://cognition.ai/blog/swe-1-6) explicitly trained the model to prefer spec-first workflows.

The idea: **treat specifications as the primary artifact and code as its compilation target.** Cascade is unusually good at this because Plan Mode + AGENTS.md + Workflows already form an SDD toolchain.

### The Spec Kit Flow

```bash
# One-time install (works in any repo)
uvx --from git+https://github.com/github/spec-kit specify init --ai cursor
# (Spec Kit has templates for Cursor, Claude Code, Copilot, Gemini CLI.
# Use --ai cursor and point the output at Cascade — details below.)
```

The seven slash commands Spec Kit gives you:

| Command | What it does |
|---|---|
| `/speckit.constitution` | Write the project's non-negotiable principles (security, testing, API shape) |
| `/speckit.specify` | Turn a user request into a formal spec doc |
| `/speckit.clarify` | Ask the clarifying questions the spec is missing |
| `/speckit.plan` | Decompose the spec into implementable tasks |
| `/speckit.tasks` | Emit the task list as checkboxes |
| `/speckit.analyze` | Audit the spec + plan before implementation |
| `/speckit.implement` | Hand the plan to the code agent |

### Wiring Spec Kit Into Cascade

Spec Kit emits prompt files (markdown) designed to be invoked as slash commands. Cascade's [Workflows](#10-workflows) system is the right host — one `.windsurf/workflows/speckit.<cmd>.md` file per command.

```bash
# From your repo root
mkdir -p .windsurf/workflows
git clone --depth 1 https://github.com/github/spec-kit /tmp/spec-kit
for cmd in constitution specify clarify plan tasks analyze implement; do
  cp /tmp/spec-kit/templates/commands/$cmd.md .windsurf/workflows/speckit-$cmd.md
done
```

Then in Cascade: `/speckit-specify Add a rate limiter for /api/auth/*` → produces `specs/001-rate-limiter.md`.

### The Native Cascade SDD Flow (No Spec Kit)

If you'd rather not depend on Spec Kit, Cascade's built-in primitives get you 90% there:

1. **Constitution** → root `AGENTS.md` with an "Invariants" section
2. **Specify** → `/plan <request>` (Plan Mode asks clarifying questions)
3. **Clarify** → `megaplan <request>` (aggressive form — asks *many* clarifying questions)
4. **Plan** → the plan file written to `~/.windsurf/plans/<name>.md`
5. **Tasks** → the plan already has checkboxed steps
6. **Analyze** → `@reviewer check this plan before we implement`
7. **Implement** → click **Implement** on the plan file (or hand to Devin)

Here's a `AGENTS.md` "Invariants" block worth copy-pasting as a starting point:

```markdown
## Invariants (Constitution)

These are never negotiable. If a request would violate them, ask first — don't silently proceed.

1. **Security:** no API key or secret in logs, commits, or tests. PII never in logs.
2. **Testing:** every new public function gets a test. Coverage must stay ≥ 80% on `src/`.
3. **API shape:** every endpoint returns `{ ok: boolean, data?: T, error?: { code, message } }`.
4. **Migrations:** schema changes are always a two-phase deploy (expand → migrate → contract).
5. **Dependencies:** no new dependency with < 6 months of commit history or < 100 stars.
6. **AI changes:** every Cascade-generated diff over 50 lines gets a `reviewer` subagent pass before commit.
```

### SDD + Subagents + Worktrees = The Killer Flow

```
Space: "Add rate limiter"
├── Worktree A (@architect):   /speckit-specify + /speckit-clarify → spec.md
├── Worktree B (@reviewer):    /speckit-analyze spec.md           → review notes
├── Worktree C (@implementer): /speckit-implement spec.md         → code + tests
└── Worktree D (@tester):      runs the suite + coverage          → report
```

All four live in one [Space](#2-agent-command-center--spaces). You orchestrate from the Kanban. Close the loop with the wiki-update hook from [§20](#20-context-engineering--the-agentic-wiki) — the decision, spec, and review become part of `vault/`.

---

## 22. Skills Ecosystem — `gh skill`, agentskills.io, and Viral Skills

The agent-skills ecosystem is suddenly one of the most active parts of the AI-tools landscape. As of mid-April 2026:

- **[agentskills.io](https://agentskills.io)** is the spec for `SKILL.md` — 30+ platforms (Claude Code, Cursor, Codex, Gemini CLI, Copilot, OpenClaw, Hermes, Windsurf) follow it.
- **[`gh skill` CLI](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli)** — landed **April 16**. Install, update, publish, pin, verify provenance of any SKILL.md-formatted skill from GitHub directly into any supported agent, including Cascade.
- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** — #1 on GitHub Trending April 16, 22k stars, 1.8k forks. The canonical example of a "does one thing extremely well" skill.
- **[jezweb/skills](https://github.com/jezweb/skills)** — a curated list of 300+ community skills that install with `gh skill install`.

### Installing Skills with the New `gh skill` CLI

```bash
# One-time install of the CLI extension
gh extension install github/gh-skill

# Search for skills
gh skill search research multi-source

# Install into Cascade (target flag writes to .windsurf/skills/)
gh skill install mvanhorn/last30days-skill --target windsurf

# Pin a version (skills are content-addressed, so this is immutable)
gh skill install mvanhorn/last30days-skill@v3.0.5 --target windsurf

# Check for updates
gh skill outdated --target windsurf

# Publish your own
gh skill publish .windsurf/skills/deep-recall
```

Target flags the CLI currently supports: `--target claude-code`, `--target cursor`, `--target codex`, `--target copilot`, `--target gemini-cli`, `--target windsurf`, `--target openclaw`, `--target hermes`. One skill repo, N targets.

**Under the hood**, `--target windsurf` just copies the SKILL.md (and any bundled `resources/`, `scripts/`, etc.) into `.windsurf/skills/<name>/` and sets the right permissions — exactly what [§5 Skills System](#5-skills-system) describes, but with provenance + version pinning.

### Installing `last30days` in Cascade (without the CLI)

If you don't want the GitHub CLI dependency:

```bash
mkdir -p .windsurf/skills
git clone --depth 1 https://github.com/mvanhorn/last30days-skill /tmp/l30d
cp -r /tmp/l30d/skills/last30days .windsurf/skills/
```

Then in Cascade: `/last30days windsurf 2.0` — synthesizes a brief across Reddit, X, YouTube, HN, Polymarket, GitHub, Bluesky, Perplexity, and five others.

**Why this matters in this guide:** `last30days` does *exactly* what the "What's Hot Right Now" block above does — but on demand, for any topic. Install it once and you have an always-current research tool without standing up your own MCP server. It's what took this guide from static to live.

### Writing Skills Worth Publishing

The viral skills all follow the same shape:

1. **Single-purpose.** `last30days` researches across platforms. `pr-review` reviews PRs. Not "research and review and deploy."
2. **Description is a trigger.** The `description:` YAML field is the only thing Cascade sees when deciding whether to invoke. Write it as a condition: "*Use when the user asks about...*"
3. **Progressive disclosure.** The skill body is short; details live in `resources/` files the agent reads on demand.
4. **Bundled scripts.** If there's deterministic logic (rate limit, dedup, format), write it in a script — don't make the LLM redo it.
5. **Zero-config if possible.** Work immediately with sensible defaults; require secrets only if invoked for a gated source.
6. **Cross-target.** Test on at least Claude Code + Cursor + Windsurf before publishing. A SKILL.md that assumes a specific slash-command runner won't travel.

### The Skills Worth Installing Today

| Skill | What it does | Why |
|---|---|---|
| [last30days](https://github.com/mvanhorn/last30days-skill) | Parallel multi-platform research + AI synthesis | Trending #1 for a reason |
| [commit-surgeon](https://github.com/anthropics/claude-code-skills) | Rewrites git history, splits messy commits, interactive rebase driver | Saves you from `git rebase -i` hell |
| [pr-surgeon](https://github.com/anthropics/claude-code-skills) | Turns a local branch into a clean PR (squash, rename, describe) | Use after any non-trivial Cascade session |
| [test-backfill](https://github.com/anthropics/claude-code-skills) | Adds missing tests for uncovered lines, aware of your test framework | Pairs with the `tester` subagent |
| [docs-writer](https://github.com/anthropics/claude-code-skills) | README / AGENTS.md / CHANGELOG keeper | Pairs with `post_cascade_response` hook |
| [changelog-bot](https://github.com/jezweb/skills) | Keeps `CHANGELOG.md` in conventional-commits format | Release hygiene |
| [secret-scrubber](https://github.com/jezweb/skills) | Scans diffs for secrets before commit | Complements the hook in [§8](#8-hooks) |

### Publishing Your Own Skill

```bash
# Create a new skill scaffold
gh skill new my-skill --target windsurf

# Edits .windsurf/skills/my-skill/SKILL.md + scripts/ + resources/
$EDITOR .windsurf/skills/my-skill/SKILL.md

# Test locally — Cascade should see it immediately
# Then publish to GitHub with provenance
gh skill publish .windsurf/skills/my-skill
# → publishes to github.com/<you>/my-skill-skill with verified build attestation
```

Anyone in any supported agent can now install yours with a single `gh skill install <you>/my-skill`. This is how `last30days` went from zero to 22k stars in three months — the distribution story is solved.

---

## 23. Observability & Evals for Cascade

Agent observability went from "nice to have" to "listed in 67% of AI-engineer job postings" in Q1 2026. ([AgenticCareers](https://agenticcareers.co/blog/ai-agent-observability-stack-2026) tracks the numbers.) Cascade doesn't ship a first-party dashboard — but Cascade *hooks* fire on every file read, command, response, and rule application, so you can pipe into any of the major platforms in 20 lines of Python.

### The Platforms

| Tool | Best for | Pricing | Cascade fit |
|---|---|---|---|
| [**LangSmith**](https://smith.langchain.com) | Teams already on LangChain/LangGraph | Tiered SaaS | Good if your MCP servers use LangChain; otherwise overkill |
| [**Langfuse**](https://langfuse.com) | OSS-friendly, self-hostable, vendor-agnostic | Free OSS + SaaS | **Best general-purpose choice for Cascade** — no framework lock-in |
| [**Arize Phoenix**](https://phoenix.arize.com) | ML-ops teams, OpenInference/OTel native | Free OSS + Arize SaaS | Great if you already emit OTel |
| [**Helicone**](https://helicone.ai) | Simple LLM proxy + logging | Cheap, fast setup | Fine for basic cost tracking, limited for agent traces |
| [**Braintrust**](https://braintrust.dev) | Eval-first, regression testing | SaaS | **Best eval platform** — the one you pair with whatever you use for tracing |

**Recommended pairing for most teams:** Langfuse for tracing + Braintrust for evals. Both have free tiers that cover individual power users.

### Wiring Cascade into Langfuse with a Hook

Add to `.windsurf/hooks.json`:

```jsonc
{
  "hooks": {
    "post_cascade_response_with_transcript": [
      {
        "command": "python3 .windsurf/hooks/langfuse_logger.py"
      }
    ]
  }
}
```

`.windsurf/hooks/langfuse_logger.py`:

```python
#!/usr/bin/env python3
"""Pipe every Cascade response into Langfuse as a trace."""
import json, os, sys
from langfuse import Langfuse

lf = Langfuse(
    public_key=os.environ["LANGFUSE_PUBLIC_KEY"],
    secret_key=os.environ["LANGFUSE_SECRET_KEY"],
    host=os.environ.get("LANGFUSE_HOST", "https://cloud.langfuse.com"),
)

ctx = json.load(sys.stdin)
trace = lf.trace(
    name="cascade-response",
    user_id=ctx.get("user_id"),
    session_id=ctx.get("session_id"),
    metadata={
        "model": ctx.get("model"),
        "mode": ctx.get("mode"),             # code / plan / ask
        "rules_applied": ctx.get("rules_applied", []),
        "tool_calls": len(ctx.get("tool_calls", [])),
        "workspace": ctx.get("workspace"),
    },
)
trace.generation(
    name="cascade",
    model=ctx.get("model"),
    input=ctx.get("prompt"),
    output=ctx.get("response"),
    usage={
        "input": ctx.get("input_tokens"),
        "output": ctx.get("output_tokens"),
        "cache_read": ctx.get("cache_read_tokens"),
    },
)
for call in ctx.get("tool_calls", []):
    trace.span(
        name=f"tool:{call['name']}",
        input=call.get("args"),
        output=call.get("result"),
        metadata={"duration_ms": call.get("duration_ms")},
    )
lf.flush()
```

Set `LANGFUSE_PUBLIC_KEY` / `LANGFUSE_SECRET_KEY` in your shell profile and every Cascade turn streams into your Langfuse project. You get latency breakdowns, token-spend-per-rule, tool-call heatmaps, and — critically — a searchable trace every time something goes wrong.

### Running Evals with Braintrust

The workflow that's emerging in April 2026:

1. Keep a `.windsurf/evals/` folder of **golden prompts** — real tasks you've completed before, with the ideal output captured
2. Nightly (or on every `AGENTS.md` change), run each prompt through Cascade via the [Windsurf API](https://docs.windsurf.com/api) or a headless Cascade session
3. Pipe the outputs into Braintrust; grade with an LLM-as-judge + simple heuristics (did it touch the right files? pass tests? obey the invariants?)
4. Watch the score when you change a rule, add an MCP, pin a new model

This is how you tell whether editing `AGENTS.md` helped or hurt. It's also how Cognition validates SWE 1.6 internally — the [blog post](https://cognition.ai/blog/swe-1-6) walks through their eval-first methodology.

### The `rules_applied` Telemetry Gold Mine

Cascade's [`rules_applied`](#9-memories--rules) field in the hook context tells you **which of your rules actually fired for each response**. Pipe it into Langfuse as metadata (shown above) and you get:

- Which rules are load-bearing (fire often, correlate with good outcomes)
- Which rules are dead weight (never fire — delete them)
- Which rules conflict (co-occur in failed turns)

This is the single highest-ROI piece of instrumentation in Cascade and nobody is using it. Turn it on.

---

## 24. Gotchas & Known Issues (April 2026)

Current quirks worth knowing before you hit them. All of these are fresh as of mid-April; expect them to be patched in subsequent 2.0.x releases.

### Nested Git Repos Multiply Rule Loads ([#305](https://github.com/Exafunction/codeium/issues/305))

If your workspace root contains multiple `.git/` directories (monorepos, submodules, nested clones), Cascade loads `.windsurfrules` / `AGENTS.md` 2×–9× per response. Every load burns the full token count of the file.

**Fix until patched:** Either flatten the layout (open the specific repo folder, not the parent) or set a workspace-level override to pin the rules file path. Monitor the issue; the fix is in the patch queue.

### SSE MCP Servers Silently Dying (April–June 2026)

Every remote MCP server still on the legacy SSE transport will stop working on its vendor's cutoff date (Keboola: Apr 1, Atlassian: Jun 30, others tbd). Cascade won't warn you — the tool just disappears from the agent's available list.

**Fix:** Audit `mcp_config.json` for `"transport": "sse"` on any remote URL. Switch to `"streamable-http"` or wait for the vendor's migration. See [§6 MCP](#sse-is-deprecated--migrate-to-streamable-http-april-2026).

### MCP TypeScript SDK 1.25–1.27 Keepalive Bug

If you wrote your own Streamable-HTTP MCP server on the TS SDK between 1.25 and 1.27, long-running Cascade sessions will lose connections on TCP keepalive. Pin to 1.24.x or keep an SSE GET stream open during idle. Fix is in 1.28 beta.

### Adaptive Router Promo Pricing Ends Soon

The current promo rate ($0.50/M input, $2/M output, $0.10/M cache-read) is a launch promo — Windsurf has not committed to permanence. If you're building cost projections, assume the rate could normalize to the average of the underlying models (roughly 2× the promo) after the Adaptive public-beta window.

### SWE 1.6 Fast "Free for 3 Months" Expires in July 2026

The free-tier promo for SWE 1.6 started April 7, 2026 and is explicitly a 3-month window. If your production workflow is built around its cost structure, pencil in a July 7, 2026 re-evaluation. Fireworks hosting (200 tok/s) will likely remain free on the Free plan; the 950 tok/s Cerebras variant will likely move to paid quota.

### Rules File 6k-Token Soft Limit

Cascade has a soft cap around 6k tokens on the combined rules context per session. Past it, the tail gets silently truncated. If your `AGENTS.md` + Memories + active Rules push over this, pull rarely-used sections into `vault/` or skills and `@mention` them on demand.

### Windsurf Browser CORS Quirks

The 2.0 Windsurf Browser runs inside the editor, which means some sites see it as a non-standard user agent and block or rate-limit. If Cascade reports "couldn't read page" consistently for a site that works in Chrome, fall back to Chrome DevTools MCP ([§6](#6-mcp-server-integration)) or `@web` URL paste.

### Agent Command Center Kanban Can Drift on Restart

The Kanban position of archived agent sessions sometimes reorders after a Windsurf restart. Pending sessions are preserved; completed/archived cards may need a manual drag back. Low-impact; patch is noted as "in review" by Windsurf staff.

### If a Gotcha Is Costing You Hours, File It

The [Exafunction/codeium issue tracker](https://github.com/Exafunction/codeium/issues) is the canonical place. Windsurf staff actively triage; issues with a clear repro and impact numbers tend to land fixes within a 2.0.x cycle.

---

## 25. Troubleshooting

### "Connecting to Language Server" Stuck

Cascade shows "Connecting to language server..." and won't respond:

1. Kill all Windsurf processes: `Get-Process windsurf | Stop-Process -Force` (PowerShell)
2. Check `%APPDATA%\Windsurf\User\settings.json` for malformed JSON
3. Your user config in `.codeium/windsurf/` survives reinstalls — only app files are affected
4. If all else fails: `winget uninstall Codeium.Windsurf && winget install Codeium.Windsurf`

### MCP Server Not Appearing

- Verify `mcp_config.json` is at `~/.codeium/windsurf/mcp_config.json` (user) or `.windsurf/mcp_config.json` (workspace)
- Check that the command is globally available (`npx -y` handles this for Node servers)
- Restart Windsurf after adding new servers — MCP config loads at startup
- Check Cascade output panel for MCP connection errors
- Marketplace servers: Cascade panel → MCPs icon → search and install
- Hit the 100-tool ceiling? Disable individual tools in each MCP's settings page
- HTTP/SSE with OAuth: Cascade should auto-open the login page — if it doesn't, try the MCP Refresh button

### Skills Not Auto-Executing

- Verify the file path: `.windsurf/skills/<skill-name>/SKILL.md` (case-sensitive on Linux/Mac)
- Check the `description` field — Cascade uses it for matching, not the filename
- Skills require a workspace (not an empty window)
- Try manual invocation with `@skill-name` to verify it loads
- Also check global path: `~/.codeium/windsurf/skills/` and `.agents/skills/` / `.claude/skills/`

### Hooks Not Firing

- Verify `.windsurf/hooks.json` matches the official format: nested under `"hooks"`, each event is an array
- Check `"command"` or `"powershell"` key (use `"powershell"` on Windows for cross-compat)
- Test the hook manually: `echo '{"file_path":"test.py"}' | python .windsurf/hooks/check_secrets.py`
- Check exit codes: `0` = allow, `2` = block
- Hook merge order: workspace overrides user overrides system
- Enterprise: cloud-dashboard hooks may override yours — check with your admin

### Terminal Issues

- Shell RC conflicts: if commands fail silently, check `.bashrc` / `.zshrc` for interactive-only configs
- PATH differences: Cascade may use a different PATH than your terminal. Use absolute paths in hooks.
- Windows: use `"powershell"` key in hooks.json for cross-shell compatibility
- MCP whitelist regex gotchas: test your patterns against actual command strings

### Worktrees Break the Build

- Relative paths outside the repo (`../shared-lib`) won't resolve inside a worktree
- Use a `post_setup_worktree` hook to symlink or copy what's needed (see [Section 11](#11-worktrees--parallel-cascade))
- `.env` files aren't copied automatically — handle in the setup hook

### Devin Not Showing Up

- Access rolls out gradually — log out of both the website and the IDE, then log back in
- Enterprise accounts: Devin Cloud is disabled by default; admin must enable in org settings
- Devin draws from your existing Windsurf quota — if you're out of quota, it won't spin up

### Cascade Gets Stuck on a Step

Cascade sometimes hangs on a single step — spinning forever without progressing or erroring. Two things help:

**Prevention: Set timeouts in AGENTS.md**

Add this to your root `AGENTS.md` to prevent hangs:

```markdown
## Execution Rules
- If a command takes more than 10 seconds with no output, kill it and try a different approach.
- If you've been on the same step for more than 60 seconds, stop and explain what's blocking you.
- Never retry the exact same command that just failed. Diagnose first.
```

**Recovery: Interrupt and force self-diagnosis**

When Cascade is stuck, don't just restart. Interrupt it (click the stop/interrupt button) and send a message like:

> Why are you stuck on this step? We need to learn what makes you get stuck and permanently solve it. Whatever is causing this, figure it out, save the solution to your memory so you never hit this again.

This works because Cascade can introspect on what went wrong and save the fix. After a few rounds of this, it stops making the same mistakes. It's iterative self-improvement — each stuck moment becomes a permanent lesson if you force the diagnosis.

**Why this matters:** Most people restart when Cascade hangs and lose the learning opportunity. Interrupting + forcing self-diagnosis turns every failure into a durable fix.

---

## Feature Matrix

| Feature | Config Location | Discovery | Override Level |
|---------|----------------|-----------|----------------|
| Cascade Modes (Code/Plan/Ask) | Mode toggle under input (`⌘+.`) | Built-in | Per-session |
| Agent Command Center | Sidebar | Built-in (2.0) | N/A |
| Spaces | Sidebar | Built-in (2.0) | Per-session |
| Devin in Windsurf | Command Center | Built-in (2.0) | Per-plan |
| Terminal execution | Settings UI + hooks.json | Built-in | System → User → Workspace → Org |
| Skills | `.windsurf/skills/` + global + `.agents/` + `.claude/` | Auto-scan | Workspace + User + Enterprise MDM |
| MCP servers | `mcp_config.json` (user + workspace) | Startup load + Marketplace | User + Workspace + Org registry |
| AGENTS.md | Any directory | Per-file | Root → Subdirectory |
| Hooks | `.windsurf/hooks.json` + user + cloud dashboard | Startup load | System → User → Workspace → Cloud |
| Memories & Rules | Cascade UI | Session-persist | User only |
| Workflows | `.windsurf/workflows/*.md` | Auto-scan | Workspace only |
| Worktrees | Mode toggle + `post_setup_worktree` hook | Per-session | Workspace only |
| Arena Mode | Model picker → Arena tab | Per-session | User only |
| Web Search | Settings + `@web`/`@docs`/URL paste | Contextual | User + Org admin toggle |
| Windsurf Browser | In-editor browser tool | Built-in (2.0) | Per-session |
| App Deploys | Ask Cascade to deploy | On-demand | User / Team account |
| DeepWiki | `Cmd+Shift+Click` symbol | Built-in | Per-session |
| Codemaps | Activity Bar / Command Palette | On-demand | Workspace (shareable) |
| Vibe and Replace | Find/Replace panel | Built-in | Per-file |
| Model selector | Prompt hints (`/fast`, `/deep`) + picker + pinning | Contextual | Auto-detected |
| Adaptive router | Model picker | Per-turn | User |
| Subagent profiles | `.windsurf/agents/*/AGENT.md` | `@mention` | Workspace only |

---

## Awesome-Windsurf — Curated Ecosystem Index

> Community-maintained list of the best things you can plug into Cascade. PRs that add a single high-quality resource are very welcome (bar is *top-tier* — not "a thing that exists"). See [CONTRIBUTING.md](./CONTRIBUTING.md).

### 🧩 MCP Servers (production-ready, Streamable HTTP or stdio)

| Server | What it does | Notes |
|---|---|---|
| [github/github-mcp-server](https://github.com/github/github-mcp-server) | Full GitHub API: PRs, issues, code, actions | v0.33 added OAuth auto-trigger |
| [Azure MCP Server 2.0](https://github.com/Azure/azure-mcp) | 276 tools across 57 Azure services | GA April 2026 |
| [modelcontextprotocol/servers — filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) | Scoped filesystem access | Reference implementation |
| [modelcontextprotocol/servers — postgres](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) | Read-only Postgres | Safe to hand to Cascade |
| [modelcontextprotocol/servers — memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) | Persistent key-value store | Official memory |
| [Keboola MCP](https://keboola.com/blog/mcp-streamable-http) | Data pipelines, reference Streamable HTTP implementation | Apr 1 cutover set industry precedent |
| [Chrome DevTools MCP](https://developer.chrome.com/blog/mcp-chrome-devtools) | Drive DevTools from Cascade | Useful for perf debugging |
| [microsoft/mcp-playwright](https://github.com/microsoft/mcp-playwright) | Browser automation for E2E | Works with Windsurf Browser |
| [jlowin/fastmcp](https://github.com/jlowin/fastmcp) | Build your own MCP server in Python fast | Best DX for custom servers |
| [Slack MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) | Read cross-team context | Requires bot token |
| [Linear MCP](https://linear.app/docs/mcp) | Issue tracker from Cascade | Official |

### 🧠 Skills (install via `gh skill install`)

| Skill | What it does | Source |
|---|---|---|
| [last30days-skill](https://github.com/mvanhorn/last30days-skill) | Parallel search of Reddit / X / YouTube / HN / GitHub, AI-synthesized brief | GitHub Trending #1, 22k⭐ |
| [anthropics/claude-code-skills](https://github.com/anthropics/claude-code-skills) | Anthropic's canonical skill collection | Official |
| [jezweb/skills](https://github.com/jezweb/skills) | 300+ curated community skills | Community |
| [windsurf-unlocked starter skills](./starter/.windsurf/skills) | wiki-update, wiki-query, pr-ready, test-backfill, secret-scrubber | This repo |

### 🚀 Starter Templates & Configs

| Template | What you get | Fit |
|---|---|---|
| [**windsurf-unlocked/starter**](./starter) | 8 subagents, hooks, skills, vault, Spec Kit workflows, MCP config | General-purpose |
| [github/spec-kit](https://github.com/github/spec-kit) | `/speckit.*` workflows for SDD | Spec-Driven teams |
| [agentskills.io](https://agentskills.io) | SKILL.md specification + examples | Skill authors |
| [karpathy's LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) | The `vault/`-style agentic-wiki pattern | Memory-hungry teams |

### 📊 Observability & Evals

| Tool | Model | Notes |
|---|---|---|
| [Langfuse](https://langfuse.com) | OSS + SaaS | Best for self-hosters |
| [LangSmith](https://smith.langchain.com) | SaaS | Best if you're already in LangChain |
| [Arize Phoenix](https://phoenix.arize.com) | OSS + SaaS | OpenInference / OTel-native |
| [Helicone](https://helicone.ai) | SaaS (OSS proxy) | Lightweight logging + caching |
| [Braintrust](https://braintrust.dev) | SaaS | Eval-first workflow |

Covered in depth in [§23](#23-observability--evals-for-cascade) with a working Langfuse hook in the starter kit.

### 🎥 Talks, Videos, and Posts Worth Watching

| Resource | Why |
|---|---|
| [Cognition — SWE 1.6 launch](https://cognition.ai/blog/swe-1-6) | The model + the Cerebras deal |
| [Anthropic — Subagents docs](https://docs.anthropic.com/en/docs/claude-code/sub-agents) | Canonical description of the pattern |
| [Supermemory — What is Context Engineering](https://supermemory.ai/blog/what-is-context-engineering-complete-guide/) | The four-moves framework |
| [Epsilla — RAG is Dead](https://www.epsilla.com/blogs/karpathy-agentic-wiki-beyond-rag-enterprise-memory) | Why agentic wiki > embeddings-only RAG |
| [Steve Kinney — The Ralph Wiggum Loop](https://stevekinney.com/writing/the-ralph-loop) | The persistent-until-green pattern — with skeptics |
| [Steve Kinney — Driving vs. Debugging the Browser](https://stevekinney.com/writing/driving-vs-debugging-the-browser) | Playwright MCP vs Chrome DevTools MCP — when each wins |
| [MindStudio — /compact command](https://www.mindstudio.ai/blog/claude-code-compact-command-context-management/) | Proactive compaction + preservation instructions |
| [ToolHalla — Reflection Pattern](https://toolhalla.ai/blog/reflection-pattern-ai-agents-2026) | 80% → 91% HumanEval with structured reflection |
| [vibecoding.app — Anti-Drift Workflows](https://vibecoding.app/blog/anti-drift-workflows-vibe-coders-guide) | PRD, Spec Kit, Planning-with-Files, Ralph Loop side-by-side |
| [Andrew Shu — Markdown Plan Files](https://www.ashu.co/markdown-plan-files-vibe-coding/) | Why file-based plans beat in-IDE planners |
| [Karpathy — LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) | The original call for an agentic wiki |

### 🧰 Companion Harness Guides (if you use more than one)

- [OpenClaw Optimization Guide](https://github.com/OnlyTerp/openclaw-optimization-guide)
- [Hermes Optimization Guide](https://github.com/OnlyTerp/hermes-optimization-guide)

### 🌍 Community

- [Windsurf Discord](https://discord.gg/windsurf) — #help, #skills, #mcp
- [r/windsurf](https://www.reddit.com/r/windsurf/) — discussion and show-and-tell
- [Windsurf X (Twitter)](https://x.com/windsurf_ai) — official announcements
- [Cognition blog](https://cognition.ai/blog) — SWE models, Devin, research

> **Want to be on this list?** Open a PR. We accept one-resource-per-PR to keep reviews fast. Bar: top-tier, production-ready, accessible without corporate gating.

---

## Resources

### Windsurf Primary Sources

- [Windsurf Documentation](https://docs.windsurf.com)
- [Windsurf Changelog](https://windsurf.com/changelog)
- [Windsurf Blog — Windsurf 2.0 announcement](https://windsurf.com/blog/windsurf-2-0)
- [SWE 1.6 Research Post (Cognition)](https://cognition.ai/blog/swe-1-6)
- [Agent Command Center docs](https://docs.windsurf.com/windsurf/agent-command-center)
- [Spaces docs](https://docs.windsurf.com/windsurf/spaces)
- [Devin in Windsurf docs](https://docs.windsurf.com/windsurf/devin)
- [Cascade Hooks docs](https://docs.windsurf.com/windsurf/cascade/hooks)
- [Arena Leaderboard](https://windsurf.com/leaderboard)

### MCP & Protocol

- [MCP Specification](https://spec.modelcontextprotocol.io)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
- [MCP Server Directory](https://github.com/modelcontextprotocol/servers)
- [GitHub MCP Server](https://github.com/github/github-mcp-server)
- [Azure MCP Server](https://github.com/Azure/azure-mcp)
- [fastmcp (Python)](https://github.com/jlowin/fastmcp)
- [SSE → Streamable HTTP migration guide](https://www.channel.tel/blog/mcp-sse-to-streamable-http-migration)

### Skills Ecosystem

- [Agent Skills Spec (agentskills.io)](https://agentskills.io)
- [`gh skill` CLI announcement](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli)
- [last30days-skill](https://github.com/mvanhorn/last30days-skill) — GitHub Trending #1, April 16
- [jezweb/skills](https://github.com/jezweb/skills) — 300+ curated community skills
- [Anthropic's claude-code-skills](https://github.com/anthropics/claude-code-skills)

### Spec-Driven Development

- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [AWS Kiro](https://kiro.dev) — AWS's SDD IDE
- [Tessl Spec Studio](https://tessl.io)

### Context Engineering & Memory

- [Karpathy's LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [Supermemory: Context Engineering Complete Guide (Apr 2026)](https://supermemory.ai/blog/what-is-context-engineering-complete-guide/)
- [Epsilla: Why Karpathy is Right — RAG is Dead](https://www.epsilla.com/blogs/karpathy-agentic-wiki-beyond-rag-enterprise-memory)

### Observability & Evals

- [Langfuse](https://langfuse.com) — OSS + SaaS agent observability
- [LangSmith](https://smith.langchain.com) — LangChain-native
- [Arize Phoenix](https://phoenix.arize.com) — OpenInference/OTel
- [Helicone](https://helicone.ai) — lightweight LLM proxy + logging
- [Braintrust](https://braintrust.dev) — eval-first
- [AI Agent Observability Stack comparison (AgenticCareers)](https://agenticcareers.co/blog/ai-agent-observability-stack-2026)

### Competitor Harness Guides

- [OpenClaw Optimization Guide](https://github.com/OnlyTerp/openclaw-optimization-guide) — companion guide for the OpenClaw harness
- [Hermes Optimization Guide](https://github.com/OnlyTerp/hermes-optimization-guide) — companion guide for the Hermes harness

---

*Last updated: April 17, 2026 · Built by [Terp AI Labs](https://x.com/OnlyTerp) · Ship fast, iterate constantly.*

*Covers: Windsurf 2.0.50 · SWE 1.6 / SWE 1.6 Fast · Agent Command Center · Spaces · Devin in Windsurf · `gh skill` CLI · Spec Kit v0.5.0 · MCP Streamable HTTP · last30days-skill · Claude Code Subagents pattern · Context Engineering · and every other thing that went viral in the first 17 days of April 2026.*
