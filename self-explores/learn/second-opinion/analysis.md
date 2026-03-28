# Deep Dive: second-opinion

## Score: 7/10

### Sub-scores
- **Completeness: 7/10** — Covers both Codex and Gemini CLI invocation. 3 review scopes (uncommitted/branch/commit). Parallel execution. Structured JSON output from Codex (--output-schema). Interactive question flow. Diff-aware optimizations. Large diff warning (>2000 lines). Reference files for each tool. Missing: no Rationalizations-to-Reject, no finding aggregation/dedup across models.
- **Usability: 8/10** — 294 lines. Quick Reference with copy-paste commands. Interactive AskUserQuestion flow collects all params in one shot. Both tools run in parallel (parallel Bash calls).
- **Modularity: 7/10** — codex-invocation.md + gemini-invocation.md. Bundles codex-mcp-server. But tightly coupled to specific CLI tool versions.
- **Safety: 6/10** — `--yolo` flag on Gemini explicitly noted as security concern. No data sensitivity warning (code sent to external APIs). No rate limit / cost guidance.

## Strengths
1. **Parallel multi-model execution** — Run Codex + Gemini simultaneously, compare findings
2. **Structured JSON output from Codex** — Machine-parseable results, not just text
3. **Diff-aware optimization** — Skip dependency scanning if no manifest files changed
4. **Interactive parameter collection** — One AskUserQuestion with up to 4 questions

## Weaknesses
1. **No data sensitivity warning** — Code is sent to external APIs (OpenAI, Google)
2. **`--yolo` Gemini flag auto-approves all actions** — Security risk not mitigated
3. **No finding dedup/aggregation** — Two models may report same issue differently

## Kha nang tich hop: MEDIUM — requires Codex/Gemini CLI installed + API keys
## Key Patterns: Parallel multi-model review, structured JSON output schema, diff-aware scanning
