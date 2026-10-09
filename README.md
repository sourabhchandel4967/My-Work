# My-Work
This repo contains reproduction of papers
# Reproduction Study — Strategic Commitments Shape Collective Cybersecurity under AI Inequality

## 1. Paper Information

**Title:** Strategic commitments shape collective cybersecurity under AI inequality  
**Authors:** Adeela Bashir, Zia Ush Shamszaman, Zhao Song, Matjaz Perc, The Anh Han  
**Journal:** *Chaos, Solitons & Fractals*  
**Year:** 2026  
**Volume:** 210  
**Article:** 118728  
**DOI:** 10.1016/j.chaos.2026.118728  
**arXiv:** 2605.09415

The paper studies collective cybersecurity using Evolutionary Game Theory (EGT), with particular attention to unequal access to AI-based defence, committed defenders, and subsidies/incentives.

> **Important:** The publisher states that no data was used for the research described in the article. The work is primarily a mathematical/computational evolutionary-game analysis.

---

## 2. Purpose of This Repository / Reproduction Work

The purpose of this reproduction study is to:

1. Understand the mathematical model used in the paper.
2. Re-implement the main equations in Python.
3. Reproduce the stationary distributions and social-welfare calculations.
4. Examine the effects of committed defenders (`z`) and subsidies.
5. Compare the published four-state formulation with the implementation available in the authors' GitHub repository.
6. Check whether the reported values in the paper can be reproduced independently.

This is an **independent reproduction/audit**, not a claim that the original authors' implementation has been exactly reconstructed.

---

## 3. Model Overview

The paper considers a finite population of organisations/players.

There are two main strategic dimensions:

### Attack strategy

- **A** = Attacker / attack
- **NA** = Non-attacker / no attack

### Defence capability

- **H** = High-level defence
- **L** = Low-level defence

Combining the two dimensions gives four population states:

1. `(A,H)` — attacker with high-level defence
2. `(A,L)` — attacker with low-level defence
3. `(NA,H)` — non-attacker with high-level defence
4. `(NA,L)` — non-attacker with low-level defence

The paper studies how the population moves between these states and what the long-run stationary distribution looks like.

---

## 4. Population and Evolutionary Dynamics

The baseline population size is:

```text
N = 100
```

The model is a **finite-population evolutionary game**.

Strategy changes are driven by evolutionary imitation and are represented using a **Fermi imitation function**.

The paper also considers rare mutation and an embedded Markov-chain formulation.

The long-run stationary distribution is represented by:

```text
π = [π(A,H), π(A,L), π(NA,H), π(NA,L)]
```

where each value represents the long-run probability/frequency of the corresponding state.

The stationary distribution satisfies:

```text
πM = π
```

where `M` is the transition matrix.

### Simple interpretation

- The transition equations describe **how the population moves**.
- The stationary distribution describes **where the population eventually settles in the long run**.

---

## 5. Differential AI Access

A central feature of the paper is that defenders can have different levels of AI-based defence.

The two levels are:

- **H:** high-level defence
- **L:** low-level defence

The model allows these groups to have different:

- attack costs
- attack benefits
- defence success probabilities
- security benefits
- defence costs
- potential losses

This represents **AI inequality** between organisations.

---

## 6. Payoff Functions

The model uses different payoff functions for attackers and defenders.

### Attacker with high-level defence

```text
f_A^H = -c_aH + b_aH(1-p_dH)
```

### Attacker with low-level defence

```text
f_A^L = -c_aL + b_aL(1-p_dL)
```

### Non-attacker

```text
f_NA^H = 0
f_NA^L = 0
```

### High-level defender against attack

```text
f_H^A = p_dH B_H - C_H - (1-p_dH)W_H
```

### Low-level defender against attack

```text
f_L^A = p_dL B_L - C_L - (1-p_dL)W_L
```

### High-level defender against a non-attacker

```text
f_H^NA = B_H - C_H
```

### Low-level defender against a non-attacker

```text
f_L^NA = B_L - C_L
```

---

## 7. Population Payoffs

With `z` committed high-level defenders, the average payoffs are calculated from the composition of the population.

For example:

```text
Π_H = [m_A f_H^A + (N-m_A)f_H^NA] / N
```

```text
Π_L = [m_A f_L^A + (N-m_A)f_L^NA] / N
```

