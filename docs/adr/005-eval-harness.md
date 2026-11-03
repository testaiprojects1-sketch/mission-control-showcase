# ADR 005: Custom Eval Harness with BPMN Change Triggers

**Date:** 2025-11-01
**Status:** Accepted
**Deciders:** Jane Riveros

## Context
Need regression testing, red-teaming, BPMN semantic validation, and drift detection. BPMN changes must trigger eval.

## Decision
Custom Python (pytest) eval harness. GitHub Actions runs on PR + workflow save (via Supabase webhook) + nightly.

## Rationale
- Domain-specific thresholds (risk drift, citation accuracy, compliance pass rate)
- BPMN semantic validation: custom rules for AI node types
- Hard gates: blocks PR merge + workflow save on failure
- Red-team prompts version-controlled
- No external dependency for core governance

## Consequences
- Maintenance burden (solo-owned)
- Supabase webhook → GitHub Actions integration complexity
- No managed dashboard (GitHub Actions summary)
- Must implement parallelization (pytest-xdist)