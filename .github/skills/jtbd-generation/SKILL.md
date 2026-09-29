---
name: jtbd-generation
description: 'Write strong Jobs To Be Done statements from stakeholder quotes or repository evidence. Use when asked to create JTBD statements and, only if explicitly requested, output a JTBD table with evidence fields.'
argument-hint: 'Provide quotes or point to source files. Ask explicitly if you want a JTBD table output.'
user-invocable: true
---

# JTBD Generation

Write high-quality, evidence-grounded JTBD statements first. Create a JTBD table only when the user explicitly asks for it.

## When to Use

Use this skill when the user asks to:
- create JTBD statements from stakeholder quotes or research notes
- rewrite feature requests into underlying jobs and outcomes
- generate JTBDs from repeated signals in repository evidence
- optionally produce a JTBD table when explicitly requested

## JTBD Standard

Every statement must use this exact structure:
- When ...
- I want to ...
- So that ...

Non-negotiable rule:
- describe the underlying job, not the requested tool or feature

Bad example:
- I need a dashboard

Good example:
- When I review workload, I want reliable visibility of self-serve and agent-routed cases so that I can manage the team accurately

## Preferred Inputs

Primary input:
- direct stakeholder quote(s) provided by the user

Optional repository inputs:
- `phase_2/theme_summary.csv`
- `phase_2/stakeholder_evidence_table.csv`
- `data/stakeholder_interview_notes.csv`
- `phase_1/TBA W1 Data - Stakeholder Overview.csv`

If repository files are unavailable, continue with the provided quote(s).

## Default Output Mode

Unless the user asks for a table, output JTBD statements only.

A table is created only when the user explicitly asks for one, for example:
- build a JTBD table
- output a csv with JTBD columns
- fill this table: `| JTBD ID | Actor | Statement | Evidence link | Portal relevance | Priority |`

## Procedure

### 1) Parse input quotes
- Accept one or many quotes.
- If using repository evidence, identify candidate quotes from repeated sub-signals.

### 2) Write JTBD statements
- Produce one JTBD per quote.
- Use exact structure:
  - When ...
  - I want to ...
  - So that ...

### 3) Apply quality checks (required)
For every statement:
- need-focused, not feature-focused
- tool-independent
- outcome-oriented
- traceable to source quote
- concise and specific
- exact `When / I want to / So that` structure

### 4) Optional table generation (explicit request only)
If the user explicitly asks for a table:
- build rows with these fields:
  - `JTBD ID` as `JTBD-01`, `JTBD-02`, ...
  - `Actor`
  - `Statement`
  - `Evidence link`
  - `Portal relevance`
  - `Priority`
- use actor from source data when available; otherwise infer
- use evidence link from source row IDs or URLs when available; otherwise `N/A`
- infer portal relevance and priority when absent
- produce markdown preview in chat
- if asked for CSV, write with exact header and order:
  - `JTBD ID,Actor,Statement,Evidence link,Portal relevance,Priority`

## Output Contract

Return in this order:
1. `JTBD Statements` section (always)
2. table preview only if explicitly requested
3. CSV write confirmation only if explicitly requested

## Acceptance Criteria

- one JTBD per selected quote
- every JTBD uses exact structure
- table output only when explicitly requested
- if table requested: CSV header order exactly matches specification
- if table requested: row count equals processed quote count
- if table requested: IDs are unique and sequential
