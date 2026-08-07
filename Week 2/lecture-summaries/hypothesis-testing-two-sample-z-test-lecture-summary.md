# Lecture Summary: Two-Sample Z-Test for Equality of Means

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Two independent samples z-test — media channel customer satisfaction comparison  
**Format:** Recorded lecture (~6+ min)

---

## Overview

This lecture covers the **test of equality of means** in a **two-sample situation** — comparing means from two independent populations when **population variances (σ₁, σ₂) are known**. The worked example compares **customer satisfaction between two media channels** (Channel 1 vs Channel 2) using a one-tailed z-test and a custom Python function, concluding that one channel significantly outperforms the other.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Test of equality of means |
| **00:11** | Two-sample situation |
| **00:36** | Comparing means from different populations |
| **01:13** | One-tailed hypothesis test |
| **02:04** | Two independent samples z-test |
| **04:14** | User-defined function for z-test |
| **05:31** | Statistical significance and p-value |

---

## Key Themes

### 1. Two-sample situation

**Question:** Do two **independent groups** have the same mean, or does one exceed the other?

**When to use:**
- Two separate samples from different populations
- Observations are **independent** (no pairing between groups)
- Comparing means — e.g., satisfaction scores, sales, response times

**Marketing example:** Which media channel (Channel 1 or Channel 2) delivers higher customer satisfaction?

---

### 2. Hypothesis setup (one-tailed)

When the research question is **directional** — predicting one group will score higher:

```
H₀:  μ₁ ≤ μ₂     (Channel 1 satisfaction ≤ Channel 2)
H₁:  μ₁ > μ₂     (Channel 1 satisfaction > Channel 2)
α   = 0.05
```

For a two-tailed test (any difference): H₀: μ₁ = μ₂, H₁: μ₁ ≠ μ₂.

---

### 3. Two independent samples z-test

**Use when:**
- Population **variances σ₁ and σ₂ are known**
- Sample sizes are **large** (n₁, n₂ ≥ 30) — CLT applies
- Groups are **independent**

**Test statistic:**

```
         (x̄₁ − x̄₂) − (μ₁ − μ₂)
z = ─────────────────────────────────
      √(σ₁²/n₁ + σ₂²/n₂)
```

Under H₀ (μ₁ = μ₂), this simplifies to:

```
         x̄₁ − x̄₂
z = ─────────────────────
      √(σ₁²/n₁ + σ₂²/n₂)
```

The sampling distribution of the difference between means is **approximately normal** for large samples.

---

### 4. User-defined function for z-test

SciPy does not provide a dedicated two-sample z-test function — build one manually:

```python
from scipy.stats import norm
import numpy as np

def two_sample_z_test(sample1, sample2, sigma1, sigma2):
    x1 = np.mean(sample1)
    x2 = np.mean(sample2)
    n1 = len(sample1)
    n2 = len(sample2)

    # Test statistic
    z = (x1 - x2) / np.sqrt(sigma1**2 / n1 + sigma2**2 / n2)

    # One-tailed p-value (H₁: μ₁ > μ₂)
    p_value = 1 - norm.cdf(z)

    return z, p_value
```

**Function steps:**
1. Read data for both samples
2. Input known population standard deviations (σ₁, σ₂)
3. Calculate sample means (x̄₁, x̄₂)
4. Compute z-statistic
5. Compute one-sided p-value using `norm.cdf`

---

### 5. Interpreting the results

**Result from the lecture:**

```
p-value = 5.879 × 10⁻⁹  (≈ 0.000000006)
α       = 0.05

p-value << α  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. There is strong evidence that customer satisfaction differs significantly between the two channels (p = 5.879 × 10⁻⁹). One channel performs significantly better than the other."

**Business action:** Allocate more budget to the higher-performing channel; investigate what drives its superior satisfaction scores.

---

### 6. Two-sample z-test vs t-test

| | Two-sample z-test | Two-sample t-test |
|---|-------------------|-------------------|
| σ₁, σ₂ | **Known** | **Unknown** (estimated from samples) |
| Distribution | Standard normal (z) | t (Welch's or pooled) |
| Sample size | Large (n ≥ 30) | Any n |
| SciPy | Custom function | `ttest_ind` |

When σ is unknown, use **`scipy.stats.ttest_ind`** instead.

---

## Takeaways

1. **Two-sample z-test** — compare means of two independent groups when σ₁ and σ₂ are known.
2. **One-tailed test** when you predict direction; two-tailed when any difference matters.
3. **Test statistic** uses the standard error of the difference: √(σ₁²/n₁ + σ₂²/n₂).
4. **No built-in SciPy function** — write a custom z-test using `norm.cdf`.
5. **Media channel example** — p = 5.879 × 10⁻⁹ → one channel significantly outperforms the other.
6. **Use t-test** when population variances are unknown.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| One-sample t-test | [`hypothesis-testing-one-sample-t-test-lecture-summary.md`](hypothesis-testing-one-sample-t-test-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| One- and two-tailed tests | [`hypothesis-testing-one-two-tailed-lecture-summary.md`](hypothesis-testing-one-two-tailed-lecture-summary.md) |
| P-value and e-commerce example | [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Two-sample z-test (independent groups, σ known):
  H₀: μ₁ = μ₂     H₁: μ₁ ≠ μ₂  (or > / < for one-tailed)

  z = (x̄₁ − x̄₂) / √(σ₁²/n₁ + σ₂²/n₂)

  One-tailed p-value:  1 − norm.cdf(z)   (if H₁: μ₁ > μ₂)

Media channel example:
  H₀: μ₁ ≤ μ₂   H₁: μ₁ > μ₂
  p = 5.879 × 10⁻⁹  →  reject H₀ (Channel 1 > Channel 2)
```

**Remember:** Independence is critical — if observations are paired (before/after, matched subjects), use a **paired t-test** instead.
