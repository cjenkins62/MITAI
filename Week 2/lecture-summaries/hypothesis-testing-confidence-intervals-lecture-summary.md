# Lecture Summary: Hypothesis Testing and Confidence Intervals

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** The duality between confidence intervals and two-sided hypothesis tests  
**Format:** Recorded lecture (short)

---

## Overview

This lecture connects two core inferential tools — **confidence intervals** and **hypothesis testing** — showing they answer the same underlying question from different angles. A **95% confidence interval** gives a range of plausible parameter values; a **two-sided hypothesis test** checks whether a specific value is plausible. The key insight: **any parameter value outside the confidence interval would be rejected** in a corresponding two-sided test at the same significance level.

Understanding this duality provides a powerful heuristic for interpreting both tools together.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Connection between hypothesis testing and confidence intervals |

---

## Key Themes

### 1. Confidence intervals — what they tell you

A **95% confidence interval** is the range within which the true parameter value is likely to fall, with 95% confidence.

**Example:** A 95% CI of **[9, 11]** for a population mean means:
- The true mean is **likely between 9 and 11**
- Values inside the interval are **consistent with the sample data**
- Values outside the interval are **not supported** by the data at the 5% significance level

**Interpretation:** "We are 95% confident the true parameter lies in this range."

---

### 2. Hypothesis testing — what it tells you

Hypothesis testing evaluates whether a **specific parameter value** (stated in H₀) is supported by the sample data.

**Example:** Testing H₀: μ = 10
- Collect sample data
- Compute test statistic and p-value
- If p-value < 0.05 → reject H₀ (μ = 10 is not supported)
- If p-value ≥ 0.05 → fail to reject H₀ (μ = 10 is plausible)

Both tools ask: **"Is this parameter value consistent with what we observed?"**

---

### 3. The duality — CI and two-sided tests are equivalent

For a **two-sided hypothesis test** at significance level α:

> The **(1 − α) confidence interval** contains **all parameter values for which H₀ would NOT be rejected**.

| Relationship | Rule |
|--------------|------|
| Value **inside** CI | Fail to reject H₀ at level α |
| Value **outside** CI | Reject H₀ at level α |
| 95% CI ↔ two-sided test at α = 0.05 | Same conclusion, different framing |

**Practical heuristic:**

```
If you have a 95% CI of [9, 11]:
  → H₀: μ = 10  →  fail to reject (10 is inside the interval)
  → H₀: μ = 8   →  reject (8 is outside the interval)
  → H₀: μ = 12  →  reject (12 is outside the interval)
```

Building a confidence interval is equivalent to running **all possible two-sided hypothesis tests** at once — any value outside the interval would be rejected.

---

### 4. Side-by-side comparison

| | Confidence Interval | Hypothesis Test |
|---|---------------------|-----------------|
| **Question** | What range of values is plausible? | Is this specific value plausible? |
| **Output** | An interval (e.g., [9, 11]) | Reject or fail to reject H₀ |
| **Framing** | Estimation | Decision |
| **Equivalent to** | All two-sided tests at level α | One specific two-sided test |
| **Typical use** | Report uncertainty around an estimate | Test a specific claim |

Both use the same sample data, same distribution, and same α — they are two views of the same inference.

---

### 5. Why this connection matters

**For interpretation:**
- A CI that excludes a claimed value (e.g., μ₀ = 8 when CI = [9, 11]) immediately tells you H₀ would be rejected — no separate test needed.
- A hypothesis test that rejects H₀: μ = 10 implies 10 falls outside the 95% CI.

**For reporting:**
- Best practice: report **both** the confidence interval and the hypothesis test result. They reinforce each other and give a fuller picture.
- CI shows **magnitude and uncertainty**; hypothesis test gives a **formal yes/no decision**.

**For one-tailed tests:**
- The duality holds for **two-sided tests only**
- One-tailed tests correspond to one-sided confidence bounds (lower or upper bound only), not a symmetric interval

---

## Takeaways

1. **95% CI and two-sided test at α = 0.05 are dual** — same data, same conclusion, different framing.
2. **Values inside the CI → fail to reject H₀**; values outside → reject H₀.
3. **CI answers "what range is plausible?"** — hypothesis test answers "is this specific value plausible?"
4. **Report both** when possible — CI shows uncertainty, test gives a formal decision.
5. **One-tailed tests** use one-sided bounds, not symmetric intervals — duality applies to two-sided tests only.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Estimation & confidence intervals | [`estimation-confidence-intervals-lecture-summary.md`](estimation-confidence-intervals-lecture-summary.md) |
| t-distribution & standard error | [`estimation-t-distribution-lecture-summary.md`](estimation-t-distribution-lecture-summary.md) |
| One- and two-tailed tests | [`hypothesis-testing-one-two-tailed-lecture-summary.md`](hypothesis-testing-one-two-tailed-lecture-summary.md) |
| P-value and e-commerce example | [`hypothesis-testing-pvalue-ecommerce-lecture-summary.md`](hypothesis-testing-pvalue-ecommerce-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Duality rule (two-sided test at α):
  (1 − α) confidence interval = all values of θ for which H₀: θ = θ₀
  would NOT be rejected

Example:
  95% CI = [9, 11]   ↔   two-sided test at α = 0.05

  μ₀ = 10  →  inside CI   →  fail to reject H₀
  μ₀ = 8   →  outside CI  →  reject H₀
  μ₀ = 12  →  outside CI  →  reject H₀

Heuristic:
  Building a CI  ≈  running all two-sided tests at once
```

**Remember:** Confidence intervals and hypothesis tests are complementary — use both for the most complete statistical interpretation.
