# Lecture Summary: Paired Sample T-Test

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Paired t-test — comparing related measurements (house prices 2002 vs 2003)  
**Format:** Recorded lecture (~3+ min)

---

## Overview

This lecture covers the **paired sample t-test** — used when two measurements are **related** (same subjects, before/after, matched pairs) rather than independent. The worked example compares **house prices in 2002 vs 2003** for the same properties, testing whether there was a significant increase. The key insight: reduce paired data to **differences**, then run a one-sample t-test on those differences.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Understanding paired sample t-test |
| **00:24** | Data collection for paired sample t-test |
| **02:28** | Executing the paired sample t-test |

---

## Key Themes

### 1. When to use a paired t-test

Use when observations come in **natural pairs**:

| Scenario | Example |
|----------|---------|
| **Before/after** | Same patients measured pre- and post-treatment |
| **Repeated measures** | Same houses priced in 2002 and 2003 |
| **Matched pairs** | Twins, siblings, or deliberately matched subjects |
| **Same subject, two conditions** | Employee productivity with and without training |

**Do NOT use paired t-test when groups are independent** — use two-sample t-test (`ttest_ind`) instead.

**Key question:** Is each observation in group 1 linked to a specific observation in group 2?

---

### 2. Paired vs independent — decision guide

| | Paired t-test | Two-sample t-test |
|---|---------------|-------------------|
| Relationship | **Matched/related** observations | **Independent** groups |
| Data structure | Two columns, row-aligned | Two separate samples |
| What is tested | Mean of **differences** (d = x₂ − x₁) | Difference of **means** (x̄₂ − x̄₁) |
| SciPy | `ttest_rel(a, b)` | `ttest_ind(a, b)` |
| Power | Usually **higher** (controls for subject variability) | Lower (between-subject noise included) |

Paired designs are more powerful because each subject serves as its own control.

---

### 3. Data collection — house price example

**Research question:** Did house prices increase significantly from 2002 to 2003?

**Data structure:** Two columns, one row per house:

| House | Price_2002 | Price_2003 |
|-------|-----------|-----------|
| 1 | $180,000 | $195,000 |
| 2 | $220,000 | $235,000 |
| 3 | $150,000 | $160,000 |
| ... | ... | ... |

**Critical:** Rows must be **aligned** — row 1 in column A corresponds to the same house as row 1 in column B. Misalignment invalidates the test.

---

### 4. Hypothesis setup

**Two-tailed (any change):**

```
H₀:  μ_diff = 0      (no change in average house price)
H₁:  μ_diff ≠ 0      (average price changed)
```

**One-tailed (directional — increase):**

```
H₀:  μ_diff ≤ 0      (no increase)
H₁:  μ_diff > 0      (prices increased)
α   = 0.05
```

Where **μ_diff** = mean of (Price_2003 − Price_2002) across all houses.

---

### 5. Executing the paired t-test

**Concept:** Compute differences dᵢ = x₂ᵢ − x₁ᵢ for each pair, then test whether the mean difference differs from zero.

**Test statistic:**

```
         d̄ − 0
t = ─────────────
      s_d / √n

where d̄ = mean of differences
      s_d = standard deviation of differences
      df = n − 1
```

**SciPy implementation:**

```python
from scipy.stats import ttest_rel

# prices_2002 and prices_2003 must be aligned (same row = same house)
t_stat, p_value = ttest_rel(prices_2003, prices_2002)

# Equivalent manual approach:
differences = prices_2003 - prices_2002
ttest_1samp(differences, popmean=0)
```

Both approaches give the same result. `ttest_rel` is preferred for clarity.

---

### 6. Interpreting results

**Decision rule:**

```
p-value < α  →  reject H₀  (significant difference between paired measurements)
p-value ≥ α  →  fail to reject H₀  (no significant difference)
```

**Example conclusion (if significant):**

> "At α = 0.05, we reject H₀. There is sufficient evidence that average house prices increased significantly from 2002 to 2003 (p < 0.05)."

**Example conclusion (if not significant):**

> "At α = 0.05, we fail to reject H₀. There is no statistically significant change in average house prices from 2002 to 2003."

Always state the conclusion in the context of the business or research question.

---

## Takeaways

1. **Paired t-test** — for related/matched measurements, not independent groups.
2. **Reduce to differences** — d = x₂ − x₁, then test if mean(d) ≠ 0.
3. **Data must be row-aligned** — each pair must correspond correctly.
4. **More powerful than independent t-test** — controls for subject-level variability.
5. **SciPy:** `ttest_rel(group2, group1)` — order matters for one-tailed interpretation.
6. **Wrong test = wrong conclusion** — using `ttest_ind` on paired data ignores the pairing and loses power.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Two-sample t-test (independent) | [`hypothesis-testing-two-sample-t-test-lecture-summary.md`](hypothesis-testing-two-sample-t-test-lecture-summary.md) |
| One-sample t-test | [`hypothesis-testing-one-sample-t-test-lecture-summary.md`](hypothesis-testing-one-sample-t-test-lecture-summary.md) |
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Paired t-test:
  H₀: μ_diff = 0     H₁: μ_diff ≠ 0  (or > / < for one-tailed)

  d_i = x_{2i} - x_{1i}
  t = d̄ / (s_d / √n)

  SciPy:
    ttest_rel(after, before)

House price example:
  Same houses, two time points (2002 vs 2003)
  Row-aligned data → test if mean price change ≠ 0
```

**Remember:** Pairing is a feature of the study design — recognize it before choosing the test.
