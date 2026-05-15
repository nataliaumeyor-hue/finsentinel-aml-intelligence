# FINSENTINEL™ AI System Card

**NIST AI Risk Management Framework (AI RMF 1.0) Aligned**  
**Version:** 1.2  
**Status:** Pre-commercial development  
**Last Updated:** 2026  
**Developer:** Natalia Umeyor, Founder, FINSENTINEL™

---

## 1. Model Identity & Intended Use

| Field | Detail |
|---|---|
| **System Name** | FINSENTINEL™ AI Financial Crime Detection Engine |
| **Version** | v1.2-alpha (pre-commercial development build) |
| **Model Type** | Ensemble AI: supervised anomaly detection + unsupervised clustering + NLP classification + graph neural network |
| **Primary Function** | Detection and prioritisation of illicit financial activity signals across dark web, blockchain, and regulated financial system data |
| **Intended Deployment** | U.S. financial institutions (banks, fintechs, cryptocurrency exchanges); U.S. federal regulatory agencies (FinCEN, DHS, FBI, OFAC) |
| **Intended Users** | Compliance officers; AML analysts; financial crime investigators; regulatory agency personnel |
| **Decision Context** | Triage and prioritisation tool — human review is required before any SAR filing or enforcement action |
| **Out-of-Scope Uses** | Credit decisioning; hiring or employment screening; law enforcement prosecution; any use outside financial crime triage |

---

## 2. Training Dataset Documentation

| Dataset | Description | Volume | Governance |
|---|---|---|---|
| Synthetic Financial Transactions | Synthetically generated records modelled on FinCEN BSA/SAR typology patterns | 12M+ records; 47 AML typology patterns | No PII; FinCEN alignment verified |
| Blockchain Transaction Graphs | Public on-chain data from Bitcoin and Ethereum networks; labelled mixer interactions | 180M+ records; 2.3M labelled clusters | Publicly available; no PII |
| Dark Web Content Corpus | NLP-labelled text from public dark web marketplace listings (non-PII) | 8.4M document segments; 22 illicit categories | No PII; trade secret protection |
| Sanctions / Watchlist Data | OFAC SDN list; FATF high-risk jurisdiction data | 12,000+ sanctioned entities; quarterly updates | All public regulatory data |
| AML Alert Outcomes | Labelled SAR outcomes from synthetic FinCEN typology simulation | 340,000 labelled outcomes | Synthetic only; no real SAR data |

---

## 3. Performance Metrics (v1.2 Validation)

| Metric | FINSENTINEL™ v1.2 | Industry Baseline |
|---|---|---|
| False Positive Rate | **12.3%** | 65–80% |
| False Negative Rate | **4.7%** | 18–25% |
| Precision | **87.7%** | 20–35% |
| Recall | **95.3%** | 75–82% |
| F1 Score | **0.913** | 0.40–0.52 |
| Mean Time to Alert | **< 45 seconds** | 24–48 hours (batch) |
| SAR Auto-Generation Accuracy | **91.2%** | N/A (manual process) |
| Entity Resolution Precision | **94.8%** | N/A (novel capability) |

Full validation report: [`tests/benchmarks/v1.2_validation_report.md`](../tests/benchmarks/)

---

## 4. NIST AI RMF Alignment

### GOVERN
| Control | Implementation |
|---|---|
| Accountability | Founder serves as AI Accountability Officer; Chief AI Ethics Officer planned post-Series A |
| Policy Documentation | AI use policy, data governance policy, and model change management documented in `/docs/governance/` |
| Stakeholder Engagement | Advisory board includes planned AML expert and AI ethics advisor roles |
| Legal & Regulatory Review | System reviewed against BSA, AMLA 2020, ECPA, and applicable data protection laws |

### MAP
| Control | Implementation |
|---|---|
| Use Case Scoping | Scoped exclusively to financial crime triage; explicitly excluded from credit, hiring, and prosecution |
| Risk Identification | Primary risks: false positive over-alerting; false negative failure; model drift; adversarial evasion |
| Impact Assessment | Human-in-the-loop review required for all SAR filings before submission |
| Third-Party Dependencies | External data providers subject to vendor risk assessment and contractual data quality SLAs |

### MEASURE
| Control | Implementation |
|---|---|
| Performance Metrics | FPR; FNR; Precision; Recall; F1 Score; MTTA; Alert Escalation Accuracy |
| Bias & Fairness Testing | Outputs tested for differential alert rates; no statistically significant disparate impact in v1.2 |
| Ongoing Monitoring | Model drift detection pipeline; weekly automated benchmarking; 30-day threshold recalibration |
| Independent Validation | External model audit planned prior to commercial launch |

### MANAGE
| Control | Implementation |
|---|---|
| Incident Response | Detection → containment → root cause analysis → rollback or patch → stakeholder notification |
| Model Versioning | All versions maintained with full change log; rollback to any prior version within 4 hours |
| Decommissioning | F1 below 0.82 triggers mandatory review; below 0.75 triggers automatic suspension |
| Continuous Improvement | Compliance officer case closure data feeds quarterly model retraining cycle |

---

## 5. Limitations & Known Risks

| Limitation | Description | Mitigation |
|---|---|---|
| Novel adversarial techniques | Sophisticated actors may develop evasion techniques not represented in training data | Continuous retraining; quarterly red-team exercises planned |
| Dark web coverage gaps | Not all hidden services are accessible; coverage is extensive but not exhaustive | Multiple crawler nodes; diverse entry point rotation |
| Synthetic training data | Models trained on synthetic data may not capture all real-world edge cases | Pilot programme outcomes will feed real-world retraining |
| Model drift | Financial crime patterns evolve; model performance may degrade over time | Weekly drift monitoring; 30-day recalibration cycles |
| False negatives | 4.7% miss rate means some genuine threats may not be flagged | Human analyst review of borderline cases; ensemble model design |

---

## 6. Ethical AI Commitments

- **Human oversight:** No automated enforcement action — all SAR filings require human review and approval
- **Transparency:** System card and performance metrics publicly documented in this repository
- **Fairness:** Regular bias testing across entity types, geographies, and transaction structures
- **Privacy:** No collection of personal data beyond what is necessary for financial crime detection
- **Accountability:** Clear chain of responsibility from model output to human decision-maker

---

## 7. Federal Policy Alignment

| Policy | Alignment |
|---|---|
| AMLA 2020, Section 6206 | AI/ML-led AML modernisation mandate |
| U.S. Treasury NML Risk Assessment 2024 | Dark web and digital asset monitoring priority |
| FinCEN AML/CFT Priorities 2024 | Cybercrime and ransomware financing detection |
| Executive Order 14110 on AI Safety | Responsible AI standards for financial applications |
| NIST AI RMF 1.0 | Full Govern / Map / Measure / Manage alignment |
| FedRAMP Moderate | Government-grade security architecture |

---

## 8. Contact & Responsible Disclosure

**Developer:** Natalia Umeyor  
**Organisation:** FINSENTINEL™  
**Repository:** github.com/nataliaumeyor-hue/finsentinel-aml-intelligence  
**Responsible Disclosure:** Please open a GitHub Issue for any concerns
regarding model behaviour, bias, or safety.
