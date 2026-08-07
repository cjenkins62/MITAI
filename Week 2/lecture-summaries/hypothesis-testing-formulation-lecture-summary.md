# Lecture Summary: Formulating Null and Alternative Hypotheses

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Hypothesis formulation — H₀/H₁ rules, lumber and travel examples, equality placement  
**Format:** Recorded lecture (~7+ min)

---

## Overview

This lecture focuses on **how to formulate null and alternative hypotheses** — the first formal step in any hypothesis test. H₀ and H₁ are **mutually exclusive** statements about a **population parameter** (mean μ, proportion p, etc.).

The lecture uses two business examples — **lumber length specifications** for a building project and the **proportion of men traveling with companions** — to show how claims translate into testable hypotheses. It also covers the technical rule that **equality belongs in H₀** and **inequality in H₁**, which ensures the correct probability distribution is used for the test.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:05** | Understanding hypothesis testing |
| **00:41** | Formulating null and alternative hypotheses |
| **01:56** | Business context of hypothesis testing |
| **02:30** | Example: lumber length specification |
| **04:53** | Example: business travel companion proportion |
| **07:01** | Formulating hypotheses with equality and inequality |

---

## Key Themes

### 1. Understanding hypothesis testing (recap)

Hypothesis testing provides a **structured, evidence-based approach** to decision-making. Instead of assuming a claim is true, you **test assumptions against data** to validate or refute them.

**Goal:** Conclusions based on **statistical evidence**, not gut feel.

### 2. Formulating H₀ and H₁

| Hypothesis | Meaning |
|------------|---------|
| **Null (H₀)** | Status quo, baseline, or "no change" — the claim you assume true until proven otherwise |
| **Alternative (H₁ or Hₐ)** | Deviation from the baseline — what you suspect or want to demonstrate |

**Rules:**
- H₀ and H₁ must be **mutually exclusive** — they cannot both be true
- Together they must **cover all possibilities** for the parameter
- H₀ always contains the **equality** (=, ≤, or ≥)
- H₁ contains the **inequality** (≠, >, or <)

### 3. Business context

Hypothesis testing is widely used in business to support **data-driven decisions**:

- Verify supplier or product specifications
- Test marketing or demographic claims
- Validate process changes before committing resources

The lumber and travel examples show how everyday business questions map directly to formal hypotheses.

### 4. Example: lumber length specification

**Scenario:** A building project requires lumber of a specified mean length (e.g., 8 feet). A supplier delivers a batch; you sample boards to check whether the **population mean length μ** meets the spec.

**Typical formulation (two-tailed — "different from spec"):**

```
H₀:  μ = 8        (lumber meets specification)
H₁:  μ ≠ 8        (lumber does not meet specification)
```

**One-tailed variants** depend on the business question:

| Question | H₀ | H₁ |
|----------|----|----|
| Is lumber **shorter** than spec? | μ ≥ 8 | μ < 8 |
| Is lumber **longer** than spec? | μ ≤ 8 | μ > 8 |

**Parameter type:** population **mean** (μ) — use a z-test or t-test depending on sample size and whether σ is known.

### 5. Example: business travel companion proportion

**Scenario:** A travel company claims that a certain **proportion of men** travel with companions. You survey a sample to test whether the **population proportion p** matches the claimed value.

**Typical formulation:**

```
H₀:  p = 0.40     (claim is true — 40% travel with companions)
H₁:  p ≠ 0.40     (actual proportion differs from claim)
```

**One-tailed variants:**

| Question | H₀ | H₁ |
|----------|----|----|
| Is proportion **higher** than claimed? | p ≤ 0.40 | p > 0.40 |
| Is proportion **lower** than claimed? | p ≥ 0.40 | p < 0.40 |

**Parameter type:** population **proportion** (p) — use a z-test for proportions.

These two examples illustrate the same formulation pattern applied to different parameter types (mean vs. proportion).

### 6. Equality in H₀, inequality in H₁

**Critical rule:** Always place **equality (=, ≤, ≥) in H₀** and **strict inequality (<, >, ≠) in H₁**.

**Why it matters:**
- The test statistic and its **probability distribution** are derived **assuming H₀ is true**
- Putting equality in H₀ pins down a single parameter value (or boundary), which correctly specifies the sampling distribution
- Reversing the placement can lead to **wrong critical values** and unreliable conclusions

**Common mistake to avoid:**

```
✗  H₀: μ > 8     H₁: μ ≤ 8    ← wrong (inequality in H₀)
✓  H₀: μ ≤ 8     H₁: μ > 8    ← correct
```

---

## Takeaways

1. **H₀ = baseline; H₁ = what you're trying to show** — mutually exclusive, exhaustive pair.
2. **Translate business questions into parameters** — mean μ for measurements, proportion p for yes/no outcomes.
3. **Choose one-tailed vs. two-tailed** based on whether you care about direction (≠) or a specific side (< or >).
4. **Equality always goes in H₀** — required for correct distribution specification.
5. **Lumber and travel examples** are templates for specification testing and claim verification in business.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Hypothesis testing intro (bulb example) | [`hypothesis-testing-introduction-lecture-summary.md`](hypothesis-testing-introduction-lecture-summary.md) |
| Estimation & confidence intervals | [`estimation-confidence-intervals-lecture-summary.md`](estimation-confidence-intervals-lecture-summary.md) |
| Normal distribution & z-scores | [`standardization-z-scores-lecture-summary.md`](standardization-z-scores-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
Formulation checklist:
  1. Identify the population parameter (μ, p, σ², etc.)
  2. State the business claim as H₀ (status quo / equality)
  3. State what you suspect as H₁ (inequality)
  4. Confirm H₀ and H₁ are mutually exclusive and exhaustive
  5. Choose one-tailed or two-tailed based on the question

Examples:
  Mean:       H₀: μ = 8      H₁: μ ≠ 8
  Proportion: H₀: p = 0.40    H₁: p ≠ 0.40
```

**Remember:** Correct formulation is step one — a well-formed H₀/H₁ pair is required before choosing a test statistic or interpreting a p-value.
