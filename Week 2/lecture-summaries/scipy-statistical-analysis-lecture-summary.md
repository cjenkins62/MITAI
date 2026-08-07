# Lecture Summary: Statistical Analysis with SciPy — Bug Fix Time Example

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Applied statistical analysis — SciPy distributions, visualization, and probability calculations  
**Format:** Recorded lecture (~7+ min)

---

## Overview

This lecture bridges **theory and code** — using Python libraries (notably **SciPy**) to perform distribution-based statistical analysis on real data. The running example is **time to fix bugs**, a practical software development / project management use case.

The workflow covers: loading libraries → treating a **sample as a model for the population** → visualizing the data → assuming a **uniform distribution** → calculating probabilities via **CDF** → finding **percentiles and median** → and working in both **forward** and **backward** probability directions.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Introduction to required libraries |
| **00:27** | Analyzing time to fix bugs |
| **01:04** | Sample as a model for population |
| **01:38** | Visualizing data distribution |
| **02:05** | Probability density function and density plot |
| **02:54** | Uniform distribution assumption |
| **03:36** | Calculating probabilities with uniform distribution |
| **05:17** | Understanding percentile and median calculations |
| **07:00** | Forward and backward probability calculations |

---

## Key Themes

### 1. Required libraries (SciPy)

The lecture opens with the **Python libraries** needed for statistical work — **SciPy** in particular for distribution calculations (PMF, PDF, CDF, percentiles). These libraries turn distribution theory into executable analysis without hand-deriving every formula.

### 2. Bug fix time — the practical example

**Scenario:** Analyze how long it takes to fix bugs.

**Business questions:**
- What is the probability a bug is fixed within a given time window?
- What is the **median** fix time?
- How can this inform staffing, SLAs, and project planning?

Continuous time data makes this a natural fit for **PDF/CDF** methods rather than discrete counting (Binomial).

### 3. Sample → population (inferential framing)

A **sample of bug-fix times** is used as a **model for the broader population** of all bug fixes. This is core inferential statistics: you observe a subset and draw conclusions about the larger process you cannot fully observe.

**Implication:** Distribution assumptions and sample quality directly affect how trustworthy your probability estimates are.

### 4. Data visualization

Before calculating, **visualize**:

| Plot | Purpose |
|------|---------|
| **Histogram** | See how observed fix times are distributed across bins |
| **Density plot** | Smooth view of the **PDF** — where values cluster and how spread out they are |

Visualization helps you choose a reasonable distribution model and spot outliers or skew.

### 5. PDF and uniform distribution assumption

The lecture connects the **probability density function (PDF)** to **density plots** for continuous data.

For this example, a **uniform distribution** is assumed — any fix time within the observed [min, max] range is equally likely. This simplifies calculations but should be validated against the histogram/density plot.

**Continuous uniform probability:**

P(c ≤ X ≤ d) = (d − c) / (b − a)

where [a, b] is the range of the uniform distribution.

### 6. CDF for probability calculations

The **Cumulative Distribution Function (CDF)** answers threshold questions:

- P(fix time ≤ t) — "What fraction of bugs are fixed by time t?"
- Essential for **risk assessment** and **decision-making** (e.g., can we meet a deadline with 90% confidence?)

SciPy provides CDF methods directly on distribution objects — e.g., `uniform.cdf(x, loc=a, scale=b-a)`.

### 7. Percentiles and median

**Percentiles** summarize where values fall in the distribution:

- **Median (50th percentile)** — half of bug fixes finish faster, half slower
- Other percentiles (e.g., 90th) — "90% of fixes complete within X hours"

These are central tendency and spread summaries that stakeholders understand without probability notation.

### 8. Forward vs. backward probability

Two directions of the same distribution machinery:

| Direction | Question | Example |
|-----------|----------|---------|
| **Forward** | Given a time threshold, what is the probability? | P(fix ≤ 4 hours) = ? |
| **Backward (inverse CDF / ppf)** | Given a probability, what is the time threshold? | What time t gives P(fix ≤ t) = 0.90? |

- **Forward** → predictive / risk questions
- **Backward** → planning / SLA setting ("we need a deadline that 90% of fixes beat")

SciPy: `cdf` for forward, `ppf` (percent point function) for backward.

---

## Takeaways

1. **SciPy makes distribution math practical** — PDF, CDF, percentiles, and inverse CDF are one function call away.
2. **Visualize before you model** — histograms and density plots validate (or challenge) your distribution assumption.
3. **Sample models population** — inferential conclusions depend on representative sampling.
4. **Uniform is a starting assumption** — simple for continuous ranges, but check if the data actually looks flat.
5. **Forward and backward are complementary** — probability given time vs. time given probability; both matter for planning.
6. **Median and percentiles communicate clearly** — often more actionable than raw probabilities for engineering teams.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Uniform distribution theory | [`uniform-distribution-lecture-summary.md`](uniform-distribution-lecture-summary.md) |
| PDF / CDF foundations | [`probability-lecture-summary.md`](probability-lecture-summary.md) |
| Inferential statistics context | [`statistical-inference-lecture-summary.md`](statistical-inference-lecture-summary.md) |
| Hands-on practice | [`Notebook_Inferential_Statistics.ipynb`](../Notebook_Inferential_Statistics.ipynb) |

---

## Quick reference (SciPy uniform)

```python
from scipy.stats import uniform

# Uniform on [a, b]: loc=a, scale=(b-a)
# Forward:  P(X <= x)           → uniform.cdf(x, loc=a, scale=b-a)
# Backward: x where P(X <= x)=p → uniform.ppf(p, loc=a, scale=b-a)
# Median:                       → uniform.ppf(0.5, loc=a, scale=b-a)
```

**Workflow:** Load data → plot histogram/density → define range [a, b] → compute CDF probabilities and percentiles → use ppf for SLA/deadline planning.
