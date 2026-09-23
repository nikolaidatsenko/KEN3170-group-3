# Cancer-causing Mutations Analysis

**Group**: Group 3

This notebook contains the analysis of a simplified cell regulatory Boolean network, including its original behavior and three mutated versions (p53 Knockout, MYC Amplification, and MDM2 Overexpression), as well as a user-defined mutation. For each network, scenario analysis, attractor analysis, and basin of attraction analysis were performed.

---

## Assignment Questions

### 1. Which mutation is most dangerous and why? Provide quantitative evidence.

**Answer**:

### 2. Explain the role of feedback loops (e.g., MYC → MDM2 → p53) in the network's behavior.

**Answer**:

### 3. What are the limitations of this Boolean network model? Discuss 3 specific limitations.

**Answer**:
*   **Limitation 1: Nodes can only be ON or OFF**: 

Since we are using a boolean model, every molecule is represented as a 0 or 1, Real molecules, can have much more than just 2 expressions, or activity levels. for example p53 activity could have a different effect that than a large amount at yet in the model they would have the same value and be represented as p53 = 1. The model cannot represent gradual changes, thresholds, or other representations that might be possible due to it have a boolean value. 

*   **Limitation 2: All nodes are updated synchronously and deterministically**: 

The boolean model updates all nodes at the same time during each step. In real cells, these processing that are happening each occur at different speeds. Protein production, degradation etc, they dont all happen at the same time. 


*   **Limitation 3 The network is very simplified**: 

The network only contains the eight nodes: DNA damage, p53, MYC, CDK2, MDM2, p21, Growth and Death, whereas real networks contain many more genes , proteins and interactions. For example, DNA damage is treated as a constant input in this model. A real cell may repair DNA damage over time, meaning the DNA-damage signal could change during the simulation. This Boolean network is useful for understanding basic relationships and mechanisms, but it is not a true representation of how cancer develops in real cells. 
