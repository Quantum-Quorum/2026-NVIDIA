# NVIDIA Challenge: Solving the LABS problem with a Quantum Enhanced and GPU Accelerated Workflow

## Overview

The Low Autocorrelation of Binary Sequences (LABS) problem is a notoriously difficult optimization challenge, critical for high-performance radar and telecommunications.

Your objective is to take the current classical state-of-the-art Memetic Tabu Search (MTS) and evolve it. Rather than jumping to a purely quantum solution, you will engineer a hybrid quantum-enhanced workflow where samples from a quantum algorithm are used to seed the classical MTS population. You must then push the limits of performance by GPU-accelerating both the quantum simulation and the classical search components.

**We want you to vibe code!**
In modern R&D and this challenge, speed matters, but rigor and coordination matter more. We expect you to employ Agentic Strategies, utilizing AI tools that can reason across your codebase to act as your collaborators while you operate as the Technical Leadership Team. Your collective job is to decompose the problem, delegate tasks across your team and AI agents, and most importantly verify the work. As Leads, you must clearly communicate your planning, workflow, and solution, ensuring your team remains aligned and ready to pivot even as technical challenges shift your strategy.

**Milestones and Evaluation**

This challenge is divided into four milestones, all of which are graded components of your final submission:

1. Ramp Up: Master the state-of-the-art for LABS via a scaffolded tutorial.
2. Research & Plan: Perform due diligence to design a custom quantum strategy and acceleration plan.
3. Build: Validate your algorithm on a CPU in qbraid, then migrate to Brev to deploy full GPU acceleration.
4. Showcase and Retrospective: Present your solution, performance metrics, and your AI-driven workflow.

## Logistics

In this challenge, you will mimic a real-world R&D pipeline, moving from rapid prototyping to high-performance deployment. You will utilize two distinct platforms, each chosen for a specific phase of your development lifecycle:

* **Phase 1 (Prototyping): qbraid**
    For the "Ramp Up" and initial CPU validation, you will work on Milestones 1 and 2 in qbraid. This is your "Dev Environment"—a zero-setup, pre-configured cudaq sandbox that allows you to focus entirely on mastering the algorithm and logic without worrying about infrastructure overhead.

* **Phase 2 (Acceleration): Brev**
    Once your logic is validated, you will "graduate" your code to Brev to complete Milestone 3 and 4. Brev provides on-demand access to a wide variety of NVIDIA GPU architectures (L4s, T4s, A100s, ...). You will use this platform to test your solution across different hardware configurations and unlock full GPU acceleration.

---

## Milestone 1: The Ramp Up (Scaffolded Tutorial)

*Goal: Understand the problem and the baseline algorithms.*

Your first task is to complete the provided scaffolded Jupyter Notebook (`labs_tutorial.ipynb`). This notebook guides you through:

1. Understanding the LABS symmetry and problem definition.
2. Running a classical Memetic Tabu Search (MTS).
3. Implementing a **Digitized Counterdiabatic Quantum Algorithm** using CUDA-Q.
4. Creating a hybrid workflow where the quantum algorithm seeds the Classical MTS.

*The Verification Challenge:* We are not providing an answer key. In scientific R&D, you rarely know the ground truth. You must prove to yourself (and us) that your code works before you build upon it.

*The Requirement:* You must add a "Self-Validation" section to the notebook. In this section, explain how you verified your results. Did you calculate solutions by hand for small N? Did you create unit tests?  Did you cross-reference your Quantum energy values against your Classical MTS results? Did you check known symmetries?

**Deliverable 1:** A completed, executable version of the `XXXXXXXlabs_tutorial.ipynb` notebook. This must include your new "Self-Validation" section containing code or text explaining how you verified your baseline results (e.g., manual calculation for N=3, unit tests for symmetries, or brute-force comparison for small N).

---

## Milestone 2: Research and Plan

*Goal: Define the Custom Solver, Plan the Acceleration, and Assign Roles.*

Your objective for the remainder of the challenge is to evolve the tutorial code in Milestone 1 into a high-performance, custom solver. You must plan for two specific technical projects:

