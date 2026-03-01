# itensor source map: Readme

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `all.h`
- `all_mps.h`
- `core.h`
- `ITensor`
- `Index`
- `MPS`

## Fast source navigation
- `rg -n "#include \"itensor/all_mps.h\"|#include \"itensor/core.h\"" itensor`
- `rg -n "class ITensor|class Index" itensor/itensor.h itensor/index.h`
- `rg -n "TEST_CASE|ITensor|Index" unittest/itensor_test.cc unittest/index_test.cc`

## Suggested source entry points
- `itensor/all.h` | top-level convenience include
- `itensor/all_mps.h` | main MPS/MPO feature include surface
- `itensor/core.h` | core decomposition/solver include surface
- `itensor/itensor.h` | ITensor core class API
- `itensor/index.h` | Index and tagging/prime/QN-facing API
- `unittest/itensor_test.cc` | function-level reference checks for core tensor API behaviors
- `unittest/index_test.cc` | function-level reference checks for index/tagging behaviors
