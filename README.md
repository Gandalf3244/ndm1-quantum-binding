NDM-1 Binding Energy via Quantum Chemistry

Quantum chemical calculation of the product-state binding energy in New Delhi Metallo-β-lactamase 1 (NDM-1), using a fragment-based CASCI → VQE pipeline targeting IBM quantum hardware.

Background

NDM-1 is a dizinc metallo-β-lactamase responsible for broad-spectrum antibiotic resistance. This project uses the 5ZGE crystal structure, which captures NDM-1 in complex with hydrolyzed ampicillin (ligand ZZ7) — the post-catalytic product state. The binding energy computed here reflects how tightly the hydrolyzed product is retained in the active site, which is relevant to understanding the rate-limiting product release step.

Approach

The calculation is broken into three fragments:

PartDescriptionMethod1Bare dizinc active site (His120, His122, His189, Asp124, Cys208, His250 + bridging OH)HF → CASCI(2e,7o)2Full product complex (active site + ZZ7 bound)HF → CASCI(2e,7o)3Isolated ZZ7 fragment (hydrolyzed ampicillin)B3LYP → CASCI(2e,7o)

Binding energy: ΔE = E(complex) − E(active site) − E(ZZ7)

Each fragment uses a CAS(2e,7o) active space selected around the zinc-coordinating frontier orbitals. One- and two-electron integrals are extracted from PySCF and mapped to a 14-qubit Jordan-Wigner Hamiltonian via Qiskit Nature.

Validation

All three Hamiltonians are validated against exact sparse diagonalization before any QPU submission. Parts 1 and 2 agree with CASCI to within 0.3–0.5 mEh. Part 3 uses CASCI directly (2-electron CASCI = exact FCI; VQE unnecessary and spin-unsafe for the biradical ZZ7 fragment).
