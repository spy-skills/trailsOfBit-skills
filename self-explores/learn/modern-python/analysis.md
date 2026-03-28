# Deep Dive: modern-python

## Score: 8/10

### Sub-scores
- **Completeness: 8/10** — Covers full Python toolchain: uv (package mgmt), ruff (lint+format), ty (type checking), pytest (testing), prek (pre-commit). Has When/When-NOT, Anti-Patterns table (11 entries), Decision Tree, Migration Guide (4 paths), Best Practices Checklist, Quick Reference. 9 reference files covering every aspect. Missing: no Rationalizations-to-Reject section.
- **Usability: 9/10** — Decision tree routes to exact use case (script vs project vs package vs migration). Quick Start is 6 commands. Anti-patterns table is excellent — instantly shows "use X instead of Y". Progressive disclosure: 333L SKILL.md → 9 reference files.
- **Modularity: 9/10** — Clean reference split (pyproject, uv-commands, ruff-config, testing, PEP723, prek, security, dependabot, migration-checklist). Has hooks/ directory for Claude Code integration. Each reference is independently useful.
- **Safety: 6/10** — Security tools section is strong (shellcheck, detect-secrets, actionlint, zizmor, pip-audit, Dependabot). But no explicit warning about `uv run` executing arbitrary code, no supply chain attack guidance beyond pip-audit.

## Strengths

1. **Anti-patterns table is immediately actionable.** 11 "Avoid → Use Instead" pairs that save hours of debugging. `[tool.ty]` python-version → `[tool.ty.environment]` python-version is the kind of gotcha that wastes 30 minutes when you hit it.

2. **uv replaces 5 tools in one.** pip, virtualenv, pip-tools, pipx, pyenv → uv. The skill makes this clear upfront and consistently uses `uv add` / `uv run` throughout, never falling back to pip.

3. **PEP 723 for standalone scripts is a unique value-add.** Most Python guides ignore scripts-with-dependencies. The dedicated reference for inline metadata (`# /// script`) fills a real gap. This is exactly what spy-skills uses for beads/dolt scripts.

4. **Security tooling section goes beyond linting.** shellcheck, detect-secrets, actionlint, zizmor, pip-audit, Dependabot — this is a comprehensive security-first development setup, not just a coding style guide.

5. **4 migration paths are well-structured.** requirements.txt, setup.py/setup.cfg, flake8+black+isort, mypy/pyright — each with specific delete/add steps. Covers the realistic legacy scenarios.

## Weaknesses

1. **No Rationalizations-to-Reject.** Common pushbacks like "Poetry works fine for us", "mypy has better ecosystem", "We need Python 3.9 support" are not addressed. This is a ToB house standard requirement.

2. **ty is very new and may lack ecosystem support.** The skill recommends ty over mypy/pyright but ty (from Astral) was released recently. Many libraries don't have ty-compatible type stubs yet. Should note this limitation and suggest fallback to mypy for codebases with extensive type annotations.

3. **`select = ["ALL"]` for ruff is aggressive.** Enabling ALL rules then ignoring specific ones creates noisy first-run output on existing projects. Should differentiate between new projects (ALL is fine) and migrations (start with specific rule sets).

4. **No mention of uv workspace features.** For monorepos (common in larger projects), uv workspaces are important. The skill focuses on single-project setup.

## Kha nang tich hop

**VERY HIGH — directly applicable to current spy-skills setup.**
- All Python scripts in plugins/ should follow PEP 723 (CLAUDE.md already says this)
- `uv run` is already the standard for running plugin scripts
- Security tools (detect-secrets, pip-audit) directly useful for code auditing
- Migration paths useful when onboarding new plugins with legacy tooling

## Key Patterns Worth Adopting
1. **Anti-patterns table format** — "Avoid | Use Instead" is scannable and memorable
2. **Decision tree for use-case routing** — Script vs Project vs Package vs Migration
3. **PEP 723 inline metadata** — For standalone scripts with dependencies
4. **`uv run` as universal command prefix** — Never activate venvs manually
5. **dependency-groups (PEP 735)** — dev/test/docs groups instead of extras
