---
name: itensor-build-and-install
description: Use this skill for ITensor C++ build setup, compiler/linker configuration, library compilation, and external project linking.
---

# itensor: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for toolchain setup, `options.mk` configuration, library/sample build failures, and linking external apps.
- Route model setup and tutorial progression questions to `itensor-inputs-and-modeling`.
- Route DMRG/MPS algorithm tuning and correctness checks to `itensor-simulation-workflows`.
- Route MPI/OpenMP execution policy and scaling questions to `itensor-parallel-hpc`.

### Triage questions
- Which OS and compiler are you using (`g++`, `clang++`, other)?
- Did you create `options.mk` from `options.mk.sample`?
- Which BLAS/LAPACK backend and `PLATFORM` are selected?
- Do you need HDF5 (`HDF5_PREFIX`) or OpenMP (`ITENSOR_USE_OMP`)?
- Are you building core libraries, sample apps, or an external project?
- Are you using serial `make` or parallel `make -j`?

### Canonical workflow
1. Copy template options: `cp options.mk.sample options.mk` (`INSTALL.md`).
2. Set compiler in `CCCOM` and keep C++17 enabled (`INSTALL.md`, `options.mk.sample`).
3. Set `PLATFORM`, `BLAS_LAPACK_LIBFLAGS`, and optional `BLAS_LAPACK_INCLUDEFLAGS` (`INSTALL.md`, `options.mk.sample`).
4. Optionally set `HDF5_PREFIX` and/or `ITENSOR_USE_OMP=1` (`options.mk.sample`).
5. Build ITensor from repo root with `make` (`INSTALL.md`, top-level `Makefile`).
6. Build sample apps: `cd sample && make` or `make <appname>` (`INSTALL.md`, `sample/README`, `sample/Makefile`).
7. For external projects, copy `tutorial/project_template` outside the repo and set `LIBRARY_DIR` in its Makefile (`INSTALL.md`, `tutorial/project_template/README`).

### Minimal working example
```bash
cp options.mk.sample options.mk
# edit options.mk (CCCOM, PLATFORM, BLAS_LAPACK_LIBFLAGS, optional HDF5_PREFIX/ITENSOR_USE_OMP)
make
cd sample
make dmrg
./dmrg
```

```make
# from tutorial/project_template/Makefile
LIBRARY_DIR=../itensor-itensor
include $(LIBRARY_DIR)/this_dir.mk
include $(LIBRARY_DIR)/options.mk
APP=myappname
CCFILES=$(APP).cc
```

### Pitfalls and fixes
- `options.mk` missing: create it from `options.mk.sample` before any build.
- C++ feature errors: ensure `CCCOM` includes `-std=c++17`.
- BLAS/LAPACK link failures: align `PLATFORM` and `BLAS_LAPACK_LIBFLAGS` with your actual backend.
- Flaky compile errors under parallel make: retry with `make -j 1` (called out in `INSTALL.md`).
- Sample build cannot resolve ITensor paths: run root `make` first so `this_dir.mk` and `itensor/config.h` are generated.
- External app link/include issues: verify `LIBRARY_DIR`, and include both `this_dir.mk` and `options.mk`.
- OpenMP slowdown: set `OMP_NUM_THREADS`, and set BLAS thread count to 1 as advised in `options.mk.sample`.

### Convergence and validation checks
- Root build produces ITensor libraries under `lib/`.
- `dmrg` built from `sample/dmrg.cc` runs and prints initial/final energies.
- `tutorial/project_template` app builds without custom manual include/lib flags beyond template edits.
- Optional debug target links cleanly where provided (`make debug` in sample/tutorial makefiles).

## Scope
- Build and link ITensor C++ library and example programs.
- Configure platform/compiler/library flags in `options.mk`.
- Set up out-of-tree client projects using the template Makefile flow.

## Primary documentation references
- `INSTALL.md`
- `options.mk.sample`
- `Makefile`
- `sample/README`
- `sample/Makefile`
- `tutorial/project_template/README`
- `tutorial/project_template/Makefile`

## Workflow
- Start with `INSTALL.md` and `options.mk.sample`.
- Use `sample/README` and `sample/Makefile` for first successful compile/run validation.
- Use `tutorial/project_template/*` for external project linking conventions.
- If docs are insufficient, inspect this skill's `references/doc_map.md` then `references/source_map.md`.

## Tutorials and examples
- `sample`
- `tutorial/project_template`

## Test references
- `unittest/Makefile`

## Optional deeper inspection
- `itensor`
- `tools`

## Source entry points for unresolved issues
- `Makefile`
- `options.mk.sample`
- `itensor/Makefile`
- `sample/Makefile`
- `tutorial/project_template/Makefile`
- `itensor/tensor/lapack_wrap.h`
- `itensor/tensor/lapack_wrap.cc`
- `unittest/Makefile`
- Prefer targeted source search (for example: `rg -n "PLATFORM|BLAS_LAPACK|ITENSOR_USE_OMP|HDF5" Makefile options.mk.sample itensor`).
