# Deep Dive: sharp-edges

## Score: 9/10

### Sub-scores
- **Completeness: 10/10** — 6 sharp edge categories (algorithm footguns, dangerous defaults, primitive vs semantic APIs, config cliffs, silent failures, stringly-typed security). Each with detection patterns + code examples. 3 adversary models. 4-phase workflow. Severity classification table. Rationalizations-to-Reject (6). Quality Checklist (8 items). 4 category-specific references + 11 language guides. The JWT + OTP + Libsodium examples are real-world and concrete.
- **Usability: 9/10** — 293 lines, well under 500 limit. Each category has: pattern → detection → example → fix. The 3 adversary models (Scoundrel/Lazy/Confused developer) are memorable and immediately applicable. Quality checklist at the end prevents skipping steps.
- **Modularity: 9/10** — Clean split: SKILL.md (methodology + 6 categories) → 4 category references (crypto, config, auth, case-studies) → 11 language guides. Read-only tool restriction (Read/Grep/Glob only).
- **Safety: 8/10** — Rationalizations are excellent ("It's documented" → "Developers don't read docs under deadline pressure"). Tool restriction prevents modification. Missing: no `disable-model-invocation` (could trigger broadly on any API review).

## Strengths

1. **"Pit of success" as core principle is perfect framing.** One sentence that captures the entire philosophy: "Secure usage should be the path of least resistance." Every finding is measured against this standard.

2. **3 adversary models are immediately memorable.** Scoundrel (malicious), Lazy (copy-paste), Confused (misunderstanding) — these replace vague "attacker" with specific developer personas. Forces analysts to think from multiple perspectives.

3. **Concrete code examples per category are teaching-quality.** The JWT `alg: none` attack, OTP `lifetime=0` ambiguity, Libsodium vs Halite comparison, config typo `fasle` — each example demonstrates the exact footgun, not just describes it.

4. **Zero/empty/null probing technique is universal.** "What happens with 0, '', null, [], -1?" — this single question methodology catches an enormous class of bugs. Applicable to any API in any language.

5. **11 language-specific guides provide depth without bloating SKILL.md.** Language footguns vary wildly (Go's implicit zero values vs PHP's type juggling vs Rust's unsafe blocks). Separate files keep SKILL.md focused while providing deep per-language knowledge.

## Weaknesses

1. **No automation hooks.** Unlike semgrep skill which can auto-scan, this is purely manual analysis. Could suggest: "Run semgrep with `dangerous-defaults` ruleset as Phase 0 pre-filter."

2. **Severity classification lacks CVSS mapping.** Critical/High/Medium/Low is defined qualitatively but doesn't map to standard frameworks. When outputting to SARIF or security reports, a CVSS estimate would help prioritization.

3. **No output template.** The skill defines how to analyze but not how to format findings. Should have a standard finding template: Title, Category, Severity, Vulnerable Code, Secure Alternative, Exploitability.

## Kha nang tich hop

**HIGH — applicable to any codebase with security-relevant APIs.**
- Run on plugin hook code in this repo
- Pair with `insecure-defaults` (overlapping concern but different scope: insecure-defaults = config values, sharp-edges = API design)
- Pair with `audit-context-building` (Phase 3 trust boundary mapping feeds into sharp-edges analysis)
- 11 language guides useful for multi-language projects

## Key Patterns Worth Adopting
1. **"Pit of success" principle** — Secure should be the default, insecure should require effort
2. **3 adversary models** — Scoundrel / Lazy / Confused as analysis lenses
3. **Zero/empty/null probing** — Universal edge case technique for any API
4. **Category-based detection patterns** — Structured approach vs ad-hoc "look for problems"
5. **Quality checklist at end** — Prevents premature conclusion of analysis
6. **Code examples: vulnerable + secure side-by-side** — Most effective teaching format
