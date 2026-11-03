# ADR 004: Audit Log Design — Structured JSONL + Trace IDs + RLS

**Date:** 2025-11-01
**Status:** Accepted
**Deciders:** Jane Riveros

## Context
Multi-tenant workspace requires tenant-isolated audit trails for compliance (SOX, SEC Rule 17a-4, GDPR).

## Decision
Structured JSONL audit logs with UUID v7 `trace_id`. Row-Level Security (RLS) on audit tables. Dual write: Loki (hot) + PostgreSQL (cold, RLS) + S3 (raw).

## Rationale
- `trace_id` enables end-to-end correlation
- RLS enforces tenant isolation at database level
- JSONL schema-evolvable, queryable
- Tiered storage: cost vs. access patterns

## Consequences
- RLS policy complexity (must cover all audit tables)
- Storage volume (mitigated: compression, tiered retention)
- Schema evolution via ADR process
- Loki query language learning curve