# Lecture Summary: Two-Sample Z-Test for Proportions

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Comparing two proportions — assembly line defect rate example  
**Format:** Recorded lecture (~4+ min)

---

## Overview

This lecture covers how to **compare two proportions** from independent groups using a **two-sample z-test**. The worked example asks whether **defect rates differ between two car assembly lines** — a classic quality control question. Using `proportions_ztest` with defect counts and sample sizes as vectors, the test yields **p = 0.10**, leading to the conclusion that there is no statistically significant difference between the lines.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to comparing two proportions |
| **01:00** | Statistical hypothesis testing for proportions |
| **02:19** | Conducting a two-sample z-test for proportions |
| **03:43** | Interpreting the z-test results |

---

## Key Themes

### 1. When to compare two proportions

Use a **two-proportion z-test** when:
- You have **two independent groups**
- The outcome is **binary** (defect/no defect, pass/fail, yes/no)
- You want to know if **p₁ ≠ p₂** (or one is higher/lower)

**Assembly line example:**
- Line A: x₁ defects out of n₁ units produced
- Line B: x₂ defects out of n₂ units produced
- Question: Is the defect rate significantly different between lines?

---

### 2. Hypothesis setup

**Two-tailed (any difference):**

```
H₀:  p₁ = p₂     (defect rates are equal)
H₁:  p₁ ≠ p₂     (defect rates differ)
α   = 0.05
```

**One-tailed variants:**

| Question | H₀ | H₁ |
|----------|----|----|
| Is Line A defect rate **higher**? | p₁ ≤ p₂ | p₁ > p₂ |
| Is Line A defect rate **lower**? | p₁ ≥ p₂ | p₁ < p₂ |

---

### 3. CLT and sample size requirements

The two-proportion z-test relies on the **CLT** for normal approximation. Check validity for **each group**:

```
n₁p̂₁ ≥ 5   and   n₁(1 − p̂₁) ≥ 5
n₂p̂₂ ≥ 5   and   n₂(1 − p̂₂) ≥ 5
```

If conditions fail, use **Fisher's exact test** instead.

---

### 4. Conducting the two-sample z-test

**Test statistic:**

```
         p̂₁ − p̂₂
z = ──────────────────────────────
      √(p̂_pooled(1 − p̂_pooled)(1/n₁ + 1/n₂))

where p̂_pooled = (x₁ + x₂) / (n₁ + n₂)
```

**SciPy/statsmodels implementation:**

```python
from statsmodels.stats.proportion import proportions_ztest

# Defect counts and sample sizes for each line
count = [x1, x2]      # e.g., [15, 22] defects
nobs  = [n1, n2]      # e.g., [200, 250] units inspected

z_stat, p_value = proportions_ztest(count, nobs)
# No value= parameter → compares two proportions (H₀: p₁ = p₂)
```

Pass **vectors** for two-sample comparison; pass a scalar `value=p0` for one-sample tests.

---

### 5. Interpreting the results

**Result from the lecture:**

```
p-value = 0.10
α       = 0.05

p-value (0.10) > α (0.05)  →  fail to reject H₀
```

**Conclusion:**

> "At α = 0.05, we fail to reject H₀. There is no statistically significant difference in defect rates between the two assembly lines (p = 0.10)."

**Engineering/business implication:**

No need to allocate resources to investigate or fix one assembly line over the other based on current data. The observed difference in sample defect rates could plausibly be due to sampling variation.

**If p-value had been < 0.05:** Focus quality improvement efforts on the line with the higher defect rate.

---

### 6. One-sample vs two-sample proportion tests

| Test | Question | `proportions_ztest` call |
|------|----------|--------------------------|
| **One-sample** | Does p differ from p₀? | `proportions_ztest(count, nobs, value=p0)` |
| **Two-sample** | Do p₁ and p₂ differ? | `proportions_ztest([x1,x2], [n1,n2])` |

---

## Takeaways

1. **Two-proportion z-test** — compare defect/rate percentages between two independent groups.
2. **H₀: p₁ = p₂** — fail to reject means rates are statistically equivalent.
3. **Pass vectors** to `proportions_ztest` for two-sample comparison.
4. **Assembly line example** — p = 0.10 → no significant difference; no resource reallocation needed.
5. **Check np ≥ 5** for both groups before using z-test approximation.
6. **Statistical conclusion drives operational decisions** — don't fix what isn't broken.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| One-sample proportion z-test | [`hypothesis-testing-proportions-z-test-lecture-summary.md`](hypothesis-testing-proportions-z-test-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| CLT | [`central-limit-theorem-lecture-summary.md`](central-limit-theorem-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Two-sample proportion z-test:
  H₀: p₁ = p₂     H₁: p₁ ≠ p₂

  p̂₁ = x₁/n₁,  p̂₂ = x₂/n₂
  p̂_pooled = (x₁ + x₂) / (n₁ + n₂)

  statsmodels:
    proportions_ztest([x1, x2], [n1, n2])

Assembly line example:
  H₀: p₁ = p₂
  p = 0.10  →  fail to reject H₀ (no significant difference)
```

**Remember:** A non-significant result means "insufficient evidence of a difference" — not proof the rates are identical.
