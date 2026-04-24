# Windsurf Guide Rework

Status: approved
Owner: Rob
Started: 2026-04-24

## Goal
Turn the main README from a long feature dump into a terse, high-value guide for people who want the best practical Windsurf setup in April 2026: what changed, what to configure first, when to use each feature, and how to avoid wasted quota/context.

## Non-Goals
- Do not rewrite `starter/` internals unless the README points at stale facts.
- Do not add untested prompts, hooks, agents, or benchmark numbers.
- Do not replace the referral link; keep it visible and honest.
- Do not optimize for exhaustive vendor documentation parity.

## Constraints
- From AGENTS.md invariants: no secrets, no direct commits to `main`, no skipped hooks, terse docs, update docs when behavior changes.
- From user context: the guide feels cluttered and “yappy”; prioritize audit, current accuracy, and best value without overwhelm.
- From repo style: prose should be terse, factual, specific, and avoid marketing claims without verification.
- Source claims from Windsurf docs, pricing, changelog, and blog where possible.

## Approach
Replace the 3,000+ line README with a compact guide that front-loads the decision tree and setup checklist, then links to focused companion files for prompts, starter kit, benchmarks, vault protocol, and SOUL. Keep only the highest-leverage content in the main README: 2026 changes, pricing/quota model, model selection, Cascade modes, ACC/Spaces/Devin, context/rules/skills/workflows/MCP/hooks, and “power moves” as recipes.

Alternatives considered:
- **Patch individual paragraphs:** lower risk but leaves the cluttered structure intact.
- **Split the guide into many new docs:** cleaner long term but bigger navigation burden and more files to maintain.
- **Rewrite only intro/new-stuff sections:** fast but does not solve the overwhelm problem.

## Task Breakdown
- [x] 1. Draft a compact README outline with a clear “read this first” flow and source links.
- [x] 2. Replace stale/noisy README sections with terse audited content and keep the referral callout.
- [x] 3. Verify internal anchors and companion links resolve locally.
- [ ] 4. Run a markdown/link sanity pass and secret scan before commit.
- [ ] 5. Open PR using the repo template and check CI/preview status.

## Risks & Mitigations
- **Risk:** Removing useful niche material. **Mitigation:** Preserve companion-file links and keep reusable patterns as concise recipes.
- **Risk:** Official docs and pricing change quickly. **Mitigation:** Cite current official pages and frame pricing/model details as “verify before purchase.”
- **Risk:** Plan file adds repo clutter. **Mitigation:** It is required by the repo skill for this non-trivial rewrite and scoped to one PR.

## Rollback Plan
Revert the README and plan-file commit, restoring the prior guide exactly.

## Session Log
- 2026-04-24 19:58 — wiki checked; no prior Windsurf-specific vault context.
- 2026-04-24 20:01 — researched official docs, pricing, and changelog; plan drafted.
- 2026-04-24 20:14 — README rewritten from 3,253 lines to 731 lines; local anchors verified.
