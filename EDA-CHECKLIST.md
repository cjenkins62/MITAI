# EDA Checklist

Reusable exploratory data analysis plan, generalized from the [Week 1 Uber NYC EDA notebook](Week%201/uber_nyc_eda.ipynb) and mentor session themes.

Use this at the start of every new dataset or portfolio project.

---

## Phase 0 — Frame the project (before code)

Write this at the top of every notebook or README.

| Question | Example (Uber NYC) | Your project |
|----------|-------------------|--------------|
| **Business question** | When and where is demand highest? | _What are you trying to decide or predict?_ |
| **Target variable** (if modeling) | Pickup count per hour | _What is `y`?_ |
| **Key entities** | Trip, base, timestamp | _Row = customer? transaction? sensor reading?_ |
| **Risk of bad cleaning** | Fake GPS coords break maps | _What would a wrong imputation cost?_ |
| **EDA goals** (3–5 bullets) | Descriptive stats, missing values, temporal patterns | _What you need to learn before modeling_ |

---

## Phase 1 — Setup and load

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

## Phase 2 — Missing values (context-first)

**Always do:**

1. Count missing per column (`isna().sum()` + percentage)
2. For each column with gaps, decide: **drop**, **impute**, or **flag**

### Imputation decision guide

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

## Phase 3 — Domain feature extraction

Derive features that match the problem **before** plotting or modeling.

| Domain | Features to consider |
|--------|---------------------|
| **Time series** | hour, day of week, date, month, weekend flag |
| **Finance** | rolling averages, lag features, fiscal period |
| **Geospatial** | borough, distance, cluster |
| **Categorical** | top-N grouping, rare-level bucketing |
| **Text** | length, keyword flags (later: embeddings) |

---

## Phase 4 — Univariate exploration

### Numeric columns

- [ ] Histograms / KDE
- [ ] Review `describe()` — do not trust summary stats alone
- [ ] Note outliers and impossible values

### Categorical columns

- [ ] `value_counts()` for top categories
- [ ] Check cardinality (how many unique values?)

### Time

- [ ] Daily or weekly line plot of volume or target

---

## Phase 5 — Bivariate / segmented views

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

## Phase 6 — Correlation / redundancy check

For numeric features:

- [ ] Correlation heatmap
- [ ] Flag pairs with \|r\| > ~0.7–0.8 (multicollinearity risk)

A "nothing redundant here" result is still useful — it tells you which features are safe to keep.

---

## Phase 7 — Compare across slices (if applicable)

When you have multiple files, regions, or time periods:

1. Write a reusable `load_and_clean()` function
2. Concatenate or compare side by side
3. Build a summary table: total volume, average per day, key metric by slice
4. Overlay plots (e.g. hourly pattern by month)

This catches **growth, seasonality, and data drift** that single-file EDA misses.

---

## Phase 8 — Document takeaways

End every EDA with five bullets:

1. **Data quality** — missingness, drops, anomalies
2. **Main patterns** — what stands out visually
3. **Cleaning decisions** — what you did and why
4. **Feature ideas** — what to engineer for modeling
5. **Open questions** — what needs domain expert input

---

## Notebook skeleton

Copy this structure into a new notebook:

```markdown
# [Project Name] — EDA

**Dataset:** [source + link]
**Business question:** [one sentence]
**EDA goals:** [3–5 bullets]

## 1. Load and inspect
## 2. Missing values (context-aware cleaning)
## 3. Feature extraction (domain logic)
## 4. Distributions (numeric + categorical)
## 5. Segmented comparisons (box plots, groupby)
## 6. Correlation heatmap
## 7. Time / trend analysis
## 8. Cross-slice comparison (optional)
## 9. Key takeaways + next steps
```

---

## What stays the same vs. what changes

| Stays the same | Changes per project |
|----------------|---------------------|
| Load → inspect → clean → explore → document | Column names, imputation rules |
| Context-before-imputation mindset | Which plots answer *your* question |
| Reusable load/clean function | Domain features (time vs geo vs text) |
| Takeaways section | Comparison slices (months, regions, products) |

---

## Reference

- **Source notebook:** [`Week 1/uber_nyc_eda.ipynb`](Week%201/uber_nyc_eda.ipynb)
- **Session notes:** [`Week 1/session-1-summary.md`](Week%201/session-1-summary.md)
