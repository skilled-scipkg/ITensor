# itensor source map: API and Scripting

Generated from source roots:
- `itensor`
- `tools`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Topic query tokens
- `ITensor`
- `Index`
- `TagSet`
- `svd`
- `denmatDecomp`
- `diagHermitian`
- `contract`
- `davidson`
- `Args`
- `InputGroup`
- `Error`

## Fast source navigation
- `rg -n "class ITensor|class Index|TagSet|prime\(|noPrime\(" itensor`
- `rg -n "svd\(|denmatDecomp|diagHermitian|eigen\(" itensor/decomp* itensor/svd.cc`
- `rg -n "contract\(|contractloop|computeLabels" itensor/tensor/contract*`
- `rg -n "davidson|gmres" itensor/iterativesolvers.h unittest/iterativesolvers_test.cc`
- `rg -n "class Args|getInt|getReal|getBool|InputGroup|Error\(" itensor/util`
- `rg -n "TEST_CASE|SECTION|ITensor|Index|svd|contract|davidson|Args" unittest/itensor_test.cc unittest/index_test.cc unittest/decomp_test.cc unittest/contract_test.cc unittest/iterativesolvers_test.cc unittest/args_test.cc`

## Suggested source entry points
- `itensor/itensor.h` | core ITensor API declarations
- `itensor/itensor_impl.h` | ITensor template/helper implementations
- `itensor/index.h` | index/tag/QN API surface
- `itensor/decomp.h` | decomposition front-door APIs
- `itensor/svd.cc` | SVD/truncation implementation and Args handling
- `itensor/tensor/contract.h` | contraction interfaces
- `itensor/tensor/contract.cc` | contraction implementation internals
- `itensor/iterativesolvers.h` | iterative eigensolver/linear solver interfaces
- `itensor/util/args.h` | named argument framework
- `itensor/util/input.h` | structured text input parser API
- `unittest/itensor_test.cc` | function-level checks for ITensor construction/manipulation semantics
- `unittest/index_test.cc` | function-level checks for index/tag/prime behavior
- `unittest/decomp_test.cc` | function-level checks for SVD/eigen/decomposition APIs
- `unittest/contract_test.cc` | function-level checks for tensor contraction behavior
- `unittest/iterativesolvers_test.cc` | function-level checks for davidson/gmres solver surfaces
