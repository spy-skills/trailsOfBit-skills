---
date: 2026-03-27
type: task-worklog
task: tob-r3u
title: "Deep Dive: differential-review (5/5)"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [deep-dive, security, code-review, git]
---

# Deep Dive: differential-review — Detailed Design

## 1. Objective
Analyze differential-review (220L): risk-first classification, blast radius estimation, git blame regression detection, 3-tier codebase strategy.

## 2. Scope
**In-scope:** Read SKILL.md + methodology.md + adversarial.md + reporting.md + patterns.md, score 1-10
**Out-of-scope:** Running reviews, modifying code

## 3. Input / Output
**Input:** `plugins/differential-review/skills/differential-review/SKILL.md` (220L) + 4 reference files
**Output:** `self-explores/learn/differential-review/analysis.md`

## 5. Flow xu ly
### Step 1: Read SKILL.md (~5 min) — risk classification HIGH/MEDIUM/LOW, DEEP/FOCUSED/SURGICAL strategies
### Step 2: Read 4 references (~5 min) — methodology, adversarial thinking, reporting format, patterns
### Step 3: Score (~10 min) ### Step 4: Write analysis (~10 min)

## 7. Acceptance Criteria
- analysis.md exists with Score 1-10, >= 3 strengths/weaknesses

## 8. Technical Notes
Has commands/. Git blame on removed security code. Mandatory markdown report. ~25 min.

## Worklog
*(Chua bat dau)*
