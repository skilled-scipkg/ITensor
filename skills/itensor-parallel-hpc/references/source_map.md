# itensor source map: Parallel and HPC

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `ITENSOR_USE_OMP`
- `OMP_NUM_THREADS`
- `Environment`
- `MailBox`
- `MPI_`
- `NThread`
- `contract`

## Fast source navigation
- `rg -n "ITENSOR_USE_OMP|OMP_NUM_THREADS|OPENBLAS_NUM_THREADS|MKL_NUM_THREADS" options.mk.sample INSTALL.md`
- `rg -n "class Environment|class MailBox|MPI_|broadcast|allSum" itensor/util/parallel.h`
- `rg -n "NThread|contract" itensor/tensor/contract.cc itensor/tensor/contract.h`
- `rg -n "TEST_CASE|contract\(" unittest/contract_test.cc unittest/sparse_contract_test.cc`

## Suggested source entry points
- `itensor/util/parallel.h` | MPI environment, mailbox, and reduction/broadcast utilities
- `itensor/tensor/contract.cc` | threaded contraction internals and `NThread` handling
- `itensor/tensor/contract.h` | contraction interfaces and loop variants
- `options.mk.sample` | OpenMP and thread-policy build/runtime knobs
- `Makefile` | top-level build integration for threaded variants
- `unittest/contract_test.cc` | function-level contraction correctness checks under different argument patterns
- `unittest/sparse_contract_test.cc` | function-level sparse contraction behavior checks
