# itensor source map: Sci Skills Generator

Generated from source roots:
- `sci-skills-generator`
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `generate_skills_folder`
- `TopicRule`
- `DOC_EXTENSIONS`
- `SOURCE_EXTENSIONS`
- `--max-skills`
- `docs_dirs`
- `source_dirs`
- `overwrite`

## Fast source navigation
- `rg -n "TopicRule|DOC_EXTENSIONS|SOURCE_EXTENSIONS|MAX_|TOPIC_RULES" sci-skills-generator/scripts/generate_skills_folder.py`
- `rg -n "--max-skills|--docs-dirs|--source-dirs|--overwrite" sci-skills-generator/scripts/generate_skills_folder.py`
- `rg -n "^def (_find_docs_dirs|_find_source_dirs|_collect_doc_records|_collect_source_records|_render_topic_skill|_render_doc_map|_render_source_map|generate)" sci-skills-generator/scripts/generate_skills_folder.py`

## Suggested source entry points
- `sci-skills-generator/scripts/generate_skills_folder.py` | generator grouping logic and output writers
- `sci-skills-generator/SKILL.md` | generation and enrichment workflow contract
- `sci-skills-generator/references/generation-rubric.md` | quality rubric for grouping/playbooks/consolidation
- `sci-skills-generator/references/example-invocations.md` | invocation patterns for deterministic regeneration and overwrite passes
- `itensor/core.h` | representative source anchor when generated skills escalate from docs to code
- `itensor/mps/dmrg.h` | representative high-impact algorithm entry used in enriched ITensor skills
