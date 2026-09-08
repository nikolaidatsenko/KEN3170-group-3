# Epidemiological Model Assignment — Parameter Exploration

**Course**: KEN3170 — Multi-scale modeling of biological systems
**Group number**: [X]

---

## 1. Repository overview
- `analysis.ipynb` — main notebook containing all required sections (Setup, Part 1–3, Conclusions)
- `requirements.txt` — Python dependencies (numpy, matplotlib, pandas, scipy, seaborn)
- `README.md` — this file

**How to run**: [e.g. `pip install -r requirements.txt` then open and run `analysis.ipynb` top to bottom]

---

## 2. Part 1 — Parameter analysis function
**Function**: `analyze_recovery_rates(beta, mu, N, I0, simulation_days)`
- Brief description of your approach
- Output DataFrame (γ = 0.05–0.25), matching your notebook exactly

---

## 3. Part 2 — Scenario comparison
- Result tables for Scenario A (High Transmission) and Scenario B (Low Transmission)

Scenario A (High Transmission)
    γ	    R₀	    Peak infected	Peak day	Total deaths
    0.05	5.71	618.0	        21.4	    399.8
    0.10	3.33	406.7	        21.9	    196.1
    0.15	2.35	260.4	        23.4	    121.8
    0.20	1.82	156.7	        25.7	    80.0
    0.25	1.48	84.7	        28.9	    51.8

Scenario B (Low Transmission)
    γ	    R₀	    Peak infected	Peak day	Total deaths
    0.05	3.64	405.7	        43.7	    98.0
    0.10	1.90	156.3	        51.3	    39.9
    0.15	1.29	38.1	        65.9	    15.4
    0.20	0.98	5.0	            0.0	        2.3
    0.25	0.78	5.0	            0.0	        0.5

- Which scenario is worse for public health, and why
High transmission is worse in almost every case. However, when recovery rate and transmission rate are both low,
the outbreak tends to last for longer, despite resulting in less death and infections. A longer outbreak might
result in a longer lockdown, if the conditions are bad enough, regardless of the low transmission rate. 

---

## 4. Part 3 — Policy recommendations
- 4.1 Parameter impact analysis
- 4.2 Intervention analysis
- 4.3 Real-world application

---

## 5. Conclusions
