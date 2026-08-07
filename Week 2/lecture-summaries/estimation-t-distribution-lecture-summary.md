# Lecture Summary: Estimation Techniques — SE, Confidence Intervals & t-Distribution

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Applied estimation — wildfire & coffee examples, standard error, t-distribution  
**Format:** Recorded lecture (~9+ min)

---

## Overview

This lecture is the **applied companion** to [`estimation-confidence-intervals-lecture-summary.md`](estimation-confidence-intervals-lecture-summary.md). It walks through **point and interval estimation** with real examples — **wildfire damage** (n = 10) and a **coffee machine** case — and explains the tools needed to build reliable confidence intervals: **standard deviation vs. standard error**, and the **t-distribution** when σ is unknown.

The emphasis is on **accounting for uncertainty**: point estimates alone are insufficient; intervals, SE, and the correct distribution (Normal vs. t) make estimates trustworthy.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Point and interval estimation |
| **02:56** | Sample variability and confidence intervals |
| **06:32** | Standard deviation vs. standard error |
| **08:48** | t-Distribution and its application |

---

## Key Themes

### 1. Point vs. interval estimation (wildfire example)

**Point estimation:** A single sample statistic estimates the population parameter.

**Example — wildfire damages:**
- Sample of **10 incidents** used to estimate future/average wildfire damage
- Sample mean = **point estimate** of population mean damage

**Problem:** The point estimate gives one number with **no sense of uncertainty**. Different samples of 10 would yield different means.

**Interval estimation:** A **confidence interval** provides a **range** likely to contain the true population parameter, incorporating **sample variability**.

### 2. Sample variability and confidence intervals

Because samples vary, estimates vary. Confidence intervals:

- Center on the point estimate (e.g., x̄)
- Extend above and below by a margin based on variability and chosen confidence level
- Give a **more reliable** statement than a single number

**Goal:** Quantify how much trust to place in the sample-based estimate when projecting to the population or future.

### 3. Standard deviation vs. standard error

Critical distinction for building CIs:

| Measure | What it describes | Formula (typical) |
|---------|-------------------|-------------------|
| **Standard deviation (s or σ)** | Spread of **individual data points** in the sample/population | Variability of raw values |
| **Standard error (SE)** | Spread of the **sample mean** across repeated samples | **SE = s / √n** (when σ unknown, use s) |

**Why it matters:**
- Use **SD** when describing how scattered individual observations are
- Use **SE** when describing how precisely x̄ estimates μ — **SE belongs in confidence interval formulas**

Confusing SD and SE leads to incorrect intervals and over- or under-stated precision.

### 4. t-Distribution — when σ is unknown

When the **population standard deviation σ is unknown** (almost always in practice), you estimate it with sample **s** — adding extra uncertainty.

**t-distribution:**
- Similar shape to **Normal** (bell-shaped, symmetric)
- **Heavier tails** — accounts for estimating σ from the sample
- Depends on **degrees of freedom** (df = n − 1)
- As n increases, t → Normal

**When to use t:**
- σ **unknown** (use s instead)
- Especially important for **small samples (n < 30)**
- Still appropriate for larger n when σ is estimated

**Coffee machine example:** Demonstrates t-based interval estimation when working with small samples and unknown σ — gives a more accurate reflection of uncertainty than assuming a known σ.

### 5. Normal vs. t — practical rule

| Situation | Distribution |
|-----------|--------------|
| σ known, large n | **z** (Standard Normal) |
| σ unknown (use s), any n | **t** (Student's t) |
| n ≥ 30, σ unknown | t and z are close; t is still correct |

When in doubt with sample data and unknown σ, use **t**.

---

## Takeaways

1. **Point estimate alone hides uncertainty** — wildfire example shows why intervals matter.
2. **SD ≠ SE** — SD for individual spread; SE = s/√n for mean precision.
3. **Use SE in confidence intervals** — not raw standard deviation.
4. **t-distribution when σ is unknown** — heavier tails capture extra uncertainty from estimating s.
5. **Small n (< 30) → t is essential** — coffee machine example; don't use z blindly.
6. **Always account for variability** — core of responsible statistical inference.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Estimation theory & CI interpretation | [`estimation-confidence-intervals-lecture-summary.md`](estimation-confidence-intervals-lecture-summary.md) |
| Inferential statistics overview | [`statistical-inference-lecture-summary.md`](statistical-inference-lecture-summary.md) |
| Normal distribution & z-scores | [`normal-distribution-lecture-summary.md`](normal-distribution-lecture-summary.md) |
| CLT & sampling distribution of mean | [`central-limit-theorem-simulation-lecture-summary.md`](central-limit-theorem-simulation-lecture-summary.md) |
| Hands-on practice | [`../Notebook_Inferential_Statistics.ipynb`](../Notebook_Inferential_Statistics.ipynb) |

---

## Quick reference

```
Standard error:     SE = s / √n        (when σ unknown)

Confidence interval (μ, σ unknown):
  x̄ ± t* × (s / √n)                  (use t with df = n − 1)

vs. z-interval (σ known):
  x̄ ± z* × (σ / √n)

SciPy:  from scipy.stats import t
        t.ppf(0.975, df=n-1)          # critical value for 95% two-tailed
```

**Decision flow:** Have sample only? → σ unknown → use **s** and **t-distribution**.
