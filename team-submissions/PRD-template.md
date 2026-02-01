# Product Requirements Document (PRD)

**Project Name:** Q-LABS-Solv-V1 (Quantum-Enhanced Low Autocorrelation Binary Seeker)
**Team Name:** QuantumVibes
**GitHub Repository:** [[Link](https://github.com/Quantum-Quorum/2026-NVIDIA)]

---

> **Note to Students:** The questions and examples provided in the specific sections below are **prompts to guide your thinking**, not a rigid checklist.
> * **Adaptability:** If a specific question doesn't fit your strategy, you may skip or adapt it.
> * **Depth:** You are encouraged to go beyond these examples. If there are other critical technical details relevant to your specific approach, please include them.
> * **Goal:** The objective is to convince the reader that you have a solid plan, not just to fill in boxes.

---

## 1. Team Roles & Responsibilities

| Role | Name | GitHub Handle | Discord Handle |
| :--- | :--- | :--- | :--- |
| **Project Lead** (Architect) | Vikramaditya Bansal | [@handle] | [@handle] |
| **GPU Acceleration PIC** (Builder) | Goutham Arcod | [@handle] | [@handle] |
| **Quality Assurance PIC** (Verifier) | Aditi Bhat & Sanskrith Singh | [@handle] | [@handle] |
| **Technical Marketing PIC** (Storyteller) | Rakshitha KV | [@handle] | [@handle] |

---

## 2. The Architecture
**Owner:** Vikramaditya Bansal (Project Lead)

### Choice of Quantum Algorithm
* **Algorithm:** Counteradiabatic (CD) Quantum Annealing Simulation via Trotterization.
* **Motivation:**
    * **Metric-driven:** We selected the Counteradiabatic approach because standard QAOA struggles with the "Barren Plateau" problem at higher $N$. The CD term ($H_{CD}$) suppresses diabatic transitions, allowing us to find the ground state (or near-ground state) with fewer Trotter steps than standard adiabatic evolution requires.
    * **Proven Results:** Our initial MVP testing on $N=18$ (CPU verification) demonstrated that this approach successfully finds the global minimum (Energy 26.0), whereas classical random initialization stagnates at local minima (Energy ~34.0).

### Literature Review
* **Reference:** *Scaling advantage in quantum simulation of optimization problems* (Ref 2.1 in Lab).
* **Relevance:** This paper establishes that quantum-enhanced populations can improve the Time-to-Solution (TTS) scaling for LABS. We aim to replicate the "slope" advantage shown in their results, demonstrating that our hybrid solver scales better than $\mathcal{O}(1.73^N)$.

---

## 3. The Acceleration Strategy
**Owner:** Goutham Arcod (GPU Acceleration PIC)

### Quantum Acceleration (CUDA-Q)
* **Strategy:** We employ a tiered execution model to maximize credit efficiency.
    * **Phase 1 (Current):** We use the `qpp-cpu` backend for logic verification. This has successfully verified the physics for small instances ($N=18$) without consuming GPU credits.
    * **Phase 2 (Planned):** For $N > 30$, we will target the `nvidia` (cuQuantum) backend. The state vector size doubles with every qubit, making CPU simulation intractable. We will utilize NVIDIA A100s to handle the exponential memory requirements.

### Classical Acceleration (MTS)
* **Strategy:** Our classical Memetic Tabu Search (MTS) relies on a custom $\mathcal{O}(N)$ "Delta Energy" update function in NumPy.
    * **Status:** Currently validated on CPU.
    * **Upgrade Path:** For the final benchmark, we plan to implement **Batch Evaluation**. Instead of flipping 1 bit at a time, we will evaluate the energy delta of all $N$ possible flips in parallel on the GPU using `cupy`, reducing the local search complexity from serial $\mathcal{O}(N)$ to parallel $\mathcal{O}(1)$.

### Hardware Targets
* **Dev Environment:** Qbraid (CPU) - **Currently Active**. Used for low-cost physics verification (Energy 26.0 confirmed).
* **Production Environment:** Brev A100-40GB - **Target**. Required for final N=40 simulations and tensor network contractions.

---

## 4. The Verification Plan
**Owner:** Aditi Bhat & Sanskrith Singh (Quality Assurance PIC)

### Unit Testing Strategy
* **Framework:** `unittest` / `pytest`
* **AI Hallucination Guardrails:**
    * **Physics Constraints:** Every solution returned by the AI-generated kernel is checked against the "Merit Factor" limit ($N^2 / 2E$). If a result implies a Merit Factor $> 13.0$ (theoretical impossibility), the result is flagged as a hallucination/error.
    * **Integer Safety:** We enforce strict `-1 / 1` integer casting to prevent "floating point drift" (e.g., getting Energy 25 instead of 26) which we identified and fixed during CPU testing.

### Core Correctness Checks
* **Check 1 (Symmetry):** The LABS Hamiltonian has $Z_2 \times Z_2$ symmetry. We assert that `Energy(Sequence) == Energy(-Sequence)` and `Energy(Sequence) == Energy(Reverse(Sequence))`.
* **Check 2 (Ground Truth $N=18$):**
    * **Requirement:** The Global Minimum for $N=18$ is known to be **26.0**.
    * **Test:** Our integration test must consistently produce Energy=26.0 for $N=18$. Any value higher indicates the solver is stuck; any value lower (e.g., 25.0) indicates a broken energy calculation. **[Status: PASSED on CPU]**

---

## 5. Execution Strategy & Success Metrics
**Owner:** Rakshitha KV (Technical Marketing PIC)

### Agentic Workflow
* **Plan:** We utilize a "Human-in-the-Loop" validation cycle.
    1.  **Generate:** The Architect prompts the AI to generate the physics kernel.
    2.  **Verify:** The QA Lead runs the "Ground Truth" test (Energy=26 check).
    3.  **Refine:** Initial runs showed "Impossible Physics" (Energy 25.0). We traced this to a "Zero Spin" bug in the AI code and refined the prompt to enforce strict binary states.

### Success Metrics
* **Metric 1 (Accuracy):** Achieve the global minimum for $N=18$ (Energy 26) in 100% of production runs. **[Status: ACHIEVED]**
* **Metric 2 (Quantum Advantage):** Demonstrate a strictly lower initial energy for Quantum Seeding ($E_{start} \approx 80$ for $N=20$) compared to Random Seeding ($E_{start} \approx 94$).
* **Metric 3 (Scale):** Successfully complete a hybrid optimization loop for $N=40$ within the hackathon time limit.

### Visualization Plan
* **Plot 1:** "Energy vs. Generation" waterfall plot. This will visually prove the "Jump Start" effect, where the Quantum (Green) line starts at a lower energy than the Classical (Grey) line.
* **Plot 2:** "Success Rate Histogram." A bar chart showing how often the Quantum solver finds the global minimum vs. how often the Classical solver gets trapped in local minima.

---

## 6. Resource Management Plan
**Owner:** Goutham Arcod (GPU Acceleration PIC)

* **Plan:** "The Zombie Protocol"
    * **Development:** All code logic (MTS class, Energy functions) is built and tested on free CPU tiers (Qbraid/Colab) to verify physics without cost.
    * **Validation:** We run the $N=18$ verification script on the CPU.
    * **Production:** We will only spin up the high-cost A100 instance for the final "hero run" ($N=40$).
    * **Kill Switch:** We have implemented a Python `try/finally` block in our main script that triggers an automatic shutdown when the benchmark completes, ensuring no "zombie" instances burn credits overnight.
