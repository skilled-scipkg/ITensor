# itensor source map: Simulation Workflows

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `dmrg`
- `Sweeps`
- `LocalMPO`
- `davidson`
- `AutoMPO`
- `toMPO`
- `toExpH`
- `applyMPO`
- `MPS`
- `MPO`

## Fast source navigation
- `rg -n "dmrg\(|DMRGWorker|Sweeps|LocalMPO|davidson" itensor tutorial sample unittest`
- `rg -n "AutoMPO|toMPO|toExpH|applyMPO|MPS|MPO" itensor tutorial sample unittest`
- `rg -n "TEST_CASE|dmrg|applyMPO|LocalMPO|davidson|AutoMPO" unittest/mps_test.cc unittest/mpo_test.cc unittest/iterativesolvers_test.cc unittest/localop_test.cc unittest/autompo_test.cc`

## Suggested source entry points
- `itensor/mps/dmrg.h` | primary DMRG overloads and worker flow
- `itensor/mps/sweeps.h` | sweep parameterization and schedule helpers
- `itensor/mps/localmpo.h` | projected local operator used in iterative solves
- `itensor/mps/autompo.h` | Hamiltonian assembly and exponential MPO builder
- `itensor/mps/mpsalgs.cc` | key MPS algorithm implementations
- `itensor/mps/mpoalgs.cc` | MPO application/algorithm internals
- `itensor/iterativesolvers.h` | davidson/gmres interfaces used by workflows
- `itensor/decomp.h` | svd/denmat decomposition APIs for bond updates
- `unittest/autompo_test.cc` | function-level checks for Hamiltonian/MPO assembly behavior
- `unittest/mps_test.cc` | function-level MPS algorithm and canonicalization checks
- `unittest/mpo_test.cc` | function-level MPO/applyMPO behavior checks
- `unittest/iterativesolvers_test.cc` | function-level davidson/solver regression checks
- `unittest/localop_test.cc` | function-level projected-operator behavior checks