1. **The Custom Quantum Seed:** Identify and implement a *different* quantum algorithm (e.g., QAOA, VQE, a custom Ansatz, etc.) or a variation of the Counteradiabatic approach to replace the Counterdiabatic approach from Milestone 1.
2. **Full GPU Acceleration:** Design a workflow that accelerates **both** the Quantum Algorithm (using CUDA-Q) and the Classical MTS on NVIDIA GPUs.

**Warning:** Do not rush this phase. The Delveriables from Milestone 1 along with the **Product Requirements Document (PRD)** you submit accounts for **40% of your final grade**.

### **Section 1: The Artifact (What is a PRD?)**

Think of your team as an early-stage startup. Your provided GPU credits are your Seed Funding. You have a finite "runway." If you burn through your budget on inefficient experiments, or the common novice mistake of leaving a "zombie" GPU instance running overnight, your venture halts before you can deliver your product.

In this challenge, your Product Requirements Document (PRD) is your safeguard against that fate. It is your business case for compute resources. Because your GPU credits are finite, you cannot afford to "move fast and break things." You must "plan fast and build correctly."

Your PRD defines exactly what you are building and how you will verify it works. It demonstrates that you are ready to use high-performance infrastructure like a professional: with intent, precision, and efficiency.

**A Note on Agility:** While you will submit this PRD early in the hackathon to unlock your compute credits and to be graded, adjustments to the PRD later in the hackathon may be required to ensure on-time delivery. If you pivot, you do not need to resubmit a new plan to the judges, simply communicate those changes to your teammates, and reflect on these pivots in the final presentation.

### **Section 2: Assign Your Technical Roles**

High-performance engineering teams do not work in silos. While every member will write code, debug, and contribute to the strategy, you need clear lines of accountability to prevent chaos.

Assign the following roles to act as the "Person in Charge" (PIC) for each domain. Being a lead does not mean you work alone; it means you orchestrate the team's effort in that area.  If you have more or less than 4 members of the team, some individuals may take on more than one role or some teammates may share a role.

* **Project Lead**
     * **Role:** You make the final decision on the algorithmic approach. You manage time, resources, and team communication. You are responsible for keeping the PRD updated if the strategy changes.
     * **Deliverable:** You own the **PRD** (Milestone 2) and are responsible for the **Final Submission Logistics** (ensuring all files, reports, and checklists are present and submitted on time).


* **GPU Acceleration PIC**
     * **Role:** You lead the GPU acceleration. You are the bridge between the code and the hardware.
     * **Deliverable:** You own the migration to Brev and the selection of GPU architectures. Crucially, you are responsible for Resource Management: you must decide which GPU to use (e.g., L4 vs. A100) based on cost-efficiency and ensure the team does not burn through the $20 credit by leaving instances running idle ("Zombie Instances").


* **Quality Assurance PIC**
     * **Role:** You are responsible for verifying that the human and the AI-generated code are correct. You protect the team from "AI Hallucinations."
     * **Deliverable:** You own the **Verification Strategy** and the **Unit Test Suite** (`tests.py`).


* **Technical Marketing PIC**
     * **Role:** You are the Analyst. You translate raw logs into insight. You are responsible for analyzing the run-data and proving the team's success through data visualization.
     * **Deliverable:** You own the **Final Presentation** and the **Success Metric Visualizations** (Milestone 4).



### **Section 3: Define Your Verification Strategy**

**Great engineering is not about guessing; it is about intent.** As part of your PRD, the QA PIC must commit to a verification strategy *before* you prompt your AI agents to write a single line of code.

