# Trail of Bits Skills Marketplace — Catalog & Ranking

## Overview
28 plugins, 53+ sub-skills, 18,251 total SKILL.md lines across 10 categories.

## Catalog by Category

### Code Auditing (10 plugins — largest group)

| # | Plugin | Lines | Complexity | App Score | Key Capability |
|---|--------|-------|------------|-----------|----------------|
| 1 | audit-context-building | 302 | Advanced | 5/5 | Line-by-line deep analysis, mental model building |
| 2 | differential-review | 220 | Advanced | 5/5 | Risk-first PR review, blast radius estimation |
| 3 | insecure-defaults | 117 | Intermediate | 5/5 | Fail-open vs fail-secure detection |
| 4 | static-analysis (3 sub) | 1029 | Advanced | 5/5 | Semgrep + CodeQL + SARIF toolchain |
| 5 | variant-analysis | 142 | Intermediate | 4/5 | Find similar vulns via pattern generalization |
| 6 | semgrep-rule-creator | 168 | Intermediate | 4/5 | Test-first custom Semgrep rule authoring |
| 7 | semgrep-rule-variant-creator | 205 | Intermediate | 4/5 | Port rules across languages |
| 8 | sharp-edges | 292 | Intermediate | 4/5 | API footgun identification, 11 lang guides |
| 9 | burpsuite-project-parser | 358 | Intermediate | 3/5 | Parse Burp Suite .burp files |
| 10 | testing-handbook-skills (15 sub) | 7929 | Advanced | 3/5 | Fuzzing toolkit: libFuzzer, AFL++, Wycheproof |

### Smart Contract Security (2 plugins)

| # | Plugin | Lines | Complexity | App Score | Key Capability |
|---|--------|-------|------------|-----------|----------------|
| 11 | building-secure-contracts (11 sub) | 3635 | Advanced | 4/5 | 6-chain scanners + audit prep + token analyzer |
| 12 | entry-point-analyzer | 251 | Intermediate | 3/5 | Entry point identification for 7 languages |

### Verification (3 plugins)

| # | Plugin | Lines | Complexity | App Score | Key Capability |
|---|--------|-------|------------|-----------|----------------|
| 13 | property-based-testing | 123+refs | Intermediate | 5/5 | Auto pattern detection, multi-language PBT |
| 14 | constant-time-analysis | 219 | Advanced | 3/5 | Compiler timing side-channel detection |
| 15 | spec-to-code-compliance | 357 | Advanced | 2/5 | Spec-to-code alignment for blockchain audits |

### Development (7 plugins)

| # | Plugin | Lines | Complexity | App Score | Key Capability |
|---|--------|-------|------------|-----------|----------------|
| 16 | modern-python | 333+refs | Intermediate | 5/5 | uv + ruff + ty modern Python stack |
| 17 | ask-questions-if-underspecified | 85 | Basic | 5/5 | Meta-skill: clarify before implementing |
| 18 | second-opinion | 294 | Intermediate | 4/5 | Multi-LLM code review (Codex + Gemini) |
| 19 | devcontainer-setup | 300 | Intermediate | 4/5 | Auto-detect language, generate devcontainer |
| 20 | gh-cli | 100+refs | Basic | 4/5 | URL interception → gh CLI |
| 21 | git-cleanup | 364 | Intermediate | 4/5 | Safe branch cleanup with squash-merge detection |
| 22 | workflow-skill-design | 258 | Intermediate | 2/5 | Meta-skill: design workflow skills |

### Other (4 plugins)

| # | Plugin | Lines | Complexity | App Score | Key Capability |
|---|--------|-------|------------|-----------|----------------|
| 23 | yara-authoring | 645 | Advanced | 4/5 | YARA-X rule authoring + linting scripts |
| 24 | dwarf-expert | 93 | Intermediate | 2/5 | DWARF debugging format |
| 25 | firebase-apk-scanner | 197 | Intermediate | 3/5 | Android Firebase misconfiguration scanner |
| 26 | culture-index | 316 | Advanced | 2/5 | Culture Index survey interpretation |
| 27 | claude-in-chrome-troubleshooting | 251 | Basic | 2/5 | Chrome MCP extension troubleshooting |
| 28 | debug-buttercup | 281 | Advanced | 1/5 | Internal ToB Kubernetes debugging |

---

## Ranking by Priority (5 criteria)

**Criteria weights:** Practical applicability (30%), Knowledge depth (20%), OMC/spy-skills integration (20%), Independence (15%), Learning curve (15%)

### Tier 1: Learn First (Score 4.5-5.0)

