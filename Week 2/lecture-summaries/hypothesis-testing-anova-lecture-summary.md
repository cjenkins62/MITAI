# Lecture Summary: Analysis of Variance (ANOVA)

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** One-way ANOVA — comparing means across multiple groups, post-hoc Tukey HSD  
**Format:** Recorded lecture (~11+ min)

---

## Overview

This lecture introduces **Analysis of Variance (ANOVA)**, the standard method for comparing **means across three or more groups** with a single hypothesis test. When you have more than two groups, repeated t-tests inflate the Type I error rate — ANOVA solves this by partitioning total variability into **between-group** and **within-group** components. The worked example tests whether **carbon emissions differ by fuel type** (E85, LPG, Petrol) using [`AOVData.csv`](../AOVData.csv). ANOVA rejects H₀ (p ≈ 8.27e-06); **Tukey's HSD** follow-up identifies which specific pairs differ.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to Analysis of Variance (ANOVA) |
| **01:06** | Understanding variability in ANOVA |
| **01:48** | Historical context and applications of ANOVA |
| **03:10** | One-way ANOVA and its components |
| **07:14** | Assumptions and testing in ANOVA |
| **09:04** | Executing ANOVA and interpreting results |
| **10:27** | Post-ANOVA analysis: multiple comparisons |

---

## Key Themes

### 1. Why ANOVA instead of multiple t-tests?

| Approach | Problem |
|----------|---------|
| Compare 3 groups with 3 separate t-tests | Each test has α = 0.05 → family-wise error rate >> 5% |
| **One-way ANOVA** | Single test controls α across all groups |

**When to use ANOVA:**
- One **factor** (categorical predictor) with **3+ levels**
- **Continuous response** variable (e.g., emissions, yield, satisfaction score)
- Question: Do **any** group means differ?

For exactly 2 groups, use a two-sample t-test instead.

---

### 2. Understanding variability

ANOVA decomposes total variance into two sources:

```
Total variability = Between-group variability + Within-group variability

Between-group:  Do group means differ from the grand mean?
Within-group:   How much do individual observations vary within each group?
```

**F-statistic:**

```
F = MS_between / MS_within
  = (variance due to group differences) / (variance due to random error)

Large F → group means differ more than expected by chance alone
```

Compare F to the F-distribution to get the p-value. See [`hypothesis-testing-f-test-variance-lecture-summary.md`](hypothesis-testing-f-test-variance-lecture-summary.md) for the related F-distribution concept.

---

### 3. Historical context

ANOVA was developed by **R.A. Fisher** in the 1920s for **agricultural research** — comparing crop yields across different fertilizer treatments. Today it applies broadly:

- Industrial quality control (process settings)
- Marketing (campaign performance across segments)
- Environmental science (emissions by fuel type)
- Clinical trials (treatment groups)

---

### 4. One-way ANOVA example — carbon emissions by fuel type

**Research question:** Does the amount of carbon emission depend on fuel type?

**Data:** [`AOVData.csv`](../AOVData.csv) — 510 cars, three fuel types:

| Fuel type | n | Mean CO emissions |
|-----------|---|-------------------|
| E85 | 161 | 338.12 |
| LPG | 170 | 363.74 |
| Petrol | 179 | 371.72 |

**Hypotheses:**

```
H₀:  μ_E85 = μ_LPG = μ_Petrol     (all group means equal)
H₁:  At least one mean differs
α   = 0.05
```

**Response variable:** `co_emissions`  
**Factor:** `fuel_type` (3 levels)

---

### 5. Assumptions and checking them

| Assumption | Test | Result (course notebook) |
|------------|------|--------------------------|
| **Normality** of response | Shapiro-Wilk | p = 0.498 → fail to reject H₀ ✓ |
| **Equal variances** (homogeneity) | Levene's test | p = 0.194 → fail to reject H₀ ✓ |
| **Independence** | Study design | Random sample ✓ |
| **Simple random sampling** | Study design | Verified ✓ |

```python
from scipy import stats
from scipy.stats import levene, f_oneway

# Normality
w, p_norm = stats.shapiro(aovdata['co_emissions'])   # p ≈ 0.498

# Equal variances
stat, p_levene = levene(
    aovdata.loc[aovdata['fuel_type'] == 'Petrol', 'co_emissions'],
    aovdata.loc[aovdata['fuel_type'] == 'E85', 'co_emissions'],
    aovdata.loc[aovdata['fuel_type'] == 'LPG', 'co_emissions']
)   # p ≈ 0.194
```

