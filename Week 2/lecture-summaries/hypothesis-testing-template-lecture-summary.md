# Lecture Summary: Template for Hypothesis Testing

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Structured step-by-step template for conducting hypothesis tests  
**Format:** Recorded lecture (short)

---

## Overview

This lecture presents a **systematic template** for conducting hypothesis tests — a repeatable workflow that ensures accurate, meaningful results. Rather than jumping straight to calculations, the template walks through each decision in order: defining the question, stating hypotheses, preparing data, choosing the right test, validating assumptions, and drawing conclusions.

Following this structure is essential for **reliable inference** and for applying statistical methods correctly across research and business contexts.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Template for hypothesis testing |

---

## Key Themes

### The hypothesis testing template (6 steps)

```
Step 1  →  Identify the key question
Step 2  →  State H₀ and H₁
Step 3  →  Prepare the data
Step 4  →  Select the test and test statistic
Step 5  →  Check test assumptions
Step 6  →  Perform the test and draw conclusions
```

---

### Step 1: Identify the key question

Start by clarifying **what you want to know**:

- What population parameter is in question? (μ, p, difference between groups, etc.)
- Is this a one-sample, two-sample, or paired comparison?
- What decision will the result inform?

A well-defined question drives every subsequent step. Without it, you risk choosing the wrong test or misinterpreting results.

**Example questions:**
- "Does the mean bulb lifespan exceed 1,000 hours?"
- "Is the proportion of defective units above the 2% tolerance?"
- "Did the new training program improve test scores?"

---

### Step 2: Establish H₀ and H₁

Translate the question into **formal hypotheses**:

| Hypothesis | Role |
|------------|------|
| **H₀ (null)** | Status quo — contains equality (=, ≤, ≥) |
| **H₁ (alternative)** | What you suspect — contains inequality (≠, <, >) |

Also decide:
- **One-tailed vs. two-tailed** — based on whether direction matters
- **Significance level α** — typically 0.05

See [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) for detailed formulation rules.

---

### Step 3: Prepare the data

Before testing, ensure data quality and sampling validity:

- **Data collection** — was the sample collected appropriately?
- **Sampling procedure** — random, representative, independent observations?
- **Sample size** — large enough for the test to have adequate power?
- **Data cleaning** — handle missing values, outliers, and errors

Poor data preparation undermines even a correctly chosen test. **Garbage in, garbage out** applies here.

**Checklist:**
- [ ] Sample is random and representative of the population
- [ ] Observations are independent
- [ ] Data is clean and complete
- [ ] Sample size is documented

---

### Step 4: Select the test and test statistic

Choose the test based on **what you're measuring** and **what you know about the data**:

| Scenario | Typical test |
|----------|-------------|
| One mean, σ known, n large | z-test |
| One mean, σ unknown | t-test |
| One proportion | z-test for proportions |
| Two independent means | Two-sample t-test |
| Paired / matched data | Paired t-test |
| Two proportions | Two-proportion z-test |

The **test statistic** is the formula applied to sample data (e.g., z = (x̄ − μ₀) / (σ/√n)). The choice of test determines which distribution to compare against.

---

### Step 5: Check test assumptions

Every test has **conditions that must hold** for results to be valid:

| Test | Key assumptions |
|------|----------------|
| z-test (mean) | Normal population or n ≥ 30; σ known; random sample |
| t-test (mean) | Approximately normal or n ≥ 30; independent observations |
| z-test (proportion) | np ≥ 5 and n(1−p) ≥ 5; random sample |
| Two-sample t-test | Independent groups; approximately normal in each group |

If assumptions are violated:
- Use a **different test** (e.g., non-parametric alternative)
- Apply a **transformation** to the data
- Increase sample size

**Never skip this step** — an invalid test produces unreliable p-values.

---

### Step 6: Perform the test and draw conclusions

Execute the test and interpret results:

1. **Compute the test statistic** from sample data
2. **Calculate the p-value** — probability of observing data this extreme if H₀ is true
3. **Compare p-value to α:**
   - p-value < α → **reject H₀** (statistically significant)
   - p-value ≥ α → **fail to reject H₀** (insufficient evidence)
4. **State the conclusion in context** — plain language, tied to the original question

**Example conclusion:**
> "At α = 0.05, we reject H₀. There is sufficient evidence that the mean bulb lifespan exceeds 1,000 hours (p = 0.003)."

Always report the **p-value** and whether the result is statistically significant.

---

## Takeaways

1. **Follow the template every time** — question → hypotheses → data → test → assumptions → conclusion.
2. **Step 1 (define the question) is often skipped** — don't rush to calculations.
3. **Data preparation and assumption checks** are as important as the test itself.
4. **Test selection depends on parameter type, sample structure, and what is known** (σ, n, paired vs. independent).
5. **Conclusions must be stated in context** — not just "reject H₀" but what that means for the business or research question.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Hypothesis testing intro | [`hypothesis-testing-introduction-lecture-summary.md`](hypothesis-testing-introduction-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| Decisions, errors, and power | [`hypothesis-testing-decisions-errors-lecture-summary.md`](hypothesis-testing-decisions-errors-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Hypothesis testing checklist:

  1. Question     What parameter? One- or two-sample? What decision?
  2. Hypotheses   H₀ (equality) vs H₁ (inequality); set α
  3. Data         Random sample, clean, adequate n
  4. Test         Match test to parameter type and data structure
  5. Assumptions  Verify before computing; switch test if violated
  6. Conclusion   Report test statistic, p-value, reject/fail to reject,
                  and plain-language interpretation
```

**Remember:** The template is your quality control — each step exists to prevent a specific class of error.
