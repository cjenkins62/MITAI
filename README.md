# MIT Applied AI & Data Science — Portfolio

Projects and exercises from the MIT Applied AI & Data Science program (Great Learning), organized by week. Each folder includes session notes, notebooks, and external datasets with documented EDA workflows.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Projects

### Week 1 — Uber NYC Pickups EDA

Exploratory data analysis of NYC Uber TLC pickup records (April–September 2014), following the Week 1 mentor session on AI-assisted Python programming.

- **Notebook:** [`Week 1/uber_nyc_eda.ipynb`](Week%201/uber_nyc_eda.ipynb)
- **Session summary:** [`Week 1/session-1-summary.md`](Week%201/session-1-summary.md)
- **Dataset:** [FiveThirtyEight Uber TLC FOIL response](https://github.com/fivethirtyeight/uber-tlc-foil-response)

**Highlights:**
- Context-aware missing-value handling (drop invalid coordinates/timestamps rather than blind imputation)
- Temporal feature extraction (hour, day of week)
- Hour × day-of-week demand heatmap
- Month-over-month growth analysis (Apr → Sep 2014: ~1.8× total pickups)

```bash
cd "Week 1"
jupyter notebook uber_nyc_eda.ipynb
```

## Stack

- Python 3.9+
- Pandas, NumPy, Matplotlib, Seaborn, Jupyter
