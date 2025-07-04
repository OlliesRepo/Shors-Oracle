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

The full implementation is:

U |x⟩₁ |y⟩ₙ =
  if c = 1 and x < N:
    |c⟩₁ |ax mod N⟩ₙ
  else:
    |c⟩₁ |x⟩ₙ

## Benchmarking Results

For factoring \( N = 15 \) with base \( a = 7 \):

| Metric          | Value                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------|
| Gate Count      | `{'cp': 1888, 'h': 468, 'mcphase': 288, 'swap': 208, 'cx': 48, 'x': 32, 'p': 16, 'ccx': 8}` |
| Circuit Depth   | 1159                                                                                      |
| Ancilla Qubits  | 1                                                                                         

- Gate count growth: \( O(n^2 \log n) \)  
- Circuit depth: \( O(n \log n) \)  
- Ancilla usage: constant (Beauregard design)

---

## Usage Instructions

1. **Run the package imports.**

2. **(1A)** Run the `int_to_bit_array` cell.  
   - Converts an integer to its $n$-bit binary array.  
   - (Optional) Uncomment the valid code in the example usage section to see the $n = 8$ bit array representation of $a = 7$.

3. **(1B)** Run the `phiADD` cell.  
   - Implements modular addition in the Fourier basis.
   - Requires (1A)
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 8$ qubits that adds $a = 7$.
   - *(Ref: Figure 3)*

4. **(1C, 1D)** Run the `C1phiADD` and `C2phiADD` cells.  
   - Implement controlled and doubly-controlled additions.  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 8$ qubits that adds $a = 7$.

5. **(2A)** Run the `quantum_fourier_transform` cell.  
   - Converts binary values to Fourier basis.  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 3$ qubits.

6. **(2B)** Run the `inverse_quantum_fourier_transform` cell.  
   - Converts back to binary from Fourier basis.  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 3$ qubits.

7. **(2C)** Run the `C2phiADDMODN` cell.  
   - Doubly-controlled modular adder that outputs $|b + a \mod N \rangle $.  
   - Requires (1B), (1C), (1D), (2A), (2B).  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 8$ qubits that adds $a = 7$.
   - *(Ref: Figure 5)*

8. **(3A)** Run the `CMultModN` cell.  
   - Outputs $|b + ax \mod N \rangle$.  
   - Requires (2A), (2B), (2C).  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit for $n = 8$ qubits that adds $a = 7$.
   - *(Ref: Figure 6)*

9. **(3B)** Run the `CSWAP` cell.  
   - Implements a controlled-SWAP gate.  
   - (Optional) Uncomment the valid code in the example usage section to see the circuit.
   - *(Ref: Figure 10)*

10. **(3C)** Run the `ShorsMultiplier` cell.  
    - Outputs $|ax \mod N \rangle$.  
    - Requires (3A), (3B).  
    - (Optional) Uncomment the example code to view the circuit that performs modular multiplication for factoring $N=15$ with base $a = 7$ in Shor’s algorithm.
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
