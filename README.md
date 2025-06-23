# ⚛️ Shor's Algorithm Oracle Construction in Qiskit

This code implements the arithmetic subroutines and modular multiplication oracle for Shor’s algorithm, based on the circuit from:

> Beauregard, Stéphane. “Circuit for Shor’s Algorithm Using 2n + 3 Qubits.”  
> *Quantum Information and Computation*, vol. 3, no. 2, 2003.  
> [arXiv:quant-ph/0205095](https://doi.org/10.48550/arXiv.quant-ph/0205095)

---

## Overview

The code provides quantum circuit constructions for:

- **Quantum addition** in the Fourier basis  
- **Modular addition** and **modular multiplication**  
- **Controlled modular multiplication** for use in Shor’s algorithm  
- **A full oracle for modular exponentiation**, controlled on an input register

The construction uses:

- **Fourier-space addition** circuits (Figure 3)  
- **Controlled modular adders** (Figures 5–7)  
- **Controlled-SWAP** gates (Figure 10)

---

## Benchmark Results

For parameters \( a = 7 \), \( n = 4 \):

| Metric            | Value                                                                 |
|-------------------|-----------------------------------------------------------------------|
| Gate Count        | `{'cp': 288, 'h': 140, 'mcphase': 80, 'swap': 56, 'cx': 24, 'x': 16, 'p': 8, 'ccx': 4}` |
| Circuit Depth     | 355                                                                   |
| Ancilla Qubits    | 1                                                                     |

- Gate count growth: \( O(n^2 \log n) \)  
- Circuit depth: \( O(n \log n) \)  
- Ancilla usage: constant (Beauregard design)

---

## Usage Instructions

1. **Run the package imports.**

2. **(1A)** Run the `int_to_bit_array` cell.  
   - Converts an integer to its \( n \)-bit binary array.  
   - *Example*: Uncomment the usage section to convert \( a = 15 \) for \( n = 4 \).

3. **(1B)** Run the `phiADD` cell.  
   - Implements \( b + a \) in the Fourier basis.  
   - *Example*: Uncomment to construct the \( n = 4 \) circuit for \( a = 15 \).  
   - *(Ref: Figure 3)*

4. **(1C, 1D)** Run the `C1phiADD` and `C2phiADD` cells.  
   - Implement controlled and doubly-controlled additions.  
   - *Example*: View circuits for \( n = 4 \), \( a = 15 \).

5. **(2A)** Run the `quantum_fourier_transform` cell.  
   - Converts binary values to Fourier basis.  
   - *Example*: Uncomment for \( n = 3 \).

6. **(2B)** Run the `inverse_quantum_fourier_transform` cell.  
   - Converts back to binary from Fourier basis.  
   - *Example*: Uncomment for \( n = 3 \).

7. **(2C)** Run the `C2phiADDMODN` cell.  
   - Doubly-controlled modular adder.  
   - Requires (1B), (1C), (1D), (2A), (2B).  
   - *Example*: \( n = 4 \), \( a = 15 \).  
   - *(Ref: Figure 5)*

8. **(3A)** Run the `CMultModN` cell.  
   - Performs \( b + ax \mod N \).  
   - Requires (2A), (2B), (2C).  
   - *Example*: \( n = 4 \), \( a = 15 \).  
   - *(Ref: Figure 6)*

9. **(3B)** Run the `CSWAP` cell.  
   - Implements a controlled-SWAP gate.  
   - *Example*: View the circuit.  
   - *(Ref: Figure 10)*

10. **(3C)** Run the `ShorsOracle` cell.  
    - Controlled \( ax \mod N \) oracle.  
    - Requires (3A), (3B).  
    - *Example*: \( n = 4 \), \( a = 15 \).  
    - *(Ref: Figure 7)*

11. **Run the benchmarking cell.**  
    - Displays gate counts, depth, and ancilla usage.

---

## References

- Beauregard, Stéphane. “Circuit for Shor’s Algorithm Using 2n + 3 Qubits.”  
  *Quantum Information and Computation*, vol. 3, no. 2, 2003.  
  [https://doi.org/10.48550/arXiv.quant-ph/0205095](https://doi.org/10.48550/arXiv.quant-ph/0205095)  
    - Figure 3: Quantum adder in Fourier basis  
    - Figure 5: Modular addition  
    - Figure 6: Modular multiplication  
    - Figure 7: Modular exponentiation oracle  
    - Figure 10: Controlled swap (CSWAP)
