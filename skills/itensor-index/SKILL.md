---
name: itensor-index
description: Use this index to route ITensor requests to the correct topic skill with a docs-first, source-second escalation policy.
---

# itensor Skills Index

## Route the request
- Step 1: classify the user request into one topic skill below.
- Step 2: answer docs-first from that skill's primary references.
- Step 3: escalate to that skill's `references/doc_map.md` only if needed.
- Step 4: escalate to `references/source_map.md` and concrete source files only for unresolved implementation details.

## Generated topic skills
- `itensor-build-and-install`: compiler/options setup, library build, sample build, external project linking
- `itensor-inputs-and-modeling`: tutorial progression, model/input design, finite-T input files
- `itensor-simulation-workflows`: MPS/MPO construction, DMRG/time-evolution workflows, validation checks
- `itensor-parallel-hpc`: OpenMP/MPI setup and scaling/reproducibility checks
- `itensor-api-and-scripting`: core tensor/index/decomposition APIs and utility surfaces
- `itensor-advanced-topics`: consolidated low-frequency topics (release/checklist notes and sparse advanced docs)
- `itensor-sci-skills-generator`: skills generation/enrichment workflow and rubric usage
- `itensor-readme`: top-level package orientation and citation routing

## Fast simulation bootstrap
1. Build once from repo root: `cp options.mk.sample options.mk && make`.
2. Run baseline DMRG: `cd sample && make dmrg && ./dmrg`.
3. Run table-driven input workflow: `./dmrg_table inputfile_dmrg_table`.
4. Run finite-T starter: `cd ../tutorial/finiteT && make app=ancilla && ./ancilla inputfile_ancilla`.

## Validation checkpoints
- `dmrg` built from `sample/dmrg.cc` prints initial/final energies.
- `dmrg_table` built from `sample/dmrg_table.cc` accepts `inputfile_dmrg_table` without key/group parse errors.
- `ancilla` built from `tutorial/finiteT/ancilla.cc` writes `en.dat` and `sus.dat`.

## Documentation-first inputs
- `README.md`
- `INSTALL.md`
- `tutorial`
- `sample`
- `Checklists.txt`

## Tutorials and examples roots
- `tutorial`
- `sample`

## Test roots for behavior checks
- `unittest`

## Escalate only when needed
- Keep answers grounded in topic docs first.
- Use examples/tutorials as minimal reproductions.
- Use tests as behavior references.
- Inspect source only when docs do not settle behavior.

## Source directories for deeper inspection
- `itensor`
- `tools`
- `tutorial`
