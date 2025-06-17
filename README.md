# ShorsOracle
# 🧮 Modular Arithmetic for Shor's Algorithm (Beauregard 2003 Implementation)

Using only 1-qubit gates, multi-controlled phase (MCP) and X (MC X ) gates, this project implements the modular arithmetic subroutines needed for Shor’s Algorithm using Beauregard’s 2003 construction, which uses `2n + 3` qubits. All circuits are implemented in Python using Qiskit and include formal reasoning/proofs in Markdown cells above each function within the Jupyter Notebook. Each Circuit is drawn below it's function.

> 📄 Reference:  
> Stéphane Beauregard. *Circuit for Shor’s Algorithm Using 2n + 3 Qubits.*  
> Quantum Information and Computation, vol. 3, no. 2 (2003).  
> [arXiv:quant-ph/0205095v3](https://arxiv.org/abs/quant-ph/0205095)

---

## 📚 Contents

- Quantum Fourier Transform (QFT) and Inverse QFT
- Phase Addition (`phiADD`) circuits
- Controlled and doubly-controlled `phiADD` (`C1phiADD`, `C2phiADD`)
- Modular phase addition `C2phiADDMODN`
- Modular multiplication `CMultModN`
- Modular controlled unitary `CU_a`
- Circuit benchmarking: gate counts, depth, ancilla usage
- Markdown proofs for correctness of each component

---

## 🧠 Theory

All functions are annotated with mathematical derivations or justifications for their correctness, derived directly from Beauregard's paper. This includes:

- Derivations of phase angles
- Modular arithmetic over the QFT basis
- Ancilla usage and reversible computation guarantees
