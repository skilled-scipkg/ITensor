# itensor source map: Build and Install

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `options.mk`
- `CCCOM`
- `PLATFORM`
- `BLAS_LAPACK`
- `ITENSOR_USE_OMP`
- `HDF5_PREFIX`
- `Makefile`
- `project_template`

## Fast source navigation
- `rg -n "PLATFORM|BLAS_LAPACK|ITENSOR_USE_OMP|HDF5|CCCOM" options.mk.sample Makefile itensor sample tutorial`
- `rg -n "ITENSOR_LIBFLAGS|ITENSOR_INCLUDEFLAGS|this_dir.mk" Makefile sample tutorial`
- `rg -n "^dmrg:|^debug:|this_dir.mk|config.h" Makefile sample/Makefile tutorial/project_template/Makefile`

## Suggested source entry points
- `Makefile` | top-level configure/build/clean logic
- `options.mk.sample` | canonical user flags and backend configuration
- `itensor/Makefile` | library object/link rules
- `sample/Makefile` | executable link pattern against ITensor libs
- `sample/dmrg.cc` | minimal executable used for first end-to-end compile/link validation
- `tutorial/project_template/Makefile` | out-of-tree app linking template
- `itensor/tensor/lapack_wrap.h` | backend-dependent BLAS/LAPACK signatures
- `itensor/tensor/lapack_wrap.cc` | BLAS/LAPACK wrapper implementation details
- `itensor/util/parallel.h` | OpenMP/MPI-adjacent runtime integration hooks
- `unittest/Makefile` | regression build target surface for compile/link sanity checks
