# Deep Dive: differential-review

## Score: 9/10

### Sub-scores
- **Completeness: 10/10** — 7-phase workflow (Pre-Analysis → Triage → Code Analysis → Test Coverage → Blast Radius → Deep Context → Adversarial → Report). 7 rationalizations-to-reject. 3 codebase size strategies (SMALL/MEDIUM/LARGE). 3 risk levels. Quality checklist. Red flags for immediate escalation. Full supporting docs (methodology, adversarial, reporting, patterns).
- **Usability: 9/10** — Decision tree routes users to exact doc they need. Quick Reference for experienced users. 3 usage examples (quick triage ~30min, standard ~3-4h, deep audit ~6-8h). Progressive disclosure: SKILL.md → 4 reference files.
- **Modularity: 8/10** — Clean reference split. Integrates with audit-context-building (Pre-Analysis) and issue-writer (output). patterns.md references domain-specific pattern databases. However, all 4 references are at skill root level, not in a references/ subdirectory (minor structural inconsistency with repo conventions).
- **Safety: 9/10** — Evidence-based findings (no generic claims). Explicit coverage limitations stated. "Refactors break invariants — analyze as HIGH until proven LOW" prevents false sense of security.

## Strengths

1. **Adaptive depth by codebase size is rare and practical.** SMALL/MEDIUM/LARGE strategies with clear thresholds (<20/20-200/200+ files) prevent both over-analysis of small changes and under-analysis of large ones. Most review tools treat all changes equally.

2. **Git blame on removed security code catches regressions.** The specific command `git log -S "pattern" --all --grep="security\|fix\|CVE"` is immediately actionable. This catches the scenario where a security fix gets reverted months later — a real-world attack vector.

3. **Blast radius quantification is unique.** Not just "this change affects other code" but "50+ callers = HIGH blast radius → requires adversarial analysis." Quantitative thresholds enable consistent severity assessment.

4. **Adversarial modeling is structured, not ad-hoc.** Phase 5 defines WHO (attacker type), WHAT (access level), WHERE (entry points), then requires concrete attack sequences with proof of accessibility. This forces specificity over hand-waving.

5. **Rationalizations table has "Heartbleed was 2 lines."** Perfect counter to "small PR, quick review." Each rationalization has the wrong assumption, why it's wrong, and required action. Memorable and effective.

## Weaknesses

1. **No automated tooling integration.** The skill is entirely manual. Could reference: `semgrep` for automated pattern detection, `git diff --stat` pre-analysis automation, or CI integration for auto-triggering reviews on HIGH-risk file changes.

2. **methodology.md audit-context-building invocation assumes the skill is installed.** The Pre-Analysis step shows `audit-context-building --scope ...` but doesn't handle the case where that skill isn't available. Should have a fallback manual context-building approach.

3. **patterns.md references non-existent paths.** `domain-specific-audits/defi-bridges/resources/`, `not-so-smart-contracts` — these reference Trail of Bits tools that may not be in the same repo or installed. Broken references could confuse users.

## Kha nang tich hop

**HIGH — directly applicable to any PR review workflow.**
- **With `audit-context-building`:** Pre-Analysis phase explicitly integrates
- **With `insecure-defaults`:** Run insecure-defaults on changed files as Phase 1 supplement
- **With OMC code-reviewer agent:** Use methodology as the agent's review framework
- **With CI/CD:** Auto-trigger SURGICAL review on PRs touching auth/crypto files

## Key Patterns Worth Adopting
1. **Codebase size strategy** — SMALL/MEDIUM/LARGE with clear thresholds and different analysis depths
2. **Risk-first classification** — HIGH/MEDIUM/LOW based on what code does, not how much changed
3. **Git blame for security regressions** — `git log -S` with security/fix/CVE grep
4. **Quantitative blast radius** — Count callers, not just "it affects things"
5. **Always generate file output** — "I'll explain verbally" = "findings lost"
