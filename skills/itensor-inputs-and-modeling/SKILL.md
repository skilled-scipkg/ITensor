---
name: itensor-inputs-and-modeling
description: Use this skill for choosing ITensor models, tutorial progression, input-file driven workflows, and finite-temperature setup.
---

# itensor: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for model specification, parameter/input-file layout, and choosing tutorial/sample starting points.
- Route compiler/linker issues to `itensor-build-and-install`.
- Route DMRG/MPS performance and convergence tuning to `itensor-simulation-workflows`.
- Route low-level tensor/index API semantics to `itensor-api-and-scripting`.

### Triage questions
- What system class are you modeling (spin, fermion/electron, boson)?
- Is the target task ground state, finite-temperature, or time evolution?
- Do you want script/input-driven control (`InputGroup`) or code-defined parameters?
- Do you need QN conservation (`ConserveQNs=true`) or dense tensors?
- What observables do you need (energy, susceptibility, correlations, etc.)?
- What chain/lattice size and boundary assumptions are required?

### Canonical workflow
1. Start from tutorial progression `01_one_site` -> `02_two_site` -> `03_svd` to lock in Index/ITensor/SVD basics.
2. Move to `tutorial/04_mps/mps.cc` and `tutorial/05_gates/gates.cc` for MPS and gate-based workflows.
3. Use `tutorial/06_DMRG/dmrg.cc` as algorithm skeleton, then compare with complete `sample/dmrg.cc`.
4. Use table-driven sweeps/examples from `sample/dmrg_table.cc` + `sample/inputfile_dmrg_table`.
5. Use `sample/exthubbard.cc` + `sample/inputfile_exthubbard` for multi-parameter model input patterns.
6. For finite temperature, run `tutorial/finiteT/ancilla.cc` and `tutorial/finiteT/metts.cc` via `tutorial/finiteT/INSTRUCTIONS`.
7. Escalate to parser/source internals only when needed (`itensor/util/input.h`, `itensor/util/input.cc`, site-set headers).

### Minimal working example
```bash
cd tutorial/finiteT
make app=ancilla
./ancilla inputfile_ancilla
make app=metts
./metts inputfile_metts
```

```text
# sample/inputfile_dmrg_table
input
{
N = 100
nsweeps = 5
sweeps
{
maxdim  mindim  cutoff  niter  noise
50      20      1E-6    4      1E-7
80      20      1E-8    3      1E-8
100     10      1E-10   2      1E-10
}
quiet = no
}
```

### Pitfalls and fixes
- Tutorial files include `TODO` sections; use sample programs for fully runnable references.
- Missing CLI input file argument causes immediate usage/exit in input-driven codes.
- Input group/key mismatches (`input`, `sweeps`) break parameter reads in `InputGroup` workflows.
- In finite-T flows, non-commensurate `beta/2` and `tau` can trigger timestep consistency errors.
- Wrong operator labels/site types in `AutoMPO` lead to runtime/operator lookup failures.
- QN-conserving site sets require physically consistent initial states and measurements.

### Convergence and validation checks
- Increase `maxdim` and tighten `cutoff`; verify key observables stop drifting.
- Cross-check DMRG reported energy with explicit `inner(psi,H,psi)` (as in `sample/dmrg.cc`).
- For finite-T, compare `en.dat` and `sus.dat` trends when reducing `tau` and increasing `maxdim`.
- Reproduce baseline behavior from sample/tutorial before introducing custom model terms.

## Scope
- Choose practical starting points among tutorials and sample apps.
- Structure inputs/parameters for reusable study setups.
- Connect model-level decisions to the right executable pattern.

## Primary documentation references
- `tutorial/01_one_site/one.cc`
- `tutorial/02_two_site/two.cc`
- `tutorial/03_svd/svd.cc`
- `tutorial/04_mps/mps.cc`
- `tutorial/06_DMRG/dmrg.cc`
- `tutorial/finiteT/INSTRUCTIONS`
- `tutorial/finiteT/inputfile_ancilla`
- `tutorial/finiteT/inputfile_metts`
- `sample/README`
- `sample/inputfile_dmrg_table`
- `sample/inputfile_exthubbard`

## Workflow
- Start from tutorials for concept sequencing, then switch to sample apps for complete runnable patterns.
- Use finite-T tutorial inputs as reference for `InputGroup`-driven workflows.
- If docs are insufficient, inspect this skill's `references/doc_map.md`, then `references/source_map.md`.

## Tutorials and examples
- `tutorial`
- `sample`

## Test references
- `unittest/mps_test.cc`
- `unittest/mpo_test.cc`

## Optional deeper inspection
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `itensor/util/input.h`
- `itensor/util/input.cc`
- `itensor/mps/sites/spinhalf.h`
- `itensor/mps/sites/spinone.h`
- `itensor/mps/sites/electron.h`
- `itensor/mps/autompo.h`
- `itensor/mps/sweeps.h`
- `sample/Heisenberg.h`
- Prefer targeted source search (for example: `rg -n "InputGroup|getInt|getReal|AutoMPO|ConserveQNs" itensor sample tutorial`).
