# 🧬 Binary-Coded Genetic Algorithm for Rosenbrock Function Optimization

> Comparing `eaSimple` vs `(μ + λ)` Evolutionary Strategies on a Classic Benchmark Problem

---

## 📌 Overview

This project implements and compares two **Binary-Coded Genetic Algorithm (BGA)** strategies for minimizing the **Rosenbrock function** — one of the most widely used benchmark problems in numerical optimization. Built using Python's [DEAP](https://deap.readthedocs.io/) (Distributed Evolutionary Algorithms in Python) framework, the project explores how different selection and reproduction strategies affect convergence behavior and solution quality.

The two algorithms implemented are:

| Strategy | Algorithm | Description |
|---|---|---|
| `eaSimple` | Simple EA | Standard generational GA with probabilistic crossover & mutation |
| `(μ + λ)` | Mu Plus Lambda | Elitist strategy where offspring compete with parents for survival |

---

## 🎯 Problem: The Rosenbrock Function

The **Rosenbrock function** (also known as the *banana function*) is a classic non-convex optimization problem:

```
f(x₁, x₂) = 100 * (x₂ - x₁²)² + (1 - x₁)²
```

**Constraints:**
- `x₁ ∈ [-5, 5]`
- `x₂ ∈ [-4, 4]`

**Global Minimum:**
- Located at `(x₁, x₂) = (1, 1)` where `f(1, 1) = 0`

The function is notoriously difficult to optimize due to its narrow, curved valley — making it an excellent test for evolutionary algorithms.

---

## 🧠 Algorithm Design

### Binary Encoding

Each decision variable is encoded as a **5-bit binary string**, giving a total chromosome length of **10 bits** for 2 variables.

- The binary value is decoded and linearly mapped back to the real-value domain using:

```
x = lower + ((upper - lower) / (2^bits - 1)) * decimal_value
```

### GA Parameters

| Parameter | Value |
|---|---|
| Population Size | 8 |
| Generations | 200 |
| Crossover Probability | 0.9 |
| Mutation Probability | 0.1 |
| Bit-flip Probability | 1 / chromosome_length |
| Crossover Operator | One-Point |
| Mutation Operator | Bit-flip |
| Selection | Best (`selBest`) |
| Random Seed | 42 (reproducible) |

---

## 📁 Repository Structure

```
.
├── EA_Lecture_02simple.ipynb          # eaSimple algorithm implementation
├── EA_Lecture_02_mupluslambda_.ipynb  # (μ + λ) algorithm implementation
└── README.md
```

---

## 📊 Results & Comparison

### `eaSimple` Strategy
- Best chromosome found: `1010011000`
- Decoded values: `x₁ = 1.452`, `x₂ = 2.194`
- **Best objective value: `0.949904`**
- Behavior: Explores widely throughout evolution; convergence is less stable but capable of escaping local optima.

### `(μ + λ)` Strategy
- Best chromosome found: `0111101111`
- Decoded values: `x₁ = -0.161`, `x₂ = -0.129`
- **Best objective value: `3.752547`**
- Behavior: Converges quickly (within ~30 generations) and maintains a steady best-fit solution; more stable but prone to premature convergence.

> **Key Insight:** `eaSimple` achieved a better objective value in this run, demonstrating that **exploration diversity** can outperform **greedy elitism** on landscape-sensitive problems like Rosenbrock.

---

## 🔬 Key Concepts Demonstrated

- **Binary Encoding & Decoding** of continuous variables
- **Fitness Landscape Analysis** using a benchmark function
- **Elitism vs. Generational Replacement** trade-offs
- **Convergence behavior** visualization across generations
- **DEAP framework** usage for evolutionary algorithm prototyping

---

## 🛠️ Tech Stack

- **Language:** Python 3.11
- **Framework:** [DEAP](https://deap.readthedocs.io/) — Distributed Evolutionary Algorithms in Python
- **Libraries:** NumPy, Matplotlib
- **Environment:** Jupyter Notebook

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install deap numpy matplotlib jupyter
```

### Run the Notebooks

```bash
# Clone the repository
git clone https://github.com/<your-username>/binary-ga-rosenbrock-optimization.git
cd binary-ga-rosenbrock-optimization

# Launch Jupyter
jupyter notebook
```

Open either notebook:
- `EA_Lecture_02simple.ipynb` — for the simple EA
- `EA_Lecture_02_mupluslambda_.ipynb` — for the (μ + λ) strategy

---

## 📈 Visualization

Both notebooks generate a **convergence plot** showing:
- 🔵 Best objective value per generation
- 🟠 Average objective value per generation

These plots allow direct visual comparison of how each algorithm navigates the Rosenbrock landscape over 200 generations.

---

## 📚 Background & Context

This project was developed as part of an **Evolutionary Algorithms** course. It introduces foundational GA concepts:

- **Binary Genetic Algorithms (BGA):** Represent solutions as bit strings
- **Selection Pressure:** How strongly the algorithm favors fitter individuals
- **Exploration vs. Exploitation:** The fundamental trade-off in all search algorithms
- **μ + λ Selection:** An elitist mechanism where the best μ individuals from the combined pool of μ parents and λ offspring survive

---

## 🤝 Contributing

Pull requests and suggestions are welcome! If you'd like to extend this project (e.g., add real-coded GA, test on other benchmark functions, or implement tournament selection), feel free to open an issue.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

*Built with curiosity and a love for nature-inspired computation.*
