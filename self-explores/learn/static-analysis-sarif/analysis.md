# Deep Dive: static-analysis/sarif-parsing

## Score: 8/10

### Sub-scores
- **Completeness: 9/10** — Full SARIF 2.1.0 structure reference. 3 strategies (jq quick analysis, Python pysarif, sarif-tools). Fingerprinting explanation (why it matters for baseline comparison). Tool selection guide (6 tools across languages). CI/CD integration patterns. Streaming for 100MB+ files. Deduplication. jq-queries.md reference + sarif_helpers.py utility. 479 lines.
- **Usability: 8/10** — jq one-liners are copy-paste ready. SARIF structure diagram is immediately useful. Tool selection table routes to right tool. But 479 lines is near the 500-line limit; could use more reference file splitting.
- **Modularity: 7/10** — jq-queries.md reference + sarif_helpers.py script. But most content is in SKILL.md itself. Could benefit from splitting strategies into separate references.
- **Safety: 7/10** — Read-only tools (Bash/Read/Glob/Grep). No data modification. Missing: no warning about trusting SARIF tool output blindly (tools can produce false positives).

## Strengths
1. **Fingerprinting explanation is unique** — Most SARIF guides skip this; crucial for CI/CD regression detection
2. **jq one-liners are immediately actionable** — 8+ ready-to-use queries covering 90% of use cases
3. **Streaming for 100MB+ files** — Real-world guidance for enterprise-scale SARIF output
4. **SARIF structure diagram** — Visual hierarchy makes format instantly understandable
5. **6-tool selection guide** — jq/pysarif/sarif-tools/SARIF SDK/.NET/Go/JS coverage

## Weaknesses
1. **479 lines in one file** — Near limit, could split jq queries and Python strategies into references
2. **No Rationalizations-to-Reject** — "Just grep the SARIF file" should be rejected
3. **No validation guidance** — How to check if SARIF file is well-formed before processing

## Kha nang tich hop: HIGH — essential for CI/CD security pipeline integration
## Key Patterns: Fingerprinting for baseline comparison, jq one-liner library, streaming for large files
