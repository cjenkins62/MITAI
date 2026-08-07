# Lecture Summary: Overview of Hypothesis Test Types

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Catalog of hypothesis tests — means, proportions, variances, and categorical data  
**Format:** Recorded lecture (~6+ min)

---

## Overview

This lecture provides a **roadmap of hypothesis tests** used in business statistics, organized by the type of quantity being evaluated: **means**, **proportions**, **variances**, or **frequencies/categories**. Rather than diving into formulas, it focuses on **when to use each test** and what business question each one answers — giving you a framework for selecting the right tool.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to hypothesis testing |
| **00:47** | Framework for hypothesis tests |
| **01:20** | One sample Z-test |
| **01:50** | One sample T-test |
| **02:01** | Two sample Z-test and T-test |
| **02:38** | Paired T-test |
| **03:09** | ANOVA (Analysis of Variance) |
| **03:33** | Proportion tests |
| **04:30** | Chi-square test for variances |
| **05:08** | F-test for comparing variances |
| **05:51** | Chi-square test of independence |

---

## Key Themes

### 1. Framework for selecting a test

Choose a test based on **what you're measuring** and **your data structure**:

| Quantity | # of groups | Related/paired? | Test |
|----------|-------------|-----------------|------|
| **Mean (μ)** | 1 sample | — | One-sample z-test or t-test |
| **Mean (μ)** | 2 independent groups | No | Two-sample z-test or t-test |
| **Mean (μ)** | 2 related groups | Yes | Paired t-test |
| **Mean (μ)** | 3+ groups | — | ANOVA |
| **Proportion (p)** | 1 sample | — | One-sample z-test for proportions |
| **Proportion (p)** | 2 groups | — | Two-proportion z-test |
| **Variance (σ²)** | 1 sample | — | Chi-square test for variance |
| **Variance (σ²)** | 2 groups | — | F-test |
| **Categories** | 2 variables | — | Chi-square test of independence |

**Decision flow:**
1. What parameter? (mean, proportion, variance, association)
2. How many groups or samples?
3. Are observations paired/related or independent?
4. Is σ known (z) or unknown (t)?

---

### 2. Tests for means

#### One-sample Z-test
- **Question:** Does the sample mean differ from a known population mean?
- **When:** σ is **known** and n is large (or population is normal)
- **Example:** Is average delivery time different from the 5-day target?

#### One-sample T-test
- **Question:** Same as Z-test, but σ is **unknown** (estimated from sample)
- **When:** σ not known — use sample standard deviation s
- **Example:** Is average employee salary different from the industry benchmark?

#### Two-sample Z-test / T-test
- **Question:** Do two **independent** groups have different means?
- **When:** Two separate samples, no pairing between observations
- **Example:** Do sales differ between Region A and Region B?

#### Paired T-test
- **Question:** Is there a difference between **related/matched** observations?
- **When:** Same subjects measured twice (before/after), or naturally paired data
- **Example:** Did a training program improve test scores for the same employees?

#### ANOVA (Analysis of Variance)
- **Question:** Do **three or more groups** have different means?
- **When:** Comparing multiple treatment groups, product variants, or store locations
- **Note:** ANOVA tests whether *any* group differs — follow-up tests identify which pairs differ
- **Example:** Do customer satisfaction scores differ across 4 store locations?

---

### 3. Tests for proportions

#### One-sample Z-test for proportions
- **Question:** Does a sample proportion differ from a claimed population proportion?
- **When:** Evaluating yes/no or categorical outcomes against a benchmark
- **Example:** Is the defect rate higher than the 2% tolerance?

#### Two-proportion Z-test
- **Question:** Do two groups have different proportions?
- **When:** Comparing rates between two independent groups
- **Example:** Is the conversion rate different for Campaign A vs Campaign B?

**Assumption:** np ≥ 5 and n(1−p) ≥ 5 for each group.

---

### 4. Tests for variances

#### Chi-square test for variance (one sample)
- **Question:** Does sample variability differ from a specified population variance?
- **When:** Quality control — checking if process variability meets spec
- **Example:** Is the standard deviation of bottle fill volume within the 50 ml tolerance?

#### F-test (two variances)
- **Question:** Do two groups have **equal variances**?
- **When:** Comparing spread between two processes or populations
- **Example:** Is Machine A more consistent (lower variance) than Machine B?
- **Also used as:** A preliminary check before two-sample t-test (equal variance assumption)

---

### 5. Chi-square test of independence

- **Question:** Are two **categorical variables** related?
- **When:** Analyzing contingency tables (cross-tabulations)
- **Example:** Is product preference (A/B/C) associated with customer age group?
- **H₀:** Variables are independent (no association)
- **H₁:** Variables are associated

Uses **observed vs expected frequencies** — not means or proportions directly.

---

## Test selection cheat sheet

```
MEANS
  1 sample, σ known     →  One-sample z-test
  1 sample, σ unknown   →  One-sample t-test
  2 independent groups  →  Two-sample z/t-test
  2 paired groups         →  Paired t-test
  3+ groups               →  ANOVA

PROPORTIONS
  1 sample              →  One-sample z-test for proportions
  2 groups              →  Two-proportion z-test

VARIANCES
  1 sample              →  Chi-square test for variance
  2 groups              →  F-test

CATEGORICAL / FREQUENCY
  2 categorical vars    →  Chi-square test of independence
```

---

## Takeaways

1. **Match the test to the parameter** — mean, proportion, variance, or category association.
2. **Sample structure matters** — one vs two vs many groups; independent vs paired.
3. **Z vs t for means** — use z when σ is known; t when σ must be estimated from the sample.
4. **ANOVA extends two-sample t-test** to 3+ groups — don't run multiple pairwise t-tests.
5. **Variance tests support quality control** — ensuring consistency, not just average performance.
6. **Chi-square test of independence** is for categorical relationships, not numeric comparisons.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Testing template (6 steps) | [`hypothesis-testing-template-lecture-summary.md`](hypothesis-testing-template-lecture-summary.md) |
| One- and two-tailed tests | [`hypothesis-testing-one-two-tailed-lecture-summary.md`](hypothesis-testing-one-two-tailed-lecture-summary.md) |
| t-distribution | [`estimation-t-distribution-lecture-summary.md`](estimation-t-distribution-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

| Test | H₀ (typical) | Business use |
|------|-------------|--------------|
| One-sample z/t | μ = μ₀ | Does average meet spec? |
| Two-sample z/t | μ₁ = μ₂ | Do two groups differ? |
| Paired t | μ_diff = 0 | Did treatment change outcomes? |
| ANOVA | μ₁ = μ₂ = … = μ_k | Do any groups differ? |
| One-proportion z | p = p₀ | Is rate at benchmark? |
| Two-proportion z | p₁ = p₂ | Do two rates differ? |
| Chi-square (variance) | σ² = σ₀² | Is variability within spec? |
| F-test | σ₁² = σ₂² | Are two processes equally consistent? |
| Chi-square (independence) | Variables independent | Are two categories related? |

**Remember:** This catalog tells you *which* test to use — the hypothesis testing template tells you *how* to run it.
