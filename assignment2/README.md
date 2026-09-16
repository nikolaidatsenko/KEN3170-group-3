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

The table we get is:
| Reaction | Lower bound | Upper bound |
|----------|------------:|------------:|
| PFK      | 0.0         | 13.1        |
| PFL      | 0.0         | 0.0         |
| PGI      | -11.1       | 11.1        |
| PGK      | -24.0       | 24.0        |
| PGL      | 0.0         | 7.3         |
| ...      | ...         | ...         |
| NADH16   | 0.0         | 40.1        |
| NADTRHD  | 0.0         | 1.3         |
| NH4t     | -1000.0     | 1000.0      |
| O2t      | -1000.0     | 1000.0      |
| PDH      | 0.0         | 26.6        |

For the full table please see the .ipynb file.

The ATPM line has the same lower bound as the practical and is: 
ATPM         8.39      1000.00

The EX_glc__D_e line reads as, using the default bounds from the practical: 
EX_glc__D_e     -1000.00      1000.00

## Q3: Flux Balance Analysis under glucose uptake constraints

a.)

```notebook-python
# carry out Flux Balance Analysis (FBA)
solution = model.optimize()

# report maximal biomass production rate
print(f"Maximal Biomass Production Rate: {solution.objective_value:.4f} mmol/gDW/h")
```

```
Maximal Biomass Production Rate: 0.8733 mmol/gDW/h
```

**Explain what this constraint would describe in contrast to the expression-based constraints implemented in the rest of the model.**

Setting an absolute flux bound of 5 mmol/gDW/h on the glucose exchange reaction (EX_glc__D_e) restricts the rate at which the cell can take up external glucose. This specific constraint models factors such as nutrient availability and transporter capacity. In contrast, gene expression constraints limit how fast internal enzymes can work based on how much of each protein is available inside the cell, rather than focusing on outside nutrients.

```notebook-python
# re-establish absolute flux bound on EX_glc__D_e
glucose = model.reactions.get_by_id("EX_glc__D_e")
glucose.lower_bound = -5.0
glucose.upper_bound = 5.0
```

b.)

```notebook-python
# carry out FBA on new glucose bounds
solution = model.optimize()

# report new maximal biomass production rate
print(f"Maximal Biomass Production Rate: {solution.objective_value:.4f} mmol/gDW/h")
```

```
Maximal Biomass Production Rate: 0.4156 mmol/gDW/h
```

**Using the new glucose bounds, explain any differences you observe in the predicted maximal biomass production rate.**

The biomass rate dropped from 0.8733 mmol/gDW/h to 0.4156 mmol/gDW/h. This is because tightening the glucose upper limit to 5 mmol/gDW/h restricted the cell's carbon and energy supply. This shows that glucose was the limiting nutrient, as the lower external supply was directly bottlenecking the maximal growth rate.
