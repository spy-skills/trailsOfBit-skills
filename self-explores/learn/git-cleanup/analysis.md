# Deep Dive: git-cleanup

## Score: 8/10

### Sub-scores
- **Completeness: 8/10** — 7 branch categories (SAFE_TO_DELETE, SQUASH_MERGED, SUPERSEDED, REMOTE_GONE, UNPUSHED_WORK, LOCAL_WORK, SYNCED_WITH_REMOTE). 2-gate confirmation workflow. Group-related-branches-first methodology. Squash-merge detection via PR history. Protected branch list. Worktree cleanup. 364 lines, self-contained. Missing: no Rationalizations-to-Reject section.
- **Usability: 8/10** — Detailed bash commands for every analysis step. "Group by prefix BEFORE categorize" is a key insight. Squash-merge force-delete guidance prevents the common "git -d failed, now what?" confusion. 2-gate confirmation prevents accidents.
- **Modularity: 7/10** — Fully self-contained (no reference files). This is both a strength (standalone) and weakness (364 lines in one file, could split analysis vs execution).
- **Safety: 10/10** — `disable-model-invocation: true` prevents accidental triggering. 2-gate confirmation (analysis → exact commands). Protected branches regex. AskUserQuestion required. "Never delete without explicit confirmation." Best safety posture in the repo.

## Strengths
1. **`disable-model-invocation: true`** — Only runs when explicitly asked, preventing accidental branch deletion
2. **Group-related-branches-first** — Prevents analyzing superseded branches individually (saves time + better recommendations)
3. **Squash-merge aware** — Knows `git -d` fails for squash-merged branches and plans `git -D` upfront
4. **2-gate confirmation** — Analysis review → exact commands review → execute
5. **Protected branch regex** — main/master/develop/release never touched

## Weaknesses
1. **No Rationalizations-to-Reject** — "I'll just delete all gone branches" should be rejected
2. **Self-contained 364L could be split** — Analysis logic vs execution commands
3. **No worktree dirty-state detection** mentioned in quick read

## Kha nang tich hop: MEDIUM — useful but narrow (local branch cleanup only)
## Key Patterns: disable-model-invocation for destructive skills, 2-gate confirmation, group-before-categorize
