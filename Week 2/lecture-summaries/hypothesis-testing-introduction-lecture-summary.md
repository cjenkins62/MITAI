# Lecture Summary: Introduction to Hypothesis Testing

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Hypothesis testing — concepts, bulb manufacturing example, H₀/H₁, significance  
**Format:** Recorded lecture (~15+ min)

---

## Overview

This lecture introduces **hypothesis testing** — a core tool in business statistics for deciding whether sample data provides **enough evidence** to infer something about the **entire population**. It builds on **descriptive statistics**, **probability**, and **inferential statistics**.

The running example is a **bulb manufacturing company** assessing product reliability. The lecture covers **sampling variation**, **statistical significance**, formal steps (**null and alternative hypotheses**), and real-world applications in research, business claims, and decision-making.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:17** | Introduction to hypothesis testing |
| **01:26** | Quality analysis in manufacturing |
| **02:49** | Sample analysis and inferential statistics |
| **05:02** | Understanding sampling variation |
| **07:00** | Statistical significance and hypothesis testing |
| **10:28** | Formalizing hypothesis testing |
| **15:25** | Applications of hypothesis testing |

---

## Key Themes

### 1. What hypothesis testing is

**Core question:** Is there enough evidence in a **sample** to conclude a condition holds for the **population**?

Hypothesis testing combines:
- **Descriptive stats** — summarize the sample
- **Probability** — quantify uncertainty
- **Inferential stats** — generalize to the population

**Business value:** Make **informed, data-driven decisions** rather than relying on intuition or anecdote.

### 2. Bulb manufacturing example — quality analysis

**Scenario:** A bulb manufacturer wants to assess **product reliability** (e.g., lifespan, defect rate).

**Approach:**
- Cannot test every bulb → draw a **sample**
- Use sample data to **infer** whether the population meets quality standards
- Hypothesis testing formalizes: "Does our sample evidence support the claim that bulbs are reliable?"

Manufacturing quality control is a classic hypothesis testing use case.

### 3. Sample analysis and inferential statistics

**Workflow:**
1. Define the **population** parameter of interest (e.g., mean bulb life μ, proportion defective p)
2. Collect a **representative sample**
3. Compute **sample statistics** (x̄, p̂)
4. Ask: Is the observed sample result **consistent with** a stated claim, or **unlikely under** that claim?

Sample data is the evidence; population parameters are what you want to learn about.

### 4. Sampling variation

**Key insight:** Different samples from the same population give **different results** — even when the population hasn't changed.

Because of **sampling variation**, you cannot treat a single sample statistic as definitive proof. Hypothesis testing accounts for this variability when judging whether an observed difference is **real** or **random noise**.

This connects to **standard error** and the **sampling distribution** from earlier lectures.

### 5. Statistical significance

**Statistical significance** = the observed sample result is **unlikely to have occurred by chance alone** if the null hypothesis were true.

If sample evidence is extreme enough (relative to sampling variation), you conclude the result is **statistically significant** — worth acting on.

**Not the same as practical significance:** A statistically significant difference may or may not matter for business decisions (effect size matters too).

### 6. Formalizing hypothesis testing — H₀ and H₁

| Hypothesis | Role |
|------------|------|
| **Null hypothesis (H₀)** | Status quo / default claim — "no effect," "meets standard," "no difference" |
| **Alternative hypothesis (H₁ or Hₐ)** | What you suspect or want to prove — "there is an effect," "below standard," "different" |

**Process (high level):**
1. State **H₀** and **H₁**
2. Choose **significance level** α (often 0.05)
3. Collect data and compute a **test statistic**
4. Calculate **p-value** — probability of seeing results this extreme if H₀ is true
5. **Decision:** If p-value < α → reject H₀ (evidence supports H₁); otherwise fail to reject H₀

**Default:** Assume H₀ is true until sample evidence strongly suggests otherwise.

### 7. Applications

Hypothesis testing is used to:

| Application | Example |
|-------------|---------|
| **Research** | Validate whether a treatment has an effect |
| **Business claims** | Verify marketing or quality assertions |
| **Decision-making** | Assess whether a process change improved outcomes |
| **Manufacturing** | Confirm products meet specifications (bulb example) |

**Goal:** Replace gut feel with **evidence-based conclusions** while acknowledging uncertainty.

---

## Takeaways

1. **Hypothesis testing = evidence-based population inference** — sample data vs. a formal claim.
2. **Sampling variation is why testing exists** — one sample isn't enough without accounting for randomness.
3. **H₀ vs. H₁** — null = status quo; alternative = what you're trying to show.
4. **Statistical significance** — result is unlikely under H₀; not the same as "important."
5. **Manufacturing quality** — practical template: sample → test → accept/reject batch or process.
6. **Foundation for the course arc** — leads into specific tests (z, t, chi-square) in the hypothesis testing notebook.

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Inferential statistics overview | [`statistical-inference-lecture-summary.md`](statistical-inference-lecture-summary.md) |
| Estimation & confidence intervals | [`estimation-confidence-intervals-lecture-summary.md`](estimation-confidence-intervals-lecture-summary.md) |
| Sampling variation & CLT | [`central-limit-theorem-simulation-lecture-summary.md`](central-limit-theorem-simulation-lecture-summary.md) |
| Hands-on hypothesis tests | [`../Notebook_Hypothesis_Testing.ipynb`](../Notebook_Hypothesis_Testing.ipynb) |

---

## Quick reference

```
H₀:  Null hypothesis        — status quo (assume true until proven otherwise)
H₁:  Alternative hypothesis — what sample evidence may support

Decision logic:
  p-value < α  →  reject H₀  (statistically significant)
  p-value ≥ α  →  fail to reject H₀

Common α:  0.05 (5% significance level)
```

**Remember:** "Fail to reject H₀" ≠ "prove H₀ true" — you may simply lack enough evidence against it.
