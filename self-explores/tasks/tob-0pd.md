---
date: 2026-03-27
type: task-worklog
task: tob-0pd
title: "Deep Dive: yara-authoring (4/5)"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [deep-dive, malware, yara, detection-rules]
---

# Deep Dive: yara-authoring — Detailed Design

## 1. Objective
Analyze yara-authoring (645L — longest skill): YARA-X targeting, string quality decision tree, 16 rationalizations-to-reject, bundled scripts.

## 3. Input / Output
**Input:** `plugins/yara-authoring/skills/yara-rule-authoring/SKILL.md` (645L) + references/style-guide.md, performance.md, strings.md, testing.md, crx-module.md, dex-module.md + scripts/yara_lint.py, atom_analyzer.py + examples/
**Output:** `self-explores/learn/yara-authoring/analysis.md`

## 5. Steps: Read SKILL.md in chunks (~12min) → Read 6 refs + scan scripts + examples (~10min) → Score (~10min) → Write (~10min)
## 7. AC: analysis.md with Score 1-10, >= 3 strengths/weaknesses. ~40 min.
## 8. Notes: Read SKILL.md with offset/limit (645 lines). FP investigation flowchart. 5 attributed example rules.

## Worklog
*(Chua bat dau)*
