# Deep Dive: building-secure-contracts

## Score: 8/10

### Sub-scores
- **Completeness: 9/10** — 11 sub-skills covering entire smart contract security lifecycle. 6 blockchain-specific vulnerability scanners (Solana, Algorand, Cairo, Cosmos, TON, Substrate). 3 guidance skills (audit-prep, guidelines-advisor, secure-workflow). 2 analysis skills (token-integration, code-maturity). Total 3,635 lines across all sub-skills. Each scanner covers 3-11 vulnerability patterns per chain.
- **Usability: 7/10** — Individual skills are well-structured. But 11 sub-skills create navigation overhead — which one to use? No routing decision tree across all sub-skills. Each scanner is independent and actionable within its chain.
- **Modularity: 9/10** — Each sub-skill is fully independent. Can install/use blockchain-specific scanners without the others. Clean separation: scanners (detection) vs advisors (guidance) vs assessors (scoring).
- **Safety: 8/10** — Scanners are read-only analysis. Static analysis tool integration (Slither, Echidna). But no Rationalizations-to-Reject across the plugin as a whole.

## Top 3 Sub-Skills (Deep Analysis)

### 1. audit-prep-assistant (409L) — Score: 8/10
**Purpose:** Pre-audit preparation checklist (1-2 weeks before audit).
**Workflow:** Set review goals → Run static analysis (Slither/Semgrep/CodeQL) → Increase test coverage → Remove dead code → Generate documentation.
**Strengths:** Multi-language support (Solidity, Rust, Go). Practical — fixes easy issues before expensive human audit. Documentation generation (flowcharts, user stories).
**Weakness:** No estimate of preparation time. No guidance on prioritizing which issues to fix vs document.

### 2. token-integration-analyzer (362L) — Score: 9/10
**Purpose:** Analyze token implementations and integrations for 20+ weird patterns (fee-on-transfer, rebasing, pausable, blacklisted, etc.).
**Strengths:** Context-aware — distinguishes "building a token" from "integrating a token." 20+ weird token patterns is the most comprehensive catalog I've seen. On-chain scarcity analysis.
**Weakness:** ERC20/721/1155 focused — doesn't cover newer standards (ERC-4626 vaults, ERC-6551 token-bound accounts).

### 3. solana-vulnerability-scanner (389L) — Score: 8/10
**Purpose:** Scan for 6 critical Solana/Anchor vulnerabilities (arbitrary CPI, improper PDA validation, missing signer checks, sysvar spoofing, etc.).
**Strengths:** Anchor-aware (handles both raw Solana and Anchor programs). Each vulnerability has: detection pattern + code example + fix.
**Weakness:** Only 6 patterns — Solana attack surface is broader (flash loan attacks, sandwich attacks on DEXs not covered).

## Remaining 8 Sub-Skills (Summary)

| Sub-Skill | Lines | Chains | Vuln Patterns | Key Insight |
|-----------|-------|--------|---------------|-------------|
| algorand-scanner | 284 | TEAL/PyTeal | 11 patterns | Rekeying attacks unique to Algorand |
| cairo-scanner | 329 | StarkNet | 6 patterns | felt252 overflow is Cairo-specific |
| cosmos-scanner | 334 | Cosmos SDK | 9 patterns | Non-determinism = consensus failure |
| ton-scanner | 388 | FunC/Tact | 3 patterns | Integer-as-boolean misuse |
| substrate-scanner | 298 | Polkadot | 7 patterns | Incorrect weights = DoS |
| guidelines-advisor | 252 | Multi-chain | N/A | Architecture review + dependency audit |
| secure-workflow | 161 | Multi-chain | N/A | 5-step dev workflow with Slither |
| code-maturity | 218 | Multi-chain | 9 categories | Scorecard: arithmetic, access, testing, etc. |

## Kha nang tich hop

**HIGH for blockchain/DeFi projects, LOW for general development.**
- Chain-specific scanners are immediately deployable on matching codebases
- audit-prep-assistant is universally useful (not blockchain-specific)
- token-integration-analyzer is essential for any DeFi protocol integration
- code-maturity-assessor could be adapted for non-blockchain codebases

## Key Patterns Worth Adopting
1. **Chain-specific vulnerability catalogs** — Don't generalize; each blockchain has unique attack surfaces
2. **"Weird token" pattern catalog** — 20+ edge cases for token integration
3. **Pre-audit preparation workflow** — Fix easy issues before expensive human review
4. **9-category maturity scorecard** — Systematic code quality assessment framework
