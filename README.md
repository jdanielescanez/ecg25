# EGC25 Proposal
## 🔧 Implementation Overview

This project implements a simulated **Quantum Key Distribution (QKD)** proposal using the [Qiskit](https://qiskit.org/) framework. The implementation follows a modular structure, mirroring the protocol’s theoretical phases.

### 📦 Dependencies

Make sure to install the required libraries:

```bash
pip install qiskit==2.1 qiskit-aer==0.17.1
```

### ⚙️ Configuration

Global constants are defined for the number of qubit pairs, qubit indices, and whether an eavesdropper (Eve) is active:

```python
is_eve = False  # Set to True to simulate an intercept-resend attack
N = 10000       # Number of qubit pairs
```

### 🔗 Entanglement Generation

Each round begins by generating entangled qubit pairs in the Bell state `|Φ+⟩ = (|00⟩ + |11⟩)/√2` using a Hadamard and CNOT gate sequence.

### 🎲 Random Basis Selection

Alice, Bob, and optionally Eve choose measurement bases at random. Basis 0 = computational `{|0⟩, |1⟩}`, Basis 1 = Hadamard `{|+⟩, |−⟩}`.

### 🧪 Measurement and Interception

Each party measures their qubit based on the selected basis. If Eve is active, she performs an intercept-resend attack, modifying the protocol's behavior and generating detectable anomalies.

### 🔐 Key Extraction

Key bits are inferred based on announced non-orthogonal basis subsets. If a participant's result contradicts the other's announcement, the original bit can be inferred and used in the key.

### ✅ Key Validation

After key extraction, the protocol checks:

- Whether the key length is within the expected statistical bounds.
- Whether matching bases yield matching results (for integrity).

If the thresholds are not met, eavesdropping is suspected, and the protocol must restart.
