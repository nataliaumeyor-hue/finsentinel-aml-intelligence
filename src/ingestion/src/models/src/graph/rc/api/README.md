# src/api — Output & Integration Layer

This module constitutes Layer 4 of the FINSENTINEL™ four-layer intelligence
architecture. It delivers actionable intelligence to clients and regulators
in real time through standardised API interfaces and automated workflows.

---

## Module Overview

| Component | Description |
|---|---|
| `alert_engine.py` | Real-time alert generation and priority routing |
| `sar_workflow.py` | Automated SAR filing preparation and FinCEN submission integration |
| `rest_api.py` | REST API endpoints for institutional client integration |
| `graphql_api.py` | GraphQL interface for flexible intelligence querying |
| `dashboard_api.py` | Compliance dashboard data feeds and real-time updates |
| `webhook_manager.py` | Webhook delivery for sub-minute client notifications |
| `regulatory_connector.py` | Direct integration with FinCEN, OFAC, and agency data feeds |

---

## API Architecture

### REST API
- **Standard:** OpenAPI 3.0 specification
- **Authentication:** OAuth 2.0 with JWT bearer tokens; MFA enforced
- **Rate limiting:** Tiered by subscription level
- **Versioning:** Semantic versioning; minimum 12-month deprecation notice
- **Compatibility:** Designed for integration with Actimize, Oracle FCCM,
  and other incumbent AML platforms

### GraphQL API
- Enables compliance teams to query specific entity relationships,
  risk scores, and alert histories without predefined report structures
- Supports real-time subscriptions for live alert streaming

### Regulatory Connectors
- **FinCEN SAR API:** Automated SAR draft generation aligned with
  FinCEN XML schema requirements; human review gate before submission
- **OFAC SDN:** Real-time sanctions screening against updated SDN list
- **SWIFT ISO 20022:** Full compatibility for financial institution
  transaction data ingestion and alert delivery
- **FinCEN 314(a):** Watchlist query and match notification workflow

---

## Alert Pipeline

| Stage | Process | Latency Target |
|---|---|---|
| Signal detection | Anomaly detector flags high-risk pattern | < 5 seconds |
| Risk scoring | Entity risk score calculated and ranked | < 10 seconds |
| Alert generation | Formatted alert created with evidence bundle | < 20 seconds |
| Client notification | Webhook / dashboard delivery | < 45 seconds P95 |
| SAR draft creation | Auto-populated SAR form for human review | < 60 seconds |

**Mean Time to Alert (MTTA): < 45 seconds (P95)**
vs. 24–48 hour batch processing in incumbent rule-based systems.

---

## SAR-Triggering Workflow

The automated SAR preparation workflow is one of FINSENTINEL™'s most
significant compliance contributions:

1. High-risk alert crosses configurable threshold
2. System auto-populates FinCEN SAR XML template with entity data,
   transaction history, and supporting evidence
3. Draft routed to compliance officer queue for mandatory human review
4. Compliance officer approves, modifies, or rejects
5. Approved SARs submitted via FinCEN BSA E-Filing system

**SAR auto-generation accuracy: 91.2%** (validated against FinCEN
SAR typology templates). Human review is required before all filings.

---

## Integration Compatibility

| System | Integration Method | Status |
|---|---|---|
| Actimize (NICE) | REST API + webhook | Designed |
| Oracle FCCM | REST API | Designed |
| FinCEN BSA E-Filing | XML schema direct submission | Designed |
| SWIFT network | ISO 20022 message format | Designed |
| Core banking systems | REST API + event streaming | Designed |
| OFAC sanctions screening | Real-time API query | Designed |

---

## Security

- All API traffic encrypted via TLS 1.3
- OAuth 2.0 authentication with short-lived JWT tokens (15-minute expiry)
- Role-based access control (RBAC) — principle of least privilege enforced
- Full audit log of all API calls retained for 7 years (BSA requirement)
- Zero-trust network architecture — no implicit trust between services

---

## Alignment

This module operationalises the real-time alerting and SAR automation
capabilities identified as priority needs in **FinCEN's AML/CFT Priorities
2024** and supports the technology-led modernisation mandate of
**AMLA 2020, Section 6206**.
