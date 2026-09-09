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

**Function**: `analyze_recovery_rates(beta, mu, N, I0, simulation_days)`
- For Part 1, We created a function called analyze_recovery_rates(). This function is uses the SIRD model we created during the practical. The function takes the same parameters when called as the SIRD function. Since the function has the calculate for a multitude of recovery rates, we created a for loop, where we for every recovery rate it runs the SIRD model, and calculates the following:

- Peak number of infectious individuals
- Day on which the infection peak occurs
- Total deaths at the end of the simulation
- Basic reproduction number, R₀ = β / γ

These are then stored and appended into results. 
Since the function needs to generate plots of all the recovery rates of a simulation, the function then creates a plot displaying all the different epidemic curves. All data is then converted into a pandas dataframe.

For part 1.2 and 1.3 we ran the gamma values (γ = 0.05–0.25), using the SIRD parameters from Part 3 of the practical:

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
- Which scenario is worse for public health, and why

---

## 4. Part 3 — Policy recommendations
- 4.1 Parameter impact analysis
- 4.2 Intervention analysis
- 4.3 Real-world application

---

## 5. Conclusions
