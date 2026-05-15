# infra — Infrastructure & Security Architecture

**Cloud Platform:** AWS GovCloud / Azure Government  
**Security Standard:** FedRAMP Moderate Aligned  
**Status:** Pre-commercial development  
**Last Updated:** 2026

---

## 1. Overview

This directory contains the infrastructure-as-code (IaC) configurations
for the FINSENTINEL™ platform deployment. All infrastructure is designed
for government-grade security and compliance from inception, targeting
FedRAMP Moderate authorization to enable procurement by U.S. federal
agencies including FinCEN, DHS, FBI, and OFAC.

---

## 2. Cloud Architecture

### Primary: AWS GovCloud
- **Regions:** us-gov-east-1 (primary); us-gov-west-1 (failover)
- **Account type:** AWS GovCloud (US) — U.S. persons only access
- **Services:** EKS (container orchestration); RDS (relational data);
  Neptune (graph database); MSK (Kafka streaming); S3 GovCloud (storage);
  KMS (key management); CloudTrail (audit logging)

### Secondary: Azure Government
- **Regions:** USGov Virginia (primary); USGov Texas (failover)
- **Services:** AKS (container orchestration); Cosmos DB; Event Hubs;
  Azure Sentinel (SIEM); Key Vault; Azure Monitor

### Multi-Region Design
AWS GovCloud (Primary)          Azure Government (Secondary)
us-gov-east-1                   USGov Virginia
│                               │
└──────── Active-Active ────────┘
Load Balancing
│
Global Load Balancer
│
Client API Gateway
---

## 3. Security Controls

### Encryption
| Layer | Standard | Implementation |
|---|---|---|
| Data at rest | AES-256 | AWS KMS / Azure Key Vault managed keys |
| Data in transit | TLS 1.3 | Enforced across all service communication |
| Key rotation | 90-day | Automated via KMS key rotation policy |
| Database encryption | AES-256 | Transparent data encryption enabled |

### Access Control
| Control | Implementation |
|---|---|
| Authentication | OAuth 2.0 + JWT; MFA enforced for all access |
| Authorisation | Role-Based Access Control (RBAC); least privilege |
| Network | Zero-Trust architecture; no implicit trust between services |
| Privileged access | Just-in-time (JIT) access; no standing privileged sessions |
| Service accounts | Separate service accounts per microservice; scoped permissions |

### Network Security
| Control | Implementation |
|---|---|
| Perimeter | Web Application Firewall (WAF); DDoS protection |
| Segmentation | VPC with private subnets; no public internet exposure for data services |
| Monitoring | Network flow logs; anomaly detection on traffic patterns |
| Ingress | API Gateway with rate limiting and IP allowlisting for government clients |

---

## 4. FedRAMP Moderate Control Mapping

| NIST SP 800-53 Control Family | Implementation Status |
|---|---|
| AC — Access Control | Designed: RBAC; MFA; JIT access |
| AU — Audit & Accountability | Designed: CloudTrail; 7-year retention |
| CA — Assessment & Authorization | Planned: Third-party assessment pre-launch |
| CM — Configuration Management | Designed: Terraform IaC; version-controlled configs |
| CP — Contingency Planning | Designed: Multi-region active-active; RTO < 4 hours |
| IA — Identification & Authentication | Designed: OAuth 2.0; MFA; service account isolation |
| IR — Incident Response | Designed: Automated detection; 4-hour containment SLA |
| RA — Risk Assessment | Designed: Quarterly security reviews |
| SC — System & Communications Protection | Designed: TLS 1.3; VPC isolation; WAF |
| SI — System & Information Integrity | Designed: SIEM; automated vulnerability scanning |

---

## 5. Data Sovereignty & Residency

| Data Type | Residency Requirement | Implementation |
|---|---|---|
| PII (U.S. persons) | U.S. only | AWS GovCloud / Azure Government U.S. regions only |
| Financial transaction data | U.S. only | No cross-border transfer; U.S. region lock enforced |
| Dark web intelligence | U.S. only | Processing and storage in U.S. GovCloud regions |
| Blockchain analytics | U.S. only | On-chain public data processed in U.S. regions |
| Audit logs | U.S. only | CloudTrail logs stored in U.S. GovCloud S3 only |

All data residency controls enforced via AWS GovCloud and Azure Government
region restrictions. Compliant with CLOUD Act requirements for U.S.
government data access.

---

## 6. Monitoring & Observability

| Tool | Purpose | Retention |
|---|---|---|
| AWS CloudTrail | Full API and data access audit log | 7 years (BSA requirement) |
| Azure Sentinel | SIEM; threat detection; incident response | 1 year hot; 7 years cold |
| Prometheus | Infrastructure and application metrics | 90 days |
| Grafana | Real-time dashboards; alerting | — |
| PagerDuty | Incident alerting and on-call management | — |

### Key Monitoring Targets
- API response times and error rates
- Model inference latency (P50, P95, P99)
- Data pipeline throughput and lag
- Security event detection and alerting
- Cost and resource utilisation

---

## 7. Disaster Recovery

| Metric | Target |
|---|---|
| Recovery Time Objective (RTO) | < 4 hours |
| Recovery Point Objective (RPO) | < 15 minutes |
| Backup frequency | Continuous replication to secondary region |
| Failover type | Automated active-active; no manual intervention required |
| DR testing | Quarterly failover tests planned |

---

## 8. Compliance & Certification Roadmap

| Milestone | Target Timeline |
|---|---|
| FedRAMP Moderate — 3PAO assessment initiated | Pre-Series A |
| SOC 2 Type I | Year 1 post-launch |
| FedRAMP Moderate — Authorization to Operate (ATO) | Year 2 post-launch |
| SOC 2 Type II | Year 2 post-launch |
| StateRAMP (for state agency clients) | Year 3 post-launch |
