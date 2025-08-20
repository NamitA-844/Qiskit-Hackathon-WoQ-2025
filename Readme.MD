# Team: Smart Fidelity

### This is our submission for the IBM Quantum Qiskit Hackathon 2025


the file `final_notebook.ipynb` contains the code for the hackathon submission.

### Team Members:
- Namita Agrawal
- Prakrisht 
- Yaxuan Zhang
- Sasha Schütz
- Jakob Hellbardt

## Learning to Dynamically Decouple
### Smart Dynamic Decoupling system for circuit optimization


Our work takes inspiration from the paper [Learning Dynamical Decoupling](https://arxiv.org/abs/2405.08689v1) and implements a smart, adaptive Dynamical Decoupling system that learns optimal pulse-level sequences for error mitigation on quantum circuits.

In the paper, the authors implemented an optimal Gate sequence, we took the work a step further by implementing a more accurate representation taking into account the time required for each microwave pulse and optimising the pulse-level sequences for the specific quantum circuit and hardware.


## What is Dynamical Decoupling?
Dynamical Decoupling (DD) is an error suppression technique that combats decoherence by actively flipping qubits during idle periods.
These flips — typically π rotations (e.g. X or Y gates) — cause noise effects to cancel out over time, preserving the quantum information longer.
It’s like periodically “shaking off” unwanted interactions with the environment.

Standard DD uses fixed sequences like:

- CPMG (X–X)

- XY4, XY8

- Uhrig DD (non-uniform spacing)

These are general-purpose but not tailored to your specific quantum circuit or hardware. Dynamic Decoupling could be made very specific for the hardware, but it assumes we know the interactions of the circuit with the environment. We can optimize the circuit by learning the parameters from the circuit, calcuting the cost function.

## Better learned
Every quantum circuit interacts with noise in a unique way depending on:

- Its structure (which qubits are idle and when)

- The backend (gate times, coherence times, noise model)

Traditional DD sequences ignore this.
But Learning Dynamical Decoupling (LDD):

- Optimizes pulse timing and phases for specific circuits

- Learns parameters that suppress real decoherence

- Exploits hardware-specific capabilities (pulse-level control, drive channels)

This means better fidelity, less noise, and more scalable error mitigation.


In this notebook, we implement a smart, adaptive Dynamical Decoupling system based on https://arxiv.org/abs/2405.08689v1:

- Inserts custom pulse-level DD sequences
- Learns optimal parameters using real hardware characteristics
- Uses optimization (SPSA) to minimize decoherence
- Fully compatible with IBM backends and pulse scheduling
- Benchmarks LDD vs. No-DD and Standard DD sequences
