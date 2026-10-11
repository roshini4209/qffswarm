# Qiskit Fall Fest 2026 — Project Submission Template
**IIIT Kottayam Quantum Hackathon (24-Hour Sprint)**

> ⚠️ **CRITICAL INSTRUCTIONS FOR PARTICIPANTS:**
> 1. **Do NOT rename or delete the section headings** below. The automated AI evaluation and filtering system relies on this exact Markdown structure to parse and grade your project.
> 2. Replace all placeholder text enclosed in `[brackets]` with your project's details.
> 3. **Commit History Audit:** All project commits must be timestamped strictly within the 24-hour hackathon window (between **October 10, 2026 at 7:05 PM** and **October 11, 2026 at 7:05 PM**). Commits observed outside this window will result in **immediate disqualification**.
> 4. Ensure all Jupyter Notebooks have their cells **run and outputs displayed** before pushing.
> 5. Starter resources and reference guides are located in the [`references/`](./references/) folder.
> 6. **Tech Stack Flexibility:** You are free to use any external frameworks/technologies (e.g., Streamlit, React, Pygame, FastAPI, NetworkX) for your frontend, app logic, or classical baselines. However, **Qiskit MUST power the quantum core** of your project.
> 7. **Full Event Guide & Rules:** For full schedule details, track inspirations, submission steps, and grading focus areas, refer to [`HACKATHON_GUIDE.md`](./HACKATHON_GUIDE.md).

*(You may delete the instructions box above when preparing your final repository submission)*

---

# Project Title
Swarm-Quantum: Spatial Interference Optimization for Multi-Agent Robotics
## Project Metadata

* **Project Title:** Swarm-Quantum: Spatial Interference Optimization for Multi-Agent Robotics
* **Team Name:** Quantus
* **Chosen Track:** Track 2: Open-Domain Optimization & Real-World Solvers
* **Video Presentation Link:** https://drive.google.com/file/d/1PeZWOKCOcM2Pc2_WtRPjC3lsQUQ7e_PY/view?usp=sharing
  *(⚠️ Crucial: Ensure link access is set to "Anyone with the link can view" on Google Drive or "Unlisted / Public" on YouTube. Locked/inaccessible links cannot be scored!)*
* **Live Demo Timestamp in Video:** `[MM:SS]` *(e.g., "Demo starts at 03:45")*

### Team Members (Max 4 members)
| Name | Email | GitHub Username |
| :--- | :--- | :--- |
| Roshini G | roshinii42092gmail.com | @roshini4209 |



---

## 1. Project Overview & Motivation

* **Summary (3–4 sentences):**  
  This project formulates the pathing and spatial interference constraints of multi-agent swarm robotics as a combinatorial optimization problem. By representing collision risks and physical workspace bottlenecks as a weighted graph, we utilize the Quantum Approximate Optimization Algorithm (QAOA) to efficiently partition task nodes between two autonomous robots, minimizing spatial overlap.

* **Why this problem / game?**  
  As mechatronics systems and autonomous fleets scale, preventing collisions and optimizing task allocation becomes computationally explosive for classical systems. Spatial interference is a critical real-world dilemma in warehouse logistics, drone swarms, and smart manufacturing. Exploring how quantum algorithms can optimize these routing configurations offers a forward-looking solution to a genuine industrial bottleneck.

---

## 2. Quantum Architecture & Mechanics

* **Core Quantum Principles Used:**  
  The project leverages a QAOA Cost Hamiltonian. The spatial interference graph is mapped to a Max-Cut problem, which is then translated into a Quantum Ising Hamiltonian. Superposition and parameterized quantum circuits are utilized to explore the solution space, finding the ground state that minimizes the interference penalty between the robots.

* **How the Quantum Circuit is Integrated:**  
  The physical workspace is defined as a 5-node graph where edges represent interference penalties (e.g., tasks that are physically too close). The Qiskit QAOA circuit models this graph. Upon measurement, the resulting optimal bitstring dictates the task assignment (e.g., 0 for Robot A, 1 for Robot B), directly governing the physical deployment strategy of the mechatronic agents.

* **Circuit Details:**  
  * **Number of Qubits:** 5 (representing 5 spatial task nodes)
  * **Key Gates Used:** H (Superposition), RZ, CX (Entanglement for the cost Hamiltonian)
  * **Primitives Used:** StatevectorSampler
  * **Other Technologies Used:** networkx (for spatial graph generation), matplotlib (for workspace visualization), qiskit-optimization (for Quadratic Program translation).

