# Metabolic Modeling Assignment

**Course**: KEN3170 — Multi-scale modeling of biological systems
**Group number**: 3

---

## Repository overview
- `metabolic_analysis.ipynb` — main notebook containing all required code +answers
- `requirements.txt` — Python dependencies (cobra, pandas, csv)
- `README.md` — this file

**How to run**: [e.g. `pip install -r requirements.txt` then open and run `metabolic_analysis.ipynb` top to bottom]

---
## Q1: Flux Balance Analysis
a.)
After loading the provided reaction data into the Escher model, we came to this conclusion:

No, we do not observe the same thing. The reaction values in this dataset vary widely. These values range from 0.0 to 80.1 mmol/gDW/h. Unlike the linear pathway observed during the session, where mass balance forces have identical fluxes (v_1 = v_2), this metabolic network is more akin to a real metabolic network (extensive branching, loops, etc.).

b.)

The 2 different values observed are zero and no data (ND).
When a value is 0, it means that the reaction is present in the expression, however its maximal activity is 0. This is to show that the reaction has no available capacity.

## Q2: Establishing an enzyme activity-constrained metabolic model
