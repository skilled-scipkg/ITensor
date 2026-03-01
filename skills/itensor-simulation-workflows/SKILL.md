---
name: itensor-simulation-workflows
description: Use this skill for MPS/MPO construction, DMRG and time-evolution workflows, and simulation validation in ITensor C++.
---

# itensor: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for end-to-end MPS/MPO workflows: Hamiltonian build, solver setup, sweeps, and observable validation.
- Route toolchain and linking failures to `itensor-build-and-install`.
- Route model/input-shape questions to `itensor-inputs-and-modeling`.
- Route MPI/OpenMP scaling and cluster launch concerns to `itensor-parallel-hpc`.

### Triage questions
- Ground-state DMRG, finite-temperature evolution, or gate-based time evolution?
- Which site set/model family (SpinHalf, SpinOne, Electron, etc.)?
- Are QNs conserved, and is the initial state compatible with that choice?
- What accuracy target is needed (`maxdim`, `cutoff`, `noise`, `niter`)?
- Which observables define success (energy, susceptibility, correlations, gap)?
- Do you need table-driven sweep schedules from input files?

### Canonical workflow
1. Define `SiteSet` and initial `MPS` (`InitState` or `randomMPS`) from tutorial/sample patterns.
2. Build Hamiltonian via `AutoMPO` and `toMPO` (`sample/dmrg.cc`, `tutorial/06_DMRG/dmrg.cc`).
3. Configure sweeps (`Sweeps`, `maxdim`, `cutoff`, `noise`, `niter`) explicitly.
4. Run `dmrg(H,psi0,sweeps,...)` for standard ground-state workflows.
5. Validate with explicit `inner(psi,H,psi)` and compare to solver-reported energy.
6. For finite-T, construct `toExpH(...)`, apply with `applyMPO`, call `noPrime`, and renormalize (`tutorial/finiteT/*`).
7. For low-level control, use `LocalMPO` + `davidson` loop (tutorial DMRG skeleton).
8. Cross-check behavior against unit tests before scaling problem size.

### Minimal working example
```bash
cd sample
make dmrg
./dmrg
make dmrg_table
./dmrg_table inputfile_dmrg_table
```

```cpp
// minimal pattern from sample/dmrg.cc
auto sites = SpinOne(N);
auto ampo = AutoMPO(sites);
for(auto j : range1(N-1)) {
  ampo += 0.5,"S+",j,"S-",j+1;
  ampo += 0.5,"S-",j,"S+",j+1;
  ampo +=     "Sz",j,"Sz",j+1;
}
auto H = toMPO(ampo);
auto psi0 = MPS(InitState(sites));
auto sweeps = Sweeps(5);
sweeps.maxdim() = 10,20,100,100,200;
sweeps.cutoff() = 1E-10;
auto [energy,psi] = dmrg(H,psi0,sweeps,"Quiet");
auto check = inner(psi,H,psi);
```

### Pitfalls and fixes
- `applyMPO` workflows: call `psi.noPrime()` after application when needed (finite-T examples).
- Forgetting normalization in iterative evolution can mask physical trends; normalize regularly.
- Too-small `maxdim` or too-loose `cutoff` can produce false convergence.
- Keeping nonzero `noise` too long can stall final energy refinement.
- Manual local-solver loops require consistent `psi.position(b)` / `LocalMPO.position(b,psi)` calls.
- QN-conserving runs can fail silently in quality if initial state/targets are inconsistent with symmetry sector.

### Convergence and validation checks
- Energy consistency: compare DMRG-reported value with `inner(psi,H,psi)`.
- Parameter stability: increase `maxdim`, reduce `cutoff`, and verify observables stabilize.
- For finite-T, re-run with smaller `tau` and verify `en.dat`/`sus.dat` trends are robust.
- Use `unittest/mps_test.cc`, `unittest/mpo_test.cc`, and `unittest/iterativesolvers_test.cc` as regression anchors for MPS/MPO/local-solver behavior.

## Scope
- Practical ITensor simulation pipelines from Hamiltonian construction to validated outputs.
- Ground-state DMRG, finite-temperature evolution, and gate-based workflows.
- Data-quality checks for reliable physics conclusions.

## Primary documentation references
- `tutorial/04_mps/mps.cc`
- `tutorial/05_gates/gates.cc`
- `tutorial/06_DMRG/dmrg.cc`
- `tutorial/finiteT/INSTRUCTIONS`
- `tutorial/finiteT/ancilla.cc`
- `tutorial/finiteT/metts.cc`
- `sample/README`
- `sample/dmrg.cc`
- `sample/dmrg_table.cc`
- `sample/inputfile_dmrg_table`
- `sample/exthubbard.cc`

## Workflow
- Start with tutorial/sample docs for recommended usage order.
- Validate on sample cases before custom model expansion.
- Escalate to source internals only when docs/examples do not resolve behavior.

## Tutorials and examples
- `tutorial/04_mps`
- `tutorial/05_gates`
- `tutorial/06_DMRG`
- `tutorial/finiteT`
- `sample`

## Test references
- `unittest/mps_test.cc`
- `unittest/mpo_test.cc`
- `unittest/iterativesolvers_test.cc`
- `unittest/localop_test.cc`

## Optional deeper inspection
- `itensor/mps`
- `itensor`

## Source entry points for unresolved issues
- `itensor/mps/dmrg.h`
- `itensor/mps/sweeps.h`
- `itensor/mps/autompo.h`
- `itensor/mps/localmpo.h`
- `itensor/mps/mpsalgs.cc`
- `itensor/mps/mpoalgs.cc`
- `itensor/iterativesolvers.h`
- `itensor/decomp.h`
- Prefer targeted source search (for example: `rg -n "dmrg\(|Sweeps|applyMPO|toExpH|LocalMPO|davidson" itensor tutorial sample unittest`).
