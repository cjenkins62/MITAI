# Lecture Summary: F-Test for Comparing Two Variances

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Two-sample variance comparison — F-test, manufacturing quality control  
**Format:** Recorded lecture (~3+ min)

---

## Overview

This lecture covers **comparing variances between two independent samples**, with a focus on **manufacturing quality control**. The worked example compares the **weights of bags produced by two machines** — variability matters not only for meeting weight thresholds but for maintaining consistent production standards. The **F-test** compares the ratio of two sample variances against the F-distribution. A significant p-value flags a process that may be out of control. The lecture also previews **ANOVA** as the natural next step for comparing means across three or more groups.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Two-sample variance comparison |
| **01:23** | F-test for variance ratios |
| **02:54** | Application of F-test in quality control |

---

## Key Themes

### 1. Why compare variances between two groups?

In manufacturing, **variability is a quality metric** — not just the mean:

| Concern | Why variance matters |
|---------|---------------------|
| **Consistency** | Low variance = predictable, uniform output |
| **Process control** | High variance = process may need adjustment |
| **Comparing machines** | Is one line more stable than another? |

**Example:** Two machines fill bags to a target weight. Even if both hit the same average, one machine with much higher spread may produce under- or over-filled bags more often — a quality control problem.

---

### 2. Manufacturing example

**Research question:** Is there a significant difference in the variance of bag weights between Machine 1 and Machine 2?

**Data:** [`Bags1.csv`](../Bags1.csv) — two columns of bag weights (one per machine), assumed normally distributed.

```
H₀:  σ₁² = σ₂²     (equal variances)
H₁:  σ₁² ≠ σ₂²     (variances differ)     ← two-tailed (default)
α   = 0.05
```

**One-tailed alternative** (when direction matters):

```
H₁:  σ₁² > σ₂²     (Machine 1 is more variable)
H₁:  σ₁² < σ₂²     (Machine 2 is more variable)
```

Use a one-tailed test when you specifically want to know if one process is **out of control** relative to another.

---

### 3. F-test for variance ratios

The **F-test** compares two sample variances using the **F-distribution**.

**Test statistic:**

```
F = s₁² / s₂²

where s₁² = sample variance of group 1
      s₂² = sample variance of group 2
      df₁ = n₁ − 1   (numerator degrees of freedom)
      df₂ = n₂ − 1   (denominator degrees of freedom)
```

**Interpretation:**
- F ≈ 1 → variances are similar
- F >> 1 → group 1 is more variable
- F << 1 → group 2 is more variable

Compare F to the F-distribution with (df₁, df₂) to get the p-value.

**SciPy implementation (from course notebook):**

```python
import numpy as np
import pandas as pd
from scipy.stats import f

bagweight = pd.read_csv('Bags1.csv')

def f_test(x, y):
    x = np.array(x)
    y = np.array(y)
    test_stat = np.var(x, ddof=1) / np.var(y, ddof=1)
    dfn = x.size - 1
    dfd = y.size - 1
    p = (1 - f.cdf(test_stat, dfn, dfd))
    p_two_tailed = p * 2          # convert one-tail to two-tail
    return test_stat, p_two_tailed

stat, p_value = f_test(
    bagweight.dropna()['Machine 1'],
    bagweight.dropna()['Machine 2']
)
# p_value ≈ 5.1e-06
```

**Shortcut:** `scipy.stats.levene()` is a robust alternative when normality is questionable.

---

### 4. Assumptions

| Assumption | Requirement |
|------------|-------------|
| **Continuous data** | Weights, measurements on a continuous scale |
| **Normality** | Both populations normally distributed |
| **Independence** | Two separate machines → independent samples |
| **Random sampling** | Simple random sample from each process |

If normality is violated, prefer **Levene's test** over the F-test.

---

### 5. Interpreting results

**Result from the course notebook:**

```
p-value = 5.1e-06  (≈ 0.000005)
α       = 0.05

p-value << α  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. There is a statistically significant difference in the variances of bag weights between the two machines (p ≈ 5.1e-06)."

**Quality control action:** Investigate the more variable machine — check calibration, maintenance, or raw material consistency. One process may be out of control even if mean weights are similar.

**If p ≥ α:** Fail to reject H₀ — no significant evidence that variances differ; processes appear equally consistent.

---

### 6. F-test as a gateway test

The F-test serves two roles in the hypothesis testing toolkit:

1. **Direct question:** Are two processes equally consistent?
2. **Preliminary check:** Before a pooled two-sample t-test, verify σ₁² = σ₂²
   - If equal → use standard t-test (`equal_var=True`)
   - If unequal → use **Welch's t-test** (`equal_var=False`)

See [`hypothesis-testing-welch-t-test-sat-lecture-summary.md`](hypothesis-testing-welch-t-test-sat-lecture-summary.md) for the unequal-variance case.

---

## Takeaways

1. **Two-sample variance comparison** — F-test answers whether two groups have equal spread.
2. **F statistic** = ratio of sample variances: F = s₁²/s₂².
3. **Manufacturing context** — comparing bag weights from two machines; high variance = quality risk.
4. **Two-tailed default** — H₁: σ₁² ≠ σ₂²; use one-tailed when testing if one process is specifically more variable.
5. **Result:** p ≈ 5.1e-06 → reject H₀; machines differ significantly in consistency.
6. **Next up:** ANOVA extends this logic to comparing means across **three or more groups**.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| One-sample chi-square variance test | [`hypothesis-testing-variance-chi-square-lecture-summary.md`](hypothesis-testing-variance-chi-square-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Welch's t-test (unequal variances) | [`hypothesis-testing-welch-t-test-sat-lecture-summary.md`](hypothesis-testing-welch-t-test-sat-lecture-summary.md) |
| Bag weight data | [`../Bags1.csv`](../Bags1.csv) |
| Hands-on F-test code | [`../Notebook - Hypothesis Testing Optional Content.ipynb`](../Notebook%20-%20Hypothesis%20Testing%20Optional%20Content.ipynb) |
| Main hypothesis notebook | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Two-sample F-test for equal variances:
  H₀: σ₁² = σ₂²     H₁: σ₁² ≠ σ₂²

  F = s₁² / s₂²
  df₁ = n₁ − 1,  df₂ = n₂ − 1

  Assumption: both populations normally distributed

Bag weight example (Machine 1 vs Machine 2):
  p ≈ 5.1e-06  →  reject H₀ at α = 0.05
  → significant difference in process variability
```

**Remember:** Equal means do not imply equal variances — always check spread when assessing process quality.
