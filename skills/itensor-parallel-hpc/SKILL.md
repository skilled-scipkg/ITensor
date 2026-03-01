---
name: itensor-parallel-hpc
description: Use this skill for ITensor OpenMP/MPI execution setup, threading policy, and parallel validation checks.
---

# itensor: Parallel and HPC

## High-Signal Playbook
### Route conditions
- Use this skill for OpenMP enablement, MPI runtime integration (`itensor/util/parallel.h`), and scaling/throughput checks.
- Route build-system and linker setup to `itensor-build-and-install`.
- Route algorithmic accuracy and sweep tuning to `itensor-simulation-workflows`.

### Triage questions
- Do you need shared-memory threading (OpenMP), distributed memory (MPI), or both?
- Is your BLAS/LAPACK backend also threaded (MKL/OpenBLAS)?
- Which launcher/toolchain are you using (`mpirun`, vendor MPI wrappers)?
- Are you CPU-only or mixing external accelerator stacks?
- Is reproducibility or raw throughput the top priority?

### Canonical workflow
1. For OpenMP in ITensor, enable `ITENSOR_USE_OMP=1` in `options.mk` (`options.mk.sample`).
2. Build/rebuild ITensor after flag changes (`Makefile`, `itensor/Makefile`).
3. Set runtime threads: `OMP_NUM_THREADS=<n>`.
4. Prevent thread oversubscription by pinning BLAS threads to 1 (`MKL_NUM_THREADS=1` or `OPENBLAS_NUM_THREADS=1`).
5. For MPI workflows, include `itensor/util/parallel.h`, construct `Environment`, and use `broadcast`/`sum` utilities.
6. Benchmark on small deterministic workloads, then scale node/thread counts.

### Minimal working example
```bash
# OpenMP runtime policy
export OMP_NUM_THREADS=8
export MKL_NUM_THREADS=1
# or: export OPENBLAS_NUM_THREADS=1
make
cd sample && make dmrg && ./dmrg
```

```cpp
#include "itensor/util/parallel.h"
using namespace itensor;
int main(int argc, char* argv[]) {
  Environment env(argc,argv);
  double x = 1.0;
  auto total = allSum(env,x);
  if(env.firstNode()) printfln("total=%.1f",total);
  return 0;
}
```

### Pitfalls and fixes
- `mpi.h` not found: MPI toolchain/runtime is missing for `itensor/util/parallel.h` workflows.
- Parallel slowdown from oversubscription: cap BLAS threads when ITensor OpenMP is enabled.
- Inconsistent timings across runs: stabilize environment variables and process/thread affinity.
- Expecting bitwise-identical floating-point reductions across ranks/threads is unsafe; validate tolerance-based invariants.
- Forgetting rebuild after changing `ITENSOR_USE_OMP` can leave stale binaries.

### Convergence and validation checks
- Compare 1-thread/1-rank energies against multi-thread/multi-rank runs for numerical consistency.
- Record wall time and throughput vs thread/rank count; confirm scaling before production runs.
- Validate that reported rank/thread counts match expectations in logs or lightweight diagnostics.
- Re-run a known sample baseline after any toolchain or runtime policy change.

## Scope
- OpenMP and MPI execution posture for ITensor C++ workflows.
- Runtime policy for thread/process counts and BLAS interaction.
- Parallel correctness and scaling sanity checks.

## Primary documentation references
- `INSTALL.md`
- `options.mk.sample`
- `Makefile`
- `itensor/Makefile`

## Workflow
- Start from `options.mk.sample` threading guidance, then validate with sample workloads.
- Prefer minimal reproducible scale tests before full-size studies.
- Escalate to source inspection when MPI utility behavior or threading internals are unclear.

## Tutorials and examples
- `sample`
- `tutorial`

## Test references
- `unittest/contract_test.cc`
- `unittest/mps_test.cc`

## Optional deeper inspection
- `itensor/util`
- `itensor/tensor`

## Source entry points for unresolved issues
- `itensor/util/parallel.h`
- `itensor/tensor/contract.cc`
- `options.mk.sample`
- `itensor/Makefile`
- `Makefile`
- Prefer targeted source search (for example: `rg -n "ITENSOR_USE_OMP|OMP_NUM_THREADS|NThread|Environment|MPI_" itensor options.mk.sample`).
