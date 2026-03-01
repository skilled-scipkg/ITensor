# itensor documentation map: Simulation Workflows

Generated from documentation roots:
- `tutorial`
- `sample`
- `unittest`

Total docs grouped in this topic: 12

## File inventory
- `tutorial/04_mps/mps.cc` | title: MPS workflow tutorial | headings: AutoMPO; dmrg; observable measurement
- `tutorial/05_gates/gates.cc` | title: gate-based evolution tutorial | headings: Trotter gate construction; gate application loop; energy measurement
- `tutorial/06_DMRG/dmrg.cc` | title: manual DMRG workflow tutorial | headings: LocalMPO positioning; davidson solve; svd update
- `tutorial/finiteT/INSTRUCTIONS` | title: finite-T workflow instructions | headings: build ancilla/metts; run with input files
- `tutorial/finiteT/ancilla.cc` | title: ancilla finite-T workflow | headings: InputGroup parsing; applyMPO loop; output en.dat/sus.dat
- `tutorial/finiteT/metts.cc` | title: METTS finite-T workflow | headings: collapse step; imaginary-time evolution; statistics
- `sample/README` | title: sample workflow catalog | headings: dmrg; dmrg_table; exthubbard; mixedspin; trg; ctmrg
- `sample/dmrg.cc` | title: baseline DMRG workflow | headings: SiteSet; AutoMPO; Sweeps; dmrg; energy checks
- `sample/dmrg_table.cc` | title: input-table DMRG workflow | headings: InputGroup sweeps table; dmrg run
- `sample/exthubbard.cc` | title: extended Hubbard DMRG workflow | headings: parameter parsing; model build; dmrg run
- `unittest/mps_test.cc` | title: MPS behavior regression checks | headings: constructors; canonicalization; tag/QN checks
- `unittest/mpo_test.cc` | title: MPO/applyMPO regression checks | headings: applyMPO methods; tag integrity; dmrg checks
