# Deep Dive: variant-analysis

## Score: 8/10

### Sub-scores
- **Completeness: 8/10** — 5-step process (understand → exact match → identify abstractions → generalize → triage). Tool selection matrix. 4 critical pitfalls with mitigations. Abstraction points table. Ready-to-use CodeQL/Semgrep templates for 5 languages. Report template. Has METHODOLOGY.md for deep strategy. Missing: no Rationalizations-to-Reject section (though pitfalls partially cover this).
- **Usability: 9/10** — 142 lines, concise and actionable. 5-step process is easy to follow mechanically. "Stop when FP rate exceeds ~50%" is a clear, quantitative stopping criterion. Tool selection matrix eliminates guesswork.
- **Modularity: 8/10** — Templates for 5 languages (CodeQL + Semgrep), report template, METHODOLOGY.md. Resources organized by tool type. Missing: templates are in resources/ not references/ (minor inconsistency). Has commands/ directory.
- **Safety: 7/10** — "Always search ENTIRE codebase" prevents scope bias. Pitfall section prevents common mistakes. But no explicit warning about false confidence from low match counts (0 matches ≠ no variants).

## Strengths

1. **"One element at a time" generalization rule is the core insight.** Most analysts jump from exact match to overly-general pattern. This incremental approach with verify-after-each-change prevents the FP explosion that kills variant analysis efforts.

2. **"50% FP rate = stop" gives a concrete threshold.** Without this, analysts generalize until matches are meaningless or stop too early. Quantitative criterion enables consistent quality across analysts.

3. **4 critical pitfalls address the real failure modes.** Narrow scope, over-specific patterns, single vuln class, missing edge cases — these are EXACTLY what goes wrong in practice. Each pitfall has a concrete example + mitigation.

4. **Tool selection matrix is practical.** ripgrep (quick surface) → Semgrep (patterns) → CodeQL (data flow) — clear escalation path. "Non-building code → Semgrep" is a key insight for real-world codebases.

5. **Ready-to-use templates for 5 languages.** CodeQL .ql and Semgrep .yaml files per language. Starting from a template is 10x faster than writing from scratch.

## Weaknesses

1. **No Rationalizations-to-Reject.** Common shortcuts like "I only found 2 matches, so we're good" or "This pattern doesn't apply to our framework" are not addressed.

2. **No automation workflow.** The 5-step process is manual. Could describe: "After Step 4, save the final pattern as a Semgrep rule using `semgrep-rule-creator` skill for CI integration."

3. **Step 1 assumes a known vulnerability.** Skill explicitly says "NOT for initial discovery" — but doesn't bridge to `audit-context-building` or `insecure-defaults` for finding the initial issue. Should mention the skill chain.

## Kha nang tich hop

**HIGH — complements initial vulnerability finding skills.**
- Chain: `audit-context-building` → find vuln → `variant-analysis` → `semgrep-rule-creator` → CI rule
- Pairs with `insecure-defaults` (find one default issue → search for variants)
- CodeQL/Semgrep templates reusable across projects

## Key Patterns Worth Adopting
1. **One-element-at-a-time generalization** — Incremental pattern widening with verify
2. **50% FP rate stopping criterion** — Quantitative threshold for pattern quality
3. **Tool escalation path** — ripgrep → Semgrep → CodeQL based on need
4. **Abstraction points table** — "Keep specific vs Can abstract" decision framework
5. **"Search everywhere" principle** — Always entire codebase, never just the module
