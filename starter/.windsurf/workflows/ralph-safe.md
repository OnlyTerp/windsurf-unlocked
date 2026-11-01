---
name: ralph-safe
description: The "Ralph Wiggum" persistent loop — iterate Cascade until a checkable outcome is met (tests green, lint clean, build passes) — with a kill-switch, iteration cap, and cost cap so it can't run away. Safe variant of the viral while-true pattern.
---

# Ralph Safe Loop

> *"I'm helping!"* — Ralph Wiggum

A while-loop that calls Cascade repeatedly until a verifiable green signal (tests pass, lint clean, build green) — with explicit guardrails so it cannot run away with your wallet or commit nonsense to `main`.

## When to Use

- ✅ Fixing 10+ failing tests with clear error messages
- ✅ Resolving compile errors in a large refactor
- ✅ Making a linter pass (ESLint, ruff, clippy)
- ✅ Closing out a type-check sweep
- ✅ Any task where the **checkable outcome is well-defined and machine-verifiable**

## When NOT to Use

- ❌ UI flows that need human judgment
- ❌ Feature implementation (use Planning With Files instead)
- ❌ Anything involving money, destructive data operations, or production infrastructure
- ❌ Tasks where "passing" depends on subjective quality
- ❌ On shared branches without a dedicated worktree

## The Loop

```bash
#!/usr/bin/env bash
# .windsurf/workflows/ralph-safe.sh
# Usage: ./ralph-safe.sh "make pnpm test green"

set -euo pipefail

GOAL="${1:?goal required — 'make X green'}"
MAX_ITERS="${MAX_ITERS:-20}"
COST_CAP_USD="${COST_CAP_USD:-5.00}"
KILLSWITCH="${HOME}/.ralph-stop"
CHECK_CMD="${CHECK_CMD:-pnpm test --silent}"
LOGDIR=".ralph-logs/$(date +%s)"
mkdir -p "$LOGDIR"

# Pre-flight safety checks
# `git symbolic-ref` returns non-zero on a detached HEAD (common in worktrees
# and CI checkouts); fall back to empty so `pipefail` doesn't misreport the
# state as "shared branch". An empty BRANCH passes the blocklist check — the
# concern here is protecting named shared branches, not every ref.
BRANCH="$(git symbolic-ref --short HEAD 2>/dev/null || true)"
if echo "$BRANCH" | grep -Eq '^(main|master|develop)$'; then
  echo "ralph refuses to run on shared branches (current: $BRANCH)"
  exit 1
fi
[ -z "$(git status --porcelain)" ] \
  || { echo "ralph refuses to run with a dirty worktree"; exit 1; }

# `windsurf billing usage` is optional — if it fails or isn't installed we skip
# the cost cap rather than aborting the whole loop. `set -e` + `pipefail` would
# otherwise kill the script before any iteration runs.
START_COST="$(windsurf billing usage --format=json 2>/dev/null | jq -r '.session_cost_usd // empty' 2>/dev/null || true)"
if [ -z "$START_COST" ]; then
  echo "⚠ cost cap disabled (windsurf billing usage unavailable)"
fi

for i in $(seq 1 "$MAX_ITERS"); do
  echo "── Iter $i/$MAX_ITERS ──"

  # 1. Killswitch check
  if [ -f "$KILLSWITCH" ]; then
    echo "Killswitch tripped — bailing."
    rm "$KILLSWITCH"
    exit 2
  fi

  # 2. Cost cap check (only when we have a baseline)
  SPENT="0"
  if [ -n "$START_COST" ]; then
    CURR_COST="$(windsurf billing usage --format=json 2>/dev/null | jq -r '.session_cost_usd // empty' 2>/dev/null || true)"
    if [ -n "$CURR_COST" ]; then
      SPENT=$(echo "$CURR_COST - $START_COST" | bc)
      if (( $(echo "$SPENT > $COST_CAP_USD" | bc) )); then
        echo "Cost cap hit: \$$SPENT > \$$COST_CAP_USD"
        exit 3
      fi
    fi
  fi

  # 3. Check: are we already green?
  if eval "$CHECK_CMD" > "$LOGDIR/check-$i.log" 2>&1; then
    echo "✓ Green at iter $i. Spent: \$$SPENT"
    exit 0
  fi

  # 4. Not green — hand the failure to Cascade and iterate
  FAILURE=$(tail -50 "$LOGDIR/check-$i.log")
  # The windsurf CLI takes the prompt as its argument; there is no cascade
  # subcommand, and extra words are opened as files instead of running.
  windsurf "Goal: $GOAL

The check command '$CHECK_CMD' is red. Latest output:

\`\`\`
$FAILURE
\`\`\`

Fix the CODE (never weaken tests unless they are clearly wrong — if they are, STOP and ask).
Do not try to re-run the check yourself — I'll run it.
When you're done, reply with a one-line summary of what you changed." \
    > "$LOGDIR/cascade-$i.log" \
    || echo "  cascade returned non-zero on iter $i — continuing to next iteration"
done

echo "Exceeded $MAX_ITERS iterations without going green."
exit 4
```

## Guardrails (Non-Negotiable)

1. **Worktree-only.** Never run on your main/develop branch. Use [§11 Worktrees](https://github.com/OnlyTerp/windsurf-unlocked#11-worktrees--parallel-cascade) to isolate.
2. **Killswitch file.** `touch ~/.ralph-stop` from any terminal stops the loop at the next iteration.
3. **Iteration cap.** Default 20. If it hasn't gone green by then, something is structurally wrong.
4. **Cost cap.** Default $5. Sanity bound on runaway spend.
5. **Clean worktree required.** Refuses to start if there are uncommitted changes — so the diff at the end is attributable.
6. **Never weakens tests.** The prompt explicitly forbids modifying test assertions unless the tests themselves are wrong.
7. **Log everything.** Every iteration's check output and Cascade response goes to `.ralph-logs/<timestamp>/`. Add that directory to `.gitignore`.

## After It Goes Green

1. **Review the diff** — `git diff --stat` then `git diff`. Do not merge without reading.
2. **Re-run the check manually.** Sometimes caches lie.
3. **Check for suspicious weakenings** — `rg -C 2 '(skip|todo|xtest|it\.only)' $(git diff --name-only)`
4. **Squash and open the PR** with the Cascade logs attached for transparency.

## Scaling Up

For multi-check loops (tests + lint + typecheck + build all green):

```bash
CHECK_CMD='pnpm test && pnpm lint && pnpm typecheck && pnpm build' \
  MAX_ITERS=40 ./ralph-safe.sh "everything green"
```

## Credits

Named after Ralph Wiggum by Steve Kinney in his [Entering the Mind of Ralph Wiggum](https://stevekinney.com/writing/the-ralph-loop) post (Mar 31, 2026). Community critiques in the [r/ClaudeCode review thread](https://www.reddit.com/r/ClaudeCode/comments/1q2qvta/share_your_honest_and_thoughtful_review_of_ralph/) informed the guardrails above.
