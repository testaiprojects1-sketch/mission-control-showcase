# ADR 003: Supabase Edge Functions for Agent Runtime

**Date:** 2025-11-01
**Status:** Accepted
**Deciders:** Jane Riveros

## Context
Need serverless agent execution colocated with data (PostgreSQL, pgvector) for low latency and simplified auth.

## Decision
Deploy agent orchestrator + nodes as Supabase Edge Functions (Deno runtime).

## Rationale
- Colocated with Supabase: auth, RLS, Realtime, pgvector
- Auto-scaling, no server management
- Deno: TypeScript native, secure by default
- Low latency (edge locations)
- Integrated with Supabase Auth (JWT validation automatic)

## Consequences
- 2s timeout limit (mitigated: async patterns, polling)
- 150MB memory limit
- Deno ecosystem smaller than Node.js
- Cold starts (~100-500ms)
- No long-running processes (mitigated: workflow state in PG)