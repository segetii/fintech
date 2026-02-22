# AMTTP Open-Source Client SDKs

> Developer tools for the **Advanced Money Transfer Transaction Protocol** compliance platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENCE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0%2B-blue.svg)](https://www.typescriptlang.org/)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![Node.js 18+](https://img.shields.io/badge/Node.js-18%2B-green.svg)](https://nodejs.org/)

---

## 🔍 Overview

**AMTTP (Advanced Money Transfer Transaction Protocol)** is a novel compliance protocol for DeFi and crypto transactions, combining stacked-ensemble machine-learning risk scoring, regulatory compliance (FCA, FATF Travel Rule), and decentralised governance.

These open-source SDKs provide **developer-friendly access** to the full AMTTP compliance platform from both TypeScript/JavaScript and Python environments.

The platform addresses a **critical gap in the UK fintech ecosystem**: FCA-compliant AML/KYC tooling for decentralised finance. It exposes **21 integrated services** covering risk assessment, sanctions screening, KYC, PEP screening, dispute resolution, real-time monitoring, and more — all through a clean, type-safe API surface.

---

## ⚡ Key Technical Innovations

- **Stacked Ensemble ML** — XGBoost + Graph Neural Networks + heuristic rule engine for fraud detection and risk scoring
- **OFAC/EU/UN Sanctions Screening** — Real-time multi-list sanctions checking with entity matching
- **FATF Travel Rule Compliance** — Full regulatory compliance with Travel Rule originator/beneficiary data
- **Kleros Decentralised Arbitration** — On-chain dispute resolution with trustless escrow
- **MEV Protection** — Flashbots bundle integration for transaction privacy and front-run prevention
- **WYSIWYS UI Integrity** — *What You See Is What You Sign* — prevents UI-tampering attacks (cf. Bybit-style attack vectors)
- **Zero-Knowledge Proofs** — Privacy-preserving compliance verification
- **Multi-sig Governance** — Quorum-based enforcement actions with full audit trail
- **ML Explainability** — Human-readable explanations for every risk decision

---

## 📦 SDK Overview

| SDK | Language | Install | Key Features |
|-----|----------|---------|--------------|
| `@amttp/client-sdk` | TypeScript / JavaScript | `npm install @amttp/client-sdk` | Full type safety, event system, auto-retry |
| `amttp-sdk` | Python | `pip install amttp-sdk` | Async/await, Pydantic v2 models, `py.typed` |

---

## 🛠️ Available Services

Both SDKs expose all 21 AMTTP platform services:

| Service | Description |
|---------|-------------|
| **Risk Assessment** | Stacked Ensemble ML (XGBoost + GNN + rules) risk scoring |
| **KYC Verification** | Multi-tier KYC with document management and expiry tracking |
| **Transaction Management** | Full transaction lifecycle with policy enforcement |
| **Compliance Orchestration** | Unified compliance evaluation with ML integration |
| **Sanctions Screening** | Real-time OFAC, EU, and UN sanctions list checking |
| **Geographic Risk** | Country and IP risk using FATF black/grey lists |
| **PEP Screening** | Multi-provider Politically Exposed Persons checks |
| **Enhanced Due Diligence (EDD)** | Case management, document collection, and resolution workflows |
| **Real-time Monitoring** | Continuous compliance monitoring with custom alerting rules |
| **Address Labels** | Comprehensive on-chain address categorisation |
| **Policy Engine** | Configurable compliance policy creation and evaluation |
| **Dispute Resolution** | Kleros-integrated on-chain arbitration system |
| **Reputation System** | 5-tier scoring: Bronze → Silver → Gold → Platinum → Diamond |
| **Governance (WYAS multi-sig)** | Quorum-based enforcement actions with *What You Approve Summary* (WYAS) and MFA sign-off |
| **ML Explainability** | Human-readable risk-factor breakdowns and typology matching |
| **UI Integrity (WYSIWYS)** | Snapshot-hash verification before transaction signing |
| **Dashboard Analytics** | Real-time stats, Sankey flows, geographic risk maps |
| **Bulk Operations** | Batch scoring up to 10,000 transactions per job |
| **Webhooks** | HMAC-SHA256 signed real-time event notifications |
| **MEV Protection** | Flashbots bundle submission for front-run prevention |
| **Entity Profiles** | Persistent entity metadata and risk-tolerance management |

---

## 🚀 Quick Start

### TypeScript / JavaScript

```typescript
import { AMTTPClient } from '@amttp/client-sdk';

const client = new AMTTPClient({
  baseUrl: 'https://api.amttp.io',
  apiKey: 'your-api-key',
});

// Risk assessment
const risk = await client.risk.assess({
  address: '0x1234...abcd',
  amount: '1000000000000000000', // 1 ETH in wei
});
console.log(`Risk Score: ${risk.riskScore}, Level: ${risk.riskLevel}`);

// Unified compliance evaluation
const decision = await client.compliance.evaluate({
  from_address: '0x1234...abcd',
  to_address:   '0xdead...beef',
  amount: 1.5,
  currency: 'ETH',
  chain: 'ethereum',
});
console.log(`Decision: ${decision.action}`); // ALLOW | REQUIRE_INFO | BLOCK
```

For complete TypeScript SDK documentation see [`client-sdk/README.md`](client-sdk/README.md).

### Python

```python
import asyncio
from amttp import AMTTPClient
from amttp.services.risk import RiskAssessmentRequest
from amttp.services.compliance import EvaluateRequest

async def main():
    async with AMTTPClient("https://api.amttp.io", api_key="your-api-key") as client:
        # Risk assessment
        risk = await client.risk.assess(
            RiskAssessmentRequest(address="0x1234...abcd")
        )
        print(f"Risk: {risk.risk_score} ({risk.risk_level})")

        # Unified compliance evaluation
        decision = await client.compliance.evaluate(
            EvaluateRequest(
                from_address="0x1234...abcd",
                to_address="0xdead...beef",
                value_eth=1.5,
            )
        )
        print(f"Decision: {decision.action} (score: {decision.risk_score})")

asyncio.run(main())
```

For complete Python SDK documentation see [`client-sdk-python/README.md`](client-sdk-python/README.md).

---

## 🏗️ Architecture

```
Developer App
    │
    ▼
AMTTP SDK  (TypeScript or Python)
    │
    ▼
AMTTP API Gateway
    │
    ├── Risk Service          (Stacked Ensemble ML)
    ├── Sanctions Service     (OFAC / EU / UN)
    ├── KYC Service           (Multi-tier verification)
    ├── Compliance Service    (Unified orchestrator)
    ├── Policy Engine         (Configurable rules)
    ├── Dispute Service       (Kleros arbitration)
    ├── Governance Service    (Multi-sig enforcement)
    ├── MEV Protection        (Flashbots bundles)
    └── ... (21 services total)
```

---

## ⚖️ Regulatory Compliance

The AMTTP platform is designed to meet the following UK and international regulatory frameworks:

| Framework | Coverage |
|-----------|----------|
| **FCA** (Financial Conduct Authority) | UK AML/KYC requirements for crypto-asset firms |
| **FATF Travel Rule** | Originator and beneficiary data for transfers ≥ $1,000 |
| **OFAC Sanctions** | US Treasury Office of Foreign Assets Control list |
| **EU Sanctions** | European Union consolidated sanctions list |
| **UN Sanctions** | United Nations Security Council sanctions list |
| **KYC / AML** | Document verification, ongoing monitoring, and SAR workflows |
| **PEP Screening** | Politically Exposed Persons detection across multiple data sources |
| **EDD** | Enhanced Due Diligence case workflows for higher-risk entities |

---

## 📚 Documentation

| Resource | Link |
|----------|------|
| TypeScript SDK (full) | [`client-sdk/README.md`](client-sdk/README.md) |
| Python SDK (full) | [`client-sdk-python/README.md`](client-sdk-python/README.md) |
| SDK overview | [`SDK_README.md`](SDK_README.md) |

---

## 📁 Project Structure

```
├── README.md                  # This file
├── SDK_README.md              # High-level SDK summary
├── LICENCE                    # MIT Licence
├── client-sdk/                # TypeScript / JavaScript SDK
│   ├── README.md
│   ├── src/
│   └── ...
└── client-sdk-python/         # Python SDK
    ├── README.md
    ├── amttp/
    └── ...
```

---

## 📄 Licence

MIT — see [LICENCE](LICENCE) for details.

---

## 👤 About the Author

Created and maintained by <a href="https://github.com/segetii">@segetii</a>.
