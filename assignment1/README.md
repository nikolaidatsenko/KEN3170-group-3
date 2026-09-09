# Epidemiological Model Assignment — Parameter Exploration

**Course**: KEN3170 — Multi-scale modeling of biological systems
**Group number**: 3

---

## 1. Repository overview
- `analysis.ipynb` — main notebook containing all required sections (Setup, Part 1–3, Conclusions)
- `requirements.txt` — Python dependencies (numpy, matplotlib, pandas, scipy, seaborn)
- `README.md` — this file

**How to run**: [e.g. `pip install -r requirements.txt` then open and run `analysis.ipynb` top to bottom]

---
## 2. Part 1 — Parameter analysis function
**Function**: `analyze_recovery_rates(beta, mu, N, I0, simulation_days)`
In Part 1, we implemented analyze_recovery_rates() using the SIRD model developed earlier in the practical. The function accepts the same baseline parameters as the original model but evaluates a range of recovery rates (γ). By looping through each γ value, the function runs the simulation and records four key metrics:

- Peak number of infectious individuals
- Day on which the infection peak occurs
- Total deaths at the end of the simulation
- Basic reproduction number, R₀ = β / γ

It then compiles these metrics into a pandas DataFrame and generates an epidemic curve comparison plot across all tested recovery rates.

In Parts 1.2 and 1.3, we evaluated recovery rates from γ = 0.05 to 0.25 using the parameter values established in Part 3 of the practical:

- β = 0.3
- μ = 0.01
- N = 1000
- Initial infected = 10
- Simulation duration = 150 days

This resulted in an Output DataFrame (γ = 0.05–0.25):
| gamma | R0  | peak_infected | peak_day | total_deaths |
|------:|----:|--------------:|---------:|-------------:|
| 0.05  | 6.0 | 479.7         | 26       | 165.4        |
| 0.10  | 3.0 | 269.1         | 27       | 83.6         |
| 0.15  | 2.0 | 136.8         | 30       | 47.7         |
| 0.20  | 1.5 | 57.4          | 33       | 26.0         |
| 0.25  | 1.2 | 18.0          | 30       | 11.4         |
---

## 3. Part 2 — Scenario comparison
- Result tables for Scenario A (High Transmission) and Scenario B (Low Transmission)

**Scenario A (High Transmission)**

| γ    | R₀   | Peak infected | Peak day | Total deaths |
|------|------|---------------|----------|--------------|
| 0.05 | 5.71 | 618.0         | 21.4     | 399.8        |
| 0.10 | 3.33 | 406.7         | 21.9     | 196.1        |
| 0.15 | 2.35 | 260.4         | 23.4     | 121.8        |
| 0.20 | 1.82 | 156.7         | 25.7     | 80.0         |
| 0.25 | 1.48 | 84.7          | 28.9     | 51.8         |

**Scenario B (Low Transmission)**

| γ    | R₀   | Peak infected | Peak day | Total deaths |
|------|------|---------------|----------|--------------|
| 0.05 | 3.64 | 405.7         | 43.7     | 98.0         |
| 0.10 | 1.90 | 156.3         | 51.3     | 39.9         |
| 0.15 | 1.29 | 38.1          | 65.9     | 15.4         |
| 0.20 | 0.98 | 5.0           | 0.0      | 2.3          |
| 0.25 | 0.78 | 5.0           | 0.0      | 0.5          |

- Which scenario is worse for public health, and why
High transmission is worse in almost every case. The only exception is when recovery rate and transmission rate are both low,
the outbreak tends to last for longer, despite resulting in less death and infections. A longer outbreak might
result in a longer lockdown, if the conditions are bad enough, regardless of the low transmission rate. Otherwise, total deaths,
the number of peak infections and the duration of the outbreak are all greater with a higher transmission rate. 


---

## 4. Part 3 — Policy recommendations
- 4.1 Parameter impact analysis
- 4.2 Intervention analysis
- 4.3 Real-world application

---

## 5. Conclusions
In summary, this report evaluated:

- Recovery Rate Dynamics: The impact of varying gamma parameters within an SIRD framework.
- Scenario Modeling: A direct comparison between high and low transmission environments.
- Policy & Intervention: Parameter impact assessments and the real-world application of a standard medical intervention.


