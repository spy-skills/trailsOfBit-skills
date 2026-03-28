# Deep Dive: ask-questions-if-underspecified

## Score: 8/10

### Sub-scores
- **Completeness: 7/10** — Covers the core workflow well (decide → ask → pause → confirm). Has When/When-NOT, anti-patterns. Missing: Rationalizations-to-Reject section, no examples of bad vs good question sets.
- **Usability: 9/10** — Excellent progressive disclosure in 85 lines. Question templates are immediately actionable. The `defaults` fast-path and `1a 2b 3c` compact reply format are brilliant UX.
- **Modularity: 8/10** — Fully self-contained, no dependencies. Can be adopted in any project without modification. Could benefit from a references/examples.md with real-world scenarios.
- **Safety: 9/10** — "Pause before acting" rule prevents premature execution. Explicit "state assumptions → get confirmation" flow for proceed-without-answers case.

## Strengths

1. **Compact reply format (`1b 2a 3c`) is genius UX.** Reduces friction from paragraphs of answers to a single line. Most skills force verbose responses; this respects user time.

2. **Decision tree is crisp and actionable.** The 6 underspecification checks (objective, done criteria, scope, constraints, environment, safety) cover the critical dimensions. Not too many, not too few.

3. **"Pause before acting" with discovery allowance.** Allows low-risk reads (inspect repo, read configs) while blocking commits to a direction. This nuance is missing from most "ask first" approaches.

4. **Fast-path `defaults` option.** Users who trust the tool can shortcut with a single word. Power users and beginners both served.

5. **Anti-patterns section is on point.** "Don't ask questions you can answer with a quick read" prevents the annoying behavior of asking about things that are in the README.

## Weaknesses

1. **No concrete examples.** The skill has templates but no full worked example showing: "User said X → skill detected underspecification → asked these 3 questions → got answers → restated → proceeded." A single real example would make this 10x more learnable.

2. **No Rationalizations-to-Reject section.** Common shortcuts like "I'll just guess and fix later" or "The user probably means the obvious interpretation" are not explicitly called out. This is a CLAUDE.md requirement for security skills and a ToB house standard.

3. **Description is too terse.** "Clarify requirements before implementing. Use when serious doubts arise." — This undersells the skill. Better: "Asks 1-5 targeted clarifying questions with multiple-choice options before implementing underspecified requests. Prevents wrong work by detecting ambiguous objectives, scope, constraints, and acceptance criteria."

4. **No guidance on question ordering.** Should you ask scope first or objective first? The skill says "1-5 questions" but doesn't prioritize. Roadmap principle says "eliminate whole branches of work first" — could be more explicit.

5. **Missing `disable-model-invocation` consideration.** This skill triggers on ambiguity detection — but how aggressively? No guidance on threshold. Could fire too often on clear requests or too rarely on subtle ambiguity.

## Kha nang tich hop

**VERY HIGH — immediately adoptable.** This is a meta-skill that improves ALL other workflows.

**Integration opportunities:**
- **Embed in `/viec tao`:** Before creating tasks from user input, run underspecification check
- **Embed in OMC analyst agent:** Analyst should use this before writing requirements
- **Pair with audit-context-building:** Before starting an audit, clarify scope/constraints
- **Add to CLAUDE.md as default behavior:** "When request is ambiguous, follow ask-questions-if-underspecified workflow"

## Ghi chu ky thuat

### Why 1-5 questions, not more?
Cognitive load research: beyond 5 questions, users start skipping or giving low-quality answers. The skill optimizes for answer quality over coverage.

### Why multiple-choice over open-ended?
Multiple-choice eliminates ambiguity in answers themselves. "What scope?" invites a paragraph. "Scope? a) Minimal b) Refactor c) Full rewrite" gets a letter.

### Key Patterns Worth Adopting
1. **Compact reply format** — `1b 2a 3c` for multi-question responses
2. **Fast-path `defaults`** — Single word to accept all recommended choices
3. **Discovery-before-commitment** — Read configs/code but don't edit until answers arrive
4. **Bold recommended defaults** — Visual hierarchy guides users to sensible choices
5. **Restate before proceeding** — 1-3 sentence confirmation prevents misunderstanding