The attacker payoff is:

```text
Π_A =
[(m_H+z)f_A^H + (N-z-m_H)f_A^L] / N
```

and:

```text
Π_NA = 0
```

These population payoffs are then used in the evolutionary transition process.

---

## 8. Fermi Imitation

The paper uses a Fermi-type imitation mechanism.

In simple terms, an individual is more likely to adopt another strategy when that strategy has a higher payoff.

The selection intensity is controlled by:

```text
β
```

A larger value of `β` means that payoff differences have a stronger influence on strategy updating.

The paper uses:

```text
β = 0.1
```

for the baseline analysis in the implementation examined here.

---

## 9. Committed Defenders

A key mechanism in the paper is the use of **committed defenders**.

Let:

```text
z = number of committed high-level defenders
```

Committed defenders are assumed to remain committed to the high-level defence strategy.

The purpose is to investigate whether a sufficiently large committed group can influence the overall population.

This is related to the idea of a **critical mass**.

### Simple interpretation

If enough organisations commit to strong defence, they may influence the wider population toward stronger cybersecurity behaviour.

---

## 10. Subsidy / Incentive Mechanism

The paper also investigates a subsidy for committed high-level defenders.

The subsidy changes the payoff of the high-level defence strategy.

The subsidy-adjusted high-level payoff used in the reproduction is:

```text
f_H^A(z) = f_H^A + (z/N)C_H
```

and:

```text
f_H^NA(z) = f_H^NA + (z/N)C_H
```

The purpose is to examine whether financial incentives can make strong defence more attractive and improve collective cybersecurity outcomes.

---

## 11. Baseline Parameters

The baseline parameters used in the reproduction are:

| Parameter | Value |
|---|---:|
| `N` | 100 |
| `c_aH` | 0.85 |
| `b_aH` | 1.90 |
| `c_aL` | 0.10 |
| `b_aL` | 1.60 |
| `p_dH` | 0.82 |
| `p_dL` | 0.75 |
| `B_H` | 0.75 |
| `B_L` | 0.55 |
| `C_H` | 0.41 |
| `C_L` | 0.20 |
| `W_H` | 0.22 |
| `W_L` | 0.10 |
| `β` | 0.1 |

---

## 12. Social Welfare

The paper evaluates social welfare using defender and attacker welfare.

```text
SW = SW_D + SW_A
```

where:

- `SW_D` = defender social welfare
- `SW_A` = attacker social welfare
- `SW` = total social welfare

The welfare calculation is based on the stationary probabilities of the four states.

For example, successful attacks are calculated as:

```text
π_succ =
π(A,H)(1-p_dH) + π(A,L)(1-p_dL)
```

This represents the probability of an attack succeeding against high- and low-level defence.

---

## 13. Published Random-Game Experiment

The paper reports a random-game analysis using:

```text
10,000 random games
```

with:

```text
β = 1
```

The published Table 7 reports the following results:

| Scenario | Attack Attempts | High Defence | Successful Attacks |
|---|---:|---:|---:|
| `z = 0` | 0.393 ± 0.077 | 0.583 ± 0.397 | 0.134 ± 0.124 |
| `z = 6` | 0.375 ± 0.072 | 0.806 ± 0.298 | 0.108 ± 0.109 |
| `z = 100` | 0.362 ± 0.064 | 1.000 ± 0.000 | 0.091 ± 0.094 |
| `z = 6`, subsidy | 0.360 ± 0.064 | 0.998 ± 0.024 | 0.088 ± 0.092 |

The random games are filtered so that:

```text
f_A^H < f_A^L
```

This represents the condition where attacking high-defence targets is less favourable than attacking low-defence targets.

---

## 14. Published Table 8

The paper reports the following social-welfare results:

| `z` | Subsidy | `SW_D` | `SW_A` | `SW` |
|---:|:---:|---:|---:|---:|
| 0 | No | 0.264 | 0.011 | 0.275 |
| 10 | No | 0.274 | -0.190 | 0.084 |
| 10 | Yes | 0.315 | -0.191 | 0.125 |

These values are an important benchmark for the reproduction.

---

## 15. Author GitHub Repository

The authors provide an implementation repository:

**EGT_Finite_Pop_CS_Analysis**

Repository:

