# Lecture Summary: Chi-Square Test of Independence

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Chi-square test of independence — contingency tables, categorical associations  
**Format:** Recorded lecture (~5+ min)

---

## Overview

This lecture covers the **chi-square test of independence**, a frequency-based method for determining whether two **categorical variables** are associated. Data is organized in **contingency tables** (cross-tabulations) showing observed counts — e.g., gender vs smoking habits, or beverage preference vs age group. The test compares **observed vs expected frequencies** to compute a chi-square statistic. The worked example uses [`Beverage.csv`](../Beverage.csv) to test whether beverage preference depends on age, yielding **p ≈ 5.41e-10** — strong evidence of association. This differs from the **chi-square variance test** (one-sample spread); here chi-square measures **relationships between categories**.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to frequency tests |
| **00:40** | Chi-square test of independence |
| **01:11** | Contingency tables and statistical independence |
| **02:01** | Calculating chi-square statistic |
| **03:48** | Chi-square test application and assumptions |
| **04:40** | Interpreting chi-square test results |

---

## Key Themes

### 1. Frequency tests and independence

Unlike tests for means or proportions, **frequency tests** analyze **count data** in categorical tables:

| Question | Example |
|----------|---------|
| Are two variables **independent**? | Is smoking habit unrelated to gender? |
| Is there a **significant association**? | Does beverage preference vary by age group? |

**Independence** means knowing one variable tells you nothing about the other. The chi-square test checks whether observed counts deviate enough from what independence would predict.

---

### 2. Contingency tables

A **contingency table** (cross-tabulation) displays the frequency distribution of two categorical variables:

**Example 1 — Gender × Smoking (conceptual):**

| | Smoker | Non-smoker |
|---|--------|------------|
| Male | O₁₁ | O₁₂ |
| Female | O₂₁ | O₂₂ |

**Example 2 — Age × Beverage preference** ([`Beverage.csv`](../Beverage.csv)):

| Age | Tea/Coffee | Soft Drink | Others |
|-----|------------|------------|--------|
| 21–34 | 25 | 90 | 20 |
| 35–55 | 40 | 35 | 25 |
| > 55 | 24 | 15 | 30 |

Each cell contains an **observed frequency (O)** — the actual count in that category combination.

---

### 3. Hypotheses

```
H₀:  The two variables are independent (no association)
H₁:  The two variables are associated (not independent)
α   = 0.05
```

**Beverage example:**

```
H₀:  Beverage preference is independent of age
H₁:  Beverage preference depends on age
```

This is always a **right-tailed** test — large χ² values indicate departure from independence.

---

### 4. Calculating the chi-square statistic

For each cell, compute the **expected frequency (E)** under independence:

```
E = (row total × column total) / grand total
```

**Test statistic:**

```
χ² = Σ  (O − E)² / E

summed over all cells in the table
```

| Component | Meaning |
|-----------|---------|
| O | Observed count in a cell |
| E | Expected count if variables were independent |
| (O − E)² / E | Squared standardized deviation for that cell |

**Degrees of freedom:**

```
df = (r − 1)(c − 1)

where r = number of rows, c = number of columns
```

For the beverage table (3 age groups × 3 beverage types): df = (3−1)(3−1) = **4**.

Compare χ² to the chi-square distribution with df to get the p-value.

---

### 5. Assumptions

| Assumption | Requirement |
|------------|-------------|
| **Categorical variables** | Both variables are nominal or ordinal categories |
| **Expected count ≥ 5** | Each cell's expected frequency must be at least 5 |
| **Random sampling** | Observations are independent, randomly sampled |
| **Mutually exclusive** | Each observation falls in exactly one cell |

If expected counts fall below 5, combine categories or use Fisher's exact test for 2×2 tables.

---

### 6. Application — beverage preference and age

**SciPy implementation (from course notebook):**

```python
import pandas as pd
from scipy.stats import chi2_contingency

beverage = pd.read_csv('Beverage.csv')

# contingency table: rows = age groups, columns = beverage types
chi, p_value, dof, expected = chi2_contingency(
    beverage.drop('Age', axis=1)
)

print(f'χ² = {chi:.2f}, df = {dof}, p = {p_value}')
# p ≈ 5.41e-10
print(expected)   # expected frequencies under independence
```

**Alternative with `pd.crosstab`:**

```python
table = pd.crosstab(beverage['Age'], beverage.columns[1:])
chi, p_value, dof, expected = chi2_contingency(table)
```

---

### 7. Interpreting results

**Result from the course notebook:**

```
p-value ≈ 5.41e-10  (essentially 0)
α       = 0.05

p-value << α  →  reject H₀
```

**Conclusion:**

> "At α = 0.05, we reject H₀. Beverage preference is significantly associated with age (p ≈ 5.41e-10). Preference is not independent of age group."

**Practical reading:** Younger groups (21–34) heavily favor soft drinks (90 vs 25 tea/coffee), while older groups shift toward tea/coffee and "others." Marketing or product decisions can use this association.

**If p ≥ α:** Fail to reject H₀ — no significant evidence of association; the variables appear independent.

**Important:** Rejecting independence shows an association exists — it does **not** prove causation.

---

## Chi-square test family — don't confuse them

| Test | Question | Data type |
|------|----------|-----------|
| **Chi-square variance** (one sample) | Does σ² equal a known value? | Continuous numeric |
| **Chi-square independence** (this lecture) | Are two categorical variables related? | Count/frequency tables |
| **Chi-square goodness of fit** | Do observed counts match expected proportions? | Single categorical variable |

See [`hypothesis-testing-variance-chi-square-lecture-summary.md`](hypothesis-testing-variance-chi-square-lecture-summary.md) for the variance test.

---

## Takeaways

1. **Chi-square test of independence** — tests association between two categorical variables.
2. **Contingency tables** — organize observed counts; compare O vs E under independence.
3. **Formula:** χ² = Σ(O − E)²/E, df = (r−1)(c−1).
4. **Assumption:** expected count ≥ 5 in every cell.
5. **Beverage × age:** p ≈ 5.41e-10 → reject H₀; preference significantly depends on age.
6. **Low p-value** → reject independence → meaningful association between variables.
7. **Next up:** ANOVA (comparing means across groups) and regression analysis build on these foundations.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Test types overview | [`hypothesis-testing-types-overview-lecture-summary.md`](hypothesis-testing-types-overview-lecture-summary.md) |
| Chi-square variance test (different use) | [`hypothesis-testing-variance-chi-square-lecture-summary.md`](hypothesis-testing-variance-chi-square-lecture-summary.md) |
| Hypothesis testing template | [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| Beverage data | [`../Beverage.csv`](../Beverage.csv) |
| Hands-on chi-square code | [`../Notebook - Hypothesis Testing Optional Content.ipynb`](../Notebook%20-%20Hypothesis%20Testing%20Optional%20Content.ipynb) |
| Main hypothesis notebook | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Chi-square test of independence:
  H₀: variables are independent
  H₁: variables are associated

  χ² = Σ (O − E)² / E
  E  = (row total × column total) / grand total
  df = (r − 1)(c − 1)

  Assumption: expected count ≥ 5 in each cell

Beverage × age example:
  p ≈ 5.41e-10  →  reject H₀ at α = 0.05
  → beverage preference depends on age group
```

**Remember:** Association ≠ causation — a significant chi-square test identifies a relationship, not its direction or cause.
