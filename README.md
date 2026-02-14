# BlackRock Client Targeting — Predictive Analytics

## Overview

A predictive analytics project simulating a real-world client outreach optimization scenario at BlackRock. The goal was to build machine learning models that identify the most profitable clients to contact each week, maximizing investment returns under resource constraints.

## Business Problem

BlackRock's client advisory team receives ~7,500 new client leads per week but can only contact a maximum of 1,000. Each outreach costs €4.50, and the company earns an average profit of 4.0% on client investments, with clients typically investing about 28% of their current balance.

The challenge: **select the 1,000 clients per week that maximize expected profit.**

The expected profit per client was calculated as:

```
expected_profit = prob_of_invest × (expected_investment × 0.04 − 4.5)
```

## Approach

**1. Exploratory Data Analysis**
Analyzed client demographics, financial profiles, and investment behavior. Key findings included that management, blue-collar, technician, and admin roles showed the highest investment rates, while entrepreneurs consistently invested below €1,000. Clients with fewer than 10 prior marketing contacts tended to invest more, suggesting diminishing returns from repeated outreach.

**2. Feature Engineering**
Created derived features including age groups, marital status combined with job titles, and categorical variables to capture nuanced client characteristics and improve model performance.

**3. Model Experimentation**
Tested multiple algorithms across 7 weekly campaign periods: Logistic Regression, K-Nearest Neighbors, SVM, Decision Trees, Random Forests, and Boosted Trees. Models were iteratively retrained each week as new outcome data became available.

**4. Calibration & Tuning**
Applied hyperparameter tuning via grid search and cross-validation. Calibrated predicted probabilities using logistic regression fitted to primary model outputs for more reliable predictions.

**5. Profit-Based Ranking**
Ranked all clients by expected profit and selected the top 1,000 for weekly submission to the call center.

## Best Model — Random Forest

The Random Forest classifier was selected as the best performer. It uses demographic variables (age, job, marital status), financial indicators (balance, loans), and behavioral features (prior marketing contacts, call length) to predict investment likelihood.

| Metric | Score |
|--------|-------|
| AUC | 0.926 |
| Accuracy | 0.801 |
| Sensitivity | 0.929 |
| Specificity | 0.794 |
| Precision | 0.200 |

## Dataset Features

| Feature | Description |
|---------|-------------|
| `id` | Client identifier |
| `age` | Client age |
| `job` | Occupation |
| `marital` | Marital status |
| `preferred_contact` | Preferred contact channel |
| `balance` | Current investment account balance (€) |
| `loan_house` | Has a housing loan |
| `loan_personal` | Has a personal loan |
| `n_marketing_contacts` | Number of prior marketing contacts |
| `call_length` | Duration of the sales call (seconds) |
| `investment` | Amount invested in the ETF product |

## Repository Structure

```
├── analysis.Rmd                        # Main R Markdown analysis
├── report/
│   └── Predictive_Analytics.pdf        # Final project report
├── data/
│   ├── period_0.csv                    # Historical training dataset
│   ├── period_1_prediction.csv         # Weekly client lead files
│   ├── period_2_prediction.csv
│   └── ...
└── README.md
```

## Tools & Technologies

- **R** / **RStudio** — Primary development environment
- **R Markdown** — Reproducible analysis and reporting
- Key packages: `tidyverse`, `ggplot2`, `caret`, `randomForest`, `ROCR`

## How to Run

1. Clone this repository
2. Open `analysis.Rmd` in RStudio
3. Ensure required packages are installed
4. Knit the R Markdown file or run chunks interactively

## License

MIT
