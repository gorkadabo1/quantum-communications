# Quantum Communications Channel Simulation

Simulation of quantum communication channels with quantum repeaters using Qiskit. This project models the challenges of long-distance quantum communication and demonstrates how quantum repeaters improve transmission fidelity through entanglement swapping.

## Overview

Long-distance quantum communication faces fundamental challenges due to quantum decoherence and the no-cloning theorem, which prevents classical signal amplification. This simulation implements:

- **Quantum channel modeling** with realistic noise (depolarizing errors, thermal relaxation)
- **Bell pair generation** for entanglement distribution
- **Quantum repeaters** using entanglement swapping protocol
- **Performance analysis** across different distances and repeater configurations

## Key Results

| Distance | No Repeaters | 2 Repeaters | 5 Repeaters |
|----------|--------------|-------------|-------------|
| 1 km     | 0.002        | 0.026       | 0.400       |
| 10 km    | 0.002        | 0.031       | 0.397       |
| 50 km    | 0.002        | 0.031       | 0.433       |

*Fidelity values (higher is better, max = 1.0)*

At 50 km, quantum repeaters improve fidelity by over **200x** compared to direct transmission.

## Technical Implementation

### Noise Model

The simulation includes two types of quantum errors:

1. **Depolarizing errors**: Model random bit/phase flips during transmission
   - Single-qubit error probability: `p = 1 - exp(-L * α / 10)`
   - Two-qubit error probability: `2p` (capped at 1.0)
   - Attenuation coefficient (α): 0.2 dB/km (realistic for optical fiber)

2. **Thermal relaxation errors**: Model coherence loss over time
   - T1 (longitudinal relaxation): 0.1 ms
   - T2 (transverse relaxation): 0.05 ms

### Entanglement Swapping Protocol

The quantum repeater implementation follows the standard Bell state measurement protocol:

1. Create Bell pairs between adjacent nodes
2. Perform CNOT and Hadamard gates on intermediate qubits
3. Measure intermediate qubits
4. Apply conditional Pauli-X and Pauli-Z corrections based on measurement outcomes

## Project Structure

```
quantum-communications/
├── notebooks/
│   └── quantum_communications.ipynb    # Main simulation notebook
├── src/
│   └── quantum_channel.py              # QuantumCommunicationChannel class
├── docs/
│   └── quantum_communications_report.pdf    # Detailed project report
└── requirements.txt
```

## Requirements

- Python 3.8+
- Qiskit 1.0+
- Qiskit Aer
- NumPy
- Matplotlib

## Usage

```python
from src.quantum_channel import QuantumCommunicationChannel

# Create a 50 km channel with 5 quantum repeaters
channel = QuantumCommunicationChannel(distance=50, num_repeaters=5)

# Run simulation
fidelity, counts = channel.simulate_communication()
print(f"Fidelity: {fidelity:.4f}")
```

## References

1. Briegel, H. J., et al. "Quantum Repeaters: The Role of Imperfect Local Operations in Quantum Communication." Physical Review Letters, 1998.
2. Muralidharan, S., et al. "Optimal Architectures for Long Distance Quantum Communication." Scientific Reports, 2016.

## Context

This project was developed for educational purposes at the University of the Basque Country (EHU).
