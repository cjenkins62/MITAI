# Lecture Summary: Hypothesis Testing Methodology and Test Selection

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Comprehensive synthesis — hypothesis formulation, test selection flowchart, p-values, Python tools  
**Format:** Recorded lecture (~5+ min)

---

## Overview

This capstone lecture synthesizes the **entire hypothesis testing toolkit** into a practical decision framework. It walks from **formulating H₀ and H₁** through **choosing the right test**, interpreting **test statistics and p-values**, and making evidence-based decisions. A **flowchart** simplifies test selection by data type and sample structure. The lecture covers one-sample, two-sample, and multi-sample tests (z, t, chi-square, F, ANOVA), proportion tests, and categorical association tests — with emphasis on **Python/SciPy implementation** and judicious use in business and scientific research.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:13** | Formulating hypotheses |
| **00:20** | Choosing the appropriate test |
| **00:33** | Understanding test statistics and p-values |
| **00:46** | Critical value comparison |
| **01:30** | Decision making in hypothesis testing |
| **01:39** | Flowchart for test selection |
| **01:51** | Tests for one sample |
| **02:28** | Tests for two samples |
| **02:50** | ANOVA and F-test for multiple samples |
| **03:15** | Discrete data and proportion tests |
| **03:35** | Bivariate data and chi-square test |
| **03:57** | ANOVA for mixed data types |
| **04:16** | Methodology and tools in Python |
| **04:57** | Importance of hypothesis testing |

---

## Key Themes

### 1. The hypothesis testing workflow

Every test follows the same logical sequence:

```
1. Formulate H₀ and H₁     ← what are you testing?
2. Choose the test          ← match data type + sample structure
3. Compute test statistic   ← z, t, F, χ², etc.
4. Assess significance      ← p-value or critical value
5. Make a decision          ← reject or fail to reject H₀
6. State conclusion         ← in context of the research question
```

See the full 6-step template in [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md).

---

### 2. Formulating hypotheses

H₀ and H₁ guide the entire process:

| Element | Rule |
|---------|------|
| **H₀** | Status quo — contains equality (=, ≤, ≥) |
| **H₁** | What you suspect — contains inequality (≠, <, >) |
| **α** | Significance level — typically 0.05 |
| **Tail** | One-tailed if direction matters; two-tailed if any difference |

See [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md).

---

### 3. Test statistics and p-values

The **test statistic** quantifies how far sample data deviates from what H₀ predicts. The **p-value** is the probability of observing a result at least this extreme if H₀ were true.

```
p-value < α   →  reject H₀   (statistically significant)
p-value ≥ α   →  fail to reject H₀   (not enough evidence)
```

**Critical value comparison** (alternative approach):

```
|test statistic| > critical value   →  reject H₀
|test statistic| ≤ critical value   →  fail to reject H₀
```

Both methods yield the same decision. P-values are more common in practice and software output; critical values require knowing the relevant distribution tables.

See [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) and [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md).

---

### 4. Flowchart for test selection

Use this decision tree to pick the right test:

```
What are you measuring?
│
├── CONTINUOUS (means)
│   ├── 1 sample
│   │   ├── σ known  →  One-sample z-test
│   │   └── σ unknown →  One-sample t-test
│   ├── 2 samples
│   │   ├── Independent  →  Two-sample z/t-test (Welch if σ unequal)
│   │   └── Paired/related →  Paired t-test
│   └── 3+ groups  →  ANOVA  (+ Tukey HSD post-hoc)
│
├── DISCRETE (proportions)
│   ├── 1 sample  →  One-proportion z-test
│   └── 2 samples →  Two-proportion z-test
│
├── VARIANCE (spread)
│   ├── 1 sample  →  Chi-square variance test
│   └── 2 samples →  F-test
│
└── CATEGORICAL (association)
    └── 2 variables →  Chi-square test of independence
```

---

### 5. Tests for one sample

| Test | Parameter | When | SciPy |
|------|-----------|------|-------|
| **Z-test** | Mean μ | σ known, large n | `ztest` (statsmodels) |
| **T-test** | Mean μ | σ unknown | `ttest_1samp` |
| **Proportion z-test** | Proportion p | Binary outcomes | `proportions_ztest` |
| **Chi-square variance** | Variance σ² | Normal data | `chi2` distribution |

**Deep dives:**
- [`hypothesis-testing-one-sample-t-test-lecture-summary.md`](hypothesis-testing-one-sample-t-test-lecture-summary.md)
- [`hypothesis-testing-proportions-z-test-lecture-summary.md`](hypothesis-testing-proportions-z-test-lecture-summary.md)
- [`hypothesis-testing-variance-chi-square-lecture-summary.md`](hypothesis-testing-variance-chi-square-lecture-summary.md)

---

### 6. Tests for two samples

| Test | Comparison | When | SciPy |
|------|-----------|------|-------|
| **Two-sample z-test** | μ₁ vs μ₂ | σ known, independent | Custom or statsmodels |
| **Two-sample t-test** | μ₁ vs μ₂ | σ unknown, equal variances | `ttest_ind(equal_var=True)` |
| **Welch's t-test** | μ₁ vs μ₂ | σ unknown, unequal variances | `ttest_ind(equal_var=False)` |
| **Paired t-test** | μ_diff | Same subjects, before/after | `ttest_rel` |
| **Two-proportion z-test** | p₁ vs p₂ | Independent groups | `proportions_ztest` |
| **F-test** | σ₁² vs σ₂² | Compare spread | Custom F ratio |

