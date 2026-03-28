# Deep Dive: property-based-testing

## Score: 9/10

### Sub-scores
- **Completeness: 9/10** — Property catalog (10 properties with formulas), strength hierarchy (No Exception → Roundtrip), pattern detection triggers (7 code patterns), decision tree routing to 7 reference files, priority table, When/When-NOT, Red Flags (5), Rationalizations-to-Reject (6). 7 reference files cover every task scenario. Missing only concrete worked examples in SKILL.md.
- **Usability: 10/10** — 124 lines SKILL.md, near-perfect progressive disclosure. Decision tree routes to exactly the right reference file based on what you're doing. "Offer PBT as an option" approach (non-prescriptive) is exactly right. Property catalog table is scannable in 10 seconds.
- **Modularity: 10/10** — 7 independent reference files (generating, strategies, design, refactoring, reviewing, interpreting-failures, libraries). Each is self-contained and task-specific. No circular references. Decision tree is the only coupling.
- **Safety: 8/10** — Rationalizations-to-Reject section has 6 entries. Red Flags prevent over-application. "If user declines, write good example-based tests without further prompting" prevents pushy behavior. Missing: no explicit warning about PBT flakiness in CI environments.

## Strengths

1. **Property strength hierarchy is the core teaching.** `No Exception → Type Preservation → Invariant → Idempotence → Roundtrip` — this single line tells developers exactly how to level up their tests. Most PBT guides dump all properties equally; this ranks them.

2. **Pattern-to-property mapping is immediately actionable.** See `encode/decode` → apply Roundtrip. See `normalize` → apply Idempotence. No guesswork. The priority table (HIGH/MEDIUM/LOW) prevents wasted effort on low-value patterns.

3. **Decision tree routing is best-in-class navigation.** 6 task scenarios → 6 specific reference files. No ambiguity about which doc to read. This is exactly what CLAUDE.md means by "progressive disclosure."

4. **Non-prescriptive suggestion pattern.** "Offer PBT as an option" with fallback to example-based tests. This respects user autonomy while still surfacing the opportunity. The two-tier approach (suggest vs direct based on existing codebase usage) is nuanced.

5. **Smart contract coverage (Echidna/Medusa) bridges two domains.** Most PBT guides are pure software engineering; this one explicitly includes smart contract state invariants and references Echidna/Medusa in libraries.md. Unique cross-domain value.

## Weaknesses

1. **No worked examples in SKILL.md itself.** The property catalog has formulas (`decode(encode(x)) == x`) but no concrete code. A 5-line Python Hypothesis example would make it 10x more tangible for newcomers.

2. **No CI flakiness guidance.** PBT with random seeds can produce non-deterministic failures. No mention of `@settings(database=...)`, `@seed`, or `--hypothesis-seed` for reproducibility in CI pipelines.

3. **libraries.md may become outdated.** Library versions and API recommendations change frequently. No mention of how to verify current compatibility or when the list was last updated.

## Kha nang tich hop

**VERY HIGH — universally applicable.**
- Any project with serialization (JSON APIs, protobuf, etc.)
- Any project with validators/normalizers
- Smart contract auditing (Echidna/Medusa integration)
- Pairs perfectly with `semgrep-rule-creator` (find patterns to test → generate PBT tests)
- Can be triggered automatically during code review via pattern detection

## Key Patterns Worth Adopting
1. **Property strength hierarchy** — Rank testing approaches from weak to strong
2. **Pattern-to-action mapping table** — "When you see X → do Y" format
3. **Decision tree routing** — Route to exact reference file based on current task
4. **Non-prescriptive suggestion** — "Offer as option, respect decline"
5. **Rationalizations with counter-arguments** — Not just "don't do X" but "why X is wrong"
