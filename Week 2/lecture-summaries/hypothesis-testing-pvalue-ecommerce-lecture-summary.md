# Lecture Summary: Hypothesis Testing — Significance, P-value, and E-commerce Example

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** α, p-value, rejection/acceptance regions — worked e-commerce delivery example  
**Format:** Recorded lecture (~15+ min)

---

## Overview

This lecture ties together the core decision tools of hypothesis testing: **level of significance (α)**, **p-value**, **test statistic**, **critical value**, and **rejection/acceptance regions**. It walks through a full **e-commerce delivery time** example — a company with a known mean delivery of 5 days suspects delays, samples 45 orders, and applies a one-sample z-test to decide whether the increase is statistically significant.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to hypothesis testing |
| **00:24** | Level of significance |
| **01:44** | Understanding p-value |
| **03:30** | Rejection and acceptance regions |
| **05:11** | Example: hypothesis testing in e-commerce |
| **07:32** | Setting up the hypothesis |
| **10:31** | Calculating the test statistic |
| **12:00** | Interpreting the test statistic and p-value |
| **15:02** | Critical value and rejection region |

---

## Key Themes

### 1. Level of significance (α)

**α** is the threshold for rejecting H₀ — the maximum acceptable probability of a **Type I error** (rejecting a true H₀).

| Context | Typical α |
|---------|-----------|
| Business | **0.05 (5%)** |
| High-stakes / medical | 0.01 or 0.001 |

**Interpretation:** At α = 0.05, you accept a 5% chance of concluding an effect exists when it doesn't.

α is set **before** collecting data — it defines the rejection boundary.

---

### 2. Understanding the p-value

**p-value** = probability of observing a test statistic **at least as extreme** as the one calculated, **assuming H₀ is true**.

| p-value vs α | Decision |
|--------------|----------|
| p-value **< α** | Reject H₀ — statistically significant |
| p-value **≥ α** | Fail to reject H₀ — not statistically significant |

**Important:** The p-value is **not** the probability that H₀ is true. It measures how compatible the sample data is with H₀.

**Smaller p-value** → stronger evidence against H₀.

---

### 3. Rejection and acceptance regions

The test statistic's distribution (under H₀) is divided into two regions:

| Region | Meaning |
|--------|---------|
| **Rejection region** | Test statistic falls here → reject H₀ |
| **Acceptance region** (non-rejection) | Test statistic falls here → fail to reject H₀ |

The boundary between them is the **critical value** — determined by α and the test type (one-tailed vs two-tailed).

**Two equivalent decision methods:**

```
Method 1 (p-value):     p-value < α  →  reject H₀
Method 2 (critical):    |z| > z_critical  →  reject H₀
```

Both always reach the same conclusion.

---

### 4. Worked example — e-commerce delivery times

**Scenario:**
- Company mean delivery time: **μ₀ = 5 days** (known from history)
- New manager suspects delivery times have **increased**
- Sample: **n = 45** orders, **x̄ = 5.25 days**

#### Step 1: Set up hypotheses (one-tailed, right)

```
H₀:  μ ≤ 5      (delivery time has not increased)
H₁:  μ > 5      (delivery time has increased)
α   = 0.05
```

#### Step 2: Calculate test statistic

Using the one-sample z-test (σ known or estimated):

```
z = (x̄ − μ₀) / (σ / √n)
z = 1.29
```

#### Step 3: Find p-value

For a one-tailed test with z = 1.29:

```
p-value = P(Z > 1.29) = 0.098
```

#### Step 4: Compare to α

```
p-value (0.098) > α (0.05)  →  fail to reject H₀
```

The observed increase from 5.00 to 5.25 days is **not statistically significant** at the 5% level — it could plausibly be due to sampling variation.

#### Step 5: Critical value check (alternative method)

For a one-tailed test at α = 0.05:

```
z_critical = 1.64
```

Since **z = 1.29 < 1.64**, the test statistic falls in the **acceptance region** → fail to reject H₀. Same conclusion.

#### Business conclusion

> "At α = 0.05, there is insufficient evidence to conclude that mean delivery time has increased beyond 5 days (z = 1.29, p = 0.098). The manager's suspicion is not supported by this sample."

---

### 5. Critical value and rejection region (visual)

For the one-tailed right test at α = 0.05:

```
        Acceptance region          |  Rejection region
   ───────────────────────────────┼──────────────────
   z = 0                    z = 1.64
                              ↑ critical value

   Our z = 1.29 falls here → fail to reject H₀
```

For a **two-tailed** test at α = 0.05, critical values are ±1.96 (α split across both tails).

---

## Takeaways

1. **α = significance level** — set before testing; controls Type I error rate (typically 0.05 in business).
2. **p-value** — probability of data this extreme if H₀ is true; compare to α for the decision.
3. **Rejection region** — where the test statistic leads to rejecting H₀; bounded by the critical value.
4. **E-commerce example** — z = 1.29, p = 0.098 → not significant at 5%; don't overreact to small sample shifts.
5. **Two decision methods** (p-value and critical value) always agree — use whichever is more convenient.
6. **Fail to reject ≠ prove H₀ true** — the sample may simply lack power to detect a real increase.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Hypothesis testing intro | [`hypothesis-testing-introduction-lecture-summary.md`](hypothesis-testing-introduction-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| Decisions, errors, and power | [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md) |
| Testing template | [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| Normal distribution & z-scores | [`standardization-z-scores-lecture-summary.md`](standardization-z-scores-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Decision rule:
  p-value < α        →  reject H₀
  p-value ≥ α        →  fail to reject H₀

  |z| > z_critical    →  reject H₀
  |z| ≤ z_critical    →  fail to reject H₀

Common critical values (α = 0.05):
  One-tailed right:   z = 1.64
  One-tailed left:    z = −1.64
  Two-tailed:         z = ±1.96

E-commerce example:
  H₀: μ ≤ 5    H₁: μ > 5    n = 45    x̄ = 5.25
  z = 1.29     p = 0.098    z_crit = 1.64
  → fail to reject H₀ (not significant at 5%)
```

**Remember:** Statistical significance is a formal evidence threshold — always interpret results in the business context alongside p-values.
