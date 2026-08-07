# Lecture Summary: Hypothesis Testing — Decisions, Test Statistics, and Errors

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Hypothesis testing mechanics — evidence, test statistics, Type I/II errors, power  
**Format:** Recorded lecture (~12+ min)

---

## Overview

This lecture deepens the **mechanics of hypothesis testing** — how evidence is evaluated, decisions are made, and errors are understood. It treats H₀ as the **default assumption** (no effect or difference) and explains how sample data and **probability calculations** determine whether H₀ can be rejected.

The lecture covers **test statistics**, **decision rules**, **Type 1 and Type 2 errors**, and **statistical power**, using a **legal verdict analogy** and **medical testing** examples to make the concepts concrete.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:06** | Core ideas of hypothesis testing |
| **00:28** | Null hypothesis and evidence |
| **01:31** | Decision making in hypothesis testing |
| **04:06** | Test statistic and decision rule |
| **06:38** | Probabilistic outcomes and errors |
| **11:53** | Conceptual examples of hypothesis testing |

---

## Key Themes

### 1. Core ideas of hypothesis testing

Hypothesis testing is a **data-driven decision framework**:

1. Start with a **claim** (H₀)
2. Collect **sample data**
3. Evaluate whether the data provides **enough evidence** to reject H₀
4. Make a **decision** — reject H₀ or fail to reject H₀

The process relies on **probability** to quantify how surprising the sample result would be if H₀ were true.

### 2. Null hypothesis and evidence

**H₀ (null hypothesis):** The **default assumption** — typically "no effect," "no difference," or "status quo holds."

**Evidence:** Sample data is weighed against H₀. Strong evidence against H₀ → reject it. Weak or inconclusive evidence → fail to reject H₀.

**Key principle:** You never "prove" H₀ true — you only determine whether the data gives sufficient reason to reject it.

### 3. Decision making — legal verdict analogy

Hypothesis testing parallels a **court trial**:

| Legal system | Hypothesis testing |
|--------------|-------------------|
| Defendant is **innocent until proven guilty** | H₀ is **assumed true** until evidence says otherwise |
| Prosecution must present **strong evidence** | Sample data must be **statistically significant** |
| Verdict based on **strength of evidence**, not certainty | Decision based on **p-value / test statistic**, not proof |
| **Acquittal** ≠ proof of innocence | **Fail to reject H₀** ≠ proof H₀ is true |

Decisions are **probabilistic**, not absolute — you act on the weight of evidence within an acceptable error rate.

### 4. Test statistic and decision rule

**Test statistic:** A number calculated from **sample data** (e.g., z-score, t-statistic) that measures how far the sample result deviates from what H₀ predicts.

**Process:**
1. Compute the test statistic from sample data
2. Compare it against a known **probability distribution** (normal, t, etc.) — assuming H₀ is true
3. Determine how **extreme** (unlikely) that value is

**Decision rule (p-value approach):**

```
p-value < α  →  reject H₀
p-value ≥ α  →  fail to reject H₀
```

**Decision rule (critical value approach):**

```
|test statistic| > critical value  →  reject H₀
otherwise                          →  fail to reject H₀
```

Both approaches reach the same conclusion; p-values are more common in practice.

### 5. Probabilistic outcomes and errors

Because decisions are based on sample data (not the full population), **errors are possible**:

| | H₀ is actually **true** | H₀ is actually **false** |
|---|--------------------------|---------------------------|
| **Reject H₀** | **Type I error (α)** — false positive | **Correct decision** — true positive |
| **Fail to reject H₀** | **Correct decision** — true negative | **Type II error (β)** — false negative |

**Type I error (α):** Reject H₀ when it is actually true.
- Probability = **significance level α** (commonly 0.05)
- "False alarm" — concluding an effect exists when it doesn't

**Type II error (β):** Fail to reject H₀ when it is actually false.
- Probability = **β** (depends on sample size, effect size, α)
- "Missed detection" — failing to find a real effect

**Statistical power:** Power = **1 − β** = probability of **correctly rejecting a false H₀**.
- Higher power = better ability to detect a real effect
- Increase power by: larger sample size, larger α, or larger true effect size

**Trade-off:** Lowering α (fewer Type I errors) generally increases β (more Type II errors), unless sample size increases.

### 6. Conceptual examples — medical testing

**Medical screening** illustrates Type I and Type II errors clearly:

| Outcome | Reality: patient is **healthy** | Reality: patient is **sick** |
|---------|--------------------------------|------------------------------|
| Test says **positive** | Type I error — false alarm | Correct — disease detected |
| Test says **negative** | Correct — healthy confirmed | Type II error — missed diagnosis |

**Implications:**
- **Screening tests** often accept higher Type I error (false positives) to minimize Type II error (missed disease)
- **Confirmatory tests** tighten criteria to reduce false positives
- Choosing α and designing sample size are **practical decisions** with real consequences

The goal is to **minimize errors** while making accurate, actionable decisions.

---

## Takeaways

1. **H₀ is the default** — assume no effect until sample evidence says otherwise.
2. **Test statistic** — quantifies how extreme sample data is under H₀.
3. **Decision rule** — compare p-value to α or test statistic to critical value.
4. **Type I error (α)** — false positive; controlled by significance level.
5. **Type II error (β)** — false negative; reduced by increasing power.
6. **Power = 1 − β** — ability to detect a real effect when one exists.
7. **Legal and medical analogies** — help intuition; real decisions always carry error risk.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Hypothesis testing intro | [`hypothesis-testing-introduction-lecture-summary.md`](hypothesis-testing-introduction-lecture-summary.md) |
| Formulating H₀ and H₁ | [`hypothesis-testing-formulation-lecture-summary.md`](hypothesis-testing-formulation-lecture-summary.md) |
| Normal distribution & z-scores | [`standardization-z-scores-lecture-summary.md`](standardization-z-scores-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Decision outcomes:
  Reject H₀        →  evidence supports H₁
  Fail to reject   →  insufficient evidence against H₀

Errors:
  Type I  (α)  =  reject true H₀     (false positive)
  Type II (β)  =  fail to reject false H₀  (false negative)
  Power (1−β)  =  correctly reject false H₀

Common α: 0.05  →  accept 5% chance of Type I error
```

**Remember:** Hypothesis testing manages uncertainty — it does not eliminate it. Design tests with appropriate α, sample size, and power for the stakes involved.
