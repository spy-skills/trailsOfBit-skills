---
date: 2026-03-27
type: task-worklog
task: tob-tlg
title: "Deep Dive: static-analysis/semgrep (5/5)"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [deep-dive, security, semgrep, static-analysis]
---

# Deep Dive: static-analysis/semgrep — Detailed Design

## 1. Objective
Read and analyze the semgrep sub-skill of the static-analysis plugin (431 lines). Assess parallel scanner agents, triage workflow, ruleset integration, and produce a standardized analysis.

## 2. Scope
**In-scope:** Read SKILL.md + references + agents/, score 1-10, document strengths/weaknesses/integration
**Out-of-scope:** Installing Semgrep, running scans, modifying plugin code

## 3. Input / Output
**Input:** `plugins/static-analysis/skills/semgrep/SKILL.md` (431L) + rulesets.md, scanner-task-prompt.md, triage-task-prompt.md
**Output:** `self-explores/learn/static-analysis-semgrep/analysis.md`

## 4. Dependencies
- None

## 5. Flow xu ly

### Step 1: Read SKILL.md (~8 min)
Read plugins/static-analysis/skills/semgrep/SKILL.md. Focus: parallel agent architecture, Pro vs OSS detection, ruleset auto-inclusion.
**Verify:** Can explain scanner+triager agent flow in 3 sentences.

### Step 2: Read references (~5 min)
Read rulesets.md (ToB + 0xdea + Decurity rulesets), scanner-task-prompt.md, triage-task-prompt.md.
**Verify:** Understand how agents are prompted and what rulesets are included.

### Step 3: Score and analyze (~10 min)
Score: Completeness, Usability, Modularity, Safety (each 1-10).
**Verify:** 4 sub-scores with reasoning.

### Step 4: Write analysis.md (~10 min)
Write to self-explores/learn/static-analysis-semgrep/analysis.md
**Verify:** File exists, Score + 3 strengths + 3 weaknesses + integration notes.

## 6. Edge Cases
| Case | Trigger | Recovery |
|------|---------|----------|
| Large file | 431 lines | Read in 2 chunks if needed |
| Agent prompts complex | scanner/triager prompts | Summarize key instructions |

## 7. Acceptance Criteria
- **Happy 1:** analysis.md has Score 1-10 with reasoning
- **Happy 2:** Strengths has >= 3 items with explanations
- **Negative:** Notes Semgrep CLI dependency without failing

## 8. Technical Notes
Has agents/ with semgrep-scanner + semgrep-triager. Auto-detects Semgrep Pro for cross-file taint. Includes ToB + 0xdea + Decurity third-party rulesets. Mandatory user-approval gate before scan.

## 9. Risks
- Subjective scoring → consistent framework
- ~40 min estimate

## Worklog

### [bat-dau] Task claimed, auto-next BẬT
- Read SKILL.md (431 lines) — parallel subagent architecture, 6-step workflow with HARD GATE
- Read rulesets.md (163 lines) — 5-step ruleset selection algorithm, 13 GA languages, 10+ third-party sources
- Read scanner-task-prompt.md (102 lines) — template for parallel scanner Tasks
- Read triage-task-prompt.md (123 lines) — template + decision tree for FP classification

### [analysis] Score: 9/10
- Completeness: 10, Usability: 8, Modularity: 9, Safety: 10
- Top strengths: parallel subagent architecture, HARD GATE approval, mandatory third-party rulesets
- Top weaknesses: no .semgrepignore, no incremental scan, SARIF merge assumes uv

### [done] Analysis written
- Output: self-explores/learn/static-analysis-semgrep/analysis.md
- 5 strengths, 5 weaknesses, integration notes, 5 key patterns worth adopting
