# Mission Control — Model Card

## Model Details
- **Model name:** Mission Control (Agent Development Environment)
- **Version:** 1.0.0
- **Date:** November 2025
- **Owner:** Jane Riveros

## Intended Use
Cloud IDE for building, testing, and monitoring multi-agent AI systems for regulated trading workflows. Target users: AI engineers, quant researchers, compliance officers.

## Limitations
- Not a trading platform (no order execution)
- Edge Function timeout: 2s (limits complex agent chains)
- Supabase free tier limits: 500MB DB, 2GB bandwidth
- Real-time collaboration: max 100 concurrent per workspace

## Evaluation Results
| Suite | Pass Rate | Threshold | Status |
|-------|-----------|-----------|--------|
| Regression | 96% | 95% | ✅ Pass |
| Red-team | 0 critical | 0 critical | ✅ Pass |
| BPMN validation | 100% | 100% | ✅ Pass |
| Drift detection | <3% | <5% | ✅ Pass |

## Data Lineage
- Market data: Alpha Vantage, Polygon.io (licensed)
- News: NewsAPI, custom RSS feeds
- SEC filings: EDGAR public database
- User data: Workspace members (Supabase Auth)

## Governance
- Audit logging: Every workflow change + node execution traced
- Eval harness: Runs on PR + workflow save + nightly
- Risk register: Reviewed quarterly
- RLS: Row-level security on all tables
- Model card: Updated per release