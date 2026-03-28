# Deep Dive: yara-authoring

## Score: 9/10

### Sub-scores
- **Completeness: 10/10** — Longest skill (645L). 5 core principles. 7-step workflow. 8 platform-specific guides (PE, Mach-O, JS, npm, Office, VS Code, Chrome crx, Android dex). Common Mistakes table. Performance optimization. 16 Rationalizations-to-Reject. FP investigation flowchart. 6 reference files + 1 workflow + 2 bundled Python scripts (yara_lint.py, atom_analyzer.py) + 5 attributed example rules. Quality checklist (11 items). String quality decision tree.
- **Usability: 8/10** — Despite 645 lines, well-organized with clear sections. Platform consideration table routes quickly. JavaScript detection decision tree is excellent. Quality checklist is comprehensive. But sheer length means users need to know which section to read.
- **Modularity: 10/10** — Best reference structure in repo: 6 topic references (style-guide, performance, strings, testing, crx-module, dex-module) + 1 workflow (rule-development.md) + 2 scripts + 5 examples. Each component is independently useful.
- **Safety: 9/10** — "Test against goodware before deployment" as core principle. 16 rationalizations prevent shortcuts. Bundled linting scripts enforce quality. FP investigation flowchart. Quality checklist as deployment gate.

## Strengths
1. **Atom theory is the killer insight** — "YARA extracts 4-byte subsequences for fast matching. Strings <4 bytes force slow bytecode verification." Most YARA guides skip this; it's the #1 performance determinant.
2. **Platform-specific guides for 8 platforms** — PE/Mach-O/JS/npm/Office/VSCode/Chrome/Android each with magic bytes, good strings, bad strings. Unique multi-platform coverage.
3. **16 Rationalizations-to-Reject** — Most comprehensive rejection list in the entire repo. Covers every shortcut an analyst might take.
4. **5 real attributed example rules** — Remcos, ProtonRAT, npm supply chain, JS obfuscation, Chrome extensions. Learn from real production rules.
5. **2 bundled validation scripts** — yara_lint.py (style) + atom_analyzer.py (string quality). Automated quality enforcement.

## Weaknesses
1. **645 lines is long** — Could split platform-specific content into separate references
2. **No CI/CD integration guidance** — How to run YARA rules in automated pipeline
3. **YARA-X is new** — Some users still on legacy YARA; migration section could be more prominent

## Kha nang tich hop: HIGH for malware/detection engineering, MEDIUM for general dev
## Key Patterns: Atom theory for performance, platform-specific detection tables, bundled validation scripts, 16 rationalizations, real attributed examples
