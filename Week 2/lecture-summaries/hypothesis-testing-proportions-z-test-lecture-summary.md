# Lecture Summary: Proportions and Z-Test for Proportions

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Testing proportions — voting survey example, binomial/CLT, `proportions_ztest`  
**Format:** Recorded lecture (~6+ min)

---

## Overview

This lecture covers **proportions** — fractions or ratios of counts — and how to test them statistically. The worked example uses a **voting survey** (24 out of 90 people support a political party) to illustrate proportion estimation and hypothesis testing. The lecture connects proportions to the **binomial distribution**, explains when the **CLT justifies a z-test**, covers sample size validity checks, and demonstrates `proportions_ztest` for conducting and interpreting proportion tests.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Understanding proportions |
| **00:22** | Example of proportions in voting |
| **01:28** | Testing proportions with binomial distribution |
| **02:08** | Central Limit Theorem and proportions |
| **03:04** | Hypothesis testing for proportions |
| **03:50** | Sample size considerations |
| **04:55** | Conducting a proportions z-test |
| **05:48** | Interpreting p-values in proportion tests |

---

## Key Themes

### 1. Understanding proportions

A **proportion** is the ratio of successes to total observations:

```
p̂ = x / n

where x = count of successes
      n = sample size
```

**Example — voting survey:**
- n = 90 people surveyed
- x = 24 voted for a specific party
- **p̂ = 24/90 ≈ 0.267 (26.7%)**

Proportions are used to estimate population rates and predict outcomes (election results, conversion rates, defect rates).

---

### 2. Binomial foundation

Each individual observation is **binary** (success/failure, yes/no, voted/didn't vote) — modeled by the **Bernoulli** distribution. For n independent trials, the count X follows a **binomial distribution**:

```
X ~ Binomial(n, p)

E[X] = np
Var(X) = np(1 − p)
```

Hypothesis testing asks: is the observed count x consistent with a hypothesized proportion p₀?

---

### 3. CLT and the z-test for proportions

For **large n**, the sampling distribution of p̂ is approximately **normal** (by CLT):

```
p̂ ~ N(p, √(p(1−p)/n))
```

This allows a **z-test** instead of exact binomial calculations:

```
         p̂ − p₀
z = ──────────────────
      √(p₀(1 − p₀) / n)
```

Use z-test when sample size conditions are met (see below).

---

### 4. Hypothesis testing for proportions

**Example — testing if party support differs from 30%:**

```
H₀:  p = 0.30     (true support is 30%)
H₁:  p ≠ 0.30     (support differs from 30%)   ← two-tailed
α   = 0.05
```

**One-tailed variants:**

| Question | H₀ | H₁ |
|----------|----|----|
| Is support **higher** than 30%? | p ≤ 0.30 | p > 0.30 |
| Is support **lower** than 30%? | p ≥ 0.30 | p < 0.30 |

The alternative hypothesis guides whether you use a one- or two-tailed test and how to interpret the p-value.

---

### 5. Sample size validity checks

Before using the z-test approximation, verify:

```
np₀ ≥ 5
n(1 − p₀) ≥ 5
```

Both conditions must hold. If either fails:
- Sample is too small for normal approximation
- Use **exact binomial test** instead (`scipy.stats.binomtest`)

**For the voting example (n = 90, p₀ = 0.30):**
- np₀ = 90 × 0.30 = 27 ≥ 5 ✓
- n(1 − p₀) = 90 × 0.70 = 63 ≥ 5 ✓

Z-test is valid.

---

### 6. Conducting a proportions z-test

**Using statsmodels:**

```python
from statsmodels.stats.proportion import proportions_ztest

count = 24          # number of successes
nobs = 90           # sample size
p0 = 0.30           # hypothesized proportion (for H₀: p = 0.30)

z_stat, p_value = proportions_ztest(count, nobs, value=p0)
```

**Manual calculation:**

```python
from scipy.stats import norm

p_hat = count / nobs
z = (p_hat - p0) / ((p0 * (1 - p0) / nobs) ** 0.5)
p_value = 2 * (1 - norm.cdf(abs(z)))   # two-tailed
```

---

### 7. Interpreting p-values

**Decision rule:**

```
p-value < α  →  reject H₀  (observed proportion is significantly different)
p-value ≥ α  →  fail to reject H₀  (insufficient evidence of difference)
```

**Example with voting data (p̂ = 0.267 vs p₀ = 0.30):**

If p-value > 0.05 → fail to reject H₀: the sample proportion of 26.7% is not significantly different from the claimed 30% support level.

If p-value < 0.05 → reject H₀: observed support significantly differs from 30%.

Always interpret in context — a non-significant result does not prove p = 0.30 exactly.

---

## Takeaways

1. **Proportion p̂ = x/n** — estimate of population rate from sample counts.
2. **Binary outcomes → binomial** — foundation for proportion testing.
3. **CLT enables z-test** — when np ≥ 5 and n(1−p) ≥ 5.
4. **Check sample size conditions** before using z-test approximation.
5. **`proportions_ztest(count, nobs, value=p0)`** — statsmodels function for one-sample proportion tests.
6. **Voting example** — 24/90 = 26.7% support; test against hypothesized rate.
7. **Alternative hypothesis determines** one-tailed vs two-tailed interpretation.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Binomial & Bernoulli | [`binomial-bernoulli-lecture-summary.md`](binomial-bernoulli-lecture-summary.md) |
| Binomial PMF/CDF | [`binomial-distribution-pmf-cdf-lecture-summary.md`](binomial-distribution-pmf-cdf-lecture-summary.md) |
| CLT | [`central-limit-theorem-lecture-summary.md`](central-limit-theorem-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
One-sample proportion z-test:
  H₀: p = p₀     H₁: p ≠ p₀  (or > / < for one-tailed)

  p̂ = x / n
  z = (p̂ − p₀) / √(p₀(1 − p₀) / n)

  Validity check:  np₀ ≥ 5  AND  n(1 − p₀) ≥ 5

  statsmodels:
    proportions_ztest(count, nobs, value=p0)

Voting example:
  x = 24, n = 90, p̂ = 0.267
  Test H₀: p = 0.30
```

**Remember:** Proportions apply to yes/no outcomes — use mean tests (t-test) for continuous variables, proportion tests (z-test) for rates and percentages.
