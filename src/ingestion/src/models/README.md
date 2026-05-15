# src/models — Intelligence Processing Layer

This module constitutes Layer 2 of the FINSENTINEL™ four-layer intelligence
architecture. It processes raw ingested data using AI and machine learning
to extract actionable risk signals from noise.

---

## Module Overview

| Component | Description |
|---|---|
| `anomaly_detector.py` | Isolation forest and autoencoder-based anomaly detection |
| `nlp_classifier.py` | NLP model for dark web content classification (22 illicit categories) |
| `risk_scorer.py` | Dynamic entity and transaction risk scoring pipeline |
| `pattern_recogniser.py` | Behavioural pattern recognition across multi-source data |
| `model_trainer.py` | Continuous retraining pipeline as operational data accumulates |
| `drift_monitor.py` | Model drift detection and automated performance benchmarking |

---

## Model Architecture

### Anomaly Detection
- **Primary model:** Isolation Forest (unsupervised; no labelled data required)
- **Secondary model:** Autoencoder neural network (reconstruction error scoring)
- **Ensemble:** Outputs combined via weighted voting; threshold calibrated
  on 30-day rolling cycles
- **Training data:** 12M+ synthetic financial transaction records modelled
  on FinCEN BSA/SAR typology patterns

### NLP Classifier
- **Architecture:** Fine-tuned transformer model (BERT-class)
- **Task:** Multi-label classification of dark web content into 22 illicit
  activity categories including narcotics, weapons, financial fraud,
  ransomware coordination, and sanctions evasion
- **Training corpus:** 8.4M dark web document segments (non-PII)
- **Accuracy:** 93.6% (validated against held-out test set)

### Risk Scoring Engine
- **Output:** Dynamic 0–100 risk score per entity and transaction
- **Inputs:** Anomaly detector output; NLP classification confidence;
  entity resolution matches; historical behavioural baseline
- **Validation:** Spearman rank correlation ρ = 0.91 against SAR outcomes

---

## Performance (v1.2 Validation)

| Metric | Result | Industry Baseline |
|---|---|---|
| False Positive Rate | **12.3%** | 65–80% |
| False Negative Rate | **4.7%** | 18–25% |
| Precision | **87.7%** | 20–35% |
| Recall | **95.3%** | 75–82% |
| F1 Score | **0.913** | 0.40–0.52 |
| NLP Classification Accuracy | **93.6%** | 85–90% (IEEE S&P 2022 baseline) |

Full report: [`tests/benchmarks/v1.2_validation_report.md`](../../tests/benchmarks/)

---

## Governance & NIST AI RMF Alignment

- **MEASURE:** Weekly automated benchmarking against holdout validation set
- **MANAGE:** Drift detection triggers mandatory review if F1 drops below 0.82;
  automatic suspension if below 0.75
- **GOVERN:** All model versions logged with full change history; rollback
  to any prior version within 4 hours
- **MAP:** Model scoped exclusively to financial crime triage — explicitly
  excluded from credit decisioning, hiring, or prosecution functions

---

## Alignment

This module directly implements the AI/ML-led detection capability mandated
by **AMLA 2020, Section 6206**, which directs FinCEN to develop standards
for artificial intelligence and machine learning in financial crime detection.
