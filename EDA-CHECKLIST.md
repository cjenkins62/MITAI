# EDA Checklist

Reusable exploratory data analysis plan, generalized from the [Week 1 Uber NYC EDA notebook](Week%201/uber_nyc_eda.ipynb) and mentor session themes.

Use this at the start of every new dataset or portfolio project.

---

## The EDA process (overview)

| Step | Focus | Question to answer |
|------|-------|--------------------|
| **1. Problem framing** | Define the question, scope, context, and KPIs | What decision are we after, and how will we measure success? |
| **2. Hypothesis generation** | Brainstorm what might be true | What patterns do we expect before looking at data? |
| **3. Data profiling** | Shape, types, nulls, distributions | What does the raw data actually look like? Does it match the data dictionary? |
| **4. Analytical dataset construction** | Clean, join, and engineer the analysis-ready dataset | What cleaned table do we need — and what rules got us there? |
| **5. Domain calibration** | Sanity-check with domain knowledge and KPI ranges | Do these numbers and patterns make real-world sense? |
| **6. Descriptive analysis** | Univariate first, then bivariate and segmented views | What does each column look like — then how do variables relate? |
| **7. Inferential statistics** | Test hypotheses with rigor | Are observed differences statistically meaningful? |
| **8. Causal reasoning** | Ask *why*, not just *what* | What might explain the pattern? What can't we claim? |
| **9. Synthesis** | Weave findings into a narrative tied to KPIs | So what? Did we learn anything that could move the metric? |

> **Note:** Steps 7–8 are optional for pure exploratory portfolio work. Use them when the business question requires formal hypothesis testing or causal claims.
>
> **Descriptive analysis order:** univariate (one column at a time on cleaned data) → bivariate/segmented (relationships and KPI breakdowns) → correlation and cross-slice comparisons.

---

## Chat vs. code

Use AI (Chat) and code where each is strongest. You verify everything code produces.

| Step | Use Chat for | Use code for |
|------|--------------|--------------|
| **Problem framing** | Framing ambiguous problems; naming actionable KPIs | — |
| **Hypothesis generation** | Generating hypotheses creatively | — |
| **Data dictionary** | Drafting field definitions from source docs | Validating columns, dtypes, and row counts against raw files |
| **Data profiling** | Interpreting odd patterns you find | Shape, types, nulls, distributions |
| **Data cleaning** | Choosing drop / impute / flag strategies per column | Types, duplicates, invalid values, joins; log rows in/out |
| **Analytical dataset construction** | Reviewing join and feature logic | Building the cleaned dataset (SQL / Python) |
| **Domain calibration** | Calibrating domain expectations; judging KPI plausibility | Validating ranges and counts against raw data |
| **Descriptive analysis (univariate)** | Choosing charts for single-column distributions | Histograms, `describe()`, `value_counts()`, KPI volume over time |
| **Descriptive analysis (bivariate+)** | Choosing comparisons for the business question | Box plots, heatmaps, groupbys, correlation, cross-slice plots |
| **Inferential statistics** | Interpreting statistical results | Executing statistical tests |
| **Causal reasoning** | Causal and counterfactual reasoning | Validating causal claims with data |
| **Synthesis** | Synthesizing findings into narrative; linking insights to KPIs | Supporting claims with reproducible outputs |

**Code-heavy work:** iterative database-connected analysis, reusable `load_and_clean()` functions, and anything that must be exact (aggregations, column names, joins).

---

## How the overview maps to notebook phases

