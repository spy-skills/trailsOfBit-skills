---
date: 2026-03-27
type: task-worklog
task: tob-uh3
title: "Tong quan + Xep hang - Catalog & Rank 28 plugins"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [overview, catalog, ranking, analysis]
---

# Tong quan + Xep hang — Detailed Design

## 1. Objective
Format the complete 28-plugin catalog from Explore agent data into a standardized analysis file. Include applicability rankings (1-5) across 5 criteria, and a 3-phase learning roadmap.

## 2. Scope
**In-scope:**
- Format 28 plugins into table with: name, category, line count, complexity, applicability score
- Rank by 5 criteria: practical applicability, knowledge depth, OMC/spy-skills integration potential, independence, learning curve
- Create 3-phase learning roadmap (Foundation → Intermediate → Advanced)

**Out-of-scope:**
- Deep analysis of individual plugins (separate deep dive tasks)
- Actually installing or testing any plugins
- Modifying any plugin code

## 3. Input / Output
**Input:**
- Explore agent catalog data (in conversation context from previous session)
- Plugin metadata from: `plugins/*/.claude-plugin/plugin.json`
- SKILL.md line counts from: `find plugins/ -name "SKILL.md" | xargs wc -l`

**Output:**
- `self-explores/learn/tob-overview/analysis.md` — main analysis file

## 4. Dependencies
- None (all data already available)

## 5. Flow xu ly

### Step 1: Collect line counts (~5 min)
```bash
find plugins/ -name "SKILL.md" -type f | xargs wc -l | sort -rn
```
**Verify:** Output shows line counts for all 55 SKILL.md files

### Step 2: Create output directory (~1 min)
```bash
mkdir -p self-explores/learn/tob-overview
```

### Step 3: Write analysis.md with catalog table (~15 min)
Format into analysis.md with sections:
- Overview table (28 plugins, 10 categories)
- Ranking table (5 criteria x 28 plugins)
- 3-phase learning roadmap
- Quick reference card

**Verify:** File exists, contains 28 rows in overview table

### Step 4: Cross-check with README (~5 min)
Compare catalog against README.md plugin table to ensure nothing missed.
**Verify:** 28 plugins accounted for, categories match README

## 6. Edge Cases & Error Handling
| Case | Trigger | Expected | Recovery |
|------|---------|----------|----------|
| Missing plugin.json | Plugin dir exists but no metadata | Skip, note in analysis | Flag as incomplete |
| New plugins since scan | git log shows recent additions | Re-scan if needed | Compare with README |

## 7. Acceptance Criteria
- **Happy 1:** Given analysis.md exists When opened Then contains table with 28 plugins across 10 categories
- **Happy 2:** Given ranking section When read Then each of top 10 plugins has reasoning paragraph
- **Negative:** Given a plugin in README When not in analysis Then analysis is incomplete (must have all 28)

## 8. Technical Notes
- Use Explore agent data as primary source (already validated)
- Scoring: 1=niche/internal only, 2=specialized, 3=moderate, 4=broad, 5=universal
- Categories from README: Code Auditing(10), Smart Contract(2), Verification(3), Development(7), Malware(1), RevEng(1), Mobile(1), Team(1), Tooling(1), Infra(1)

## 9. Risks
- Explore agent data may be slightly stale → mitigate by checking git log for recent commits
- Ranking is subjective → mitigate by documenting criteria weights

## Worklog
*(Chua bat dau)*