```text
https://github.com/Adeela-Bashir/EGT_Finite_Pop_CS_Analysis
```

The repository contains MATLAB files including:

```text
Diff_Access_Analysis_Cyber_Security.m
Diff_Access_Analysis_Z_Subsidised.m
Finite_Pop_Analysis_Cyber_Security.m
README.md
```

The repository README states that the code uses:

```text
MATLAB R2020b+
```

---

## 16. Important Implementation Observation

The current GitHub repository contains a block-chain implementation that represents states using a larger state space.

For example, the implementation constructs states involving:

```text
(A, i)
(NA, i)
```

where `i` represents the number of ordinary high-level defenders.

This is related to, but is not written in exactly the same form as, the four-state macro-level formulation described in the paper.

The repository also contains parameters such as:

```text
dFD
gA
```

in the parameter structure, but these fields are not used by the main `stationary_block_chain` calculation examined during this reproduction.

Therefore, the repository should be treated as the **current available implementation**, rather than automatically assuming that every published table was generated by exactly this version of the code.

---

## 17. Reproduction Models Used

Two implementations were examined.

### Model A — Four-State Formulation

This follows the paper's macro-state description:

```text
(A,H)
(A,L)
(NA,H)
(NA,L)
```

The transition matrix is constructed from the four-state evolutionary process, and the stationary distribution is obtained from:

```text
πM = π
```

### Model B — Author GitHub Block-Chain Translation

This translates the main logic of the available MATLAB repository into Python.

The block chain explicitly represents the number of ordinary high-level defenders and the attack/non-attack state.

The stationary distribution is calculated using power iteration.

---

## 18. Reproduction Findings

An important result of this audit is that the reported Table 8 values were **not exactly reproduced** by either implementation tested.

### Four-state implementation

At the baseline:

```text
β = 0.1
```

the independent implementation produced approximately:

| `z` | Subsidy | `SW_D` | `SW_A` | `SW` |
|---:|:---:|---:|---:|---:|
| 0 | No | 0.266 | 0.093 | 0.360 |
| 10 | No | 0.281 | -0.036 | 0.245 |
| 10 | Yes | 0.301 | -0.036 | 0.266 |

These do not match the published Table 8 values.

### GitHub block-chain translation

The translated repository implementation also produced different values.

Approximately:

| `z` | Subsidy | `SW_D` | `SW_A` | `SW` |
|---:|:---:|---:|---:|---:|
| 0 | No | 0.268 | 0.152 | 0.420 |
| 10 | No | 0.255 | -0.248 | 0.007 |
| 10 | Yes | 0.296 | -0.248 | 0.048 |

Again, these do not match Table 8.

### Conclusion

The discrepancy is not simply a rounding difference.

At the current stage of reproduction:

> **Neither the independently implemented four-state formulation nor the current GitHub block-chain implementation reproduces the published Table 8 values exactly.**

This should be reported honestly rather than forcing the implementation to match the published numbers.

---

## 19. Why the Difference Matters

The paper describes the four-state Markov-chain formulation and gives the stationary-distribution framework, but it does not explicitly state which exact code version or implementation was used to generate every published numerical table.

The current GitHub repository also appears to contain an implementation that has evolved over time.

Therefore, possible causes of the discrepancy include:

- differences between the implementation used for the paper and the current repository;
- differences in transition-probability implementation;
- differences in how committed defenders are represented;
- differences in mutation or boundary treatment;
- differences in stationary-distribution calculation;
- differences in the exact welfare calculation;
- unpublished implementation details;
- changes between development and published code.

These are **possible explanations**, not confirmed causes.

---

## 20. Reproduction Workflow

The recommended workflow for this reproduction is:

```text
1. Read and understand the paper
        ↓
2. Extract model equations
        ↓
3. Implement payoff functions
        ↓
4. Implement Fermi imitation
        ↓
5. Construct transition process
        ↓
6. Calculate stationary distribution
        ↓
7. Calculate social welfare
        ↓
8. Test z = 0 and z = 10
        ↓
9. Add subsidy
        ↓
10. Compare with Table 8
        ↓
11. Translate/check author GitHub implementation
        ↓
12. Compare both implementations
        ↓
13. Record differences honestly
```

---

## 21. Files Used in This Reproduction

The main working notebook is:

```text
Paper2_Final_Reproduction_Colab.ipynb
```

