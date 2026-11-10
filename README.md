# Do Quantum Research Project

## Team

- Travis Ferguson
- Jack Nargi
- Peter Johnston

## Hypothesis

> **As qubit count increases, CLOPS will decrease unless classical control-system capacity increases faster than qubit count.** (Jack's hypothesis)

### Terms

- **Qubit count**: the number of qubits in the quantum processor.
- **CLOPS** (Circuit Layer Operations Per Second): a measure of how many circuit layers a quantum system can execute per second. It captures speed, not just size.
- **Classical control-system capacity**: the classical hardware and software that drives the quantum processor, such as control electronics, signal generation and readout, compilation, scheduling, and data throughput.

### Rationale

Each added qubit adds gates to drive and measurements to read out. If the classical control stack does not scale at least as fast as the qubit count, it becomes the bottleneck, and CLOPS falls even as the processor gets larger.

### What would support or refute it

- **Supports**: CLOPS drops as qubit count grows on systems whose control capacity grows slower than qubit count, and holds steady or rises where control capacity grows faster.
- **Refutes**: CLOPS drops with qubit count regardless of control capacity, or stays flat even when control capacity lags behind.

## Folder Contents

This folder is currently empty. Suggested layout as the project grows:

```
DOQuantum/
├── README.md     # this file
├── data/         # published CLOPS / qubit-count / control-system figures
├── notes/        # literature notes and meeting notes
├── analysis/     # scripts or notebooks
└── figures/      # plots for the write-up
```

## Status

- [ ] Define how control-system capacity will be measured or proxied
- [ ] Gather CLOPS and qubit-count data across systems
- [ ] Analyze the trend
- [ ] Write up results
