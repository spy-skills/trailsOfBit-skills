# Deep Dive: gh-cli

## Score: 7/10

### Sub-scores
- **Completeness: 7/10** — Covers: URL interception pattern (WebFetch/curl → gh), clone-to-TMPDIR, Explore agent delegation, quick start commands, replacement table. 6 reference files (PRs, Issues, Repos, API, Releases, Actions). Has hooks/ for URL interception. Missing: Rationalizations-to-Reject, no SessionEnd hook implementation shown, no error handling guidance.
- **Usability: 9/10** — 100 lines, extremely concise. "Instead of → Use" table is the fastest possible learning format. Quick Start covers 5 most common operations in 10 lines. Clone pattern is immediately copy-paste usable.
- **Modularity: 8/10** — Clean split: SKILL.md (quick reference) → 6 topic-specific references. Read-only tool restriction (Bash/Read/Glob/Grep). Has hooks/ for automated URL interception.
- **Safety: 5/10** — No Rationalizations. No warning about token scope (gh auth provides full repo access). No rate limit monitoring. No private repo data leakage warning (cloned content persists until session end).

## Strengths
1. **"Instead of → Use" replacement table** — 7 rows covering every GitHub URL pattern
2. **Clone-to-TMPDIR with Explore agent** — Correct architecture: clone once, explore with agent
3. **100 lines for complete coverage** — Most efficient skill in the entire repo

## Weaknesses
1. **No security warnings** — Token scope, private repo data persistence, rate limit exhaustion
2. **No Rationalizations-to-Reject** — "I'll just use curl with a token" should be rejected
3. **SessionEnd hook cleanup not shown** — Referenced but implementation not in SKILL.md

## Kha nang tich hop: HIGH — daily driver for any GitHub interaction
## Key Patterns: Replacement table format, clone-to-TMPDIR, agent delegation for exploration
