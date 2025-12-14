
This project is opensource and free for people to build off of and use.
# Quantum Notary: A Time Bridge for Web3 Oracles

### An "Async Adapter" for Quantum-to-Blockchain Communication

![Status](https://img.shields.io/badge/Status-Prototype-blue) ![Platform](https://img.shields.io/badge/Platform-IBM_Quantum-purple) ![License](https://img.shields.io/badge/License-MIT-green)

**The Quantum Notary** is a proof-of-concept engineering architecture designed to solve the **Speed Mismatch** between Quantum Processors (microseconds) and Blockchains (seconds). By implementing a dynamic **Hahn Echo sequence**, this protocol acts as a "Parking Brake" for quantum states, extending their coherence time long enough to facilitate reliable verification for Oracle services.

---

## 🛑 The Problem: The Speed Mismatch

In the race to build Quantum Oracles for Web3, there is a fatal disconnect:
1.  **Blockchains are Slow:** Finality takes seconds to minutes.
2.  **Qubits are Fragile:** Quantum states decay into noise in ~100 microseconds.

If a Smart Contract requests data, the quantum state usually "dies" (decoheres) before the verification logic can even process it. This makes reliable Quantum Oracles nearly impossible with standard implementation.

## 🌉 The Solution: The "Time Bridge" Architecture

This repository contains the code for an **Async Adapter**. Instead of standard measurement, this system:
1.  **Teleports** data to a "Storage" qubit (The Grid).
2.  **Stabilizes** the state using a custom Hahn Echo sequence (Dynamical Decoupling) within a Dynamic Circuit.
3.  **Verifies** the signal integrity before releasing it to the classical layer.

![Architecture Diagram](https://github.com/damianwgriggs/Quantum-Notary-/blob/main/architecture_diagram.jpg)
*(Note: Upload the diagram generated in the previous step to your repo and name it 'architecture_diagram.jpg' to make it appear here)*

---

## 🔬 The Experiment & Results

We tested this architecture on the **IBM Heron Processor (`ibm_fez`)**. The goal was to push the qubit beyond its natural decoherence limit ($T_2^*$) to prove we could create a stable "Swap Space" for data.

### The Protocol
* **Initialization:** Mint a specific quantum state.
* **Routing:** Move state to Grid Qubit.
* **The "Parking Brake":** Apply `Wait` -> `X-Gate` -> `Wait` -> `X-Gate`.
* **Retrieval:** Move state back and measure fidelity.

### Performance Data
Standard hardware limits usually degrade the signal to noise (<50%) by 100µs. Our active stabilization achieved the following:

| Delay Duration | Signal Fidelity | Status |
| :--- | :--- | :--- |
| **0 µs** | **91.0%** | Baseline (Max Hardware Capability) |
| **50 µs** | **77.9%** | Strong Signal |
| **150 µs** | **61.9%** | **RECOVERED (Success)** |

**Conclusion:** We successfully extended the validity window of the data by **~50% beyond the hardware's natural noise floor**, creating a viable window for Oracle verification logic to execute.

---

## 🚀 Usage

### Prerequisites
* Python 3.9+
* IBM Quantum Account (API Token)

### Installation
```bash
pip install qiskit qiskit-ibm-runtime qiskit-aer pylatexenc numpy
