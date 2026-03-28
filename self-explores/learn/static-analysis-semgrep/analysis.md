# Deep Dive: static-analysis/semgrep

## Score: 9/10

### Sub-scores
- **Completeness: 10/10** — Covers entire scan lifecycle: detection → ruleset selection → approval gate → parallel scan → parallel triage → SARIF merge. Has When/When-NOT, Rationalizations-to-Reject (14 entries), Common Mistakes table, Limitations section.
- **Usability: 8/10** — Good progressive disclosure (SKILL.md → rulesets.md → scanner/triage prompts). Clear step-by-step workflow. However, 431 lines in SKILL.md is on the edge of the 500-line limit. The approval gate UX is well-designed with explicit examples.
- **Modularity: 9/10** — Excellent separation: main orchestrator (SKILL.md), ruleset catalog (rulesets.md), scanner prompt template, triage prompt template, merge script. Each component is independently useful.
- **Safety: 10/10** — HARD GATE on user approval before scanning. Explicit "Rationalizations to Reject" section. Telemetry disabled by default (--metrics=off). No auto-scan without consent.

## Strengths

1. **Parallel subagent architecture is best-in-class.** The scan/triage split into parallel Task subagents per language category is genuinely innovative. Most tools run sequentially; this maximizes throughput while maintaining isolation per language.

2. **HARD GATE approval pattern is a model for other skills.** The Step 3 approval checkpoint with explicit "what counts as approval" and "what does NOT count" is the strongest safety gate I've seen in any skill. Other security skills should adopt this pattern.

3. **Third-party rulesets are REQUIRED, not optional.** Including Trail of Bits, 0xdea, Decurity rules by default (when language matches) catches vulnerabilities that the Semgrep registry alone misses. The ruleset selection algorithm in rulesets.md is comprehensive (13 GA languages, framework detection hints, 10+ third-party sources).

4. **Triage decision tree eliminates noise.** The FALSE_POSITIVE criteria (test files, sanitized inputs, dead code, nosemgrep comments) prevent the classic problem of overwhelming users with raw findings. The triage agent reads actual source context, not just rule matches.

5. **Workflow enforcement via Task system.** Using TaskCreate with dependencies to enforce step ordering is a clever pattern — it makes the workflow auditable and prevents steps from being skipped.

## Weaknesses

1. **No .semgrepignore guidance.** The skill doesn't mention creating or managing .semgrepignore files upfront. If a codebase has vendored/generated code, the scan will waste time on irrelevant files. Should add a Step 0.5 to check for and suggest .semgrepignore.

2. **SARIF merge script assumes uv is available.** `uv run {baseDir}/scripts/merge_triaged_sarif.py` requires uv, which isn't a standard install. Fallback to `python3` not mentioned. The script also optionally uses npm's SARIF Multitool — two optional deps in one step is fragile.

3. **No incremental scan support.** The skill always does a full codebase scan. For large repos (100k+ files), this could take hours. Should mention `--baseline-commit` for diff-only scanning in CI contexts.

4. **No guidance on handling scan failures.** If one parallel scanner fails (e.g., invalid ruleset, network error cloning GitHub rules), the skill doesn't define recovery. The triage step assumes all JSON files exist ("SOFT GATE: All scan JSON files exist") but doesn't say what to do if some are missing.

5. **Ruleset verification step is weak.** Step 5 in rulesets.md says "verify official rulesets load" with a single command, but doesn't handle the case where a third-party GitHub repo is down or has moved. No caching strategy mentioned.

## Kha nang tich hop vao he thong hien tai

**HIGH.** This is immediately useful for:
- **Code review workflows:** Run before `/viec phanbien` to get automated findings
- **PR security checks:** Integrate with `differential-review` skill for changed-files-only scanning
- **OMC integration:** The parallel Task architecture maps well to OMC's team mode
- **spy-skills auditing:** Can self-audit this repo's Python hooks and scripts

**Integration steps:**
1. Install Semgrep CLI (`pip install semgrep`)
2. Add as installed plugin to Claude Code
3. Use with `differential-review` for PR-focused scans
4. Create a `/viec samples` template for "Security Scan Sprint"

## Ghi chu ky thuat (Technical Decisions)

### Why parallel Tasks instead of single multi-config scan?
Semgrep supports `--config p/python --config p/django` in a single command, but the skill splits per language. Reason: (1) better isolation — one language failing doesn't block others, (2) triage is language-specific — Python FP patterns differ from JS patterns, (3) output files stay small and parseable.

### Why HARD GATE and not just proceed?
From rationalizations: "User asked for scan, that's approval" is explicitly rejected. The skill treats the original request as intent, not permission. This is important because rulesets affect what gets scanned and reported — wrong rulesets = wrong conclusions.

### Why --pro always when available?
The skill states "Cross-file analysis catches 250% more true positives." For security auditing, missing inter-file taint flows means missing entire vulnerability classes (e.g., user input in file A → SQL query in file B). Pro is worth the slower single-threaded execution.

### Key Patterns Worth Adopting
1. **HARD GATE pattern** — Use AskUserQuestion with explicit approval criteria for any destructive/irreversible action
2. **Parallel Task subagents with typed agents** — Separate scanner vs triager agents with different tool permissions
3. **Rationalizations to Reject** — Anticipate and document shortcuts developers might take
4. **Mandatory third-party sources** — Don't limit to vendor-provided rules; community rules catch real vulns
5. **SARIF as interchange format** — Enables CI/CD integration and tool interop
