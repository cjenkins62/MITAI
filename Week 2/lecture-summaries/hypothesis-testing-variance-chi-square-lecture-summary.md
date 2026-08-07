# Lecture Summary: Variance Testing and Chi-Square Test

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** One-sample variance test — chi-square distribution, mutual fund risk example  
**Format:** Recorded lecture (~5+ min)

---

## Overview

This lecture covers **variance testing** — a statistical method for assessing whether variability in a sample differs from a known or hypothesized value. The chi-square distribution is the foundation. The worked example compares the **standard deviation of mid-cap mutual fund annual returns** to a long-term average, framing variance as a **financial risk indicator**. The test yields **p = 0.07**, failing to reject H₀ at α = 0.05, though the lecture notes that even borderline results warrant investor attention.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:09** | Introduction to variance testing |
| **00:38** | Chi-square distribution and degrees of freedom |
| **01:13** | Financial risk and variability |
| **02:01** | One-sample variance test |
| **02:39** | Assumptions and chi-square test |
| **04:24** | Interpreting chi-square test results |
| **05:15** | Implications for investors |

---

## Key Themes

### 1. Why test variance?

Variance (and standard deviation) measures **spread** — how much values deviate from the mean. Testing variance answers:

- Is this process **more or less variable** than expected?
- Has **risk increased** compared to a benchmark?
- Does quality **consistency** meet specification?

**Finance context:** Higher standard deviation of returns = more variability = **higher potential risk** for investors.

---

### 2. Chi-square distribution

The **chi-square (χ²) distribution** is used for variance tests. Key properties:

| Property | Detail |
|----------|--------|
| Shape | Right-skewed, starts at 0 |
| Parameter | **Degrees of freedom (df)** |
| One-sample variance test | **df = n − 1** |
| Always positive | Variance-related statistics cannot be negative |

As df increases, the chi-square distribution becomes more symmetric and approaches normal.

---

### 3. Financial risk example

**Research question:** Is the variability of mid-cap mutual fund annual returns different from the long-term average standard deviation?

**Setup:**
- Sample: annual returns from a set of mid-cap mutual funds
- Known benchmark: long-term average σ₀ (population standard deviation)
- Compare sample variance s² to σ₀²

Higher sample standard deviation → fund returns are more volatile → potentially riskier investment.

---

### 4. One-sample variance test

**Hypotheses (two-tailed):**

```
H₀:  σ² = σ₀²     (sample variance equals known variance)
H₁:  σ² ≠ σ₀²     (sample variance differs from known variance)
α   = 0.05
```

**Test statistic:**

```
χ² = (n − 1) × s² / σ₀²

where s²  = sample variance
      σ₀² = hypothesized population variance
      df  = n − 1
```

Compare χ² to the chi-square distribution with df = n − 1 to get the p-value.

**SciPy implementation:**

```python
from scipy.stats import chi2

n = len(returns)
s_squared = returns.var(ddof=1)       # sample variance
sigma0_squared = sigma0 ** 2          # known population variance

chi2_stat = (n - 1) * s_squared / sigma0_squared
p_value = 2 * min(chi2.cdf(chi2_stat, df=n-1),
                  1 - chi2.cdf(chi2_stat, df=n-1))   # two-tailed
```

---

### 5. Assumptions

The chi-square variance test requires:

| Assumption | Requirement |
|------------|-------------|
| **Normality** | Population must be **normally distributed** |
| **Random sample** | Observations are independent |
| **Continuous data** | Returns, measurements, etc. |

If normality is violated, the chi-square test results are unreliable. Check with a Q-Q plot or Shapiro-Wilk test before proceeding.

---

### 6. Interpreting results

**Result from the lecture:**

```
p-value = 0.07
α       = 0.05

p-value (0.07) > α (0.05)  →  fail to reject H₀
```

**Statistical conclusion:**

> "At α = 0.05, we fail to reject H₀. The observed variance is not significantly different from the known long-term variance (p = 0.07)."

**Investor implications:**

Even when failing to reject H₀, a p-value of 0.07 is **borderline** — it suggests some evidence of elevated variability. Investors should consider:
- Statistical significance ≠ practical significance
- A "non-significant" result does not guarantee low risk
- Context matters: market conditions, fund strategy, investor risk tolerance

**If p < 0.05:** Reject H₀ — sample variance significantly differs from benchmark; investigate cause and reassess risk exposure.

---

## Takeaways

1. **Variance testing** — assess whether spread/variability differs from a known value.
2. **Chi-square distribution** — foundation for variance tests; df = n − 1.
3. **Test statistic:** χ² = (n−1)s²/σ₀².
4. **Normality assumption is critical** — chi-square test invalid if data is not normal.
5. **Mutual fund example** — p = 0.07 → not significant at 5%, but borderline for risk assessment.
6. **Statistical vs practical significance** — investors should weigh p-values alongside economic context.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Normal distribution | [`normal-distribution-lecture-summary.md`](normal-distribution-lecture-summary.md) |
| Estimation & standard error | [`estimation-t-distribution-lecture-summary.md`](estimation-t-distribution-lecture-summary.md) |
| Decisions and errors | [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
One-sample chi-square variance test:
  H₀: σ² = σ₀²     H₁: σ² ≠ σ₀²

  χ² = (n − 1) × s² / σ₀²
  df = n − 1

  Assumption: population is normally distributed

Mutual fund example:
  Compare sample return variability to long-term σ₀
  p = 0.07  →  fail to reject H₀ at α = 0.05
```

**Remember:** Variance tests measure consistency and risk — not just whether the mean changed.
