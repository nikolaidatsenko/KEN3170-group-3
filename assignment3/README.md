# Cancer-causing Mutations Analysis

**Group**: Group 3

This notebook contains the analysis of a simplified cell regulatory Boolean network, including its original behavior and three mutated versions (p53 Knockout, MYC Amplification, and MDM2 Overexpression), as well as a user-defined mutation. For each network, scenario analysis, attractor analysis, and basin of attraction analysis were performed.

---

## Assignment Questions

### 1. Which mutation is most dangerous and why? Provide quantitative evidence.

**Answer**:

A, B and C are tied at 50% cancer rate. It's hard to say, from the biology alone, which is worse. A and C seem to be effectively the same, since they both have the role of knocking out p53. One could make the argument that B and C are worse since, on top of knocking out p53, they also activate malignant genes. However, according to these models, all these mutations are equally carcinogenic.

Cancer-like rate = percentage of all 256 initial states that end in an attractor with DNA_damage = 1, Growth = 1 and Death = 0.

| Network | Rule change | Attractors | Cancer-like states | Cancer-like rate | Stressed Cell outcome |
|---|---|---|---|---|---|
| Normal | none | 3 (all fixed points) | 8 / 256 | 3.1% | Death (apoptosis) |
| A: p53 Knockout | p53 = always OFF | 2 (all fixed points) | 128 / 256 | **50.0%** | Growth |
| B: MYC Amplification | MYC = always ON | 2 (all fixed points) | 128 / 256 | **50.0%** | Growth |
| C: MDM2 Overexpression | MDM2 = always ON | 2 (all fixed points) | 128 / 256 | **50.0%** | Growth |
| D: p21 Knockout | p21 = always OFF | 5 (3 fixed points, 2 limit cycles) | 8 / 256 | 3.1% | No steady state (oscillates) |

50% is the maximum possible rate, since DNA_damage is active in exactly half of all initial states.


### 2. Explain the role of feedback loops (e.g., MYC → MDM2 → p53) in the network's behavior.

**Answer**:

In this simplified model, the side that is active first suppresses the other, with no possibility of this changing. If they all start in the off state, the first to activate suppresses the other. Here the competition is between p53 (with p21) and MYC/MDM2: p53 inhibits MYC, MYC activates MDM2, and MDM2 inhibits p53. This loop contains two inhibitions, making it a positive feedback loop, which acts as a switch with two possible outcomes: p53 on with MYC/MDM2 off, or the other way around. With DNA damage, these two outcomes are two of the network's attractors: apoptosis (120/256 states) and cancer-like growth (8/256 states). Without DNA damage, p53 can never activate, so MYC/MDM2 always wins, giving the healthy growth attractor. Mutations A–C break this loop by fixing one of its nodes, so the switch can only go one way and the cancer rate rises from 3.1% to 50%.

A negative feedback loop (an odd number of inhibitions), in contrast, causes a node to switch itself off after turning on, which can lead to oscillations where the simulation never finds a stable state, as seen in the 3-node demo network.

### 3. What are the limitations of this Boolean network model? Discuss 3 specific limitations.

**Answer**:
*   **Limitation 1: Nodes can only be ON or OFF**:

Since we are using a boolean model, every molecule is represented as a 0 or 1, Real molecules, can have much more than just 2 expressions, or activity levels. for example p53 activity could have a different effect that than a large amount at yet in the model they would have the same value and be represented as p53 = 1. The model cannot represent gradual changes, thresholds, or other representations that might be possible due to it have a boolean value.

*   **Limitation 2: All nodes are updated synchronously and deterministically**:

The boolean model updates all nodes at the same time during each step. In real cells, these processing that are happening each occur at different speeds. Protein production, degradation etc, they dont all happen at the same time.


*   **Limitation 3 The network is very simplified**:

The network only contains the eight nodes: DNA damage, p53, MYC, CDK2, MDM2, p21, Growth and Death, whereas real networks contain many more genes , proteins and interactions. For example, DNA damage is treated as a constant input in this model. A real cell may repair DNA damage over time, meaning the DNA-damage signal could change during the simulation. This Boolean network is useful for understanding basic relationships and mechanisms, but it is not a true representation of how cancer develops in real cells. 

