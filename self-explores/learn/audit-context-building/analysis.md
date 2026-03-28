# Deep Dive: audit-context-building

## Score: 9/10

### Sub-scores
- **Completeness: 10/10** — 3-phase methodology (Orientation → Ultra-Granular Analysis → Global Understanding). Per-function microstructure checklist (Purpose, Inputs, Outputs, Block-by-Block with First Principles/5 Whys/5 Hows). Cross-function flow analysis (internal + external calls). Quality thresholds (min 3 invariants, 5 assumptions, 3 risks per function). Completeness checklist. Rationalizations-to-Reject (6 entries). Anti-hallucination rules. Subagent spawning via function-analyzer. Resources: FUNCTION_MICRO_ANALYSIS_EXAMPLE.md, OUTPUT_REQUIREMENTS.md, COMPLETENESS_CHECKLIST.md.
- **Usability: 8/10** — 302 lines is within the 500-line limit. Well-structured phases. However, the analysis methodology is extremely thorough — could feel heavy for smaller codebases. No "lite mode" option.
- **Modularity: 9/10** — Clean separation: SKILL.md (methodology), resources/ (3 reference files), agents/ (function-analyzer), commands/ (audit-context). Each resource serves a distinct purpose.
- **Safety: 10/10** — Explicit "pure context building" — NO vulnerability findings, NO fixes, NO exploits while active. Anti-hallucination rules: "never reshape evidence to fit assumptions," "use 'unclear; need to inspect X' instead of 'it probably...'". This prevents the common AI failure of confident wrong conclusions.

## Strengths

1. **"Slow is fast" philosophy is the key insight.** Rationalization #6: "This is taking too long → Rushed context = hallucinated vulnerabilities later." This is the fundamental truth of code auditing. By enforcing thorough context before conclusions, the skill prevents the most common AI audit failure: plausible-sounding but wrong vulnerability reports.

2. **External calls treated as adversarial by default (Case B).** When code is unavailable, the skill doesn't assume benign behavior — it considers revert, strange return values, unexpected state changes, reentrancy. This is the correct security mindset for smart contract auditing.

3. **Quality thresholds are concrete and measurable.** "Minimum 3 invariants per function, 5 assumptions documented, 3 risk considerations" — these are auditable. A reviewer can check if the analysis meets thresholds, not just "feels thorough enough."

4. **Anti-hallucination rules address the AI-specific failure mode.** "Never reshape evidence to fit earlier assumptions. When contradicted: update the model. State the correction explicitly." This is critical for LLM-based auditing where models tend to maintain consistency over accuracy.

5. **function-analyzer subagent for dense logic.** Spawning a specialized agent for cryptographic/mathematical functions preserves the main agent's context window while getting deep analysis. Smart architectural choice.

## Weaknesses

1. **No "lite mode" for small codebases.** Every function gets full micro-analysis — overkill for a 200-line utility script. Should offer SMALL/MEDIUM/LARGE strategy (like differential-review does).

2. **Heavily blockchain-oriented examples.** "DEX swap function," "contracts," "storage variables" — the examples lean heavily toward Solidity/smart contracts. Would benefit from web app or backend service examples to broaden applicability.

3. **No estimate of analysis time per function.** Quality thresholds say "3 invariants, 5 assumptions" but don't say this takes ~5-10 minutes per function. For a codebase with 200 functions, that's 20-30 hours — users should know upfront.

4. **Missing integration with static analysis tools.** The skill is pure manual analysis. Could mention: "Run semgrep first to identify hotspots, then apply ultra-granular analysis to HIGH-risk functions only" to prioritize effort.

## Kha nang tich hop

**HIGH — foundational skill for serious code auditing.**
- **Pre-audit phase:** Run before `differential-review`, `insecure-defaults`, or any vulnerability-hunting skill
- **OMC architect agent:** Use this methodology for deep codebase understanding
- **With semgrep:** Use static analysis to identify functions worth ultra-granular analysis
- **spy-skills development:** Apply to audit plugins before deployment

## Key Patterns Worth Adopting
1. **Pure context phase** — Separate understanding from conclusions (no vulns during context building)
2. **Anti-hallucination rules** — "Update model when contradicted, state correction explicitly"
3. **Quality thresholds** — Minimum counts for invariants, assumptions, risks (measurable, not subjective)
4. **External-as-adversarial** — Default assumption for any code not in the codebase
5. **Continuity rule** — "Treat entire call chain as one continuous execution flow. Never reset context."
6. **"Slow is fast"** — Rushed context leads to wrong conclusions later
