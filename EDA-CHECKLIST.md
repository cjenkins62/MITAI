# EDA Checklist

Reusable exploratory data analysis plan, generalized from the [Week 1 Uber NYC EDA notebook](Week%201/uber_nyc_eda.ipynb) and mentor session themes.

Use this at the start of every new dataset or portfolio project.

---

## The EDA process (overview)

| Step | Focus | Question to answer |
|------|-------|--------------------|
| **1. Problem framing** | Define the question and scope | What decision or insight are we after? |
| **2. Hypothesis generation** | Brainstorm what might be true | What patterns do we expect before looking at data? |
| **3. Data profiling** | Shape, types, nulls, distributions | What does the raw data actually look like? |
| **4. Analytical dataset construction** | Build the analysis-ready dataset | What cleaned, joined, and engineered table do we need? |
| **5. Domain calibration** | Sanity-check with domain knowledge | Do these numbers and patterns make real-world sense? |
| **6. Descriptive analysis** | Summarize, visualize, group | What does the data show — charts, tables, segments? |
| **7. Inferential statistics** | Test hypotheses with rigor | Are observed differences statistically meaningful? |
| **8. Causal reasoning** | Ask *why*, not just *what* | What might explain the pattern? What can't we claim? |
| **9. Synthesis** | Weave findings into a narrative | So what? What should we do next? |

> **Note:** Steps 7–8 are optional for pure exploratory portfolio work. Use them when the business question requires formal hypothesis testing or causal claims.

---

## Chat vs. code

Use AI (Chat) and code where each is strongest. You verify everything code produces.

| Step | Use Chat for | Use code for |
|------|--------------|--------------|
| **Problem framing** | Framing ambiguous problems | — |
| **Hypothesis generation** | Generating hypotheses creatively | — |
| **Data profiling** | Interpreting odd patterns you find | Shape, types, nulls, distributions |
| **Analytical dataset construction** | Reviewing join/feature logic | Building the dataset (SQL / Python) |
| **Domain calibration** | Calibrating domain expectations | Validating ranges and counts against raw data |
| **Descriptive analysis** | Choosing chart types for the question | Running statistics, groupbys, and plots |
| **Inferential statistics** | Interpreting statistical results | Executing statistical tests |
| **Causal reasoning** | Causal and counterfactual reasoning | Validating causal claims with data |
| **Synthesis** | Synthesizing findings into narrative | Supporting claims with reproducible outputs |

**Code-heavy work:** iterative database-connected analysis, reusable `load_and_clean()` functions, and anything that must be exact (aggregations, column names, joins).

---

## How the overview maps to notebook phases