| Rank | Plugin | Practical | Depth | Integration | Independence | Learning | TOTAL |
|------|--------|-----------|-------|-------------|--------------|----------|-------|
| 1 | static-analysis/semgrep | 5 | 5 | 5 | 3 | 3 | **4.45** |
| 2 | insecure-defaults | 5 | 3 | 4 | 5 | 5 | **4.45** |
| 3 | ask-questions-if-underspecified | 5 | 2 | 5 | 5 | 5 | **4.40** |
| 4 | differential-review | 5 | 5 | 4 | 4 | 3 | **4.35** |
| 5 | audit-context-building | 5 | 5 | 4 | 4 | 3 | **4.35** |
| 6 | property-based-testing | 5 | 4 | 4 | 4 | 3 | **4.15** |
| 7 | modern-python | 5 | 4 | 3 | 5 | 4 | **4.15** |

### Tier 2: Learn Second (Score 3.5-4.4)

| Rank | Plugin | TOTAL | Notes |
|------|--------|-------|-------|
| 8 | sharp-edges | 3.95 | API footgun patterns, 11 languages |
| 9 | variant-analysis | 3.85 | Pairs with any initial vuln finding |
| 10 | semgrep-rule-creator | 3.75 | Test-first rule authoring |
| 11 | yara-authoring | 3.70 | Longest skill, most comprehensive |
| 12 | git-cleanup | 3.65 | Immediately useful for branch hygiene |
| 13 | gh-cli | 3.60 | Small but high daily utility |
| 14 | second-opinion | 3.55 | Multi-LLM review, needs Codex/Gemini CLI |
| 15 | devcontainer-setup | 3.50 | Useful for new project bootstrapping |
| 16 | building-secure-contracts | 3.50 | Narrow (blockchain) but deep |

### Tier 3: Optional (Score < 3.5)

| Rank | Plugin | TOTAL | Notes |
|------|--------|-------|-------|
| 17 | static-analysis/codeql | 3.40 | Requires CodeQL install |
| 18 | static-analysis/sarif-parsing | 3.30 | Important for CI/CD integration |
| 19 | testing-handbook-skills | 3.20 | Massive (15 sub-skills), specialized |
| 20 | firebase-apk-scanner | 3.10 | Android + Firebase only |
| 21 | entry-point-analyzer | 3.00 | Smart contract focused |
| 22 | constant-time-analysis | 2.85 | Crypto-specific, narrow |
| 23 | semgrep-rule-variant-creator | 2.80 | Niche follow-up to rule-creator |
| 24 | burpsuite-project-parser | 2.75 | Requires Burp Suite Pro |
| 25 | workflow-skill-design | 2.50 | Meta-skill for skill authors |
| 26 | spec-to-code-compliance | 2.30 | Blockchain audit specific |
| 27 | dwarf-expert | 2.20 | Binary analysis niche |
| 28 | culture-index | 2.00 | Requires CI subscription |

---

## Learning Roadmap

### Phase 1: Foundation (~3 hours)
Broadly applicable skills that teach core patterns.

1. **ask-questions-if-underspecified** (~10 min) — Meta-skill, sets the right mindset
2. **insecure-defaults** (~15 min) — Small, actionable, immediate value
3. **modern-python** (~25 min) — Practical tooling upgrade
4. **static-analysis/semgrep** (~40 min) — Largest payoff, teaches parallel agent pattern
5. **audit-context-building** (~30 min) — Foundation for all auditing
6. **differential-review** (~25 min) — PR review enhancement

### Phase 2: Intermediate (~3 hours)
Deeper security patterns and tool-specific skills.

7. **property-based-testing** (~20 min) — Cross-language testing methodology
8. **sharp-edges** (~25 min) — API design analysis
9. **variant-analysis** (~20 min) — Scale findings across codebases
10. **semgrep-rule-creator** (~20 min) — Custom detection rules
11. **yara-authoring** (~40 min) — Detection engineering
12. **git-cleanup + gh-cli** (~35 min) — Developer productivity

### Phase 3: Advanced (~2 hours)
Specialized domains and infrastructure.

13. **building-secure-contracts** (top 3) (~35 min) — Blockchain security
14. **static-analysis/codeql + sarif** (~50 min) — Deep static analysis
15. **second-opinion + devcontainer** (~40 min) — Multi-LLM + dev env

---

## Key Patterns Worth Adopting (cross-cutting)

1. **HARD GATE pattern** (from semgrep) — User must explicitly approve before destructive actions
2. **Rationalizations to Reject** (from semgrep, yara) — Anticipate shortcuts that lead to bad outcomes
3. **Progressive disclosure** (from all well-structured skills) — SKILL.md < 500L, details in references/
4. **Parallel subagent architecture** (from semgrep) — Split work by language/category for parallelism
5. **When/When-NOT sections** (Anthropic standard) — Explicit trigger boundaries prevent misuse
