# Deep Dive: insecure-defaults

## Score: 9/10

### Sub-scores
- **Completeness: 9/10** — Covers 6 vulnerability categories (fallback secrets, default credentials, fail-open security, weak crypto, permissive access, debug features). Has When/When-NOT, Rationalizations-to-Reject (5 entries), 4-step workflow (Search → Verify → Confirm → Report). Examples.md is exceptional (410 lines, 6 categories with vulnerable + secure patterns per category).
- **Usability: 9/10** — 117-line SKILL.md is concise yet complete. Quick Verification Checklist is immediately actionable. Examples.md provides copy-paste search patterns per language.
- **Modularity: 9/10** — Clean separation: SKILL.md (workflow + checklist) + examples.md (detailed patterns). Self-contained — no external tool dependencies. Only Read/Grep/Glob/Bash needed.
- **Safety: 8/10** — Good context-sensitive scoping (skip test/example/docs). Rationalizations-to-Reject prevent common shortcuts. Missing: no `disable-model-invocation` (could trigger on any code review).

## Strengths

1. **Fail-open vs fail-secure distinction is the core insight.** `env.get(X) or 'default'` (CRITICAL) vs `env['KEY']` (safe crash) — this single distinction catches the majority of insecure defaults. Simple, memorable, actionable.

2. **Examples.md is best-in-class reference material.** 410 lines with vulnerable/secure pairs across Python, JavaScript, Ruby, Java for all 6 categories. Each example has "Why vulnerable" explanation. This is exactly what CLAUDE.md guidelines mean by "behavioral guidance over reference dumps."

3. **Search → Verify → Confirm → Report workflow prevents false positives.** Not just pattern matching — the skill requires tracing code paths to verify production reachability. This is what separates it from grep.

4. **Rationalizations-to-Reject section is practical.** "It's just a development default" → "If it reaches production code, it's a finding." These 5 rationalizations capture real arguments auditors face.

5. **Tool restriction is smart.** Only Read/Grep/Glob/Bash allowed — no Write, no WebFetch. This is a read-only analysis skill that can't accidentally modify code.

## Weaknesses

1. **No framework-specific guidance.** Django's `SECRET_KEY`, Rails' `secret_key_base`, Spring's `spring.security` all have unique patterns. The skill is language-agnostic but could link to framework-specific checklists.

2. **No severity scoring framework.** "CRITICAL" is mentioned for fail-open, but there's no structured way to rank findings (CVSS-like scoring, exploitation difficulty, blast radius). All findings appear equally severe.

3. **No CI integration guidance.** This skill is manual — no mention of how to make it repeatable. Could reference Semgrep rules that automate some of these checks, or suggest creating .semgrepignore patterns.

## Kha nang tich hop

**VERY HIGH — universally applicable to any codebase.**
- Run on ANY project with env vars or config files
- Pairs with `semgrep-rule-creator` to automate detected patterns
- Pairs with `differential-review` for PR-level default checks
- Low barrier: needs only Read/Grep, no external tools

## Key Patterns Worth Adopting
1. **Vulnerable/Secure pairs** in examples — show both what's wrong AND what's right
2. **Context-sensitive scoping** — explicit list of what to skip (tests, docs, examples)
3. **Code path tracing** — don't just match patterns, verify production reachability
4. **Tool restriction in frontmatter** — read-only skills shouldn't have Write permission
5. **Rationalizations-to-Reject** — anticipate the "but..." arguments
