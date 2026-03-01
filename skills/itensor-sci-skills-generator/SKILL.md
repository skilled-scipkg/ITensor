---
name: itensor-sci-skills-generator
description: Use this skill to regenerate or enrich the ITensor `skills/` folder with docs-first routing and compact high-signal core playbooks.
---

# itensor: Sci Skills Generator

## High-Signal Playbook
### Route conditions
- Use this skill when the request is about generating, regenerating, or enriching `skills/` artifacts.
- Route domain physics/workflow questions to the corresponding ITensor topic skills after generation.
- Route build/runtime issues in generated examples back to `itensor-build-and-install`.

### Triage questions
- Is this a fresh generation, overwrite/regeneration, or pass-2/pass-3 enrichment run?
- Should generation be docs-only, or include source/test/tutorial maps?
- What are the docs/source roots and max skill count?
- Which skills are core and must include `High-Signal Playbook` sections?
- Are one-doc topics noisy enough to consolidate into `<package>-advanced-topics`?

### Canonical workflow
1. Dry-run the generator to inspect grouping behavior.
2. Generate with explicit roots/limits.
3. Validate required structure (`<package>-index`, `SKILL.md`, `references/doc_map.md`, `references/source_map.md`).
4. Enrich only core skills with compact playbooks (route conditions, triage, workflow, MWE, pitfalls, validation).
5. Consolidate many one-doc low-signal topics into `<package>-advanced-topics` when routing becomes noisy.
6. Re-validate docs-first routing and concrete source entry links after edits.

### Minimal working example
```bash
python sci-skills-generator/scripts/generate_skills_folder.py \
  --package-root . \
  --package-name itensor \
  --output-dir ./skills \
  --max-skills 30
```

```bash
python sci-skills-generator/scripts/generate_skills_folder.py \
  --package-root . \
  --package-name itensor \
  --docs-dirs . \
  --source-dirs itensor,tools \
  --max-skills 30 \
  --overwrite
```

### Pitfalls and fixes
- Using `docs_dirs='.'` can pull generator/template docs into topic skills; filter aggressively during enrichment.
- Extensionless docs (for example `sample/README`, `tutorial/*/INSTRUCTIONS`) may be under-grouped by automatic extraction.
- Regeneration with `--overwrite` can erase manual playbook edits; enrich after the final generation pass.
- Missing compile-memory artifacts should be treated as warnings; proceed with docs/source auditing from repository content.

### Convergence and validation checks
- Skill count stays within configured cap.
- Index skill routes clearly and docs-first.
- Each core skill has a compact `High-Signal Playbook` with all required subsections.
- Source escalation links in skills point to concrete implementation files, not generic placeholders.
- Any consolidation keeps routing discoverable and avoids dead skill references.

## Scope
- Deterministic generation and targeted enrichment of ITensor skills.
- Practical compile-pass workflows using rubric constraints and path-verified skill maps.

## Primary documentation references
- `sci-skills-generator/SKILL.md`
- `sci-skills-generator/references/generation-rubric.md`
- `sci-skills-generator/references/example-invocations.md`
- `skills/itensor-sci-skills-generator/references/doc_map.md`
- `skills/itensor-sci-skills-generator/references/source_map.md`

## Workflow
- Start from generator instructions and rubric.
- Use topic `SKILL.md` plus each skill's `references/doc_map.md` and `references/source_map.md` to prioritize and constrain edits.
- Keep generated skills docs-first; escalate to source only when docs/examples are insufficient.

## Tutorials and examples
- `sci-skills-generator/references/example-invocations.md`

## Test references
- `unittest`

## Optional deeper inspection
- `sci-skills-generator/scripts`
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `sci-skills-generator/scripts/generate_skills_folder.py`
- `skills/itensor-sci-skills-generator/references/doc_map.md`
- `skills/itensor-sci-skills-generator/references/source_map.md`
- `itensor/core.h`
- `itensor/itensor.h`
- `itensor/mps/dmrg.h`
- Prefer targeted source search (for example: `rg -n "TopicRule|DOC_EXTENSIONS|generate_skills_folder|MAX_" sci-skills-generator/scripts`).
