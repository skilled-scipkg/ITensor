---
name: itensor-advanced-topics
description: Use this skill for low-frequency or maintainer-side ITensor topics that do not justify standalone skills.
---

# itensor: Advanced Topics

## Scope
- Consolidated home for low-signal topics that were previously single-doc skills.
- Covers release/checklist notes and sparse analysis/output guidance.

## Route the request
- Release tagging and release-process checklist questions -> use this skill.
- Sparse output-file interpretation questions (for example finite-T `en.dat`/`sus.dat`) -> start here, then route to `itensor-simulation-workflows` for full workflow context.
- API-level post-processing or tensor export internals -> route to `itensor-api-and-scripting`.

## Primary documentation references
- `Checklists.txt`
- `V3_ROADMAP`
- `tutorial/finiteT/INSTRUCTIONS`

## Workflow
- Start with docs above.
- If details are missing, inspect `references/doc_map.md`.
- If behavior remains ambiguous, inspect `references/source_map.md` and then targeted source files.

## Tutorials and examples
- `tutorial/finiteT`
- `sample`

## Test references
- `unittest`

## Optional deeper inspection
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `tutorial/finiteT/ancilla.cc`
- `tutorial/finiteT/metts.cc`
- `itensor/util/input.h`
- `itensor/util/readwrite.h`
- `itensor/util/h5/base_public.hpp`
- `itensor/util/h5/base.hpp`
- `itensor/util/h5/base.cc`
- Prefer targeted source search (for example: `rg -n "en\.dat|sus\.dat|readwrite|h5|InputGroup" itensor tutorial sample`).
