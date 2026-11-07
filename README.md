# Mission Control — Showcase
**Cloud development environment for AI trading advisory system — unified workspace for agents, data, and governance.**  
*Public architecture showcase — implementation is private.*

[![Status](https://img.shields.io/badge/Status-Production%20Ready-EC4899?style=for-the-badge)]()
[![Governance](https://img.shields.io/badge/Governance-By%20Design-EC4899?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-Private-EC4899?style=for-the-badge)]()

---

## 🎯 Problem & Outcome

**Problem:** Building and operating multi-agent AI systems for trading requires: iterative agent development, real-time market data, backtesting infrastructure, compliance monitoring, and collaborative workflows — but existing tools are fragmented (Jupyter for research, VS Code for code, separate monitoring, manual compliance).

**Outcome:**
- `Unified workspace`: Next.js 15 + React 19 + Supabase + BPMN.js in one deploy
- `Agent development`: Visual BPMN workflow editor → executable agent graphs
- `Data integration`: Real-time market data + historical backtesting + vector search
- `Governance built-in`: Audit logging, eval harness, risk register, compliance dashboard
- `Collaboration`: Multi-user, real-time, role-based access (Supabase Auth + RLS)

**Domain:** Fintech / AI Infrastructure · **Regulatory touchpoints:** SOX, Basel III, MiFID II, SEC Rule 17a-4

---

## 🎥 Demo

| Format | Link |
|--------|------|
| **Full walkthrough (5-8 min)** | [🎥 YouTube / Loom / Vimeo](https://...) |
| **Quick demo (60 sec GIF)** | ![Demo](assets/demo.gif) |
| **Architecture narrated (3 min)** | [🎥 Link](https://...) |

---

## 📐 Architecture

### System Overview
```mermaid
%%{init: {'theme': 'base', 'themeVariables': {
  'primaryColor': '#0B2D4A',
  'primaryTextColor': '#fff',
  'primaryBorderColor': '#00C9A7',
  'lineColor': '#888',
  'secondaryColor': '#1A1A2E',
  'tertiaryColor': '#E85D4D',
  'background': 'transparent',
  'mainBkg': 'transparent',
  'secondBkg': 'transparent',
  'tertiaryBkg': 'transparent'
}}}%%
flowchart LR
    subgraph Frontend[Frontend (Next.js 15 + React 19)]
        UI[Dashboard]
        BPMN[BPMN Editor]
        Viz[Three.js Viz]
        Collab[Real-time Collab]
    end
    subgraph Backend[Backend (Supabase + Edge Functions)]
        Auth[Auth + RLS]
        Realtime[Realtime Subscriptions]
        Edge[Edge Functions]
        PG[(PostgreSQL + pgvector)]
    end
    subgraph Agents[Agent Runtime]
        Orch[Orchestrator]
        Research[Research Agent]
        Risk[Risk Agent]
        Comply[Compliance Agent]
    end
    subgraph Data[Data Layer]
        Market[Market Data APIs]
        News[News Feeds]
        Vector[Vector Search]
        Cache[Redis Cache]
    end
    subgraph Governance[Governance]
        Audit[Audit Logger]
        Eval[Eval Harness]
        Dashboard[Compliance Dashboard]
    end

    UI --> Auth
    UI --> Realtime
    BPMN --> Edge
    Viz --> PG
    Collab --> Realtime
    Edge --> Orch
    Orch --> Research
    Orch --> Risk
    Orch --> Comply
    Research --> Market
    Research --> News
    Research --> Vector
    Risk --> Market
    Comply --> PG
    Orch --> Audit
    Audit --> Dashboard
    Eval --> Audit

    style Frontend fill:#0B2D4A,color:#fff
    style Backend fill:#1A1A2E,color:#fff
    style Agents fill:#1A1A2E,color:#fff
    style Data fill:#00C9A7,color:#0B2D4A
    style Governance fill:#E85D4D,color:#fff
```

### High-Level Data Flow (Excalidraw)
![Architecture Overview](diagrams/system-overview.svg)  
*Hand-drawn style for architectural thinking — [editable Excalidraw file](diagrams/system-overview.excalidraw)*

### Key Components

| Component | Responsibility | Tech | Governance Hook |
|-----------|----------------|------|-----------------|
| `BPMN Editor` | Visual workflow definition → executable graph | bpmn-js + custom React wrapper | Workflow version-controlled; changes trigger eval |
| `Agent Orchestrator` | Executes BPMN-defined agent graphs | TypeScript (Edge Functions) | Every node emits audit entry |
| `Research Agent` | Market analysis, news synthesis, thesis generation | Anthropic SDK + tool registry | Tool calls logged; citations verified |
| `Risk Agent` | Portfolio risk, VaR, stress testing | Python (Edge Function) + financial models | `risk_assessment` audit entry; hard gates |
| `Compliance Agent` | Rule validation, disclosure generation | TypeScript rule engine | `compliance_check` audit entry; fail-closed |
| `Realtime Sync` | Multi-user collaboration, live updates | Supabase Realtime + CRDT | All edits audit-logged |
| `Compliance Dashboard` | Auditor view: decisions, trails, eval results | Next.js + Recharts + Loki | Read-only; real-time |

---

## ⚙️ Tech Stack (What I Built vs. Leveraged)

| Layer | Built by Me | Leveraged / Configured |
|-------|-------------|------------------------|
| **Frontend** | Dashboard, BPMN editor wrapper, Three.js viz, realtime collaboration | Next.js 15, React 19, TypeScript, Tailwind, Framer Motion, GSAP, bpmn-js, React Three Fiber, recharts, zustand |
| **Backend** | Edge Functions for agents, Supabase schema, RLS policies, Realtime config | Supabase (PostgreSQL + Auth + Realtime + Edge Functions + pgvector) |
| **Agents** | Custom orchestrator, research/risk/compliance agents, tool registry | Anthropic SDK, custom TypeScript orchestration |
| **Data** | Market data adapters, vector index strategy, cache layer | Alpha Vantage, Polygon.io, SEC EDGAR, Redis, pgvector |
| **Eval & Governance** | **Custom eval harness, structured audit logs, risk register, model cards, ADRs** | (Private — not in showcase) |
| **Infra & Deploy** | Vercel config, Supabase migrations, GitHub Actions CI/CD | Vercel, Supabase CLI, GitHub Actions, Docker (local) |
| **Visualization** | Three.js portfolio viz, BPMN workflow editor, compliance charts | React Three Fiber, bpmn-js, recharts, Framer Motion |

> **Governance-by-design note:** Every agent node execution emits trace ID → audit log → eval harness. BPMN workflow changes trigger regression tests. Compliance Agent runs as hard gate before any output.

---

## 🛡️ Governance & Compliance Artifacts

| Artifact | Location | Purpose |
|----------|----------|---------|
| **Model Card** | `docs/model-card.md` | Intended use, limitations, eval results, data lineage |
| **Risk Register** | `docs/risk-register.csv` | Identified risks, likelihood, impact, mitigations, owner |
| **Eval Harness** | `evals/` | Regression tests, red-team prompts, threshold gates |
| **Audit Log Schema** | `docs/audit-log-schema.json` | Structured schema for every decision trace |
| **ADRs** | `docs/adr/` | Architecture Decision Records (numbered, dated) |

---

## 🚀 How to Run (High-Level)

> **Implementation is private.** This section describes the *operational model* for reference.

```bash
# 1. Infrastructure
supabase db push
supabase functions deploy

# 2. Frontend
cd apps/web && npm install && npm run dev

# 3. Eval harness (local)
cd evals && python -m pytest --tb=short

# 4. Observability
# Grafana dashboards + Loki + compliance dashboard
```

**Environment variables required** (see `.env.example` in private repo):
- `ANTHROPIC_API_KEY`, `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`, `MARKET_DATA_API_KEY`, `EVAL_THRESHOLD`, `AUDIT_LOG_LEVEL`

---

## 📁 Repository Structure

```
mission-control-showcase/
├── README.md                    ← This file
├── ARCHITECTURE.md              ← Deep-dive: decisions, trade-offs, failure modes
├── diagrams/
│   ├── system-overview.mermaid  ← Mermaid source for system diagram
│   ├── system-overview.svg      ← Excalidraw export (architecture)
│   ├── data-flow.mermaid
│   ├── data-flow.svg
│   ├── sequence-research.mermaid
│   ├── sequence-risk.mermaid
│   └── sequence-compliance.mermaid
├── assets/
│   ├── demo.gif                 ← 60-sec demo GIF (<2MB, 720p)
│   ├── screenshot-bpmn.png      ← BPMN editor (1440px)
│   ├── screenshot-dashboard.png ← Compliance dashboard
│   └── screenshot-viz.png       ← Three.js visualization
├── docs/
│   ├── model-card.md
│   ├── risk-register.csv
│   ├── audit-log-schema.json
│   └── adr/
│       ├── 001-nextjs-supabase.md
│       ├── 002-bpmn-integration.md
│       ├── 003-edge-functions.md
│       ├── 004-audit-log-design.md
│       └── 005-eval-harness.md
└── evals/
    ├── test_regression.py
    ├── test_redteam.py
    └── thresholds.yaml
```

---

## 🔗 Private Repo Access

**Full implementation, CI/CD, infra-as-code, and eval runs** are in a private repository.

**Access process:**  
1. Initial screening call (30 min)  
2. Mutual NDA (template provided)  
3. Temporary read access to private repo + 1-hour walkthrough with me  
4. Access revoked after evaluation period

**Contact:** `jdriveros232@gmail.com` — subject: `Mission Control Private Repo Access`

---

## 📌 Related Showcases

- [Novaxis OS / Atlas](https://github.com/testaiprojects1-sketch/novaxis-showcase)
- [MAVIS — Personal AI](https://github.com/testaiprojects1-sketch/mavis-showcase)
- [Dental Clinic Platform](https://github.com/testaiprojects1-sketch/dental-clinic-showcase)
- [Tattoo Artist Platform](https://github.com/testaiprojects1-sketch/tattoo-platform-showcase)
- [All showcases](https://github.com/testaiprojects1-sketch?tab=repositories&q=showcase)

---

*Part of the **testaiprojects1-sketch** AI Systems Engineering portfolio — Governance by Design.*