The [detailed phases](#detailed-phases-notebook-workflow) below are the executable checklist for steps 3–6 and 9:

| Process step | Notebook phase(s) |
|--------------|-------------------|
| Problem framing | Phase 0 |
| Hypothesis generation | _Write 2–3 hypotheses in notebook header before profiling_ |
| Data profiling | Phases 1–2 |
| Analytical dataset construction | Phases 2–3 |
| Domain calibration | Phase 2 imputation guide; sanity checks throughout |
| Descriptive analysis | Phases 4–7 |
| Inferential statistics | _Add when testing formal hypotheses_ |
| Causal reasoning | _Add when explaining why, not just what_ |
| Synthesis | Phase 8 |

---

## Detailed phases (notebook workflow)

### Phase 0 — Frame the project (before code)

Write this at the top of every notebook or README.

| Question | Example (Uber NYC) | Your project |
|----------|-------------------|--------------|
| **Business question** | When and where is demand highest? | _What are you trying to decide or predict?_ |
| **Target variable** (if modeling) | Pickup count per hour | _What is `y`?_ |
| **Key entities** | Trip, base, timestamp | _Row = customer? transaction? sensor reading?_ |
| **Risk of bad cleaning** | Fake GPS coords break maps | _What would a wrong imputation cost?_ |
| **EDA goals** (3–5 bullets) | Descriptive stats, missing values, temporal patterns | _What you need to learn before modeling_ |
| **Hypotheses** (2–3 bullets) | Evening rush peaks; weekday > weekend | _What you expect before plotting_ |

---

### Phase 1 — Setup and load

**Always do:**

1. Standard imports and plot defaults
2. Load raw data **without** cleaning
3. Rename columns to clear, consistent names
4. Print row count, `head()`, `info()`, `describe(include="all")`

**Why:** Understand raw shape and dtypes before aggregating anything.

**Checklist:**

- [ ] How many rows and columns?
- [ ] Any duplicate or unnamed columns?
- [ ] Are dtypes correct (e.g. dates stored as `object` vs `datetime`)?
- [ ] Any obvious junk values in `head()`?

---

### Phase 2 — Missing values (context-first)

**Always do:**

1. Count missing per column (`isna().sum()` + percentage)
2. For each column with gaps, decide: **drop**, **impute**, or **flag**

#### Imputation decision guide

Ask for every column: *What does this data actually look like, and what imputation strategy fits the business context?*

| Column type | Usually | Rarely |
|-------------|---------|--------|
| **IDs / keys** | Drop or investigate | Mean impute |
| **Coordinates / locations** | Drop invalid rows | Impute a "center" point |
| **Timestamps** | Parse with `errors="coerce"`, then drop or fix | Fill with an arbitrary date |
| **Target variable** | Drop or separate analysis | Blind imputation |
| **Optional survey fields** | Treat "missing" as its own category | Mean / median |
| **Sensor / time-series gaps** | Interpolate, forward-fill, or segment | Global mean |

**Always log:** rows before and after cleaning, what you dropped, and why.

---

### Phase 3 — Domain feature extraction

Derive features that match the problem **before** plotting or modeling.

| Domain | Features to consider |
|--------|---------------------|
| **Time series** | hour, day of week, date, month, weekend flag |
| **Finance** | rolling averages, lag features, fiscal period |
| **Geospatial** | borough, distance, cluster |
| **Categorical** | top-N grouping, rare-level bucketing |
| **Text** | length, keyword flags (later: embeddings) |

---

### Phase 4 — Univariate exploration

#### Numeric columns

- [ ] Histograms / KDE
- [ ] Review `describe()` — do not trust summary stats alone
- [ ] Note outliers and impossible values

#### Categorical columns

- [ ] `value_counts()` for top categories
- [ ] Check cardinality (how many unique values?)

#### Time

- [ ] Daily or weekly line plot of volume or target

---

### Phase 5 — Bivariate / segmented views

Pick 2–3 comparisons that directly answer the business question.

| Plot type | Use when |
|-----------|----------|
| **Box plot** (`x` = category, `y` = numeric) | Compare groups across categories |
| **Heatmap** (two dimensions + count/mean) | Surface rhythm or interaction patterns |
| **Line plot** (time × metric) | Show trends over time |
| **Bar chart** | Compare totals across segments |
| **Scatter** | Explore two numeric features (watch scale) |

**Rule:** Limit to top-N categories when cardinality is high.

---

### Phase 6 — Correlation / redundancy check

For numeric features:

- [ ] Correlation heatmap
- [ ] Flag pairs with \|r\| > ~0.7–0.8 (multicollinearity risk)

A "nothing redundant here" result is still useful — it tells you which features are safe to keep.

---

### Phase 7 — Compare across slices (if applicable)

When you have multiple files, regions, or time periods:

1. Write a reusable `load_and_clean()` function
2. Concatenate or compare side by side
3. Build a summary table: total volume, average per day, key metric by slice
4. Overlay plots (e.g. hourly pattern by month)

This catches **growth, seasonality, and data drift** that single-file EDA misses.

---

### Phase 8 — Document takeaways (synthesis)

End every EDA with five bullets:

1. **Data quality** — missingness, drops, anomalies
2. **Main patterns** — what stands out visually
3. **Cleaning decisions** — what you did and why
4. **Feature ideas** — what to engineer for modeling
5. **Open questions** — what needs domain expert input

When steps 7–8 of [the EDA process](#the-eda-process-overview) apply, also include:

6. **Hypothesis results** — what was supported or rejected
7. **Causal claims** — what you can and cannot conclude

---

## Notebook skeleton

Copy this structure into a new notebook:

```markdown
# [Project Name] — EDA

**Dataset:** [source + link]
**Business question:** [one sentence]
**Hypotheses:** [2–3 bullets]
**EDA goals:** [3–5 bullets]

## 1. Load and inspect
## 2. Missing values (context-aware cleaning)
## 3. Feature extraction (domain logic)
## 4. Distributions (numeric + categorical)
## 5. Segmented comparisons (box plots, groupby)
## 6. Correlation heatmap
## 7. Time / trend analysis
## 8. Cross-slice comparison (optional)
## 9. Inferential tests (optional)
## 10. Causal reasoning (optional)
## 11. Key takeaways + next steps
```

---

## What stays the same vs. what changes

| Stays the same | Changes per project |
|----------------|---------------------|
| Process: frame → hypothesize → profile → build → explore → synthesize | Business question and hypotheses |
| Context-before-imputation mindset | Column names, imputation rules |
| Chat for thinking; code for execution | Which plots answer *your* question |
| Reusable load/clean function | Domain features (time vs geo vs text) |
| Takeaways / synthesis section | Comparison slices (months, regions, products) |

---

## Reference

- **Source notebook:** [`Week 1/uber_nyc_eda.ipynb`](Week%201/uber_nyc_eda.ipynb)
- **Session notes:** [`Week 1/session-1-summary.md`](Week%201/session-1-summary.md)
