# Lecture Summary: One-Sample T-Test

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** One-sample t-test — food delivery example with SciPy `ttest_1samp`  
**Format:** Recorded lecture (~4+ min)

---

## Overview

This lecture walks through the **one-sample t-test** — used when you want to determine whether a sample mean differs significantly from a hypothesized population mean, and the **population standard deviation (σ) is unknown**. The worked example is a **food delivery aggregator** that must keep deliveries under 40 minutes to stay competitive. The test confirms that average delivery time significantly exceeds the target, triggering a need for operational improvements.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to one-sample t-test |
| **00:15** | Application in food delivery context |
| **01:19** | Hypothesis setup and assumptions |
| **02:07** | Execution of one-sample t-test |
| **04:00** | Interpreting the results |

---

## Key Themes

### 1. When to use the one-sample t-test

Use when:
- You have **one sample** and want to compare its mean to a **known/hypothesized value**
- Population **σ is unknown** (estimated from sample standard deviation s)
- Data is **continuous** and approximately **normally distributed**
- Sample size is typically **small (n < 30)** — though t-test works for any n when σ is unknown

**Contrast with z-test:** Use z-test when σ is known; use t-test when σ must be estimated.

---

### 2. Food delivery context

**Business question:** Is the food aggregator meeting its 40-minute delivery target?

**Stakes:** Deliveries beyond 40 minutes hurt competitiveness — this is an operational KPI, not just a statistic.

---

### 3. Hypothesis setup and assumptions

**Hypotheses (one-tailed right):**

```
H₀:  μ = 40        (mean delivery time is 40 minutes)
H₁:  μ > 40        (mean delivery time exceeds 40 minutes)
α   = 0.05
```

**Assumptions to verify before running:**

| Assumption | Requirement |
|------------|-------------|
| Data type | **Continuous** (delivery time in minutes) |
| Distribution | Approximately **normal** (or n ≥ 30 by CLT) |
| Sample size | Typically **n < 30** (t-test's primary use case) |
| σ | **Unknown** — estimated from sample |
| Independence | Observations are **independent** (random sample) |

---

### 4. Execution with SciPy

**Test statistic formula:**

```
t = (x̄ − μ₀) / (s / √n)
```

**SciPy implementation:**

```python
from scipy.stats import ttest_1samp

# sample: array of delivery times in minutes
# popmean: hypothesized population mean (40)
statistic, p_value = ttest_1samp(sample, popmean=40)

# For one-tailed test (H₁: μ > 40), divide two-tailed p-value by 2
# if t-statistic is positive; otherwise p = 1 - p_two_tailed/2
```

`ttest_1samp` returns a **two-tailed p-value** by default — adjust for one-tailed tests based on the direction of the t-statistic.

---

### 5. Interpreting the results

**Result from the lecture:**

```
p-value = 1.48 × 10⁻⁵  (≈ 0.000015)
α       = 0.05

p-value << α  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. There is strong evidence that mean delivery time exceeds 40 minutes (p = 1.48 × 10⁻⁵). The aggregator is not meeting its delivery target and requires operational improvements."

**Business action:** Investigate bottlenecks — routing, kitchen prep time, driver availability — to bring average delivery time back under 40 minutes.

---

### 6. One-sample t-test vs z-test

| | One-sample t-test | One-sample z-test |
|---|-------------------|-------------------|
| σ | **Unknown** (use s) | **Known** |
| Distribution | t (df = n − 1) | Standard normal (z) |
| Sample size | Typically small (n < 30) | Typically large (n ≥ 30) |
| SciPy function | `ttest_1samp` | Manual z calculation or `ztest` |

When in doubt and σ is unknown, use the **t-test** — it is the safer default.

---

## Takeaways

1. **One-sample t-test** — compare sample mean to a hypothesized μ when σ is unknown.
2. **Assumptions matter** — continuous data, approximate normality, independent observations.
3. **`ttest_1samp(sample, popmean)`** — SciPy returns two-tailed p-value; adjust for one-tailed tests.
4. **Food delivery example** — p = 1.48 × 10⁻⁵ → delivery times significantly exceed 40-minute target.
5. **Statistical significance drives business action** — reject H₀ → investigate and fix operations.
6. **Use t over z** when σ is unknown, regardless of sample size.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| t-distribution & standard error | [`estimation-t-distribution-lecture-summary.md`](estimation-t-distribution-lecture-summary.md) |
| P-value and e-commerce example | [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) |
| One- and two-tailed tests | [`hypothesis-testing-one-two-tailed-lecture-summary.md`](hypothesis-testing-one-two-tailed-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
One-sample t-test:
  H₀: μ = μ₀
  H₁: μ ≠ μ₀  (two-tailed)  or  μ > μ₀ / μ < μ₀  (one-tailed)

  t = (x̄ − μ₀) / (s / √n)
  df = n − 1

SciPy:
  from scipy.stats import ttest_1samp
  t_stat, p_value = ttest_1samp(data, popmean=μ₀)

Food delivery example:
  H₀: μ = 40 min   H₁: μ > 40 min
  p = 1.48 × 10⁻⁵  →  reject H₀ (delivery too slow)
```

**Remember:** A significant result tells you *that* the mean differs — follow up with effect size and confidence intervals to understand *how much* it differs.
