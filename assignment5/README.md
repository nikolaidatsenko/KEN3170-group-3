# Plant systems biology — Infection Analysis of Plant tissue

**Course**: KEN3170 — Multi-scale modeling of biological systems
**Group number**: 3

---

## 1. Repository overview
- `README.md` — this file

## Q1 — Initial Tissue Observations

| Initial | 30 min | 1 hr | 1 hr 30 min | 2 hr |
| :---: | :---: | :---: | :---: | :---: |
| ![Initial](initial.png) | ![30 min](30min.png) | ![1 hr](1hr.png) | ![1 hr 30 min](1hr30.png) | ![2 hr](2hr.png) |

## Simulation Timeline

| Time | Observation |
| :--- | :--- |
| **Initial** | From observation alone, there are two distinct shades of plant tissue and some kind of cell emerging from the left side. |
| **30 min** | The red cell on the left has now started to infect the healthy plant tissue (cyan). The healthy plant tissue is now turning a light purple-ish hue. The red cell has not moved/is the same size compared to initial observations. |
| **1 hr** | The infection from the red cell has now mostly spread to the sides of the tissue sample. As the red cell moves its way into the tissue, it manipulates and distorts the cell walls of the plant tissue. |
| **1 hr 30 min** | The red cell is now pushing deeper into the tissue. More of the healthy tissue is being infected by the red cell, with the cell walls being distorted as the red cell pushes its way forward. |
| **2 hr** | The red cell continues to grow in size. The result of this growth is causing more distortions in the cell walls, and at the same time, more healthy tissue is being infected. |

## Q2 — Function Analysis: `CellHouseKeeping`

### How is a cell's wall stiffness reduced as a function of its chemical level?

When the plant cell is healthy (chemical level near 0), the wall stiffness value remains at the maximum value of **3**. As the pathogen spreads, the wall stiffness is reduced. 

Based on the code snippet, because the chemical level is capped at **1.2**, the lowest the wall stiffness can drop to is **1.8**, which can be deduced using the reduction formula:

`stiffness_inf = 3 - (patho_chem_level)`

Low stiffness implies low wall rigidity, which from our observed screenshots, is why the walls stretch and distort with respect to the pathogen's position. 

### What does the pathogen do differently?

The pathogen differs from the regular plant cells because the code runs a check to see if it is Type 2. While it makes the surrounding cell walls weak and distorts them, the pathogen itself stays rigid. Because the pathogen remains rigid and capable of growing and splitting, it acts like a wedge, consistently pushing into the plant tissue and spreading the infection in the process. 