Other audit notebooks include:

```text
Paper2_Deep_Reproduction.ipynb
Paper2_Exact_Reproduction_Audit.ipynb
Paper2_Table8_Reverse_Engineering.ipynb
Paper2_Compare_Both_Models_Table8.ipynb
```

A terminology/study guide was also prepared:

```text
Paper_2_Terminology_Study_Guide.docx
```

---

## 22. Main Concepts to Understand

Before presenting the reproduction, the following terms should be understood:

### Evolutionary Game Theory

A framework for studying how strategies change in a population when individuals receive different payoffs.

### Finite Population

A population with a fixed number of individuals rather than an infinite population.

### Fermi Imitation

A probabilistic rule describing how likely one individual is to copy another individual's strategy based on their payoff difference.

### Markov Chain

A mathematical model describing movement between different states.

### Stationary Distribution

The long-run probability of being in each state once the system has reached equilibrium/stationarity.

### Committed Defender

A defender that remains committed to the high-level defence strategy.

### Critical Mass

The approximate level of committed participation needed to substantially influence the population.

### Subsidy

An incentive that improves the payoff associated with strong defence.

### Social Welfare

The combined welfare of the defender and attacker populations:

```text
SW = SW_D + SW_A
```

---

## 23. Research Interpretation

The main research message of the paper is that **strategic commitment can influence collective cybersecurity**, particularly when organisations have unequal access to AI-based defence.

The model suggests that:

- unequal defence capabilities can affect attack behaviour;
- committed high-level defenders can influence the population;
- increasing commitment can increase high-level defence;
- subsidies can further encourage strong defence;
- collective cybersecurity outcomes depend on strategic interactions rather than on individual behaviour alone.

---

## 24. Reproducibility Statement

This work should be described as an **independent reproduction and implementation audit**.

The goal is not to artificially reproduce the published numbers by changing parameters until they match.

Instead, the approach is:

1. implement the equations as described;
2. implement the available author code where possible;
3. use the published parameters;
4. calculate the results;
5. compare the outputs with the paper;
6. document any discrepancies.

The fact that a numerical result does not exactly reproduce is itself a valid reproducibility finding.

---

## 25. Suggested Question for the Authors

If clarification is required, the following question can be sent to the authors:

> Could you please confirm which exact implementation/version was used to generate Table 8, including the code used to obtain the stationary distribution and welfare values? We have tested both the published four-state equations and the current GitHub block-chain implementation, but neither reproduces the reported Table 8 values.

This is preferable to assuming that one of the current implementations must be identical to the implementation used to produce the published table.

---

## 26. Key Takeaway

The paper develops a finite-population evolutionary game for cybersecurity under unequal AI access.

The model combines:

```text
Attack / No Attack
        +
High / Low Defence
        +
Committed Defenders
        +
Subsidies
        +
Evolutionary Dynamics
        ↓
Stationary Population Behaviour
        ↓
Cybersecurity Outcomes
        ↓
Social Welfare
```

The independent reproduction successfully reconstructs the main modelling framework, payoff structure, stationary-distribution approach, subsidy mechanism, and welfare calculations.

However, the published Table 8 values are **not exactly reproduced** by either the independently implemented four-state model or the current author GitHub block-chain implementation. This discrepancy is therefore retained as a documented reproducibility finding rather than being hidden or adjusted away.

---

## 27. Citation

Bashir, A., Shamszaman, Z. U., Song, Z., Perc, M., & Han, T. A. (2026). *Strategic commitments shape collective cybersecurity under AI inequality*. Chaos, Solitons & Fractals, 210, 118728.

DOI:

```text
10.1016/j.chaos.2026.118728
```

Author repository:

```text
https://github.com/Adeela-Bashir/EGT_Finite_Pop_CS_Analysis
```

---

## 28. Reproduction Status

**Model understanding:** Complete  
**Payoff implementation:** Complete  
**Four-state implementation:** Complete  
**GitHub block-chain translation:** Complete  
**Stationary distribution:** Implemented  
**Subsidy mechanism:** Implemented  
**Social welfare:** Implemented  
**Table 7 benchmark:** Documented  
**Table 8 benchmark:** Documented  
**Exact Table 8 reproduction:** **Not achieved**  
**Implementation discrepancy audit:** Complete

