# Bell Inequalities and CHSH Violation in Qiskit

This repository contains the material for my seminar report **"Prueba del Teorema de Bell y violación desigualdad CHSH"**, written for the Master's program in Physics at the Universidad de San Carlos de Guatemala.

The project has two connected parts. First, it reviews the theoretical argument behind Bell-type inequalities, starting from the EPR discussion, spin correlations, and the idea of local hidden variables. Second, it implements a small Qiskit experiment where an entangled two-qubit state is prepared and CHSH observables are evaluated numerically.

The goal is to show the central point of Bell's theorem in a concrete way: if the correlations between Alice and Bob were produced by local hidden variables, they would obey a classical bound. Quantum mechanics predicts correlations that can go beyond that bound, and the Qiskit simulation reproduces that violation.

## What this repository is about

Bell's theorem separates two different ways of thinking about physical reality:

- **Local hidden-variable theories**, where measurement outcomes are assumed to be fixed in advance by local properties of the particles.
- **Quantum mechanics**, where entangled states can produce correlations that are stronger than any local hidden-variable explanation allows.

The report first discusses the problem using spin-singlet correlations. It then moves to the CHSH inequality, which is the version of Bell's theorem most commonly used in experimental and computational demonstrations.

In plain terms, local hidden-variable theories impose the classical CHSH bound:

```math
\lvert \langle S \rangle \rvert \le 2
```

Quantum mechanics can exceed this value for an appropriate entangled state and suitable measurement bases:

```math
\lvert \langle S \rangle \rvert > 2
```

This is the violation shown in the Qiskit part of the project.

## Contents

The report covers the following topics:

- EPR paradox and the question of whether quantum mechanics is complete.
- Spin-1/2 systems and spin-singlet states.
- Perfect anti-correlation when both particles are measured along the same direction.
- Bell's inequality from local hidden-variable assumptions.
- Quantum-mechanical probabilities for different measurement directions.
- CHSH inequality as an experimentally testable Bell inequality.
- Construction of Bell states with quantum circuits.
- Use of Pauli operators and Qiskit observables.
- Numerical evaluation of CHSH expectation values.
- Visualization of the region where the CHSH bound is violated.

## Main files

The central file is:

```text
Bell_inequalities_CHSH.tex
```

This is the LaTeX source of the full report.

The report also refers to auxiliary files and generated figures, including code snippets and plots such as:

```text
pauli_example.txt
observable
psi_state.txt
angles
Estimator
psi_state_circuit.png
CHSH_violation.png
evaluation_P.png
```

Depending on how the repository is organized, these files may be placed directly in the root directory or moved into folders such as `figures/`, `src/`, `snippets/`, or `notebooks/`.

## Theory summary

The starting point is the two-particle spin-singlet state. When two spin-1/2 particles are prepared in this state, measurements along the same direction are perfectly anti-correlated.

The singlet state is the antisymmetric Bell state:

```math
\lvert \psi^- \rangle = \frac{\lvert 01 \rangle - \lvert 10 \rangle}{\sqrt{2}}
```

The hidden-variable argument tries to assign definite outcomes in advance for measurements along different directions. Under locality, these preassigned outcomes imply Bell-type inequalities. One form discussed in the report can be written schematically as:

```math
P(\hat{a}^{+}; \hat{b}^{+}) \le P(\hat{a}^{+}; \hat{c}^{+}) + P(\hat{c}^{+}; \hat{b}^{+})
```

Quantum mechanics predicts probabilities that do not always satisfy this inequality. For a particular geometric choice of measurement directions, the report obtains a contradiction of the form:

```math
0.500 \nleq 0.292
```

The important point is not only the numerical mismatch. The contradiction means that the quantum prediction violates the restriction imposed by local hidden-variable reasoning.

## CHSH experiment

The CHSH version uses two possible measurements for Alice and two possible measurements for Bob.

In the report, Alice's observables are represented by:

```math
A, a \in \{IX, IZ\}
```

Bob's observables are represented by:

```math
B, b \in \{XI, ZI\}
```

One CHSH quantity is built from the combination:

```math
S_1 = A(B - b) + a(B + b)
```

Expanding this in terms of expectation values gives the classical bound:

```math
\lvert \langle AB \rangle - \langle Ab \rangle + \langle aB \rangle + \langle ab \rangle \rvert \le 2
```

A second equivalent CHSH expression is also considered:

