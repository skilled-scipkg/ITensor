# itensor source map: Advanced Topics

Generated from source roots:
- `itensor`
- `tools`
- `tutorial`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `en.dat`
- `sus.dat`
- `InputGroup`
- `readwrite`
- `h5`
- `release`

## Fast source navigation
- `rg -n "en\.dat|sus\.dat|InputGroup|GetInt|GetReal" tutorial itensor`
- `rg -n "readwrite|h5|base_public" itensor/util`
- `rg -n "h5_open|h5_write|h5_read|TEST_CASE" unittest/hdf5_test.cc`

## Suggested source entry points
- `tutorial/finiteT/ancilla.cc` | finite-T output generation (`en.dat`, `sus.dat`)
- `tutorial/finiteT/metts.cc` | finite-T sampling and reporting workflow
- `itensor/util/input.h` | input parser interface used by advanced examples
- `itensor/util/input.cc` | concrete `InputGroup` parsing and typed getter behavior
- `itensor/util/readwrite.h` | serialization helpers
- `itensor/util/h5/base_public.hpp` | HDF5-facing utility API
- `itensor/util/h5/base.hpp` | HDF5 utility declarations
- `itensor/util/h5/base.cc` | HDF5 utility implementation
- `unittest/hdf5_test.cc` | function-level serialization checks for tags, indices, tensors, MPS/MPO
