# Bell Inequalities and CHSH Violation with Qiskit

This repository contains a theoretical and computational study of Bell's theorem, the CHSH inequality, and the incompatibility between local hidden-variable theories and the predictions of quantum mechanics. The project develops the physics background from spin correlations and the Einstein-Podolsky-Rosen paradox, then implements a quantum-circuit experiment in Qiskit to show a violation of the CHSH bound.

The main report is written in LaTeX and is based on the seminar work:

> **Prueba del Teorema de Bell y violación desigualdad CHSH**  
> Lic. Julio A. Medina  
> Universidad de San Carlos de Guatemala, Escuela de Ciencias Físicas y Matemáticas  
> Maestría en Física

## Overview

Bell's theorem shows that no physical theory based on local hidden variables can reproduce all predictions of quantum mechanics. The CHSH inequality, introduced by Clauser, Horne, Shimony, and Holt, provides an experimentally testable form of Bell's theorem.

This project explains and demonstrates that quantum-mechanical correlations from entangled states can violate the classical CHSH bound:

\[
|\langle S \rangle| \leq 2
\]

while quantum mechanics can produce values larger than 2 for suitable measurement settings. The computational part uses Qiskit to construct entangled two-qubit states, define Pauli observables, estimate expectation values, and visualize CHSH inequality violations.

## Main Goals

- Explain the EPR paradox and its connection to locality, realism, and hidden-variable theories.
- Derive Bell-type inequalities from spin correlations in a two-particle singlet state.
- Introduce the CHSH inequality as an experimentally testable version of Bell's theorem.
- Build a two-qubit Bell-state circuit using Qiskit.
- Define CHSH observables with Pauli operators.
- Use Qiskit's estimator workflow to compute expectation values.
- Show that quantum predictions violate the classical CHSH limit.

## Physics Background

The theoretical discussion begins with a two-particle spin-singlet state:

\[
|\text{singlet}\rangle = \frac{1}{\sqrt{2}}\left(|\hat{z}+;\hat{z}-\rangle - |\hat{z}-;\hat{z}+\rangle\right).
\]

This state exhibits perfect anti-correlation when both particles are measured along the same axis. The report then discusses how this behavior becomes non-classical when different measurement bases are allowed.

The project covers:

- spin-\(1/2\) systems,
- angular momentum conservation,
- measurement correlations,
- local hidden-variable assignments,
- Bell's inequality,
- quantum-mechanical probabilities,
- and the geometric violation of Bell-type bounds.

## CHSH Inequality

The CHSH formulation considers two possible measurement bases for Alice and two possible measurement bases for Bob. With observables \(A\), \(a\), \(B\), and \(b\), one CHSH quantity is

\[
S_1 = A(B-b) + a(B+b),
\]

which leads to the inequality

\[
|\langle AB\rangle - \langle Ab\rangle + \langle aB\rangle + \langle ab\rangle| \leq 2.
\]

A second CHSH quantity is also considered:

\[
|\langle AB\rangle + \langle Ab\rangle - \langle aB\rangle + \langle ab\rangle| \leq 2.
\]

If local hidden-variable theories were sufficient to describe quantum correlations, these inequalities would always hold. The Qiskit implementation demonstrates that entangled quantum states can violate them.

## Qiskit Implementation

The computational experiment uses Qiskit to construct and evaluate a CHSH test. The implementation includes:

1. Construction of a Bell state:

   \[
   |\Phi^+\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}.
   \]

2. Application of parameterized rotations to vary the measurement basis.
3. Definition of Pauli observables using `SparsePauliOp`.
4. Evaluation of expectation values with Qiskit's estimator primitive.
5. Computation of CHSH values across several angles.
6. Visualization of the violation region where

   \[
   |\langle \text{CHSH} \rangle| > 2.
   \]

The report includes circuit diagrams and a CHSH violation plot showing points outside the classical limit.

## Suggested Repository Structure

A clean repository layout could look like this:

```text
.
├── README.md
├── Bell_inequalities_CHSH.tex
├── figures/
│   ├── spin_correlation_spin_singlet.png
│   ├── evaluation_P.png
│   ├── psi_state_circuit.png
│   └── CHSH_violation.png
├── notebooks/
│   └── chsh_qiskit_experiment.ipynb
├── src/
│   └── chsh_experiment.py
├── outputs/
│   └── chsh_results.csv
└── requirements.txt
```

The exact structure may differ, but separating the LaTeX report, source code, notebooks, figures, and generated outputs will make the repository easier to navigate.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### 2. Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

A minimal `requirements.txt` could include:

```text
qiskit
qiskit-aer
matplotlib
numpy
jupyter
```

Depending on the Qiskit version used, the estimator interface may require package-specific updates.

## Running the Experiment

If the project includes a Python script, run:

```bash
python src/chsh_experiment.py
```

If the project uses a notebook, open:

```bash
jupyter notebook notebooks/chsh_qiskit_experiment.ipynb
```

The expected output is a set of CHSH expectation values and a plot showing the violation of the classical bound \(\pm 2\).

## Building the LaTeX Report

To compile the report locally, run:

```bash
pdflatex Bell_inequalities_CHSH.tex
pdflatex Bell_inequalities_CHSH.tex
```

The second compilation helps resolve references and figure labels.

Make sure the image files referenced by the LaTeX document are available in the expected paths.

## Key Results

The project shows that:

- Bell inequalities follow from assumptions of locality and predetermined measurement outcomes.
- Quantum mechanics predicts correlations that cannot be reproduced by local hidden-variable theories.
- The CHSH inequality provides a practical experimental test of Bell's theorem.
- A Qiskit simulation of entangled qubits can produce CHSH values larger than the classical limit of 2.
- The result supports the standard conclusion that local hidden-variable theories are incompatible with quantum-mechanical predictions.

## References

The report discusses and cites foundational and pedagogical sources, including:

- J. S. Bell, *On the Einstein Podolsky Rosen Paradox*.
- J. F. Clauser, M. A. Horne, A. Shimony, and R. A. Holt, *Proposed Experiment to Test Local Hidden-Variable Theories*.
- A. Einstein, B. Podolsky, and N. Rosen, *Can Quantum-Mechanical Description of Physical Reality be Considered Complete?*
- J. J. Sakurai, *Modern Quantum Mechanics*.
- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
- R. P. Feynman, *Simulating Physics with Computers*.
- Qiskit documentation and textbook material.

## Notes for Future Improvements

Possible next steps for the repository include:

- Add a reproducible notebook with all Qiskit code used in the report.
- Save numerical CHSH results to a CSV file for validation.
- Include a dedicated `figures/` directory and update LaTeX paths accordingly.
- Add a small test script to verify that the computed CHSH values exceed 2 for selected angles.
- Document the Qiskit version used, since APIs such as `Estimator` may change across releases.
- Add an English abstract if the repository is intended for an international audience.

## License

Add a license that matches the intended use of this work. For academic repositories, common choices include MIT for code and Creative Commons licenses for written material.
