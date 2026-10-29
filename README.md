# SollmaFin A/B Test: Onboarding Experiment Analysis

Analysis of an A/B test for **SollmaFin**, a mobile and web app for online trading of financial assets (stocks, currencies, crypto, ETFs and more). The project is part of the Yandex Practicum data analyst track. The task is to evaluate whether a new educational onboarding improves user investment activity without hurting conversion to the first deposit.

## Business context

SollmaFin targets beginner investors in four Latin American markets: Mexico, Brazil, Colombia and Argentina. The app gets roughly 700 new installs per day, but many users do not buy assets after their first deposit, and many who do never make a second deposit. Key product metrics have stopped growing.

The product team suspects low financial literacy: users buy high-risk assets without understanding the risks, lose money and churn. To address this, they redesigned onboarding to explain the differences between asset types and their risks. The concern was that a heavier onboarding could scare users away from depositing and from riskier investments, so an A/B test was run.

## Experiment design

- **Participants:** new users who registered between 2 and 15 June 2025.
- **Groups:** users were randomly split into two equal groups.
  - **Control:** standard onboarding with no mandatory education.
  - **Test:** updated onboarding with detailed information about assets and risks.
- **Observation window:** one week of activity after assignment.

### Hypotheses

1. **Growth:** educational onboarding helps users understand investing, so more of them will make a second deposit.
2. **Risk:** information about possible losses will discourage some beginners, lowering conversion to the first deposit.
3. **Additional:** users who choose high-risk assets after the new onboarding will return and make a second deposit more often than before.

### Metrics

| Role | Metric |
|---|---|
| Key | Average total deposit amount per user (including users who only installed or opened the app) |
| Guardrail | Conversion from registration to first deposit |
| Supporting 1 | Conversion from first deposit to second deposit |
| Supporting 2 | Average total deposit amount per user with at least one deposit |

The key and guardrail metrics were expected not to decline, and the supporting metrics were expected to grow.

## What this project does

1. **Historical data analysis** (users acquired 1 April – 1 June 2025)
   - New user acquisition dynamics and segmentation (country, platform)
   - Key steps of the user funnel
   - Deposit metrics, including average deposit amounts
2. **A/B test analysis**
   - Comparing control and test groups and checking the statistical significance of differences
   - Studying the effect of the new onboarding on paying users with a **bootstrap**, focusing on the lower and upper percentiles of the deposit distribution
3. **Conclusions and recommendations** on rolling out the feature and improving user experience and monetization

## Data

Two CSV files are used, expected in a `/datasets/` folder (they are not included in this repository):

- `pa_sollmafin_hist.csv`: historical actions of new users acquired from 1 April to 1 June 2025, up to their second deposit.
- `pa_sollmafin_abt.csv`: all actions of users who registered from 2 to 15 June 2025, already assigned to A/B groups.

| Field | Description |
|---|---|
| `user_id` | Unique user identifier |
| `country_code` | ISO country code (BR, MX, AR, CO) |
| `platform` | `mobile` or `web` |
| `first_ts` / `first_dt` | Timestamp and date of the user's first appearance |
| `event_ts` | Event timestamp |
| `event_name` | Event name |
| `amount` | Deposit amount |
| `asset` | Type of asset purchased |
| `risk_level` | `low`, `medium` or `high` |
| `ab_test` | A/B experiment name (A/B dataset only) |
| `group` | Experiment group (A/B dataset only) |

## Repository structure

```
sollmafin-ab-test/
├── sollmafin_ab_test.ipynb   # full analysis
├── README.md
└── requirements.txt
```

## Running the notebook

```bash
pip install -r requirements.txt
jupyter notebook sollmafin_ab_test.ipynb
```

If you run it locally, update the `/datasets/...` paths in the loading cell to point to where you saved the CSV files.

## Stack

Python, pandas, NumPy, matplotlib, seaborn, SciPy / statsmodels (statistical tests and bootstrap).

## Results

_Add a short summary of your findings here: effect on the key and guardrail metrics, the supporting metrics, the bootstrap results for low and high deposit percentiles, and the final recommendation._