```math
\lvert \langle AB \rangle + \langle Ab \rangle - \langle aB \rangle + \langle ab \rangle \rvert \le 2
```

In a local hidden-variable model, these quantities cannot exceed 2 in absolute value. In the quantum-circuit simulation, the expectation values are computed for an entangled state and the bound is violated.

## Qiskit implementation

The computational part uses Qiskit to prepare a Bell state and evaluate CHSH observables.

The Bell state used in the circuit is:

```math
\lvert \Phi^+ \rangle = \frac{\lvert 00 \rangle + \lvert 11 \rangle}{\sqrt{2}}
```

The circuit is built using:

- a Hadamard gate,
- a CNOT gate,
- a parameterized Ry rotation,
- Pauli observables constructed with `SparsePauliOp`, and
- Qiskit's estimator workflow to compute expectation values.

The Pauli operators represent measurements in different bases. The report discusses how strings such as `ZX` encode tensor products of Pauli operators acting on different qubits.

The experiment evaluates the CHSH observable for a sequence of angles and plots the resulting expectation values. The relevant result is that some points lie outside the classical interval:

```math
-2 \le \langle \mathrm{CHSH} \rangle \le 2
```

This is the numerical evidence of CHSH violation in the simulation.

## Expected result

When the experiment is run correctly, the output should include CHSH expectation values. At least some of them should satisfy:

```math
\lvert \langle \mathrm{CHSH} \rangle \rvert > 2
```

The report includes a plot named:

```text
CHSH_violation.png
```

where the violation is shown visually.

## Suggested repository structure

A clean organization for the repository would be:

```text
.
├── README.md
├── Bell_inequalities_CHSH.tex
├── figures/
│   ├── evaluation_P.png
│   ├── psi_state_circuit.png
│   └── CHSH_violation.png
├── snippets/
│   ├── pauli_example.txt
│   ├── observable
│   ├── psi_state.txt
│   ├── angles
│   └── Estimator
├── notebooks/
│   └── chsh_qiskit_experiment.ipynb
├── src/
│   └── chsh_experiment.py
└── requirements.txt
```

The repository does not need to follow this exact layout, but keeping the report, figures, snippets, notebooks, and source code separated makes the project easier to maintain.

## How to run the Qiskit experiment

Create a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

A minimal `requirements.txt` may look like:

```text
qiskit
qiskit-aer
numpy
matplotlib
jupyter
```

Run the experiment as a script:

```bash
python src/chsh_experiment.py
```

Or open the notebook:

```bash
jupyter notebook notebooks/chsh_qiskit_experiment.ipynb
```

The exact command depends on whether the implementation is stored as a script, a notebook, or code snippets included in the LaTeX report.

## How to compile the report

To compile the LaTeX report locally, run:

```bash
pdflatex Bell_inequalities_CHSH.tex
pdflatex Bell_inequalities_CHSH.tex
```

The second compilation helps resolve references and figure labels.

Make sure the referenced images and snippet files are available in the paths expected by the `.tex` file.

## Notes on Markdown math

The equations in this README use GitHub's fenced math-block syntax. This is intentional: it avoids the common rendering problems caused by placing dollar-delimited equations inside headings, lists, tables, or paragraphs.

The headings are plain text, and every display equation appears as its own independent math block. The full mathematical derivation remains in the LaTeX report, where longer derivations, labels, references, and figure captions are handled properly.

## References

The report cites foundational and pedagogical sources, including:

- J. S. Bell, *On the Einstein Podolsky Rosen Paradox*.
- J. F. Clauser, M. A. Horne, A. Shimony, and R. A. Holt, *Proposed Experiment to Test Local Hidden-Variable Theories*.
- A. Einstein, B. Podolsky, and N. Rosen, *Can Quantum-Mechanical Description of Physical Reality be Considered Complete?*
- J. J. Sakurai, *Modern Quantum Mechanics*.
- M. A. Nielsen and I. Chuang, *Quantum Computation and Quantum Information*.
- R. P. Feynman, *Simulating Physics with Computers*.
- N. David Mermin, *Quantum Computer Science: An Introduction*.
- Qiskit textbook and documentation material.

## Future work

Some natural next steps for this project are:

- move the Qiskit code from report snippets into a reproducible notebook or Python script,
- save the CHSH expectation values to a CSV file,
- add a short explanation of each generated figure,
- include instructions for running the same experiment on a simulator and, later, on IBM Quantum hardware,
- add a small section comparing the ideal simulator result with noisy real-device behavior.
