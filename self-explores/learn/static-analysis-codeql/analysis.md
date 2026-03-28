# Deep Dive: static-analysis/codeql

## Score: 8/10

### Sub-scores
- **Completeness: 9/10** — 3-workflow pipeline (build-database → create-data-extensions → run-analysis). Auto-detection logic (DB exists? extensions exist?). 6 Rationalizations-to-Reject (excellent: "security-extended is enough" → always add ToB+Community packs). Build method sequence. Language support (8 languages). Decision prompt for ambiguous requests. Quick Start verification.
- **Usability: 8/10** — 119 lines SKILL.md, clean. Decision table for conditional logic. Quick Start is 6 lines. But requires CodeQL CLI installed — no fallback if missing.
- **Modularity: 8/10** — 3 separate workflow files keep each phase focused. Task tool permissions for parallel execution. auto-detection routes to correct workflow.
- **Safety: 8/10** — Rationalizations prevent false confidence ("No findings ≠ secure code", "Built DB ≠ good extraction"). Explicit "build-mode=none is last resort" for compiled langs.

## Strengths
1. **"No findings means secure" rationalization** — Explicitly addresses the false confidence trap
2. **Data extensions workflow is mandatory, not optional** — Custom frameworks need custom models
3. **3-method build sequence** — Tries autobuild → manual build → build-mode=none (graceful degradation)
4. **Database quality assessment step** — Check file counts against expected source files

## Weaknesses
1. **Requires CodeQL CLI** — No guidance on installation or fallback
2. **No estimate of scan time** — Large codebases can take hours; users should know
3. **No SARIF output integration** — Should reference sarif-parsing skill for result processing

## Kha nang tich hop: HIGH — deep analysis complement to semgrep (speed vs depth tradeoff)
## Key Patterns: 3-workflow pipeline, "no findings ≠ secure" rationalization, graceful build degradation
