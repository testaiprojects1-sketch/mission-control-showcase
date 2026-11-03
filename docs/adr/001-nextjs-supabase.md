# ADR 001: Next.js 15 + Supabase over Custom Stack

**Date:** 2025-11-01
**Status:** Accepted
**Deciders:** Jane Riveros

## Context
Need unified platform for: dashboard, BPMN editor, real-time collaboration, agent runtime, auth, database, vector search.

## Decision
Next.js 15 (App Router) + Supabase (PostgreSQL + Auth + Realtime + Edge Functions + pgvector) + Vercel.

## Rationale
- TypeScript end-to-end (frontend + Edge Functions)
- Supabase provides managed: Auth (RLS), Realtime (CRDT sync), Edge Functions (Deno), pgvector
- Vercel: zero-config deploy, preview deployments, edge caching
- Single vendor for most infrastructure
- Fast iteration for solo founder

## Consequences
- Vendor lock-in (Supabase/Vercel)
- Edge Function limits: 2s timeout, 150MB memory, Deno runtime
- Supabase pricing at scale
- Less control over PostgreSQL tuning