# Lecture Summary: Two-Sample T-Test Framework

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Two-sample t-test with equal variances — TV vs radio usage comparison  
**Format:** Recorded lecture (~4+ min)

---

## Overview

This lecture covers the **two-sample t-test** — the standard method for comparing means between two independent groups when **population variances are unknown** (estimated from sample data). It contrasts t-test vs z-test, walks through hypothesis setup with an **equal variances assumption**, and demonstrates execution with SciPy's `ttest_ind`. The worked example compares **daily TV and radio usage**, finding no statistically significant difference (p = 0.549).

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to t-test framework |
| **00:24** | Comparing means with t-test |
| **02:02** | Two-sample t-test with equal variances |
| **03:49** | Interpreting t-test results |

---

## Key Themes

### 1. T-test vs z-test — when to use each

| | Z-test | T-test |
|---|--------|--------|
| σ known? | **Yes** | **No** (estimated from sample) |
| Sample size | Large (n ≥ 30) | Any size (especially n < 30) |
| Distribution | Standard normal | t (df depends on sample sizes) |
| Common use | Known σ, large n | **Default choice** when σ is unknown |

**Rule of thumb:** When variances are unknown — which is almost always in practice — use the **t-test**.

---

### 2. Comparing means with t-test

**Question:** Do two independent groups have significantly different means?

**TV vs radio example:** Is daily TV usage significantly different from daily radio usage?

**Setup:**
- Two **independent** samples (different people, not paired)
- Continuous data (hours of usage per day)
- Variances **unknown** — estimated from each sample

---

### 3. Two-sample t-test with equal variances

**Hypotheses (two-tailed):**

```
H₀:  μ_TV = μ_Radio     (no difference in mean daily usage)
H₁:  μ_TV ≠ μ_Radio     (means differ)
α   = 0.05
```

**Equal variances assumption:** Assume σ²_TV = σ²_Radio (pooled variance estimate). If variances are unequal, use Welch's t-test (`equal_var=False` in SciPy).

**Pooled standard error:**

```
         x̄₁ − x̄₂
t = ─────────────────────
      s_p × √(1/n₁ + 1/n₂)

where s_p = pooled sample standard deviation
df = n₁ + n₂ − 2
```

**SciPy implementation:**

```python
from scipy.stats import ttest_ind

# Equal variances (default)
t_stat, p_value = ttest_ind(tv_usage, radio_usage)

# Unequal variances (Welch's t-test)
t_stat, p_value = ttest_ind(tv_usage, radio_usage, equal_var=False)
```

`ttest_ind` returns a **two-tailed p-value** by default.

---

### 4. Interpreting t-test results

**Result from the lecture:**

```
p-value = 0.549
α       = 0.05

p-value (0.549) > α (0.05)  →  fail to reject H₀
```

**Conclusion:**

> "At α = 0.05, we fail to reject H₀. There is no statistically significant difference in mean daily usage between TV and radio (p = 0.549). The observed difference in sample means could plausibly be due to sampling variation."

**Business interpretation:** TV and radio reach audiences for similar amounts of daily time — neither medium dominates on usage hours alone. Marketing decisions should consider other factors (demographics, engagement, cost) alongside this finding.

---

### 5. Assumptions checklist

| Assumption | Requirement |
|------------|-------------|
| Independence | Two samples are **independent** (not paired) |
| Normality | Data approximately **normal** in each group (or n ≥ 30) |
| Equal variances | σ₁² ≈ σ₂² (use Welch's if violated) |
| Continuous data | Outcome is a **continuous** numeric variable |
| Random sampling | Observations are **randomly sampled** |

---

### 6. Equal vs unequal variances

| Scenario | SciPy call | Method |
|----------|-----------|--------|
| Equal variances assumed | `ttest_ind(a, b)` | Pooled t-test |
| Unequal variances | `ttest_ind(a, b, equal_var=False)` | Welch's t-test |

When unsure, **Welch's t-test is safer** — it does not require equal variance and performs well even when variances are equal.

---

## Takeaways

1. **Use t-test when σ is unknown** — the default for comparing two group means in practice.
2. **Equal variances assumption** — pooled t-test; use Welch's (`equal_var=False`) when unsure.
3. **`ttest_ind(sample1, sample2)`** — SciPy's two-sample independent t-test.
4. **TV vs radio example** — p = 0.549 → no significant difference in daily usage.
5. **Fail to reject H₀** does not prove means are equal — sample may lack power to detect a real difference.
6. **Check assumptions** before interpreting — independence, normality, and variance equality.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Two-sample z-test | [`hypothesis-testing-two-sample-z-test-lecture-summary.md`](hypothesis-testing-two-sample-z-test-lecture-summary.md) |
| One-sample t-test | [`hypothesis-testing-one-sample-t-test-lecture-summary.md`](hypothesis-testing-one-sample-t-test-lecture-summary.md) |
| t-distribution & standard error | [`estimation-t-distribution-lecture-summary.md`](estimation-t-distribution-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| TV/Radio data | [`../TVRadio.csv`](../TVRadio.csv) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Two-sample t-test (independent groups, σ unknown):
  H₀: μ₁ = μ₂     H₁: μ₁ ≠ μ₂

  SciPy (equal variances):
    ttest_ind(group1, group2)

  SciPy (Welch's — unequal variances):
    ttest_ind(group1, group2, equal_var=False)

TV vs radio example:
  H₀: μ_TV = μ_Radio
  p = 0.549  →  fail to reject H₀ (no significant difference)
```

**Remember:** A non-significant result (p > α) means insufficient evidence of a difference — not proof that the groups are identical.
