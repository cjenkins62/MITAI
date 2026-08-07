# Lecture Summary: Normal Distribution Calculations — SAT Scores with SciPy

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Applied Normal distribution analysis — SAT scores, SciPy, PDF/CDF, and percentiles  
**Format:** Recorded lecture (~12+ min)

---

## Overview

This lecture is the **hands-on companion** to [`normal-distribution-lecture-summary.md`](normal-distribution-lecture-summary.md) — applying Normal distribution theory in Python using **SciPy**. The case study is **SAT exam scores**: calculating probabilities for score ranges, determining **percentile ranks**, and comparing empirical data to a theoretical Normal curve.

The workflow mirrors real statistical analysis: set up the problem → compute sample statistics → visualize → assess normality → calculate forward probabilities (CDF) and reverse probabilities (percentiles / ppf) → draw conclusions about the population from sample data.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:06** | Introduction to Normal distribution calculations |
| **00:31** | SAT exam scores analysis |
| **02:03** | Population vs. sample in Normal distribution |
| **02:19** | Calculating mean and standard deviation |
| **03:50** | Probability density function (PDF) and data visualization |
| **04:48** | Understanding data distribution through plotting |
| **06:45** | Calculating probabilities with CDF |
| **10:18** | Reverse probability calculations and percentiles |
| **12:33** | Conclusion and applications of Normal distribution |

---

## Key Themes

### 1. Problem setup and workflow

The lecture walks through a structured analysis pipeline:

1. Define the business/statistical question
2. Load and inspect the data (SAT scores)
3. Compute descriptive statistics (mean, standard deviation)
4. Visualize empirical vs. theoretical distribution
5. Calculate probabilities and percentiles
6. Interpret results in population terms

Understanding **how data is distributed** is the prerequisite for valid Normal-based inference.

### 2. SAT scores case study

**SAT scores** serve as a realistic example because:

- Scores are continuous and roughly bell-shaped
- Questions are natural: "What percentage of students score above 1200?" or "What score puts you in the 90th percentile?"
- **Percentile rank** — where a given score falls relative to all test-takers — is a direct CDF application

### 3. Population vs. sample

| Concept | Role |
|---------|------|
| **Sample** | Observed SAT scores in your dataset |
| **Population** | All SAT test-takers (or the broader group you want to infer about) |

**Sample statistics** (x̄, s) **estimate population parameters** (μ, σ). Normal distribution calculations use these estimates to model the population and answer inferential questions.

This distinction is critical: probabilities and percentiles describe the **population model**, estimated from **sample data**.

### 4. Mean and standard deviation with SciPy

Using **`scipy.stats`**, compute the foundation for all further analysis:

```python
from scipy.stats import norm
import numpy as np

mu = np.mean(scores)       # sample mean → estimate of μ
sigma = np.std(scores)     # sample std → estimate of σ
```

These two numbers fully parameterize the Normal model: X ~ N(μ, σ²).

### 5. PDF and data visualization

Compare **empirical** and **theoretical** distributions:

| Visualization | Purpose |
|---------------|---------|
| **Histogram / density plot** | Show actual score distribution from data |
| **Theoretical PDF overlay** | Plot N(μ, σ²) curve using sample μ and σ |

**Why compare?** If empirical and theoretical curves align, the Normal assumption is reasonable and CDF-based probabilities are trustworthy. Large gaps suggest skew, outliers, or a different distribution — invalidating Normal-based conclusions.

### 6. CDF — forward probability calculations

The **Cumulative Distribution Function** answers: "What is P(score ≤ x)?"

**Examples:**
- P(score ≤ 1000) — fraction of students at or below 1000
- P(1100 ≤ score ≤ 1300) = CDF(1300) − CDF(1100) — probability of landing in a score band

**SciPy:** `norm.cdf(x, loc=mu, scale=sigma)`

Percentile rank of a score = CDF value × 100 (e.g., CDF = 0.85 → 85th percentile).

### 7. Reverse probability and percentiles

**Reverse (inverse) calculations:** Given a probability, find the score.

**Examples:**
- "What score corresponds to the 90th percentile?" → score where P(X ≤ x) = 0.90
- "What is the cutoff for the top 10%?" → 90th percentile

**SciPy:** `norm.ppf(p, loc=mu, scale=sigma)` — percent point function (inverse CDF)

| Direction | Function | Question |
|-----------|----------|----------|
| **Forward** | `cdf(x)` | Score → probability / percentile |
| **Backward** | `ppf(p)` | Probability / percentile → score |

### 8. Conclusion — Normal as foundation

The Normal distribution is foundational for:

- **Statistical inference** — confidence intervals, hypothesis tests
- **Machine learning** — many algorithms assume or benefit from Normal-like features
- **Decision-making** — risk thresholds, cutoff scores, benchmarking

The lecture sets up the **Central Limit Theorem** as the next topic — explaining why Normal thinking extends even when individual data points are not perfectly Normal.

---

## Takeaways

1. **Sample μ and σ parameterize the model** — use SciPy to compute them, then plug into `norm`.
2. **Plot before you calculate** — overlay empirical density with theoretical PDF to check normality.
3. **CDF for score → percentile** — forward probability; essential for ranking and benchmarking.
4. **ppf for percentile → score** — reverse probability; essential for cutoffs and targets.
5. **Sample estimates population** — always state whether conclusions apply to the sample or inferred population.
6. **Validate assumptions** — Normal-based answers are only as good as the fit between data and bell curve.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Normal distribution theory | [`normal-distribution-lecture-summary.md`](normal-distribution-lecture-summary.md) |
| SciPy uniform / bug-fix example | [`scipy-statistical-analysis-lecture-summary.md`](scipy-statistical-analysis-lecture-summary.md) |
| PDF / CDF foundations | [`probability-lecture-summary.md`](probability-lecture-summary.md) |
| Inferential statistics context | [`statistical-inference-lecture-summary.md`](statistical-inference-lecture-summary.md) |
| Hands-on practice | [`Notebook_Inferential_Statistics.ipynb`](../Notebook_Inferential_Statistics.ipynb) |

---

## Quick reference (SciPy Normal)

```python
from scipy.stats import norm
import numpy as np

mu    = np.mean(scores)
sigma = np.std(scores)

# Forward:  P(X <= x)              → norm.cdf(x, loc=mu, scale=sigma)
# Range:    P(a <= X <= b)         → norm.cdf(b, ...) - norm.cdf(a, ...)
# Backward: score at percentile p  → norm.ppf(p, loc=mu, scale=sigma)
# PDF plot: theoretical curve      → norm.pdf(x, loc=mu, scale=sigma)
```

**Workflow:** Load SAT data → compute μ, σ → plot histogram + PDF overlay → CDF for probabilities → ppf for percentile cutoffs.
