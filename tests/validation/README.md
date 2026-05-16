# tests/validation — Validation Methodology

**Model Version:** v1.2-alpha  
**Status:** Pre-commercial development  
**Last Updated:** Q1 2026  
**Aligned With:** NIST AI RMF 1.0 — MEASURE Function

---

## 1. Overview

This directory documents the complete validation methodology used to
generate the performance metrics reported in
[`tests/benchmarks/`](../benchmarks/).

All validation is conducted on holdout datasets never used in model
training. Results are independently reproducible using the scripts
and data documentation provided in this directory.

---

## 2. Validation Design

### Holdout Strategy
- **Split ratio:** 80% training / 20% holdout validation
- **Stratification:** Stratified sampling ensures proportional
  representation of all 47 AML typology patterns in both sets
- **Contamination prevention:** Strict data pipeline separation;
  holdout set never accessed during training or hyperparameter tuning

### Cross-Validation
- **Method:** 5-fold stratified cross-validation on training set
- **Purpose:** Hyperparameter selection and model selection only;
  final performance reported on holdout set exclusively
- **Aggregation:** Mean and standard deviation reported across folds

### Statistical Significance
- All reported improvements tested at significance level p < 0.05
- McNemar's test used for classifier comparison against baseline
- Bootstrap confidence intervals (n=1,000) reported for all metrics

---

## 3. Ground Truth Sources

| Dataset | Ground Truth Source | Labelling Method |
|---|---|---|
| Financial transactions | FinCEN published SAR typology patterns | Rule-based labelling against 47 typologies |
| Blockchain anomalies | Chainalysis mixer-detection benchmarks | Known mixer/tumbler address labels |
| Dark web content | Manual expert annotation | 3-annotator consensus; Cohen's κ = 0.84 |
| Entity resolution | Synthetic identity ground truth | Deterministic generation with known links |
| SAR outcomes | FinCEN SAR XML template compliance | Template field completion scoring |

---

## 4. Metrics Definitions

| Metric | Definition | Formula |
|---|---|---|
| **False Positive Rate** | Proportion of legitimate alerts incorrectly flagged | FP / (FP + TN) |
| **False Negative Rate** | Proportion of genuine threats missed | FN / (FN + TP) |
| **Precision** | Proportion of flagged alerts that are genuine threats | TP / (TP + FP) |
| **Recall** | Proportion of all genuine threats that are flagged | TP / (TP + FN) |
| **F1 Score** | Harmonic mean of precision and recall | 2 × (P × R) / (P + R) |
| **Spearman ρ** | Rank correlation between risk scores and SAR outcomes | Rank correlation coefficient |
| **MTTA** | Mean time from signal detection to client alert delivery | End-to-end pipeline timing |

---

## 5. Baseline Comparison Methodology

FINSENTINEL™ v1.2 performance is compared against a rule-based AML
baseline constructed to reflect published industry performance data:

- **Primary source:** LexisNexis Risk Solutions, True Cost of Financial
  Crime Report (2023) — false positive rate data
- **Secondary source:** Celent AML Technology Report (2023) — precision
  and recall benchmarks for rule-based systems
- **Academic reference:** IEEE Security & Privacy (2022) — dark web
  NLP classification accuracy benchmarks
- **Blockchain reference:** Chainalysis publicly stated mixer detection
  recall (~95%) used as cryptocurrency module benchmark

---

## 6. Bias & Fairness Validation

### Methodology
Differential alert rate testing conducted across four dimensions:

1. **Geographic:** U.S.-domiciled vs. international entities
2. **Transaction size:** High-value (> $10,000) vs. low-value transactions
3. **Entity type:** Natural persons vs. legal entities
4. **Industry sector:** Financial services vs. non-financial sectors

### Test
- Chi-squared test for independence applied to alert rates across groups
- Significance threshold: p < 0.05
- Sample size: minimum 1,000 observations per group

### Results (v1.2)
No statistically significant disparate impact identified across any
tested dimension. Full results in
[`tests/benchmarks/README.md`](../benchmarks/).

---

## 7. Ongoing Monitoring Protocol

| Monitor | Frequency | Trigger for Action |
|---|---|---|
| F1 Score vs. baseline | Weekly | Drop > 5% from deployment baseline |
| False positive rate | Weekly | Rise > 3 percentage points |
| False negative rate | Weekly | Rise > 2 percentage points |
| Bias testing | Monthly | Any statistically significant disparity |
| Full revalidation | Quarterly | Or following any model update |
| External audit | Annually | Prior to any government contract renewal |

### Drift Detection
- Automated drift detection pipeline monitors input data distribution
- Population Stability Index (PSI) calculated weekly
- PSI > 0.2 triggers mandatory model review
- PSI > 0.25 triggers automatic model suspension pending human review

---

## 8. Independent Validation Plan

Prior to commercial launch, FINSENTINEL™ will commission an independent
external validation of model performance:

- **Scope:** Full replication of benchmark methodology by independent party
- **Validator:** Target — academic institution or accredited AI audit firm
- **Output:** Independent validation report to be published in this directory
- **Timeline:** Planned for completion prior to first commercial pilot
