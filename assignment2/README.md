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

```
Maximal Biomass Production Rate: 0.8733 mmol/gDW/h
```

**Explain what this constraint would describe in contrast to the expression-based constraints implemented in the rest of the model.**

Setting an absolute flux bound of 5 mmol/gDW/h on the glucose exchange reaction (EX_glc__D_e) restricts the rate at which the cell can take up external glucose. This specific constraint models factors such as nutrient availability and transporter capacity. In contrast, gene expression constraints limit how fast internal enzymes can work based on how much of each protein is available inside the cell, rather than focusing on outside nutrients.

b.)

```
Maximal Biomass Production Rate: 0.4156 mmol/gDW/h
```

**Using the new glucose bounds, explain any differences you observe in the predicted maximal biomass production rate.**

The biomass rate dropped from 0.8733 mmol/gDW/h to 0.4156 mmol/gDW/h. This is because tightening the glucose upper limit to 5 mmol/gDW/h restricted the cell's carbon and energy supply. This shows that glucose was the limiting nutrient, as the lower external supply was directly bottlenecking the maximal growth rate.

## Q4: Glucose uptake sensitivity and exchange reaction activation

### Part A

A plot was prepared of the maximal biomass production rate as a function of the glucose exchange reaction flux bound, scanning the uptake bound over the interval [1, 15] mmol/gDW/h in increments of 0.1 mmol/gDW/h.

```
First activated at glucose uptake = 9.40 mmol/gDW/h
Newly active exchange reaction(s): {'EX_ac_e': np.float64(0.05367170526640648)}
```

![Biomass production as a function of glucose uptake bound](figures/q4_biomass_vs_glucose_uptake.png)

### Part B

**Does the growth rate increase indefinitely with increasing glucose exchange reaction flux bound?**

No, it maxes out at around 11 mmol/(gDW·h) of glucose intake. The biomass production rate increases linearly as glucose intake goes from 1 until around 9, when an increase in glucose results in a proportionally lower increase in biomass production rate. The relationship is still linear, but the slope is smaller in the interval around 9 to 11. Then at 11 there is a plateau as mentioned.

This is likely due to bottlenecks in the metabolic pathway. By looking at Escher, I...

### Part C

**At what glucose uptake rate does a new exchange reaction first become active, and which one?**

```
First activated at glucose uptake = 9.40 mmol/gDW/h
Newly active exchange reaction(s): {'EX_ac_e': np.float64(0.053671705266407514)}
```

### Bonus

Changing the glucose secretion bound (`upper_bound`) never changes the maximal biomass rate. The reason is that the optimiser will never pick a solution that secretes glucose, because doing so is suboptimal — so increasing the upper bound has no effect on the output.

A heatmap of biomass production as a function of both the glucose uptake bound (`|lower_bound|`) and the glucose secretion bound (`upper_bound`), varied independently, confirms this: biomass depends only on the uptake magnitude (x-axis) and is completely flat along the secretion-bound axis (y-axis).

![Biomass production vs. glucose exchange lower and upper bounds](figures/q4_bonus_heatmap.png)

---

## Conclusion

Overall, this assignment showed how much the *E. coli* core model's growth depends on the constraints you put on it. The expression data alone (Q1) already showed this network is way more complex than the simple pathway from the practical, with reaction capacities spanning a huge range and some reactions completely shut off.

Once we constrained glucose uptake (Q2/Q3), it became clear that glucose is the limiting factor for growth — cutting the bound to 5 mmol/gDW/h roughly halved the maximal biomass rate. The scan in Q4 showed this more clearly: growth increases almost linearly with glucose uptake at first, then slows down once acetate secretion kicks in around 9.4 mmol/gDW/h, and eventually plateaus completely once something else in the network becomes the bottleneck instead of glucose. This lines up with the acetate overflow behavior that's known to happen in *E. coli* when glucose is abundant.

The bonus part also made sense in hindsight: since FBA always optimizes for growth, the model will never choose to waste glucose by secreting it back out, so changing the secretion bound simply doesn't matter.

Overall, the exercises gave a good picture of how FBA can be used to find limiting nutrients and pinpoint where a metabolic network switches strategy as more resources become available.
