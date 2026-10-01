# FAERS Pharmacovigilance Signal Detection

## Overview

This project performs a pharmacovigilance analysis of FDA Adverse Event Reporting System (FAERS) quarterly data using Python.

The analysis includes:

- Loading and inspecting DEMO, DRUG, and REAC files
- Data cleaning and merging
- Primary Suspect drug filtering
- Descriptive analysis of drugs and adverse reactions
- PRR and ROR signal detection
- Chi-square and Fisher's exact testing
- Time-trend analysis
- Visualization of candidate safety signals

## Dataset

Data source: FDA Adverse Event Reporting System (FAERS)

Dataset period: Q3 2020

The raw FAERS files are not included in this repository.

## Methodology

### Primary Suspect Drug Filtering

For the basic signal-detection analysis, only drug records with
`ROLE_COD = 'PS'` (Primary Suspect) were retained.

This focuses the analysis on drugs identified in the FAERS report as the
primary suspected drug associated with the reported adverse event.
Concomitant or secondary-suspect drugs were excluded from the basic
signal-detection analysis to reduce background noise from other
medications reported in the same case.

This filtering defines the analysis population and does not establish
a causal relationship between the drug and adverse event.

### Signal Detection

Drug–ADR pairs were evaluated using:

- Proportional Reporting Ratio (PRR)
- Reporting Odds Ratio (ROR)
- 95% confidence interval for ROR
- Chi-square test
- Fisher's exact test for small counts

Potential signals were defined using:

- a >= 3
- PRR >= 2
- Chi-square >= 4

## Key Findings

The analysis identified multiple potential drug–ADR signals showing
disproportionate reporting in the FAERS database.

The results should be interpreted as candidate safety signals rather
than evidence of causality.

## Time-Trend Analysis

FAERS report dates were converted to datetime format and aggregated
by month for Q3 2020.

Unique `PRIMARYID` values were used to avoid counting multiple
drug or reaction records from the same report as separate reports.

Because FAERS is a spontaneous reporting system, changes in reporting
volume should not automatically be interpreted as changes in the true
incidence of an adverse event.

## Repository Structure

```text
FAERS-Pharmacovigilance-Analysis/
│
├── Assignment1_FAERS.ipynb
├── README.md
├── requirements.txt
│
├── results/
│   └── FAERS_signals.csv
│
└── figures/
    ├── top_20_drugs.png
    ├── top_20_reactions.png
    ├── age_sex_distribution.png
    ├── time_series_trends.png
    └── signal_heatmap.png
