---
name: itensor-api-and-scripting
description: Use this skill for ITensor C++ API navigation across tensor/index classes, decomposition/solver entry points, and utility/config surfaces.
---

# itensor: API and Scripting

## Scope
- Navigate core C++ API surfaces for tensors, indices, decompositions, and contractions.
- Identify the right utility/configuration APIs (`Args`, input parsing, error handling, parallel helpers).
- Route algorithm workflow usage to simulation/modeling skills when questions are not API-level.

## Route the request
- Tensor object semantics (`ITensor`, priming/tags, element access) -> this skill.
- Index and QN/tag behavior (`Index`, `TagSet`, prime levels) -> this skill.
- Decompositions/contractions (`svd`, `denmatDecomp`, `contract`, `eigen`, `diagHermitian`) -> this skill.
- DMRG or full workflow usage questions -> `itensor-simulation-workflows`.
- Build or linking errors -> `itensor-build-and-install`.

## Primary documentation references
- `itensor/all.h`
- `itensor/core.h`
- `itensor/itensor.h`
- `itensor/index.h`
- `itensor/decomp.h`
- `itensor/tensor/contract.h`
- `itensor/iterativesolvers.h`
- `itensor/util/args.h`
- `itensor/util/error.h`
- `itensor/util/input.h`

## Workflow
- Start from `itensor/all.h` / `itensor/core.h` to identify high-level include surfaces.
- Inspect `itensor/itensor.h` and `itensor/index.h` for object-level APIs.
- Inspect `itensor/decomp.h`, `itensor/tensor/contract.h`, and `itensor/iterativesolvers.h` for numerical kernels.
- Inspect utility surfaces (`itensor/util/args.h`, `itensor/util/error.h`, `itensor/util/input.h`) for configuration and diagnostics.
- If details are missing, inspect `references/doc_map.md`, then `references/source_map.md`.

## Tutorials and examples
- `tutorial`
- `sample`

## Test references
- `unittest/itensor_test.cc`
- `unittest/index_test.cc`
- `unittest/decomp_test.cc`
- `unittest/contract_test.cc`
- `unittest/iterativesolvers_test.cc`

## Optional deeper inspection
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `itensor/itensor.h`
- `itensor/index.h`
- `itensor/decomp.h`
- `itensor/tensor/contract.h`
- `itensor/iterativesolvers.h`
- `itensor/util/args.h`
- `itensor/util/error.h`
- `itensor/util/input.h`
- Prefer targeted source search (for example: `rg -n "class ITensor|class Index|svd\(|denmatDecomp|contract\(|davidson|Args" itensor unittest tutorial sample`).
