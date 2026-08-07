# Lecture Summary: Standardization & Z-Scores

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Standardizing normally distributed variables — SAT/ACT comparison and applications  
**Format:** Recorded lecture (~6+ min)

---

## Overview

This lecture focuses on **standardization** — rescaling data by subtracting the mean and dividing by the standard deviation to convert any Normal distribution into the **Standard Normal** N(0, 1). That gives a **universal metric (Z-scores)** for comparing values from different scales, units, or distributions.

The main example is **college admissions**: comparing **SAT** and **ACT** scores, which use different scales. Z-scores show which candidate performed better **relative to their exam population**, not just by raw score.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Standardization of normally distributed variables |
| **00:35** | Application of standardization in college admissions |
| **01:54** | Comparing SAT and ACT scores using Z-scores |
| **06:03** | Broader applications of standardization |

---

## Key Themes

### 1. What standardization does

**Formula:**

Z = (X − μ) / σ

| Step | Effect |
|------|--------|
| Subtract μ | Centers data at 0 |
| Divide by σ | Scales spread to 1 |

**Result:** Any X ~ N(μ, σ²) becomes Z ~ N(0, 1) — the **Standard Normal distribution**.

This removes the effect of different **units** and **magnitudes**, enabling fair cross-dataset comparison.

### 2. College admissions — SAT vs. ACT

**Problem:** SAT and ACT use different scales; raw scores aren't directly comparable.

**Example from the course notebook:**

| Exam | Distribution | Highest applicant score |
|------|--------------|-------------------------|
| **SAT** | N(1000, 200²) | 1350 |
| **ACT** | N(20, 5²) | 30 |

**Z-scores:**

- SAT: Z = (1350 − 1000) / 200 = **1.75**
- ACT: Z = (30 − 20) / 5 = **2.0**

**Conclusion:** The ACT top scorer is **2 standard deviations** above the ACT mean vs. **1.75** for SAT — so the ACT applicant performed better **relative to their exam population**, even though raw scales differ.

### 3. Why Z-scores beat raw comparison

- **1350 vs. 30** tells you nothing useful on its own
- **Z = 1.75 vs. Z = 2.0** answers: "How many σ above the mean is each score?"
- Both can be plotted on the **same Standard Normal curve** for visual comparison

### 4. Broader applications

Standardization is used wherever scales differ:

| Field | Use case |
|-------|----------|
| **Medicine** | Compare lab values to reference ranges |
| **Social sciences** | Compare test scores across instruments |
| **Business** | Normalize KPIs for benchmarking |
| **Machine learning** | Feature scaling (related concept) |

The common thread: a **consistent, unit-free metric** for informed decisions.

---

## Takeaways

1. **Standardization = (X − μ) / σ** — converts any Normal to N(0, 1).
2. **Z-score = "how many σ from the mean"** — positive above mean, negative below.
3. **Compare across scales with Z, not raw values** — essential for SAT vs. ACT and similar problems.
4. **Higher Z = better relative performance** — when comparing top performers across populations.
5. **Foundation for inference** — Z-scores underpin z-tests, confidence intervals, and many ML preprocessing steps.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Normal distribution & Z-scores (theory) | [`normal-distribution-lecture-summary.md`](normal-distribution-lecture-summary.md) |
| SAT calculations with SciPy | [`normal-distribution-scipy-sat-lecture-summary.md`](normal-distribution-scipy-sat-lecture-summary.md) |
| Hands-on SAT/ACT example | [`../Notebook_Inferential_Statistics.ipynb`](../Notebook_Inferential_Statistics.ipynb) |

---

## Quick reference

```python
# Z-score (manual)
z = (x - mu) / sigma

# SAT example: 1350 with mu=1000, sigma=200 → Z = 1.75
# ACT example:  30 with mu=20, sigma=5     → Z = 2.0  → ACT wins
```

**Interpretation:** Z = 1.75 means 1.75 standard deviations above the mean; compare Z-values across exams to rank relative performance.
