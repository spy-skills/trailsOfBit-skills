---
date: 2026-03-27
type: task-worklog
task: tob-6v2
title: "Review & Notion - Tong hop tat ca"
status: open
detailed_at: 2026-03-27
detail_score: ready-for-dev
tags: [review, notion, trello, tracking, summary]
---

# Review & Notion — Detailed Design

## 1. Objective
Synthesize completed deep dive analyses into final summary. Create daily log, push to Notion (Experiments > Skills > 17_trailsOfBit-security) and Trello. Partial review OK.

## 2. Scope
**In-scope:** Aggregate scores from completed deep dives, create daily log, push Notion + Trello
**Out-of-scope:** Re-analyzing skills, waiting for ALL deep dives

## 3. Input / Output
**Input:** self-explores/learn/*/analysis.md (whatever exists), bd stats, bd list --status=done
**Output:** self-explores/daily/YYYY-MM-DD.md, Notion page, Trello cards

## 4. Dependencies
- tob-uh3 (overview must exist for baseline)

## 5. Flow xu ly
### Step 1: Collect completed analyses (~5 min)
ls self-explores/learn/*/analysis.md + bd stats
### Step 2: Aggregate into summary table (~10 min)
Extract scores, strengths, weaknesses from each analysis.md
### Step 3: Create daily log (~5 min)
Write self-explores/daily/YYYY-MM-DD.md
### Step 4: Push Notion (~5 min)
Search for Experiments page, create sub-page. Fallback: local only.
### Step 5: Push Trello (~5 min)
Find/create Tracking list, add cards. Fallback: local only.

## 6. Edge Cases
| Case | Trigger | Recovery |
|------|---------|----------|
| No deep dives done | 0 analysis files | Create review with overview only |
| Notion MCP down | API error | Save locally, log warning |
| Trello MCP down | API error | Save locally, log warning |

## 7. Acceptance Criteria
- **Happy 1:** Daily log exists with entries for completed deep dives
- **Happy 2:** Notion page created (or fallback logged)
- **Negative:** MCP unavailable → local save succeeds, warning logged

## Worklog
*(Chua bat dau)*