**Deep dives:**
- [`hypothesis-testing-two-sample-z-test-lecture-summary.md`](hypothesis-testing-two-sample-z-test-lecture-summary.md)
- [`hypothesis-testing-two-sample-t-test-lecture-summary.md`](hypothesis-testing-two-sample-t-test-lecture-summary.md)
- [`hypothesis-testing-welch-t-test-sat-lecture-summary.md`](hypothesis-testing-welch-t-test-sat-lecture-summary.md)
- [`hypothesis-testing-paired-t-test-lecture-summary.md`](hypothesis-testing-paired-t-test-lecture-summary.md)
- [`hypothesis-testing-two-proportion-z-test-lecture-summary.md`](hypothesis-testing-two-proportion-z-test-lecture-summary.md)
- [`hypothesis-testing-f-test-variance-lecture-summary.md`](hypothesis-testing-f-test-variance-lecture-summary.md)

---

### 7. ANOVA and F-test for multiple samples

| Test | Comparison | When | SciPy |
|------|-----------|------|-------|
| **One-way ANOVA** | μ₁ = μ₂ = … = μ_k | 3+ groups, continuous response | `f_oneway` |
| **Tukey HSD** | Pairwise means | Post-ANOVA follow-up | `pairwise_tukeyhsd` |

**Mixed data types:** ANOVA uses a **categorical factor** (e.g., fuel type) to compare a **continuous response** (e.g., CO emissions). The factor defines groups; the response is what you measure.

See [`hypothesis-testing-anova-lecture-summary.md`](hypothesis-testing-anova-lecture-summary.md).

---

### 8. Discrete data, proportions, and categorical tests

| Data type | Test | Question |
|-----------|------|----------|
| **Binary/count (1 sample)** | One-proportion z-test | Does rate equal benchmark? |
| **Binary/count (2 samples)** | Two-proportion z-test | Do two rates differ? |
| **Two categorical variables** | Chi-square independence | Are variables associated? |

**Assumption for proportions:** np ≥ 5 and n(1−p) ≥ 5  
**Assumption for chi-square:** expected count ≥ 5 per cell

See [`hypothesis-testing-chi-square-independence-lecture-summary.md`](hypothesis-testing-chi-square-independence-lecture-summary.md).

---

### 9. Python tools and methodology

SciPy and statsmodels provide functions for every test in this course:

```python
from scipy.stats import (
    ttest_1samp, ttest_ind, ttest_rel,    # t-tests
    f_oneway,                              # ANOVA
    chi2_contingency,                      # chi-square independence
    shapiro, levene                        # assumption checks
)
from statsmodels.stats.proportion import proportions_ztest
from statsmodels.stats.multicomp import pairwise_tukeyhsd
```

**Standard workflow in Python:**

```python
# 1. Load and explore data
# 2. State H₀ and H₁
# 3. Check assumptions (normality, equal variance, sample size)
# 4. Run the test
statistic, p_value = ttest_ind(group_a, group_b)
# 5. Compare p_value to alpha
# 6. State conclusion in plain language
```

**Notebooks:**
- [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) — core tests
- [`../Notebook - Hypothesis Testing Optional Content.ipynb`](../Notebook%20-%20Hypothesis%20Testing%20Optional%20Content.ipynb) — variance, chi-square, ANOVA

---

### 10. Importance and judicious use

Hypothesis testing provides **quantitative evidence** for or against assumptions:

| Domain | Application |
|--------|-------------|
| **Business** | A/B testing, quality control, pricing decisions |
| **Science** | Validating theories, comparing treatments |
| **Data science** | Feature significance, model comparisons |

**Use judiciously:**
- Statistical significance ≠ practical significance
- Always check assumptions before interpreting
- Report effect sizes alongside p-values
- Avoid p-hacking — pre-specify hypotheses and α
- A non-significant result is not proof of "no effect"

---

## Takeaways

1. **Start with H₀ and H₁** — they determine everything that follows.
2. **Match test to data** — parameter type, sample count, independence vs paired.
3. **P-value vs critical value** — two equivalent paths to the same decision.
4. **Flowchart simplifies selection** — continuous vs discrete vs categorical first.
5. **One sample → two sample → ANOVA** — the mean-comparison hierarchy.
6. **Proportions and chi-square** handle discrete and categorical data.
7. **Python/SciPy** implements every test — focus on choosing correctly, not coding from scratch.
8. **Use hypothesis testing wisely** — it validates assumptions and guides decisions, but requires careful interpretation.

---

## Connection to course arc

This lecture is the **capstone** — it ties together all individual test lectures:

| Category | Summaries |
|----------|-----------|
| Foundations | [`hypothesis-testing-introduction-lecture-summary.md`](hypothesis-testing-introduction-lecture-summary.md), [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md), [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| Decisions & errors | [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md), [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) |
| Test catalog | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Mean tests | One-sample t, two-sample z/t, Welch, paired, ANOVA summaries |
| Proportion tests | One- and two-proportion z-test summaries |
| Variance tests | Chi-square variance, F-test summaries |
| Categorical | Chi-square independence summary |

---

## Quick reference

```
Hypothesis testing decision framework:

  1. Formulate H₀ and H₁
  2. Identify parameter: mean | proportion | variance | association
  3. Count groups: 1 | 2 | 3+
  4. Check pairing: independent | paired
  5. Select test from flowchart
  6. Verify assumptions
  7. Compute p-value (or compare to critical value)
  8. Reject H₀ if p < α; otherwise fail to reject
  9. State conclusion in business/research context

Python: scipy.stats + statsmodels cover all tests in this course.
```

**Remember:** Choosing the right test is as important as running it correctly — when in doubt, consult the flowchart and check your data type first.
