# Meniscus Injuries in Professional Football

## Research question
What happens to professional football players after a serious meniscal injury in Europe’s top five leagues?

## Who could benefit from this analysis?

The analysis provides football agents with a base-rate view of how players typically recover their playing time and competitive level after a prolonged meniscal injury, supporting better-informed transfer, contract and career-planning decisions.

## Notebooks

| Notebook | What it does |
|---|---|
| [`notebooks/01_data_audit.ipynb`](notebooks/01_data_audit.ipynb) | Data audit: checks what the Transfermarkt data can and cannot measure (tables, keys, coverage of matches before and after a meniscal injury). Findings are written at the end of each step. |
| [`notebooks/02_cohort.ipynb`](notebooks/02_cohort.ipynb) | Builds the cohort step by step, from 1,863 meniscal injuries to 158 players (one row per player). After every step the numbers are checked against the audit. Saves `data/processed/cohort.csv` (27 columns). |
| `03_data_analysis.ipynb` (in progress) | The analysis. Reads only `data/processed/cohort.csv`, never the raw tables. |


## Data

The six CSV files (`player_injuries`, `player_performances`, `players`, `appearances`, `games`, `transfers`) are not stored in the repository. Put them in `data/`. They come from two Kaggle datasets with Transfermarkt data, both under the CC0 licence:

- [`xfkzujqjvx97n/football-datasets`](https://www.kaggle.com/datasets/xfkzujqjvx97n/football-datasets)
- [`davidcariboo/player-scores`](https://www.kaggle.com/datasets/davidcariboo/player-scores) (code: [transfermarkt-datasets](https://github.com/dcaribou/transfermarkt-datasets))

## The cohort

A serious injury is an absence of 29 days or more (Fuller et al. 2006). The cohort has one index injury per player, the earliest one.

| Step | Rule | Injuries | Players |
|---|---|---|---|
| 0 | All meniscal injuries (five labels) | 1,863 | 1,657 |
| 1 | Start and end date present | 1,838 | 1,632 |
| 2 | Both windows inside `appearances` (12 months before, 24 months after) | 1,277 | 1,164 |
| 3 | No cruciate ligament injury within 30 days | 1,248 | 1,138 |
| 4 | At least 1 minute in a top-5 league in the 12 months before | 195 | 181 |
| 5 | Absence of 29 days or more | 169 | 158 |
| 6 | One index injury per player | 158 | 158 |


## Environment

Python 3.14, pandas 3.0.6

## Status

Data audit and cohort are finished (158 players). The analysis notebook is in progress.