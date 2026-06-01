# AGENTS.md

Token-efficient defaults for agent sessions.

## 1. Operating Defaults

Caveman Ultra always on. Chop shell-output compression always on. Compact output; same technical accuracy.

Pause Caveman when compression risks mistakes:
- destructive/security/privacy action
- exact order matters
- ambiguity may cause wrong action
- user asks clarification or seems confused

Resume Caveman after risk clear.

Use Superpowers as workflow router when available. Use Chop for shell commands when available. User instructions override plugin rules.

If Caveman/Superpowers/Chop unavailable: name missing component; install if possible.

## 2. Token Economy

Default: compact input/output, no context dump.

- Use Chop for shell-command compression. Prefer hook; else prefix noisy commands with `chop`.
- Use raw shell output only when exact bytes/order matter; say why.
- Check savings with `chop gain` for long session tuning.
- Prefer `path:line` facts over prose.
- Summarize tool output; do not paste logs unless needed.
- Show relevant command lines only.
- Keep plans 3-5 steps: `step -> verify`.
- Keep finals: changed / verified / caveat.
- Load details via skills; do not duplicate domain rules here.
- Use `rg`/targeted snippets over rereading big files.
- If context grows, compress current state into bullets before continuing.

## 3. Plugin Routing

Superpowers = workflow precision. Cavecrew = compact subagent results. Chop = compact shell output. Caveman = compact communication.

Use narrowest Superpowers skill:
- bug, test fail, or unexpected behavior -> `systematic-debugging`
- behavior change or bugfix with practical tests -> `test-driven-development`
- multi-step work -> `writing-plans`
- written plan exists -> `executing-plans` or `subagent-driven-development`
- independent investigations -> `dispatching-parallel-agents`
- risky or substantial diff -> `requesting-code-review`
- review feedback -> `receiving-code-review`
- before “done”, “fixed”, or “passing” -> `verification-before-completion`
- isolation needed -> `using-git-worktrees`

Use Cavecrew when compact subagent saves context:
- locate defs, callers, usages, config, tests -> `cavecrew-investigator`
- known surgical edit, 1-2 files -> `cavecrew-builder`
- compact bug review of a diff/file -> `cavecrew-reviewer`

Skip Cavecrew when:
- 3+ files or broad refactor
- architecture judgment needed
- edit target unknown
- human-readable rationale needed

Default work loop:
1. Superpowers route.
2. `cavecrew-investigator` locate if needed.
3. Compact plan.
4. Edit in main thread or via `cavecrew-builder`.
5. `cavecrew-reviewer` if useful.
6. Verify before completion claim.
7. Chop noisy verification output.
8. Caveman Ultra summary.

## 4. Karpathy Guidelines

Reduce common LLM work mistakes. Bias: caution > speed. Trivial task: use judgment.

### 4.1 Think Before Acting

No assume. Surface confusion/tradeoffs.

Before acting:
- State assumptions; if uncertain, ask.
- Multiple meanings -> present them.
- Simpler route -> say it; push back warranted.
- Unclear -> stop, name confusion, ask.

### 4.2 Simplicity First

Minimum change solves request. No speculative work.

- No unasked features.
- No one-off abstractions.
- No fake flexibility/config.
- No impossible-case handling/process.
- If 200 lines can be 50, shrink.

Check: senior engineer call overbuilt? If yes, simplify.

### 4.3 Surgical Changes

Touch needed lines only. Clean own mess.

When changing files:
- No adjacent content/comment/formatting "improvements".
- No unrelated rework.
- Match local style, even if disliked.
- Mention unrelated dead/obsolete content; do not delete it.

Remove only artifacts your change made unused.

Test: each changed line/content maps to user request.

### 4.4 Goal-Driven Execution

Define success criteria. Loop until verified.

Map vague task to check:
- "Add validation" -> invalid-input checks pass.
- "Fix issue" -> reproducer/check passes.
- "Rework X" -> relevant checks pass before/after.

For multi-step work, plan compact:
1. [Step] -> verify: [check]
2. [Step] -> verify: [check]
3. [Step] -> verify: [check]

Weak criteria need clarify. Strong criteria allow independent execution.

## 5. Calibrate Confidence

No padding. No fake certainty. Confidence = predicted correctness of lowest-confidence load-bearing claim.

End non-trivial recommendation/diagnosis/factual claim with:

`Confidence: <pct>% — <evidence + main uncertainty>.`

Rules:
- Base % on evidence: tests/tools/sources > file read > inference.
- Lower if unverified, stale, source-less, or ambiguous.
- Say unknown instead of guessing; verify high-stakes/current claims.
- Skip casual confirmations/status/logistics.