If assumptions fail, consider Welch's ANOVA or non-parametric alternatives (Kruskal-Wallis).

---

### 6. Executing one-way ANOVA

```python
from scipy.stats import f_oneway

test_stat, p_value = f_oneway(
    aovdata.loc[aovdata['fuel_type'] == 'Petrol', 'co_emissions'],
    aovdata.loc[aovdata['fuel_type'] == 'E85', 'co_emissions'],
    aovdata.loc[aovdata['fuel_type'] == 'LPG', 'co_emissions']
)
# p ≈ 8.27e-06
```

**Result:**

```
p-value ≈ 8.27e-06
α       = 0.05

p-value << α  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. At least one fuel type has a significantly different mean carbon emission (p ≈ 8.27e-06)."

**Limitation:** ANOVA tells you *that* a difference exists — not *which* groups differ. That requires a **post-hoc test**.

---

### 7. Post-ANOVA: Tukey's HSD

**Tukey's Honestly Significant Difference (HSD)** compares all pairs of group means while controlling the family-wise error rate.

```python
from statsmodels.stats.multicomp import pairwise_tukeyhsd

m_comp = pairwise_tukeyhsd(
    endog=aovdata['co_emissions'],
    groups=aovdata['fuel_type'],
    alpha=0.05
)
print(m_comp)
```

**Results:**

| Pair | Mean diff | p-adj | Significant? |
|------|-----------|-------|--------------|
| E85 vs LPG | 25.62 | 0.0012 | Yes |
| E85 vs Petrol | 33.60 | 0.0000 | Yes |
| LPG vs Petrol | 7.98 | 0.4916 | No |

**Interpretation:**

- **E85** emissions are significantly **lower** than both LPG and Petrol
- **LPG and Petrol** are **not significantly different** from each other
- E85 appears to be the cleaner fuel option in this dataset

---

## Takeaways

1. **ANOVA** compares means across 3+ groups in a single test — avoids multiple-comparison inflation.
2. **H₀:** all group means equal; **H₁:** at least one differs.
3. **F-statistic** = between-group variance / within-group variance.
4. **Assumptions:** normality, equal variances, independence — check before interpreting.
5. **Fuel type example:** p ≈ 8.27e-06 → reject H₀; emissions differ by fuel type.
6. **Tukey HSD** pinpoints which pairs differ — E85 vs others, not LPG vs Petrol.
7. **ANOVA is omnibus** — always follow a significant result with post-hoc comparisons.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Two-sample t-test (2 groups) | [`hypothesis-testing-two-sample-t-test-lecture-summary.md`](hypothesis-testing-two-sample-t-test-lecture-summary.md) |
| F-test (variance comparison) | [`hypothesis-testing-f-test-variance-lecture-summary.md`](hypothesis-testing-f-test-variance-lecture-summary.md) |
| Chi-square independence (categorical) | [`hypothesis-testing-chi-square-independence-lecture-summary.md`](hypothesis-testing-chi-square-independence-lecture-summary.md) |
| Hypothesis testing template | [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| Emissions data | [`../AOVData.csv`](../AOVData.csv) |
| Hands-on ANOVA + Tukey code | [`../Notebook - Hypothesis Testing Optional Content.ipynb`](../Notebook%20-%20Hypothesis%20Testing%20Optional%20Content.ipynb) |
| Main hypothesis notebook | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
One-way ANOVA:
  H₀: μ₁ = μ₂ = ... = μₖ     H₁: at least one μᵢ differs

  F = MS_between / MS_within

  Assumptions: normality, equal variances, independence

Fuel type example (E85, LPG, Petrol):
  ANOVA p ≈ 8.27e-06  →  reject H₀

  Tukey HSD:
    E85 vs LPG     → significant (p-adj = 0.0012)
    E85 vs Petrol  → significant (p-adj ≈ 0)
    LPG vs Petrol  → not significant (p-adj = 0.49)
```

**Remember:** A significant ANOVA only tells you *something* differs — use Tukey HSD (or similar) to find out *what*.
