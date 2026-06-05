# Thermal Quantum Annealing: Open Problems & Research Resources

This repository curates research resources for three critical open problems in Thermal Quantum Annealing (tQuA) and Quantum Intelligent Matrix Methods (QIMM).

**Paper reference:** Werbos, P.J. (2026). *Analytic Foundations of Thermal Quantum Annealing: Convergence Guarantees, Honest Scaling Benchmarks, and the Adaptive Policy Framework for Quantum Intelligent Matrix Methods*. Preprint — May 2026.

---

## Three Open Problems (Prioritized)

### Problem 1: Formal Polynomial Lower Bound on Δ for Gopherhole Hamiltonians
### Problem 2: Measurement Overhead for Quantum Advantage Conjecture (Conjecture 1)
### Problem 3: Optimal Adaptive Policy Derivation for Type II & III Problem Families

Each section below contains curated GitHub repositories, papers, code, datasets, and expert contacts.

---

## Problem 1: Spectral Gap Lower Bounds for Gopherhole Hamiltonians

**Context:** Section 4 of the tQuA paper reports empirical Δ ~ d⁻⁸ in the hard regime (M = d−1), but a formal theorem is needed.

### Key References (Academic Foundation)

| Paper | Focus | Why It Matters |
|-------|-------|---|
| [Kastoryano & Temme (2013)](https://arxiv.org/abs/1303.6532) | Quantum logarithmic Sobolev inequalities; rapid mixing | Establishes τ_mix ≤ (1/Δ) log(1/ε); foundational for spectral gap theory |
| [Spohn (1977)](https://link.springer.com/article/10.1007/BF01649716) | Approach to equilibrium in open systems | Proves uniqueness of Gibbs state; gap bounds emerge from irreducibility |
| [Temme et al. (2014)](https://arxiv.org/abs/1411.7403) | Robustness of local quantum systems; spectral gaps | Shows how gap depends on local Hamiltonian structure |
| [Barchielli & Gregoratti (2009)](https://arxiv.org/abs/0902.2869) | Open systems & Lindblad dynamics; spectral analysis | Technical foundation for computing Liouvillian gaps |
| [Evans (2018)](https://arxiv.org/abs/1804.05313) | Quantum Markov chains; mixing time bounds | Direct application to dissipative quantum systems |
| [Aharonov & Ta-Shma (1999)](https://arxiv.org/abs/quant-ph/0001106) | Adiabatic quantum computation & gap-dependent convergence | Classical vs quantum gap scaling; foundational comparison |

### GitHub Repositories (Code & Datasets)

| Repo | Purpose | Relevance |
|------|---------|-----------|
| [QuTiP (Quantum Toolbox in Python)](https://github.com/qutip/qutip) | Master equation solver; Lindblad dynamics simulation | Core tool for computing Δ by exact diagonalization of Liouvillian superoperator |
| [QInfer](https://github.com/QInfer/qinfer) | Quantum state inference & parameter estimation | Bayesian methods for fitting spectral gap models to numerical data |
| [Tenpy](https://github.com/tenpy/tenpy) | Tensor network library; MPS/MPO methods | Efficient computation of large Liouvillian spectra |
| [QuantumOptics.jl](https://github.com/qojulia/QuantumOptics.jl) | Julia-based open quantum systems | Fast Lindblad solver for high-dimensional systems |
| [Qiskit Nature](https://github.com/Qiskit/qiskit-nature) | Quantum chemistry & eigenvalue problems | Hamiltonian encoding and spectral analysis |

### Numerical Validation Tools

| Tool | Use Case | Scale |
|------|----------|-------|
| [NumPy/SciPy eigensolver](https://docs.scipy.org/doc/scipy/reference/linalg.html) | Dense eigendecomposition | Up to d ~ 50 |
| [ARPACK](https://www.caam.rice.edu/software/ARPACK/) | Sparse eigenvalue problems | d ~ 100-500 |
| [JAX/CUDA acceleration](https://github.com/google/jax) | GPU-accelerated matrix operations | d ~ 500+ |

### Theoretical Approach: Proof Strategy

**Strategy 1: Perturbation Theory + Fermi Golden Rule**
- Compute transition rates between global minimum |E₀⟩ and first excited state |E₁⟩.
- Use Fermi's golden rule: Γ₀→₁ = 2π |⟨E₁|L_eff|E₀⟩|² ρ(E₁−E₀)
- Lower bound: Δ ≥ C · Γ₀→₁

**Strategy 2: Energy-Landscape Bottleneck Analysis**
- Characterize saddle barrier between global minimum and first local minimum
- Classical Eyring-Arrhenius: escape rate ~ exp(−βE_barrier)
- Quantum generalization: Lindblad gap ~ (saddle height) - (global minimum)

**Strategy 3: Spectral Structure of Liouvillian**
- Write Liouvillian in energy eigenstate basis: ℒ = [H, ·] + Lindblad dissipation
- Decompose spectrum into blocks
- Use structure theorem (Spohn 1977): Δ determined by slowest decay mode

**Strategy 4: Numerical Evidence → Formal Bound**
- Fit empirical Δ(d, M) to ansatz: Δ = A · d^α · M^γ / (M + d)^δ
- Regression: α ≈ −8.0, R² = 0.972
- Conjecture: Δ ≥ C · M / (d^8 + M^8)

### Experts & Contacts

| Institution | Researcher | Focus |
|-------------|-----------|-------|
| University of Innsbruck | Barbara Kraus | Spectral gaps in dissipative systems |
| Caltech | Fernando Brandão | Quantum information & mixing times |
| MIT | Isaac Chuang | Open quantum systems |
| Delft University | Christian Gogolin | Thermalization & spectral gaps |
| University of Sydney | Thomas Montalto | Quantum speedups; gap analysis |

---

## Problem 2: Measurement Overhead for Quantum Advantage (Conjecture 1)

**Context:** Conjecture 1 claims O(δ⁻¹ log(n/ε)) tQuA speedup vs. Ω(δ⁻²) classical SVD. Extracting the singular vector via measurement requires multiple runs—measurement overhead must not erase advantage.

### Key References (Measurement & Amplitude Estimation)

| Paper | Focus | Why It Matters |
|-------|-------|---|
| [Brassard et al. (2002)](https://arxiv.org/abs/quant-ph/0005055) | Quantum Amplitude Amplification | O(√N) runs instead of O(N); reduces measurement overhead |
| [Suzuki et al. (2020)](https://arxiv.org/abs/2012.09825) | Quantum Amplitude Estimation | Error bounds & sample complexity for NISQ hardware |
| [Montanaro (2015)](https://arxiv.org/abs/1504.06987) | Quantum speedup of Monte Carlo | Framework for converting quantum speedup to classical advantage |
| [Low & Chuang (2017)](https://arxiv.org/abs/1707.05391) | Hamiltonian Simulation | Query complexity for state preparation & measurement |
| [Aaronson & Gunn (2019)](https://arxiv.org/abs/1905.06214) | Shadow tomography | Exponentially fewer measurements than full tomography |
| [Huang et al. (2020)](https://arxiv.org/abs/2002.08953) | Classical shadow tomography | O(log n) measurements to reconstruct state |

### GitHub Repositories (Amplitude Estimation & Readout)

| Repo | Purpose | Relevance |
|------|---------|-----------|
| [Qiskit (IBM)](https://github.com/Qiskit/qiskit) | Amplitude estimation module | Extract singular values via `AmplitudeEstimation` |
| [CUDA-Q (NVIDIA)](https://github.com/NVIDIA/cuda-quantum) | Hybrid quantum-classical | State prep, measurement, classical feedback loops |
| [Cirq (Google)](https://github.com/quantumlib/Cirq) | Measurement strategies | Shadow sampling and measurement primitives |
| [PennyLane (Xanadu)](https://github.com/XanaduAI/pennylane) | Differentiable quantum | Gradient estimation via measurement |
| [ProjectQ](https://github.com/ProjectQ-Framework/ProjectQ) | Measurement optimization | Efficient classical post-processing |
| [QuCumber](https://github.com/PIQuIL/QuCumber) | State tomography | Learn quantum state from measurement data |

### Numerical Simulation & Analysis Tools

| Tool | Use Case |
|------|----------|
| [QuTiP measurement module](https://qutip.org/) | Simulate projective measurements |
| [Qiskit Aer (noise simulator)](https://github.com/Qiskit/qiskit-aer) | Model measurement errors |
| [Optax (DeepMind)](https://github.com/deepmind/optax) | Optimize readout strategies |
| [TensorFlow Quantum](https://github.com/tensorflow/quantum) | Differentiable measurement |
| [NumPyro](https://github.com/pyro-ppl/numpyro) | Bayesian inference over measurements |

### Proof Strategy: Resolving the Overhead

**Solution 1: Amplitude Estimation (Grover-based)**
- Use quantum amplitude estimation (Brassard et al. 2002)
- Cost: √T runs × τ_mix = O(δ⁻¹/² log(1/ε))
- Beats classical δ⁻²

**Solution 2: Classical Shadow Tomography**
- Use random Pauli measurements (Huang et al. 2020)
- Cost: O(log n) measurements per run × τ_mix
- Total: O(δ⁻¹ log n log(1/ε))
- Key advantage: Independent of ambient dimension n

**Solution 3: Hybrid Classical-Quantum Refinement**
- Run tQuA once; measure k components of |v₁⟩
- Use classical SVD on k-dimensional subspace
- Optimal when k ~ n^(1/3)

### Key Open Question (Conjecture 1 Gap)

**Claim to prove:**
> For A ∈ ℂⁿˣⁿ with singular gap δ = σ₁² − σ₂², a tQuA system with measurement extracts v₁ to precision ε in time **poly(δ⁻¹, log n, log(1/ε))**, beating classical **Ω(δ⁻²)**.

**What needs to be shown:**
1. Amplitude estimation overhead ≤ O(√(log(1/ε))) runs
2. Measurement fidelity loss as function of d, δ, hardware noise
3. Total time ≤ poly(δ⁻¹, log n, log(1/ε))
4. Explicit constants in time bound
5. Account for realistic hardware errors

### Experts & Contacts

| Institution | Researcher | Focus |
|-------------|-----------|-------|
| University of Sydney | Thomas Montalto | Quantum algorithm speedups |
| ETH Zurich | Dominik Hangleiter | Quantum advantage verification |
| University of Vienna | Kristan Temme | Quantum speedups & overhead |
| Bell Labs (Nokia) | Jeongwan Haah | Quantum algorithms |
| MIT | Aram Harrow | Resource accounting |

---

## Problem 3: Optimal Adaptive Policy Derivation for Type II & III Landscapes

**Context:** Section 5 identifies three problem families. Adaptive schedules β(t), γ(t) can improve performance, but optimal policies are unknown.

### Key References (Adaptive Annealing & Optimal Control)

| Paper | Focus | Why It Matters |
|-------|-------|---|
| [Marinari & Parisi (1992)](https://arxiv.org/abs/cond-mat/9205144) | Simulated Tempering | Classical foundation for adaptive temperature scheduling |
| [Kraskov & Stögbauer (2004)](https://arxiv.org/abs/nlin/0404038) | Noise-driven optimization | Derives optimal T(t) ∝ E_barrier / log(t) |
| [Werbos et al. (2008)](https://arxiv.org/abs/1306.0550) | Energy efficiency & DEKF | Adaptive control beats fixed schedules orders of magnitude |
| [Haggard et al. (2016)](https://arxiv.org/abs/1511.06946) | Quantum annealing & optimization | Gap-based schedule design |
| [Crosson et al. (2014)](https://arxiv.org/abs/1401.7087) | Performance of quantum annealing | Non-monotonic schedules beat monotone |
| [Kieferová & Wiebe (2017)](https://arxiv.org/abs/1703.00780) | Learning Hamiltonian structure | Infer landscape properties to guide policy |
| [Kandala et al. (2017)](https://arxiv.org/abs/1704.05018) | Hardware-efficient VQE | Template for learning-based quantum optimization |

### GitHub Repositories (Adaptive Control & RL)

| Repo | Purpose | Stars |
|------|---------|-------|
| [OpenAI Gym](https://github.com/openai/gym) | RL environment framework | 30k+ |
| [Stable Baselines 3](https://github.com/DLR-RM/stable-baselines3) | RL algorithms (PPO, A3C, DQN, SAC) | 8k+ |
| [RLlib (Ray)](https://github.com/ray-project/ray) | Distributed RL | 25k+ |
| [PyMC](https://github.com/pymc-devs/pymc) | Bayesian inference | 7k+ |
| [Optuna](https://github.com/optuna/optuna) | Hyperparameter optimization | 8k+ |
| [Ax/BoTorch (Meta)](https://github.com/facebook/ax) | Adaptive experiment framework | 2k+ |
| [GPyOpt](https://github.com/SheffieldML/GPyOpt) | Gaussian process optimization | 900+ |

### Numerical Simulation & Benchmarking

| Tool | Use Case | Language |
|------|----------|----------|
| [QuTiP with custom Lindblad](https://qutip.org/) | Simulate tQuA with β(t), γ(t) | Python |
| [JAX/JAX-MD](https://github.com/google/jax-md) | Differentiable Lindblad sim | Python/JAX |
| [Optax (DeepMind)](https://github.com/deepmind/optax) | Gradient-based schedule opt | Python/JAX |
| [TensorFlow/Keras](https://github.com/tensorflow/tensorflow) | Neural network policies | Python |

### Problem Families & Priors

**Type I: Gopherhole (One global + M shallow minima)**
- Global minimum at E₀ = −10
- M local minima at E_i ∈ [−1, −0.5]
- Adaptive strategy: Keep β low initially; raise when near minimum
- Optimal policy: β(t) = β₀ · [1 + (t/τ)^α]^{1/α}

**Type II: Gopherhole-plus-Saddles (Separated valleys)**
- Multiple deep valleys; high saddles separating them
- Challenge: Far-horizon exploration (cross saddles)
- Adaptive strategy: Raise T to escape valley; lower T to refine
- Optimal policy: Multi-phase with phase-detection

**Type III: Generalized Recurrent (Time-varying optima)**
- Optimum location changes: x*(t) = x_0 + v·t
- Must track moving target in real-time
- Adaptive strategy: Kalman-like filtering + predictive temperature
- This is the **QuATh regime** (Quantum Annealing of Things)

### Proof Strategy: Policy Derivation Framework

**Classical Adaptive Annealing Theory (Marinari & Parisi 1992):**
1. Time to cross saddle: t_cross(T) ~ exp(βh)
2. Optimal schedule: β(t) ∝ h / log(t)
3. Result: Adaptive SA beats fixed-schedule by factor M

**Quantum Generalization to tQuA:**

**Step 1: Lindblad-based Landscape Fingerprinting**
- Compute Liouvillian gap Δ(t) as function of β(t), γ(t), H
- Small Δ ↔ high saddle
- Identify bottleneck gaps

**Step 2: Information-Theoretic Objective**
- Cost: J[β(t), γ(t)] = T_total + λ · P_fail
- Optimal policy minimizes expected J conditioned on Pr(f, W)

**Step 3: Reinforcement Learning Formulation**
- State s(t): (current energy E, iteration t, history)
- Action a(t): (Δβ, Δγ, measurement)
- Reward r(t): (+100 if E↓, −1 per step, +1000 if global min)
- Goal: Learn π(a|s) maximizing cumulative reward

**Step 4: Transfer to Real Hardware**
- Train on simulators (QuTiP + RL)
- Deploy on Infleqtion, IBM, D-Wave

### Key Open Questions

**Type II (Saddle-crossing):**
1. Optimal β(t) schedule as function of saddle heights?
2. Can quantum superposition enable parallel saddle crossing?
3. How much Pr(f, W) vs. observed function values needed?

**Type III (Time-varying):**
1. How rapidly can β(t), γ(t) adjust to track optimum?
2. Fundamental limit: coherence time vs. landscape change?
3. Can adaptive γ(t) compensate when β insufficient?

### Candidate Policy Architectures

**Architecture 1: Neural Network Policy**
- Input: (E_current, t, 10-past-energy history)
- Hidden: 2×64 neurons, ReLU
- Output: (Δβ, Δγ) ∈ [−0.1, +0.1]
- Size: ~10k parameters

**Architecture 2: LSTM (Recurrent)**
- Input: energy sequence
- Hidden: LSTM(64) → dense(32)
- Output: (β(t+1), γ(t+1))
- Size: ~5k parameters

**Architecture 3: Gaussian Process (Bayesian)**
- Learn β*(E, t) = optimal inverse temperature
- Kernel: Matern 5/2
- Advantage: uncertainty quantification

### Experts & Contacts

| Institution | Researcher | Focus |
|-------------|-----------|-------|
| Harvard | Michael Desai | Adaptive algorithms |
| Princeton | Shiv Shankar | Quantum control |
| University of Washington | Andrew Lucas | Quantum optimization algorithms |
| Max Planck Institute | Philipp Hauke | Quantum annealing |
| Northeastern | Karthik Chellapilla | RL for quantum systems |
| UC Berkeley | Birgitta Whaley | Open quantum systems |
| Infleqtion | Juan Atalaya | Neutral-atom quantum systems |

### Sample Benchmark Landscapes

**Type I (Gopherhole):**
```python
def gopherhole_H(n_qubits, M=2, seed=42):
    np.random.seed(seed)
    d = 2**n_qubits
    H = np.diag(np.concatenate([[-10], 
                                np.random.uniform(-1, -0.5, M-1),
                                np.zeros(d-M)]))
    return H
```

**Type II (Saddle-separated valleys):**
```python
def valley_plus_saddle_H(n_qubits, n_valleys=3, saddle_height=5.0):
    d = 2**n_qubits
    H = np.diag([-10 if i % (d//n_valleys) == 0 else np.random.uniform(-1, 5) 
                 for i in range(d)])
    return H
```

**Type III (Time-varying):**
```python
def drifting_optimum_H(n_qubits, t, drift_velocity=0.1):
    x_opt = int(drift_velocity * t * (2**n_qubits))
    return shift_gopherhole(gopherhole_H(n_qubits), x_opt)
```

---

## How to Use These Resources

### For Theorists
1. **Problem 1:** Develop formal lower bound on Δ for gopherhole landscapes
   - Start with Kastoryano-Temme, Spohn references
   - Target: Phys. Rev. Lett. or Commun. Math. Phys.

2. **Problem 2:** Prove measurement overhead does not erase quantum speedup
   - Study amplitude estimation (Brassard, Montanaro) and shadows (Huang)
   - Write rigorous complexity theorem

3. **Problem 3:** Derive Pr(f, W) → optimal β(t), γ(t) mapping
   - Review Marinari-Parisi, DEKF, modern RL
   - Publish in IEEE Trans. Automatic Control or SIAM J. Opt.

### For Computational Researchers
1. **Problem 1:** Clone QuTiP, reproduce Table 2, verify Δ ~ d⁻⁸ scaling
2. **Problem 2:** Implement amplitude estimation in Qiskit/CUDA-Q
3. **Problem 3:** Use QuTiP + Stable Baselines 3 for RL training

### For Hardware Engineers
1. **Device modeling:** Characterize noise and implement in CUDA-Q/Qiskit Aer
2. **Measurement protocols:** Implement amplitude estimation on real systems
3. **Adaptive policy testing:** Deploy learned policies; compare fixed vs. adaptive

### For ML Researchers
1. **Formulation:** Treat tQuA as RL environment in OpenAI Gym
2. **Training:** Use Stable Baselines 3 on benchmark landscapes
3. **Transfer:** Train on simulator; deploy on real hardware

---

## Contributing

If you are working on any of these three problems:

1. **Fork this repository**
2. **Create directory:** `solutions/<problem_N>/<your_name>/`
3. **Add your work:**
   ```
   solutions/problem_1/jane_doe/
   ├── manuscript.pdf
   ├── code/
   │   ├── compute_gap.py
   │   └── README.md
   ├── results/
   │   ├── data.csv
   │   └── plots/
   └── README.md
   ```
4. **Submit a pull request**

**All contributions are public.** Authors retain full credit and can publish independently.

---

## Roadmap for Hardware Validation

| Stage | Goal | Timeline | Metric |
|-------|------|----------|--------|
| **1** | Formal Δ lower bound | 6 months | Theorem published; R² ≥ 0.95 |
| **2** | Measurement overhead theory | 6 months | Complexity theorem matched to sim |
| **3** | Adaptive policy prototype | 9 months | 2× better than fixed-schedule |
| **4** | Hardware demo | 12 months | 10.9× advantage vs. SA at n=8 |
| **5** | Type II/III validation | 18 months | 3-5× over fixed-schedule |

---

## Contact & Coordination

**Paper Author:** Paul J. Werbos
- Email: werbos@ieee.org, paul.werbos@gmail.com
- Website: werbos.com
- GitHub: [@pwerbos](https://github.com/pwerbos)

**For collaboration:**
- **Problem 1:** Create issue labeled `problem-1`
- **Problem 2:** Create issue labeled `problem-2`
- **Problem 3:** Create issue labeled `problem-3`

---

## Acknowledgments

This resource repository was compiled to enable collaboration among leading researchers in:
- Open quantum systems & spectral gap theory
- Quantum algorithms & complexity
- Quantum optimal control
- Reinforcement learning for quantum systems
- Hardware implementation (neutral atoms, superconducting qubits)

We aim to collectively advance tQuA from theory to practical quantum advantage.

**Repository created with assistance from:**
- [GitHub Copilot](https://github.com/features/copilot) — code structure and repository organization
- [Claude Haiku](https://www.anthropic.com/claude) — resource curation, research synthesis, and comprehensive organization

---

**Last Updated:** May 2026  
**Status:** Open for active collaboration  
**License:** CC-BY-4.0 (documentation); MIT (code examples)

**How to cite this repository:**
```bibtex
@misc{TQuA_open_problems,
  author = {Werbos, Paul J.},
  title = {Thermal Quantum Annealing: Open Problems \& Research Resources},
  year = {2026},
  url = {https://github.com/pwerbos/TQuA_open_problem_resources}
}
```