The [detailed phases](#detailed-phases-notebook-workflow) below are the executable checklist for steps 3–6 and 9:

| Process step | Notebook phase(s) |
|--------------|-------------------|
| Problem framing | Phase 0 (business context, KPIs) |
| Hypothesis generation | _Write 2–3 hypotheses in notebook header before profiling_ |
| Data dictionary | Phase 0–1 (`data/data_dictionary.md`) |
| Data profiling | Phase 1 |
| Data cleaning | Phase 2 |
| Analytical dataset construction | Phases 2–3 (clean, then feature-engineer) |
| Domain calibration | Phase 2 cleaning log and calibration checks |
| Descriptive analysis (univariate) | Phase 4 — one column at a time on cleaned data |
| Descriptive analysis (bivariate+) | Phases 5–7 — segmented views, correlation, cross-slice KPIs |
| Inferential statistics | _Add when testing formal hypotheses_ |
| Causal reasoning | _Add when explaining why, not just what_ |
| Synthesis | Phase 8 (KPI impact and recommendations) |

---

## Detailed phases (notebook workflow)

### Phase 0 — Frame the project (before code)

Write this at the top of every notebook or README.

| Question | Example (Uber NYC) | Your project |
|----------|-------------------|--------------|
| **Business context** | Ride-hailing ops in NYC; TLC bases dispatch drivers; 2014 = rapid Uber growth | _Industry, situation, and constraints around the data_ |
| **Stakeholder / decision** | Ops planning — where and when to allocate supply | _Who acts on this analysis? What decision does it inform?_ |
| **Business question** | When and where is demand highest? | _What are you trying to decide or predict?_ |
| **Primary KPI(s)** | Pickups per hour; pickups per day | _The 1–2 metrics that define success_ |
| **Secondary KPI(s)** | Peak-hour demand; demand by base; weekday vs weekend ratio | _Supporting metrics that add context_ |
| **Target variable** (if modeling) | Pickup count per hour | _What is `y`?_ |
| **Key entities** | Trip, base, timestamp | _Row = customer? transaction? sensor reading?_ |
| **Risk of bad cleaning** | Fake GPS coords break supply placement | _What would a wrong imputation or assumption cost?_ |
| **EDA goals** (3–5 bullets) | Descriptive stats, missing values, temporal patterns | _What you need to learn before modeling_ |
| **Hypotheses** (2–3 bullets) | Evening rush peaks; weekday > weekend | _What you expect before plotting_ |

> For portfolio or course EDA, define at least one **primary KPI** even if the stakeholder is hypothetical.

---

### Phase 0b — Data dictionary (before profiling)

Document the schema **after framing, before cleaning**. Store one file per project:

```
[data/]data_dictionary.md
```

If the source already publishes a dictionary, link it — then add your **renamed columns**, **derived features**, and **KPI linkage**.

| Section | What to include |
|---------|-----------------|
| **Source & grain** | URL, date range, one row = what |
| **Raw columns** | Raw name, analysis name, type, description, valid range |
| **Derived features** | Engineered columns added in Phase 3 |
| **Cleaning rules** | Per-column actions: drop, impute, flag, parse, filter — with row counts |
| **KPI linkage** | Which columns feed primary and secondary KPIs |
| **Join keys** | For multi-table datasets — keys, cardinality, known orphans |
| **Data quality notes** | Known missingness, outliers, parsing quirks |

**When required:** multi-file datasets, unfamiliar external sources, portfolio repos.  
**When optional:** trivial single-file data with obvious columns — link the source docs instead.

**Example:** [`Week 1/data/data_dictionary.md`](Week%201/data/data_dictionary.md)

---

### Phase 1 — Setup and load

**Always do:**

1. Create or link a [data dictionary](#phase-0b--data-dictionary-before-profiling)
2. Standard imports and plot defaults
3. Load raw data **without** cleaning
4. Rename columns to clear, consistent names (match the dictionary)
5. Print row count, `head()`, `info()`, `describe(include="all")`

**Why:** Understand raw shape and dtypes before aggregating anything.

**Checklist:**

- [ ] Data dictionary exists or source dictionary is linked
- [ ] Column names match the dictionary (raw → analysis names)
- [ ] How many rows and columns?
- [ ] Any duplicate or unnamed columns?
- [ ] Are dtypes correct (e.g. dates stored as `object` vs `datetime`)?
- [ ] Any obvious junk values in `head()`?
- [ ] Do row counts and dtypes match dictionary expectations?

---

### Phase 2 — Data cleaning (context-first)

Work from a copy — keep raw `df`, build cleaned `eda`. Profile first (Phase 1), then clean. **Document every rule in the data dictionary cleaning rules section.**

Ask for every column: *What does this data actually look like, and what strategy fits the business context?*

#### Quick checklist

- [ ] **Missing values:** drop / impute / flag (per column, with reason)
- [ ] **Types and parsing:** dates, numerics stored as strings, categoricals
- [ ] **Duplicates and grain:** exact dupes and key-based dupes; confirm one row = one entity
- [ ] **Invalid values:** domain rules applied (ranges, codes, sign checks)
- [ ] **Outliers:** policy documented — drop, cap, flag, or keep with justification
- [ ] **Joins** (if multi-table): orphan rows and duplicate keys handled
- [ ] **Cleaning log:** rows before → after each major rule
- [ ] **Dictionary updated** with cleaning rules and row counts

#### 2a — Missing values

1. Count missing per column (`isna().sum()` + percentage)
2. For each column with gaps, decide: **drop**, **impute**, or **flag**

| Column type | Usually | Rarely |
|-------------|---------|--------|
| **IDs / keys** | Drop or investigate | Mean impute |
| **Coordinates / locations** | Drop invalid rows | Impute a "center" point |
| **Timestamps** | Parse with `errors="coerce"`, then drop or fix | Fill with an arbitrary date |
| **Target variable** | Drop or separate analysis | Blind imputation |
| **Optional survey fields** | Treat "missing" as its own category | Mean / median |
| **Sensor / time-series gaps** | Interpolate, forward-fill, or segment | Global mean |

#### 2b — Types and parsing

- [ ] Parse datetimes; coerce invalid to `NaT` and handle explicitly
- [ ] Convert numeric strings; flag coercion failures
- [ ] Normalize categoricals (trim whitespace, consistent casing)
- [ ] Fix encoding issues in text columns

#### 2c — Duplicates and grain

- [ ] Check exact duplicate rows (`duplicated()`)
- [ ] Check duplicate business keys (if grain = one row per entity)
- [ ] Confirm row-level grain matches the data dictionary

#### 2d — Invalid values and outliers

- [ ] Apply domain range filters (e.g. lat/lon bounds, non-negative amounts)
- [ ] Decide outlier policy before deleting — document keep/drop/cap/flag
- [ ] Never apply a global rule without checking business impact on KPIs

#### 2e — Joins (multi-table only)

- [ ] Validate join keys: cardinality, null keys, orphan rows
- [ ] Log rows gained/lost after each join
- [ ] Resolve duplicate column names from merges

#### Cleaning log (always)

Record after each major rule:

```
Rule: drop rows with null lat/lon
Rows before: 564,516 → after: 564,516 (0 dropped)
```

#### Domain calibration checks

After cleaning, sanity-check results against business context and KPI expectations:

- [ ] Are KPI values in a plausible range for this domain? (e.g. ~19K daily pickups in NYC, not 19)
- [ ] Do temporal patterns match known behavior? (e.g. evening rush, weekday vs weekend)
- [ ] Do geographic values make sense? (e.g. lat/lon within expected city bounds)
- [ ] Would a stakeholder recognize these numbers as credible?

---

### Phase 3 — Domain feature extraction

Derive features that match the problem **before** plotting or modeling. **Add each derived column to `data/data_dictionary.md`.**

| Domain | Features to consider |
|--------|---------------------|
| **Time series** | hour, day of week, date, month, weekend flag |
| **Finance** | rolling averages, lag features, fiscal period |
| **Geospatial** | borough, distance, cluster |
| **Categorical** | top-N grouping, rare-level bucketing |
| **Text** | length, keyword flags (later: embeddings) |

---

### Phase 4 — Univariate exploration

Explore **one variable at a time** on the cleaned `eda` dataset. This is deeper than [Phase 1 profiling](#phase-1--setup-and-load) (which runs on raw data to validate the dictionary).

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

Pick 2–3 comparisons that directly answer the business question and illuminate **primary KPIs**.

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
3. Build a summary table: primary KPI totals, averages per day, and key metric by slice
4. Overlay plots (e.g. hourly KPI pattern by month)

This catches **growth, seasonality, and data drift** — and shows whether KPIs are improving or shifting across slices.

---

### Phase 8 — Document takeaways (synthesis)

End every EDA with five bullets:

1. **Data quality** — missingness, drops, anomalies
2. **Main patterns** — what stands out visually
3. **KPI findings** — how primary and secondary KPIs behave; what moved or differs by segment
4. **Cleaning decisions** — what you did and why
5. **Feature ideas** — what to engineer for modeling
6. **Recommendations** — what a stakeholder could do next based on KPI insights
7. **Open questions** — what needs domain expert input

When steps 7–8 of [the EDA process](#the-eda-process-overview) apply, also include:

8. **Hypothesis results** — what was supported or rejected
9. **Causal claims** — what you can and cannot conclude

---

## Notebook skeleton

Copy this structure into a new notebook:

```markdown
# [Project Name] — EDA

**Dataset:** [source + link]
**Data dictionary:** [data/data_dictionary.md]
**Business context:** [industry, situation, constraints]
**Stakeholder / decision:** [who acts on this]
**Business question:** [one sentence]
**Primary KPI(s):** [1–2 metrics]
**Secondary KPI(s):** [supporting metrics]
**Hypotheses:** [2–3 bullets]
**EDA goals:** [3–5 bullets]

## 1. Load and inspect
## 2. Data cleaning (context-first)
## 3. Feature extraction (domain logic)
## 4. Univariate exploration (one column at a time)
## 5. Bivariate / segmented comparisons (box plots, groupby)
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
| Process: frame → document → hypothesize → profile → clean → build → univariate → bivariate → synthesize | Business context, KPIs, hypotheses, and data dictionary |
| Univariate before bivariate | Which columns and segments matter for KPIs |
| Data dictionary before profiling | Column definitions, cleaning rules, join keys, KPI linkage |
| Context-first cleaning (not blind imputation) | Per-column drop / impute / flag decisions |
| Chat for thinking; code for execution | Which plots and KPIs answer *your* question |
| Reusable load/clean function | Domain features (time vs geo vs text) |
| Takeaways / synthesis section | Comparison slices (months, regions, products) |

---

## Reference

- **Source notebook:** [`Week 1/uber_nyc_eda.ipynb`](Week%201/uber_nyc_eda.ipynb)
- **Session notes:** [`Week 1/session-1-summary.md`](Week%201/session-1-summary.md)
- **Example data dictionary:** [`Week 1/data/data_dictionary.md`](Week%201/data/data_dictionary.md)
