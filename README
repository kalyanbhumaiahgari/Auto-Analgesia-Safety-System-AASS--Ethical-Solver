# 🏥 Auto-Analgesia Safety System (AASS)

> **An AI & Ethics Project: Teaching a Medical AI to Make Safe, Ethical Decisions using Mathematical Logic.**

By: Kalyan Kumar B & Adam Brennan  
Course: COMP41820 – AI & Ethics (University College Dublin)

---

## 👋 1. What is this project?
Imagine a hospital machine that automatically gives pain medication (opioids) to patients after surgery. If the patient is in severe pain, the machine wants to help them (this is called **Beneficence**). However, opioids can dangerously slow down a patient's breathing (this is the rule of **Non-maleficence**—do no harm). 

This project explores how we can build an **Explicit Ethical Agent**—a software system that doesn't just guess what to do, but actually uses mathematical logic to *prove* that its decisions are 100% safe and ethically sound.

## ⚖️ 2. The Clinical Dilemma 
The system takes in data from the patient (like pain levels and breathing rate) and has to decide what to do. 

If a patient is in extreme pain, but their breathing is dangerously low, what should the machine do? 
* If it gives the drug, the patient might stop breathing.
* If it doesn't give the drug, the patient suffers in agony. 

This creates a logical "deadlock" (the machine freezes because two rules contradict). This project is all about how we programmed the AI to solve this deadlock safely without abandoning the patient.

## 🧠 3. The Ethical Rules We Used
Instead of letting an AI figure it out on its own, we translated human ethical frameworks into hard code:
* ❌ **Utilitarianism (Rejected):** This is the idea of "doing the most good for the most people" (like a cost-benefit analysis). We rejected this because a 5% chance of a patient stopping breathing is never an acceptable risk, no matter how much pain they are in.
* ✅ **Deontology (Strict Rules):** This means following absolute rules. We programmed the system with a strict Kantian rule: *Never administer drugs if breathing is low, and never administer without explicit consent.* Safety absolutely overrides pain relief.
* ✅ **Virtue Ethics (Practical Wisdom):** A "virtuous" doctor knows when a problem is too complex for them and asks for help. We programmed the machine to do the same. If it encounters a conflict, it doesn't guess—it triggers an alarm to call a human nurse.

## ⚙️ 4. How the Code Works (Formal Logic)
We didn't use a standard generative AI (like a neural network) because neural networks are basically just guessing machines. In a hospital, we can't have an AI guessing.

Instead, we used **Propositional Logic** (True/False math) and a tool called the **Z3 SMT Solver** (a super-calculator built by Microsoft that checks if logic rules are mathematically sound). 

We gave the system **4 Inputs (Sensors & State):**
* `p` = Patient is in pain? (True/False)
* `r` = Breathing is dangerously low? (True/False)
* `c` = Patient gave consent? (True/False)
* `n` = Is a nurse present to acknowledge the alarm? (True/False)

And **4 Outputs (Actions):**
* `d` = Give the opioid dose.
* `a` = Sound the medical alarm.
* `w` = Withhold the dose and wait.
* `e` = Escalate to the attending physician (if the nurse isn't around).

## 🛡️ 5. Proving it is 100% Safe (Verification)
The coolest part of using the Z3 Solver is that it provides **mathematical proofs**. 
* **Mutual Exclusivity Guarantee:** We asked the computer: *"Is there ANY possible scenario where you give the drug AND sound the low-breathing alarm at the exact same time?"* The computer outputted `UNSAT` (Unsatisfiable)—meaning it mathematically proved it will **never** accidentally overdose a patient while trying to warn the doctor.
* **Liveness Guarantee (No Abandonment):** We also proved that if the alarm goes off and the nurse doesn't answer, the machine will *always* escalate to the senior doctor. It will never just let the patient suffer in silence.

## 🤖 6. Why not just use ChatGPT? (LLMs vs. Symbolic AI)
We gave this exact same medical scenario to ChatGPT-4o to see what it would do. 

ChatGPT failed. Because it is a text-predictor, it tried to find a "compromise" and suggested we "lower the dose and monitor closely." In our binary medical hardware, we can't just "lower" the dose—the machine is either ON or OFF. 

If a system uses an LLM (like ChatGPT), it is probabilistic (it guesses based on words). If it makes a mistake and hurts someone, nobody is held accountable. Our Z3 logic model is **deterministic**—it acts exactly the same way every single time, giving a mathematical guarantee of safety.

## 🚧 7. Limitations & Future Work
While our logic model is 100% mathematically safe, real life is messier than simple "True" or "False" rules. 
* Right now, the system thinks 12 breaths-per-minute is perfectly safe (`False`), but 11 breaths is an absolute emergency (`True`). In reality, human biology is a sliding scale. This is known as the "Crisp Threshold" trap.
* In the future, this system should be upgraded using **Fuzzy Logic**, which allows the machine to understand concepts like "breathing is *slightly* low" rather than just safe vs. danger.


