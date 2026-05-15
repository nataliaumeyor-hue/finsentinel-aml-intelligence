# src/ingestion — Data Ingestion Layer

This module constitutes Layer 1 of the FINSENTINEL™ four-layer intelligence
architecture. It is responsible for the continuous capture and aggregation of
raw intelligence from multiple high-risk digital environments simultaneously.

---

## Module Overview

| Component | Description |
|---|---|
| `dark_web_crawler.py` | Tor/I2P network crawler for hidden marketplace and forum monitoring |
| `blockchain_connector.py` | Bitcoin, Ethereum, and Monero on-chain transaction feed ingestion |
| `kyc_feed_parser.py` | KYC provider API integration and identity data normalisation |
| `sar_data_ingestor.py` | FinCEN SAR typology pattern feed and watchlist synchronisation |
| `financial_tx_api.py` | Core banking and payment system transaction data connectors |
| `stream_manager.py` | Apache Kafka-class real-time streaming pipeline orchestration |

---

## Data Sources

- **Dark Web:** Tor hidden services (.onion); I2P eepsites; paste sites
- **Blockchain:** Bitcoin UTXO graph; Ethereum transaction logs; Monero ring
  signature analysis; cross-chain bridge monitoring
- **KYC / Identity:** Third-party KYC provider APIs; PEP and sanctions lists
- **Financial Systems:** Core banking APIs; SWIFT ISO 20022 message feeds;
  card network transaction streams
- **Regulatory Feeds:** OFAC SDN list (updated daily); FinCEN 314(a)
  analogues; FATF high-risk jurisdiction data

---

## Security & Governance

- All data in transit encrypted via TLS 1.3
- Dark web collection restricted to non-PII marketplace and forum content
- Blockchain data sourced from public ledgers only
- Data residency: U.S.-only (AWS GovCloud us-east-1 / us-west-2)
- Retention policy: raw feeds retained 90 days; processed signals retained
  7 years in accordance with BSA record-keeping requirements

---

## Performance Targets

| Metric | Target |
|---|---|
| Dark web document ingestion rate | 2.4M documents/hour (dev); 10M/hour (prod) |
| Blockchain transaction throughput | 120,000 TPS (load tested); 500,000 TPS (prod target) |
| Feed latency (raw to pipeline) | < 5 seconds P95 |
| Uptime SLA | 99.9% |

---

## Alignment

This module directly addresses the intelligence gap identified in the
**U.S. Treasury National Money Laundering Risk Assessment 2024**, which
names dark web financial ecosystems and digital asset monitoring as
priority areas requiring urgent technological response.
