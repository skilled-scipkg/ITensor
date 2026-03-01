# itensor source map: Inputs and Modeling

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `InputGroup`
- `InputFile`
- `getInt`
- `getReal`
- `getYesNo`
- `AutoMPO`
- `SiteSet`
- `ConserveQNs`
- `SpinHalf`
- `SpinOne`
- `Electron`

## Fast source navigation
- `rg -n "InputGroup|InputFile|getInt|getReal|getYesNo" itensor sample tutorial`
- `rg -n "AutoMPO|SiteSet|ConserveQNs|SpinHalf|SpinOne|Electron" itensor sample tutorial`
- `rg -n "InputGroup|Sweeps|maxdim|cutoff|ConserveQNs|AutoMPO" sample/dmrg_table.cc sample/exthubbard.cc unittest/autompo_test.cc unittest/siteset_test.cc`

## Suggested source entry points
- `itensor/util/input.h` | public API for input-file groups and typed value extraction
- `itensor/util/input.cc` | parser behavior and error paths
- `itensor/mps/autompo.h` | Hamiltonian term accumulation and conversion to MPO/exp(H)
- `itensor/mps/sweeps.h` | sweep schedule definitions and table parsing
- `itensor/mps/sites/spinhalf.h` | spin-1/2 operator/state definitions
- `itensor/mps/sites/spinone.h` | spin-1 operator/state definitions
- `itensor/mps/sites/electron.h` | electron site operators/states
- `sample/Heisenberg.h` | compact model-construction reference used in tests/samples
- `sample/dmrg_table.cc` | function-level check for sweeps-table parsing via `InputGroup`
- `unittest/autompo_test.cc` | function-level checks for operator/model term construction
- `unittest/siteset_test.cc` | function-level checks for site-set and operator/state availability