> **A Note for the QA PIC: From "Sanity Check" to "System Check"**
> 
> In Milestone 1, we asked you to explain *how* you convinced yourself your tutorial code was correct. You may have conducted ad-hoc "Sanity Checks" (e.g., printing a small array and nodding your head that the result looked correct).
> **Now, you must professionalize that instinct.**
> In the next milestone (Build), you cannot rely on manual print statements. You must implement automated **Unit Tests**.
> * **For Example:** Instead of manually looking at `N=3` output, you will write a script that *asserts* `calculate_energy([1, -1, 1]) == 1.0` or `energy([1, -1]) == energy([-1, 1])`.
> * **Why?** You are about to use AI to generate code. If you don't have a reliable test suite, you will have no way to distinguish a brilliant code from a subtle hallucination. You need a way to check your work every time you make a change.
> * **Resource:** [Getting Started with Testing in Python](https://realpython.com/python-testing/).
> 
> 

### **Section 4: The Research Requirement**

To fill out your PRD, you must do the homework. You cannot simply guess a solution. You must answer:

* **Choice of Quantum Algorithm and Motivation:** Why did you choose this specific algorithm to challenge the tutorial's Counterdiabatic approach? Your reasoning can be metric-driven (expecting better Time to Solution, Approximation Ratio, circuit depth, etc.) or exploratory (e.g., selecting a foundational algorithm like QAOA to gain mastery, or testing a novel ansatz). Regardless of the motivation, you must cite papers to explain the theoretical interest of this algorithm.
* **GPU Acceleration:** How exactly will you accelerate the quantum and/or classical portions of the algorithm? (e.g., Will you use CUDA-Q's GPU-accelerated backends? Will you replace `numpy` with `cupy`? Will you explore batch-processing neighbors?) 

### **Section 5: Define Execution Tactics**

Finally, define the operational details of your workflow:

* **Agentic Workflow:** How will you orchestrate your AI agents? (e.g., "Agent A generates tests; Agent B refactors for CUDA").
* **Success Metrics:** Define your targets. (e.g., "We are targeting an Approximation Ratio > 0.85 for N=20," or "We aim to reduce the Classical Tabu Search runtime by 50% using CuPy for N>30").
* **Resource Management:** How will you manage your workflow so that you do not deplete your Brev credits? (e.g., "We'll set an alarm every 30 minutes to check that we don't have any instances running idly in the background." "We will test on an L4 GPU before attempting to run on an A100"). How will you allocate your $20 credit? Create a rough estimate. (e.g., "5 hours of dev on L4 ($5.00) + 4 hours of heavy benchmarking on A100 ($8.00) + Buffer ($4.00).")

### **Deliverable 2: The PRD Submission**

Submit a link to your `PRD.md` (hosted in your GitHub repo) to the **#challenge-submissions** Discord channel.

The **Project Lead** is responsible for submitting the link, but the document requires a specific section from each role:

1. **The Team:** List your members and their assigned roles.
2. **The Architecture (Written by Project Lead):** Define your quantum algorithm, your motivation, and cited literature.
3. **The Acceleration Strategy (Written by Acceleration PIC):** Define how you will use CUDA-Q, the specific GPU targets (L4 vs A100), and your resource management plans.
4. **The Verification Plan (Written by QA PIC):** Detail your strategy for Unit Tests and correctness checks (from Section 3).
5. **The Execution Strategy (Written by Tech Marketing PIC):** Define exactly which graphs you will plot (e.g., "Time vs. N"), what your success metrics are, and how you will visualize them.

**Once your PRD is submitted and approved by a mentor, you will receive your Brev credit allocation needed to complete Milestone 3, Step B. You may begin Step A of Milestone 3 in the interim.**

## Milestone 3: Build

*Goal: Implement, Test, and Accelerate.*

This milestone is broken into three three steps:

### Step A: CPU Validation

Implement your chosen custom quantum algorithm (from the PRD in Milestone 2) using CUDA-Q, running on a CPU backend in .

* **Requirement:** Demonstrate that your custom quantum-enhanced workflow finds valid solutions for small (e.g. N=3 to N=10).
* **Verification:** You must include a rigorous test suite (`tests.py`) covering your energy functions and quantum kernels.

### Step B: GPU Acceleration and Hardware Migration

Now that your logic is proven on qbraid's CPU backend, it is time to scale.

**The Migration:** Provision an instance on Brev. You must select a specific NVIDIA GPU architecture (we recommend starting with an L4 or T4) to serve as your target backend.
Next, migrate your code, switch your CUDA-Q target to the NVIDIA GPU backend, and begin your acceleration benchmarks.

Optional:  Rewrite your code for the quantum algorithm to exploit additional opportunities for parallelization.  Experiment with different GPUs or multiple GPUs.

* **Requirement:** Scale up. Run your simulation for larger N.  
* **Metrics:** Conmpute your success metrics as defined in your PRD and compare them to the CPU run (e.g., the time-to-solution and approximation ratio)

### Step C: GPU Acceleration of the classical algorithm

Carry out your GPU acceleration strategy to accelerate the classical MTS algorithm.  This might have been to replace numpy with cupy, or to rewrite the code to exploit further opportunities for parallelization.  Put this together with your work in step B.

* **Goal:** A fully GPU-accelerated workflow with comparisons made to the CPU-only runs and to the example from Milestone 1.

* **Tip:** Occasionally, refer back to your PRD.md to stay on track and/or make changes to your overall strategy based on progress.

---

## Phase 4: Showcase & Retrospective

*Goal: Communicate your results and your AI strategy.*

The final phase is about packaging your work. You will submit your code, a presentation, and a detailed report on how you utilized Artificial Intelligence.

### Part A: The AI Post-Mortem Report

We want to see how you leveraged AI to accelerate your development and, crucially, how you verified it.

**Format:** `AI_REPORT.md`
> **Note to Students:** > The questions and examples provided in the specific sections below are **prompts to guide your thinking**, not a rigid checklist. 
> * **Adaptability:** If a specific question doesn't fit your strategy, you may skip or adapt it.
> * **Depth:** You are encouraged to go beyond these examples. If there are other critical technical details relevant to your specific approach, please include them.
> * **Goal:** The objective is to convince the reader that you have employed AI agents in a thoughtful way.

**Required Sections:**

1. **The Workflow:** How did you organize your AI agents? (e.g., "We used a Cursor agent for coding and a separate ChatGPT instance for documentation").
2. **Verification Strategy:** How did you validate code created by AI?
* *Requirement:* You must describe specific **Unit Tests** you wrote to catch AI hallucinations or logic errors.


3. **The "Vibe" Log:**
* *Win:* One instance where AI saved you hours.
* *Learn:* One instance where you altered your prompting strategy (provided context, created a skills.md file, etc) to get better results from your interaction with the AI agent.
* *Fail:* One instance where AI failed/hallucinated, and how you fixed it.
* *Context Dump:* Share any prompts, `skills.md` files, etc. that demonstrate thoughtful prompting.



### Part B: The Presentation

You must produce a cohesive story of your project.

* **If In-Person:** A live 5-10 minute presentation to the judges.
* **If Remote:** A 5-10 minute voice-over slide deck (MP4 format) included in your final submission.

**Example Presentation Agenda:**

1. The Plan & The Pivot:

* Briefly outline your original strategy from the PRD. Did you stick to the plan? If you had to change your algorithm or acceleration strategy mid-stream, explain why. Engineering is about adaptation; tell us about the obstacles you overcame.

2. Results: 

* Present your results based on the Success Metrics defined in your PRD. For example, use charts to visualize your Time-to-Solution and Approximation Ratio compared to the baseline.

3. The Retrospective:

* Conclude with a personal touch. Each team member should share one specific technical or strategic takeaway from the challenge (e.g., "I learned that moving data to GPU is slower than computing on CPU if the batch size is too small").


---

## Resources

* **Tutorial:** [Provided `labs_tutorial.ipynb`]
* **Docs:** [NVIDIA CUDA-Q Documentation](https://nvidia.github.io/cuda-quantum/latest/index.html)
* **Vibe-coding:** [Cursor & The "Vibe" Workflow](https://youware.medium.com/cursor-for-vibe-coding-a-complete-guide-b0863d4a2330), [Responsible AI Coding: Best Practices](https://cloud.google.com/blog/topics/developers-practitioners/five-best-practices-for-using-ai-coding-assistants)
* **Reference:** [Scaling advantage with quantum-enhanced memetic tabu search](https://arxiv.org/html/2511.04553v1)
* **Reference:** [Parallel MTS by JPMorgan Chase](https://arxiv.org/pdf/2504.00987)

**Good luck. Let the agents build the code, you build the architecture.**
