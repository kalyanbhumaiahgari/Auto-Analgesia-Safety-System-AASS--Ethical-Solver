# Auto-Analgesia Safety System (AASS) 
**COMP41820 - AI & Ethics | University College Dublin**  
**Authors:** Kalyan Kumar & Adam Brennan

## Project Overview
This repository contains the symbolic logic verification for the **Auto-Analgesia Safety System (AASS)**, a conceptual autonomous post-operative opioid administration pump. 

Autonomous medical devices operate in high-stakes environments where decisions carry immediate life-or-death consequences. Rather than relying on probabilistic Large Language Models (LLMs)—which our testing showed are highly susceptible to prompt-framing and will illegally "compromise" on safety rules—we modeled the system as an **Explicit Ethical Agent**. We encoded clinical ethical constraints using **Propositional Logic** and verified them exhaustively using the **Z3 SMT Solver**.

## Ethical Frameworks & Logical Mapping
We translated high-level philosophical frameworks into executable Boolean algebra:

* **Deontology (Categorical Safety):** We implemented the Kantian imperative of non-maleficence as a strict negative constraint. If patient respiration is dangerously low ($r$), the system is mathematically forbidden from dosing ($d$), regardless of pain levels. 
  * *Constraint:* `r -> Not(d)`
* **Virtue Ethics (Phronesis & Escalation):** A virtuous agent knows the limits of its own authority. If the system encounters a conflict (High Pain + Low Respiration), it triggers an Alert ($a$). 
* **Linear Temporal Logic (LTL) Liveness:** To avoid the "Immobility Paradox" (a machine that is perfectly safe because it does nothing while a patient suffers), we formalized an escalation pathway. If an alert fires and a nurse is absent ($\neg n$), the system *must* escalate ($e$) to a physician.
  * *Proof:* `e == And(a, Not(n))`

## Future Work: Overcoming the "Crisp" Threshold Trap
Our current Z3 implementation treats physiological states as crisp Boolean variables (e.g., respiration is either perfectly safe or totally failing). As covered in Week 7 of the module, ethical concepts are inherently graded phenomena. 

A future iteration of the AASS architecture should integrate **Fuzzy Logic** membership functions (e.g., grading respiration as $\mu_{low}(x)$ or $\mu_{critical}(x)$). This would allow for a graceful degradation of the opioid dosage rather than the binary "freeze" behavior exhibited by pure Propositional Logic.

## Files in this Repository
* `AASS_Z3_Implementation.ipynb`: The primary Jupyter Notebook (exported from Google Colab). It contains the complete Python code, the Z3 solver setup, the ethical deadlock demonstration, and the 16-scenario exhaustive truth-table evaluation.

## Running the Code Locally
To run the Jupyter Notebook on your local machine, you will need the Z3 theorem prover installed.

```bash
# Install the Z3 SMT Solver
pip install z3-solver

# Run Jupyter Notebook
jupyter notebook
