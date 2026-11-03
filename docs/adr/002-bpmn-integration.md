# ADR 002: BPMN.js Integration for Visual Workflow Definition

**Date:** 2025-11-01
**Status:** Accepted
**Deciders:** Jane Riveros

## Context
Domain experts (compliance, risk) need to read/modify agent workflows. Code-only creates bottleneck.

## Decision
Integrate bpmn-js for visual BPMN 2.0 workflow definition. Custom extensions for AI node types. Executable XML → agent graph parser.

## Rationale
- BPMN is standard; compliance/risk teams know it
- bpmn-js mature, extensible, React-integrable
- XML diffable, reviewable in PRs
- Executable: parser converts BPMN → agent graph at deploy

## Consequences
- Bundle size impact (~500KB gzipped)
- BPMN semantic gaps for AI agents (mitigated: custom extensions)
- Runtime execution engine needed (custom, lightweight)
- Version migration for BPMN XML changes