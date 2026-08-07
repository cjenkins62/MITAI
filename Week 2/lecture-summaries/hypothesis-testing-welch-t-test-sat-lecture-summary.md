# Lecture Summary: Two-Sample T-Test with Unequal Variances (Welch's T-Test)

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Welch's t-test — SAT verbal scores by parental education background  
**Format:** Recorded lecture (~3+ min)

---

## Overview

This lecture covers how to handle **unequal standard deviations** between two groups when comparing means. When variances differ, the standard pooled t-test is inappropriate — **Welch's t-test** (`equal_var=False`) adjusts for this inequality. The worked example compares **verbal SAT scores** for students whose parents attended college vs those whose parents completed only high school, finding a statistically significant advantage for the college-educated group (p = 0.008).

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:06** | Handling unequal standard deviations in statistical tests |
| **00:28** | SAT scores and parental educational background |
| **01:10** | One-tailed hypothesis testing in education |
| **01:47** | Executing a two-sample t-test with unequal variances |
| **02:49** | Interpreting statistical results in educational research |

---

## Key Themes

### 1. Why unequal variances matter

The standard two-sample t-test **assumes equal variances** (σ₁² = σ₂²) and pools them into a single estimate. When variances differ:

- Pooled standard error is **misleading**
- Test statistic and p-value are **inaccurate**
- Type I error rate may be **inflated**

**Solution:** Use **Welch's t-test**, which does not assume equal variances and adjusts degrees of freedom accordingly.

```
Pooled t-test:     assumes σ₁² = σ₂²
Welch's t-test:    allows σ₁² ≠ σ₂²  ← use when variances differ
```

**When in doubt, default to Welch's** — it performs well even when variances are equal.

---

### 2. SAT scores and parental education

**Research question:** Does parental educational background influence student SAT verbal performance?

**Two groups:**
- **Group 1:** Students whose parents attended college
- **Group 2:** Students whose parents completed only high school

**Data:** Verbal SAT scores from [`../SATVerbal1.csv`](../SATVerbal1.csv)

**Why unequal variances likely:** Different groups may have different score spreads — college-educated families may show more or less variability in outcomes.

---

### 3. One-tailed hypothesis setup

When the research question is **directional** — predicting one group will score higher:

```
H₀:  μ_college ≤ μ_highschool    (college-parent students ≤ high-school-parent students)
H₁:  μ_college > μ_highschool    (college-parent students score higher)
α   = 0.05
```

**One-tailed vs two-tailed:** Use one-tailed when you have a specific directional prediction before seeing the data. Use two-tailed when any difference matters.

---

### 4. Executing Welch's t-test

**SciPy implementation:**

```python
from scipy.stats import ttest_ind

# Welch's t-test (unequal variances)
t_stat, p_value = ttest_ind(
    college_parent_scores,
    highschool_parent_scores,
    equal_var=False    # ← key parameter for Welch's t-test
)

# For one-tailed test (H₁: μ_college > μ_highschool):
# if t_stat > 0:  p_one_tailed = p_value / 2
# else:           p_one_tailed = 1 - p_value / 2
```

**Welch's standard error** (does not pool variances):

```
         x̄₁ − x̄₂
t = ─────────────────────
      √(s₁²/n₁ + s₂²/n₂)

df ≈ Welch-Satterthwaite equation (non-integer, computed automatically)
```

---

### 5. Interpreting the results

**Result from the lecture:**

```
p-value = 0.008  (one-tailed)
α       = 0.05

p-value (0.008) < α (0.05)  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. There is strong evidence that students with college-educated parents have significantly higher average verbal SAT scores than students whose parents completed only high school (p = 0.008)."

**Educational implications:**
- Parental education appears to be associated with student verbal achievement
- Findings may inform educational policy — support programs for first-generation college-bound students
- **Caution:** Statistical association ≠ causation — many confounding factors (income, school quality, home environment) may explain the difference

---

### 6. Pooled vs Welch's — decision guide

| Situation | Test | SciPy |
|-----------|------|-------|
| Variances appear equal | Pooled t-test | `ttest_ind(a, b)` |
| Variances appear unequal | Welch's t-test | `ttest_ind(a, b, equal_var=False)` |
| Unsure | **Welch's (safer default)** | `ttest_ind(a, b, equal_var=False)` |

Check variance equality visually (box plots) or with an **F-test** before choosing, but Welch's is robust either way.

---

## Takeaways

1. **Unequal variances invalidate the pooled t-test** — use Welch's t-test instead.
2. **`equal_var=False`** in `ttest_ind` activates Welch's t-test in SciPy.
3. **One-tailed test** when you predict direction before collecting data.
4. **SAT example** — p = 0.008 → college-parent students score significantly higher on verbal SAT.
5. **Statistical significance ≠ causation** — parental education correlates with SAT scores; many factors may drive this.
6. **Default to Welch's** when uncertain about variance equality.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Two-sample t-test (equal variances) | [`hypothesis-testing-two-sample-t-test-lecture-summary.md`](hypothesis-testing-two-sample-t-test-lecture-summary.md) |
| One- and two-tailed tests | [`hypothesis-testing-one-two-tailed-lecture-summary.md`](hypothesis-testing-one-two-tailed-lecture-summary.md) |
| Normal distribution & SAT scores | [`normal-distribution-scipy-sat-lecture-summary.md`](normal-distribution-scipy-sat-lecture-summary.md) |
| SAT verbal data | [`../SATVerbal1.csv`](../SATVerbal1.csv) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Welch's t-test (unequal variances):
  H₀: μ₁ = μ₂     H₁: μ₁ > μ₂  (one-tailed example)

  ttest_ind(group1, group2, equal_var=False)

SAT verbal example:
  H₀: μ_college ≤ μ_highschool
  H₁: μ_college > μ_highschool
  p = 0.008  →  reject H₀ (college-parent students score higher)
```

**Remember:** Welch's t-test is the safer default — it handles both equal and unequal variances correctly.