```python
# Optional: Paste a representative snippet of your core Qiskit circuit code here
```

---

## 3. Repository Structure & How to Run

### Project Structure
```text
├── README.md               # Project documentation (this file)
├── requirements.txt        # Python dependencies
├── src/                    # Source code scripts or game application
│   └── main.py             # Main entry point (or streamlit app)
├── notebooks/              # Jupyter notebooks containing experiments
│   └── solution.ipynb      # Main runnable notebook with outputs
└── references/             # Hackathon reference guides (Track 1 & Track 2)
```

### Installation & Execution Instructions

> 💡 **Environment Recommendation:** To avoid package conflicts, we strongly suggest using a fresh Python virtual environment or Google Colab:
> ```bash
> python -m venv venv
> source venv/bin/activate    # On Windows: venv\Scripts\activate
> pip install -r requirements.txt
> ```

1. **Clone the repository:**
   ```bash
   git clone [your-repo-url]
   cd [your-repo-folder]
   ```
2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the project / demo:**
   ```bash
   # If running a script or CLI game:
   python src/main.py

   # If running a Streamlit web app:
   streamlit run src/app.py

   # Or open the Jupyter Notebook:
   jupyter notebook notebooks/solution.ipynb
   ```

---

## 4. Implementation Walkthrough & Live Demo

* **Walkthrough of Gameplay / Optimization Pipeline:**  
  Graph Generation: A spatial interference graph is generated using networkx, defining 5 tasks and 6 weighted edges representing collision risks.

   Translation: The graph is parsed into a Max-Cut problem and converted into a classical Quadratic Program, which is then mapped to a Quantum     Ising Hamiltonian (SparsePauliOp).

   Quantum Optimization: QAOA is initialized with the COBYLA optimizer (100 max iterations) and StatevectorSampler. The MinimumEigenOptimizer wraps the QAOA instance to solve the Quadratic Program.

   Physical Assignment: The quantum solver outputs an optimal bitstring. A 0 assigns the task node to Robot A (visualized in blue), and a 1 assigns it to Robot B (visualized in red), successfully isolating conflicting tasks

* **Key Screenshots / Terminal Output:**  
  ``
--- Optimization Results ---
Optimal Bitstring: [0. 0. 1. 1. 0.]

Nodes assigned to Robot A: [0, 1, 4]
Nodes assigned to Robot B: [2, 3]

--- Baseline Comparison ---
Quantum QAOA Bitstring:     [0. 0. 1. 1. 0.]
Classical Exact Bitstring:  [0. 0. 1. 1. 0.]

Success! The quantum algorithm matched the perfect classical baseline.


## 5. Classical vs. Quantum Comparison

* **Classical Baseline / Counterpart:**  
  To verify the quantum solution's accuracy, the exact same Quadratic Program was solved using a classical brute-force exact solver (NumPyMinimumEigensolver).

* **Comparative Analysis:**  
  The QAOA output successfully identified the exact optimal ground state. Both the quantum algorithm and the classical exact solver produced the optimal task distribution bitstring of [0. 0. 1. 1. 0.]. This confirms that the QAOA implementation is flawlessly navigating the Hilbert space for this instance scale and yielding a 100% feasibility and approximation ratio.
---

## 6. Performance, Results & Limitations

* **Key Results & Observations:**  
  The QAOA implementation rapidly converged to the optimal solution, effectively isolating Task 0, 1, and 4 to Robot A, and Tasks 2 and 3 to Robot B. This partitioning completely severs the highest-penalty spatial interference edges, proving the viability of using parameterized quantum circuits for multi-agent path deconfliction.

* **Critical Reflection on Limitations:**  
  While successful in simulation, deploying this on near-term intermediate-scale quantum (NISQ) hardware would introduce significant challenges. The current StatevectorSampler simulates an ideal environment. On a physical QPU, gate errors, readout noise, and decoherence would likely degrade the success probability of measuring the optimal bitstring. Furthermore, scaling this to a realistic mechatronic swarm of 50+ robots would require hardware with significantly more qubits and higher quantum volume than is currently available without severe barren plateau issues during the classical COBYLA optimization phase.

---

## 7. References & Acknowledgments

* Qiskit Optimization & QAOA Documentation
*  NetworkX Documentation
* IIIT Kottayam Quantum Hackathon Track 2 Reference Guides
