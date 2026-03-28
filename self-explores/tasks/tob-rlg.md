---
date: 2026-03-27
type: task-worklog
task: tob-rlg
title: "Deep Dive: second-opinion (4/5)"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [deep-dive, multi-llm, code-review]
---

# Deep Dive: second-opinion — Detailed Design

## 1. Objective
Analyze second-opinion (294L): parallel Codex+Gemini code reviews, 3 review scopes, structured JSON output, bundled codex-mcp-server.

## 3. Input / Output
**Input:** `plugins/second-opinion/skills/second-opinion/SKILL.md` (294L) + references/codex-invocation.md, gemini-invocation.md
**Output:** `self-explores/learn/second-opinion/analysis.md`

## 5. Steps: Read SKILL.md (~6min) → Read 2 invocation refs (~3min) → Score (~10min) → Write (~10min)
## 7. AC: analysis.md with Score 1-10, note tool availability (Codex/Gemini CLI). ~20 min.

## Worklog
*(Chua bat dau)*
