# Lecture Summary: One-Tailed and Two-Tailed Hypothesis Tests

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** One-tailed vs two-tailed tests, critical values, soft drink manufacturing example  
**Format:** Recorded lecture (~7+ min)

---

## Overview

This lecture explains the difference between **one-tailed** and **two-tailed** hypothesis tests — when to use each, how critical values change, and how rejection regions shift on the distribution. A **soft drink manufacturing** example (bottles claimed to contain 600 ml) demonstrates a full z-test where the sample mean of 580 ml leads to rejecting H₀.

The key takeaway: **match the test type to the business question** — direction matters.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:06** | One-tailed and two-tailed tests |
| **00:38** | Setting up hypotheses |
| **01:56** | Rejection regions and test statistics |
| **03:03** | Example: hypothesis testing in manufacturing |
| **06:34** | Critical values and rejection regions |

---

## Key Themes

### 1. One-tailed vs two-tailed tests

| Test type | When to use | H₁ form | Rejection region |
|-----------|-------------|---------|------------------|
| **One-tailed** | Alternative specifies a **direction** (greater than or less than) | μ > μ₀ or μ < μ₀ | **One side** of the distribution |
| **Two-tailed** | Alternative only says **not equal** — direction unknown | μ ≠ μ₀ | **Both tails** of the distribution |

**One-tailed:** You suspect the parameter is specifically higher **or** specifically lower — not just different.

**Two-tailed:** You care about deviation in **either direction** — above or below the claimed value.

**Business rule:** Align the hypothesis with the **business question**. If a manager only cares whether delivery times *increased*, use one-tailed. If they care about any change from spec, use two-tailed.

---

### 2. Setting up hypotheses

**One-tailed right (greater than):**
```
H₀:  μ ≤ μ₀
H₁:  μ > μ₀
```

**One-tailed left (less than):**
```
H₀:  μ ≥ μ₀
H₁:  μ < μ₀
```

**Two-tailed (not equal):**
```
H₀:  μ = μ₀
H₁:  μ ≠ μ₀
```

Equality always belongs in H₀. The test type follows directly from how H₁ is stated.

---

### 3. Critical values at α = 0.05

| Test type | Critical value(s) | α allocation |
|-----------|-------------------|--------------|
| **One-tailed** | **±1.645** | Full 5% in one tail |
| **Two-tailed** | **±1.96** | 2.5% in each tail |

**Why two-tailed critical value is larger:** α is split across both tails, so each tail gets less area — but the total rejection region spans both sides, requiring a larger |z| to reject.

**Decision rule:**
```
One-tailed right:   reject H₀ if z > 1.645
One-tailed left:    reject H₀ if z < −1.645
Two-tailed:         reject H₀ if |z| > 1.96
```

---

### 4. Rejection regions and test statistics

The **test statistic** (z) is a standardized measure of how far the sample result deviates from H₀:

```
z = (x̄ − μ₀) / (σ / √n)
```

Compare z to the critical value(s) to determine which region it falls in:

```
One-tailed left:
  Rejection region:  z < −1.645
  Acceptance:        z ≥ −1.645

Two-tailed:
  Rejection region:  z < −1.96  or  z > 1.96
  Acceptance:        −1.96 ≤ z ≤ 1.96
```

---

### 5. Worked example — soft drink manufacturing

**Scenario:**
- Manufacturer claims each bottle contains **μ₀ = 600 ml**
- Known **σ = 50 ml**
- Quality check: sample of **n = 36** bottles, **x̄ = 580 ml**
- Concern: bottles may be **underfilled**

#### Step 1: Set up hypotheses (one-tailed left)

```
H₀:  μ = 600     (bottles meet the 600 ml claim)
H₁:  μ < 600     (bottles are underfilled)
α   = 0.05
```

#### Step 2: Calculate test statistic

```
z = (x̄ − μ₀) / (σ / √n)
z = (580 − 600) / (50 / √36)
z = −20 / 8.33
z = −2.4
```

The sample mean is **2.4 standard errors below** the claimed population mean.

#### Step 3: Compare to critical value

```
z_critical (one-tailed left, α = 0.05) = −1.645

z = −2.4  <  −1.645  →  falls in rejection region  →  reject H₀
```

#### Step 4: Two-tailed check (for comparison)

```
|z| = 2.4  >  1.96  →  also reject H₀ (two-tailed)
```

Either test type leads to rejection here — the underfill is large enough to detect either way.

#### Business conclusion

> "At α = 0.05, we reject H₀. There is sufficient evidence that mean bottle volume is less than 600 ml (z = −2.4). The manufacturing process may be underfilling bottles and requires investigation."

---

### 6. Critical values and rejection regions (visual)

**One-tailed left (soft drink example):**

```
  Rejection region     |     Acceptance region
  ─────────────────────┼──────────────────────────────
  z = −2.4          z = −1.645              z = 0
       ↑                  ↑ critical value
  (our test stat)    (boundary)
```

**Two-tailed:**

```
  Rejection   |  Acceptance  |  Rejection
  ────────────┼──────────────┼────────────
  z = −1.96   z = 0          z = 1.96
```

---

## Takeaways

1. **One-tailed** when H₁ specifies direction; **two-tailed** when H₁ is ≠ only.
2. **Critical values differ:** one-tailed ±1.645 vs two-tailed ±1.96 at α = 0.05.
3. **Match test type to business question** — don't default to two-tailed if direction matters.
4. **Soft drink example:** z = −2.4 → reject H₀; bottles are significantly underfilled.
5. **A large |z|** (here 2.4) provides strong evidence regardless of tail choice.
6. **Rejection region** = where the test statistic leads to rejecting H₀; determined by α and test type.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| P-value and e-commerce example | [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) |
| Decisions, errors, and power | [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md) |
| Testing template | [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| Normal distribution & z-scores | [`standardization-z-scores-lecture-summary.md`](standardization-z-scores-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Choosing test type:
  H₁: μ > μ₀   →  one-tailed right   (z_crit = +1.645)
  H₁: μ < μ₀   →  one-tailed left    (z_crit = −1.645)
  H₁: μ ≠ μ₀   →  two-tailed         (z_crit = ±1.96)

Soft drink example:
  H₀: μ = 600   H₁: μ < 600   n = 36   x̄ = 580   σ = 50
  z = −2.4      z_crit = −1.645
  → reject H₀ (significantly underfilled)
```

**Remember:** One-tailed tests have more power to detect an effect in the specified direction, but only test that direction. Use two-tailed when any deviation from the claim matters.
