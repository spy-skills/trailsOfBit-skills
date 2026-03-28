# Deep Dive: semgrep-rule-creator

## Score: 9/10

### Sub-scores
- **Completeness: 9/10** — 7-step workflow with progress checklist. Test-first methodology enforced (100% pass required). Taint mode prioritization with clear rationale (FP reduction). Anti-patterns section (3 examples: too broad, missing safe cases, overly specific). Rationalizations-to-Reject (6 entries). Quick Reference + Workflow reference files. Documentation links (5 required reads). Output structure spec (exactly 2 files per rule). Strictness rules (9 rules including no todoruleid, one rule per YAML, no generic patterns).
- **Usability: 9/10** — 168 lines. Quick Start with complete working example (taint mode rule + test file + run command). Progress checklist is copy-paste ready. Anti-patterns have vulnerable vs correct side-by-side code. Clear "when to switch" guidance between taint and pattern matching.
- **Modularity: 8/10** — quick-reference.md (commands/operators/syntax) + workflow.md (detailed steps). Has commands/ directory. References to semgrep.dev docs for latest API. Tool permissions include WebFetch (to read live docs).
- **Safety: 9/10** — "100% test pass required" with "no todoruleid" (can't mark known failures as acceptable). Rationalizations prevent common shortcuts. "Optimization comes last" prevents premature simplification.

## Strengths

1. **Test-first is not optional — it's the core architecture.** Step 2 (Write Tests) comes before Step 4 (Write Rule). The skill doesn't just recommend testing; it makes untested rules impossible by design. "100% test pass is required" with 0 exceptions.

2. **Taint mode prioritization with clear switching guidance.** "If pattern matching produces too many FPs, switch to taint. If taint doesn't propagate, switch to pattern." This pragmatic flexibility avoids dogmatic attachment to one approach.

3. **Anti-patterns section teaches through contrast.** BAD: `$FUNC(...)` (matches everything). GOOD: `eval(...)` (specific). BAD: only test vulnerable case. GOOD: test vulnerable + safe + sanitized. Visual contrast is the fastest way to learn.

4. **"No todoruleid" strictness rule is unique.** Most tools allow `@expected-failure` annotations that rot into permanent technical debt. Banning this forces all tests to pass or the rule doesn't ship. High-quality output guaranteed.

5. **AST analysis step (Step 3) prevents pattern guessing.** `semgrep --dump-ast` reveals how Semgrep actually parses code. Patterns based on AST match reliably; patterns based on source text fail on syntactic variations.

## Weaknesses

1. **Required WebFetch of 5 URLs is fragile.** If Semgrep documentation changes URLs or goes offline, the skill breaks. Should include a local cache or summary of key concepts as fallback.

2. **No rule testing CI integration guidance.** The skill creates rules locally but doesn't cover: adding to CI pipeline, managing rule regressions across codebase updates, or version-pinning Semgrep.

3. **No guidance on rule performance.** Complex taint patterns on large codebases can be slow. No mention of `--timeout`, pattern optimization for speed, or benchmarking rule performance.

## Kha nang tich hop

**HIGH — natural extension of variant-analysis and semgrep scanner.**
- Chain: find vuln → `variant-analysis` → `semgrep-rule-creator` → CI rule
- Rules from this skill feed into `static-analysis/semgrep` scanner
- Can create custom rules for patterns found by `insecure-defaults` or `sharp-edges`

## Key Patterns Worth Adopting
1. **Test-first mandatory** — Write tests before implementation, 100% pass, no exceptions
2. **"No todoruleid" rule** — Ban expected-failure annotations to prevent tech debt
3. **Taint-first with switching guidance** — Start sophisticated, simplify if needed
4. **AST-before-pattern** — Inspect how tool parses before writing patterns
5. **Exactly 2 files output** — Predictable structure enables automation
6. **Anti-patterns with BAD/GOOD contrast** — Most effective teaching format
