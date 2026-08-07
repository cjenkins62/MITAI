# Lecture Summary: Binomial Distribution — PMF, CDF & Applications

**Course:** MIT Applied AI & Data Science Program (Great Learning)  
**Topic:** Applied Binomial distribution — probability calculations and visualization  
**Format:** Recorded lecture (~15+ min)

---

## Overview

This lecture is a **hands-on deep dive** into the **Binomial distribution** — how to calculate and visualize probabilities for binary outcomes across a fixed number of independent trials. It builds on foundational concepts from [`binomial-bernoulli-lecture-summary.md`](binomial-bernoulli-lecture-summary.md) with a practical **museum visitor purchase** example (80% buy probability).

The focus shifts from theory to **tools**: the **Probability Mass Function (PMF)** for exact outcomes, the **Cumulative Distribution Function (CDF)** for "at most" / "at least" questions, and **bar plots** to see how the distribution shape changes when **p** (success probability) changes.

---

## Video Topics (chronological)

| Time | Topic |
|------|-------|
| **00:06** | Introduction to distributions and inferential statistics |
| **00:19** | Understanding the Binomial distribution |
| **00:22** | Example: Binomial distribution with museum visitors |
| **01:52** | Probability calculations using Binomial distribution |
| **06:11** | Visualizing Binomial probabilities |
| **10:14** | Cumulative Distribution Function (CDF) in Binomial distribution |
| **13:04** | Exploring different probability scenarios |
| **15:18** | Conclusion on Binomial distribution |

---

## Key Themes

### 1. What the Binomial models

The Binomial distribution models the **number of successes** in **n independent Bernoulli trials**, each with the same success probability **p**.

**Core question:** If each trial has probability p of success, what is the probability of exactly k successes in n trials?

### 2. Museum visitor example

**Scenario:** Museum visitors — each visitor has an **80% probability of making a purchase** (p = 0.8).

**Binary outcome per visitor:** buy (success) or don't buy (failure).

**Binomial setup:** Given n visitors, calculate the probability of different numbers of purchases — e.g. exactly 3 out of 5 buy, or at least 4 out of 10 buy.

This grounds abstract formulas in a concrete business/revenue planning context.

### 3. PMF vs. CDF

| Function | Question it answers | Example |
|----------|---------------------|---------|
| **PMF** (Probability Mass Function) | P(**exactly** k successes) | "What is the probability exactly 3 visitors buy?" |
| **CDF** (Cumulative Distribution Function) | P(**at most** k successes) — sum of PMF values up to k | "What is the probability 3 or fewer visitors buy?" |

Use **PMF** for precise counts; use **CDF** for threshold questions ("at most," "no more than") — common in risk and capacity planning.

### 4. Visualization

**Bar plots** of Binomial probabilities help you see:

- Which outcomes are most likely
- How probability spreads across possible success counts (0 to n)
- How the distribution **shape shifts** when **p** changes

Visualization makes it easier to sanity-check calculations and communicate results to stakeholders.

### 5. Changing the success probability (p)

The lecture explores **different probability scenarios** — varying **p** changes the distribution:

- **Higher p** (e.g. 0.8) → distribution skews toward more successes
- **Lower p** → skews toward fewer successes
- **p = 0.5** → symmetric distribution

Same n, different p = different business assumptions → different decision implications.

### 6. Real-world applications

The Binomial is useful whenever outcomes are **binary**:

- **Purchases** — buy / don't buy
- **Defaults** — default / no default
- **Weather** — rain / no rain
- **Quality control** — defective / not defective

---

## Takeaways

1. **PMF for exact counts, CDF for cumulative thresholds** — pick the right tool for the business question.
2. **Define n and p clearly** — number of trials and per-trial success probability.
3. **Visualize with bar plots** — shape reveals likely outcomes faster than a single number.
4. **Sensitivity to p** — always ask how robust your conclusion is if the true success rate differs from your assumption.
5. **Foundation for inference** — Binomial thinking feeds into hypothesis tests and binary outcome modeling (logistic regression).

---

## Connection to course arc

| This lecture | Related materials |
|--------------|-------------------|
| Binomial theory & assumptions | [`binomial-bernoulli-lecture-summary.md`](binomial-bernoulli-lecture-summary.md) |
| PMF / discrete distributions | [`probability-lecture-summary.md`](probability-lecture-summary.md) |
| Inferential statistics context | [`statistical-inference-lecture-summary.md`](statistical-inference-lecture-summary.md) |
| Hands-on practice | [`Notebook_Inferential_Statistics.ipynb`](../Notebook_Inferential_Statistics.ipynb) |

---

## Quick reference

```
PMF:  P(X = k)     → exactly k successes
CDF:  P(X ≤ k)     → at most k successes
      P(X ≥ k)     → at least k successes (use 1 − P(X ≤ k−1))
```

Parameters: **n** = number of trials, **p** = probability of success per trial, **k** = number of successes of interest.
