---
name: itensor-readme
description: Use this skill for top-level ITensor orientation (what the package is, where to start, and citation routing).
---

# itensor: Readme

## High-Signal Playbook
### Route conditions
- Use this skill for initial orientation, package identity, and citation/start-here questions.
- Route all concrete build steps to `itensor-build-and-install`.
- Route runnable model/simulation workflows to `itensor-inputs-and-modeling` or `itensor-simulation-workflows`.

### Triage questions
- Is the request conceptual (what ITensor is) or operational (how to build/run)?
- Does the user need a first runnable example or citation guidance?
- Is the user asking about C++ library workflow or broader ITensor ecosystem context?

### Canonical workflow
1. Use `README.md` to establish package purpose and the core ITensor abstraction.
2. Route installation immediately to `INSTALL.md`.
3. Route first runnable calculations to `sample/README` and tutorial directories.
4. Route implementation-level API questions to source entry headers (`itensor/all.h`, `itensor/all_mps.h`, `itensor/core.h`).

### Minimal working example
```bash
# after following INSTALL.md
make
cd sample
make dmrg
./dmrg
```

### Pitfalls and fixes
- `README.md` is intentionally brief; do not treat it as full build or API documentation.
- Citation text references ITensors.jl preprint; keep routing precise when user asks about C++ usage details.
- Users often stop at README and miss `INSTALL.md`; explicitly redirect for build issues.

### Convergence and validation checks
- First success criterion: library builds and at least one sample executable runs.
- Orientation succeeds when the request is routed to a concrete topic skill with runnable next steps.

## Scope
- Entry-point orientation for ITensor C++.
- Routing from high-level questions to the correct operational skill.

## Primary documentation references
- `README.md`
- `INSTALL.md`
- `sample/README`

## Workflow
- Start from `README.md` for concise framing.
- Move immediately to build/tutorial/sample docs based on user intent.
- Use source headers only when high-level docs do not answer the question.

## Tutorials and examples
- `sample`
- `tutorial`

## Test references
- `unittest`

## Optional deeper inspection
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `itensor/all.h`
- `itensor/all_mps.h`
- `itensor/core.h`
- `itensor/itensor.h`
- `itensor/index.h`
- Prefer targeted source search (for example: `rg -n "all_mps|core\.h|ITensor" itensor`).
