---
name: evidence-theming
description: 'Turn stakeholder interview notes into 6 simple root-cause themes and a concise stakeholder evidence table with representative quotes. Use when users ask to theme, group, cluster, or synthesise interview notes, research quotes, stakeholder feedback, or to produce a stakeholder evidence table for discovery and prioritisation.'
argument-hint: 'Provide the notes source path(s) and any scope constraints (e.g., specific stakeholders, date range, or team).'
user-invocable: true
---

# Evidence Theming

Convert raw stakeholder interview notes into a defensible, decision-ready evidence synthesis for business analysis discovery work.

This skill removes duplicated quote lines, excludes vague non-specific signals, and outputs a concise representative table while still tracking supporting counts.

## When to Use

Use this skill when the user asks to:
- theme, group, cluster, or synthesise stakeholder interview notes
- analyse interview evidence, research quotes, or feedback into recurring themes
- produce a stakeholder evidence table
- separate high-signal structural problems from low-signal one-off comments

## Inputs

Expect one or more note sources (CSV or sheet export), with fields such as:
- stakeholder name or role
- quote, observation, or paraphrase
- optional metadata: date, team, account, region, channel

If metadata is missing, continue with available fields and record gaps under assumptions and limitations.

## Non-Negotiable Rules

1. Read every note before proposing any theme. Never theme from a sample.
2. Propose exactly 6 themes unless the dataset is genuinely too small or narrow; if not possible, explain why and use the nearest defensible number.
3. Themes must represent underlying need or structural problem, not a symptom restatement.
4. Name the cause, not the complaint.
5. Assign each cited note to exactly one theme.
6. Remove exact duplicate quote lines before thematic coding (even when duplicated across different stakeholders).
7. Exclude vague or non-specific notes that cannot be mapped to a clear structural issue; report exclusions explicitly.
8. Confidence must be calculated from a fixed theme-level rubric and applied consistently to all rows in the same theme.
9. Do not drop low-frequency but specific notes; include them where they add material range.
10. Remain evidence-led and neutral; do not jump to solution design unless explicitly asked.
11. Output only 2-4 representative quotes per theme, while still counting all supporting notes and sources behind each theme.
12. Prioritise evidence range over repetition: include breadth of sub-signals, not just the most repeated complaint.

## Default Theme Labels (plain language)

Use these theme names by default for debt-recovery stakeholder note packs unless the user requests alternatives:
- No single record of an account
- Nothing enforces a follow-up
- Status reports cannot be trusted
- Customers cannot see or settle their own case
- Risky cases are not separated from straightforward ones
- Agents and managers may not adopt it

## Procedure

### 1) Ingest and normalise
- Parse all available rows from every provided source.
- Remove exact duplicate quote lines before coding.
- Keep a running count of notes reviewed.

### 1a) Exclude weak signals
- Identify vague or non-specific statements that cannot be defensibly tied to one structural problem.
- Exclude these from coded evidence and track them in an exclusions list with reason.

### 2) First-pass coding
- Label each note with a short provisional root-cause code.
- Avoid feature labels and UI labels.

### 3) Build candidate themes
- Merge related provisional codes into 6 root-cause themes (or nearest defensible number when justified).
- Validate themes are distinct and collectively cover all notes.

### 4) Single-theme assignment
- Map each note to one best-fit theme only.
- If ambiguous, choose strongest fit and note ambiguity in rationale.

### 4a) Consolidate repeated signals
- Cluster near-duplicate quotes that express essentially the same point.
- Keep one representative quote for each repeated cluster in the final table.
- Record cluster strength as deduplicated supporting note count and supporting note IDs.

### 5) Business impact tagging
- Add one concise business impact statement per note.
- Typical impact categories:
  - operational delay or rework
  - financial leakage or recovery loss
  - compliance or risk exposure
  - customer friction or trust erosion
  - adoption resistance or delivery risk

### 6) Data quality audit (required before confidence scoring)
Run all checks:
- Coverage check: 100% of notes reviewed and assigned.
- Exclusivity check: each note assigned to one theme only.
- Distinctness check: no overlapping theme definitions.
- Evidence depth check: each theme has multiple notes unless flagged as emerging.
- Stakeholder spread check: identify single-role vs cross-role signals.
- Contradiction check: identify conflicting evidence and handling.
- Outlier check: preserve one-off signals without over-weighting.
- Misc bucket check: avoid generic miscellaneous themes unless strictly justified.

### 7) Confidence calibration (fixed rubric)
Use a single rubric and apply at the theme level (not per quote):
- High: >= 12 coded notes AND >= 10 unique stakeholders AND >= 5 roles.
- Medium: 7-11 coded notes OR 6-9 unique stakeholders, with >= 4 roles.
- Low: below Medium thresholds or very narrow signal spread.

Provide this rubric as a separate output table/file so confidence logic is explicit and reusable.

### 8) Representative evidence selection
- For each of the 6 themes, select 2-4 representative rows only.
- Ensure selected rows span the range of sub-issues inside the theme.
- If many rows are near-duplicates, keep one clear representative quote and carry the rest into support counts.
- Preserve minority but material signals where they change risk, impact, or implementation implications.

## Output Contract

Return results in this exact order.

### A) Theme summary
For each theme include:
- Theme name
- Underlying structural problem
- Why it matters now
- Evidence volume (coded notes, deduplicated)
- Unique stakeholders
- Unique roles
- Top repeated sub-signal
- Top repeated sub-signal backing count (deduplicated)
- Confidence (High, Medium, Low)

### B) Stakeholder evidence table
Use these columns exactly and return 2-4 rows per theme:
- stakeholder
- stakeholder role
- quote or observation
- theme
- business impact
- confidence level
- sub-signal
- signal backing count (deduplicated)
- supporting note IDs

### C) Confidence rubric
Return a compact rubric table with:
- confidence level
- criteria

### D) Prioritisation hints
For each theme include:
- urgency signal now
- likely consequence if ignored
- implication for discovery framing

### E) Assumptions and limitations
State:
- missing metadata
- interpretation ambiguity
- source data quality concerns

## Quality Bar

The output is only acceptable when:
- every note is reviewed
- every note is assigned once
- themes are root-cause oriented and clearly distinct
- there are 6 themes (or a clearly justified exception)
- each theme has 2-4 representative rows in the final table
- representative rows show range of sub-signals, not only the most repeated signal
- confidence comes from one explicit theme-level rubric
- summary includes note volume, stakeholder spread, and top sub-signal backing counts
- duplicate quote lines are removed before coding
- vague/unclassifiable notes are excluded with reasons
- the table is decision-ready for BA discovery

## Failure Handling

If data is unreadable, incomplete, or malformed:
- state exactly what is broken
- state minimum required fields to proceed
- continue only with clearly labeled provisional analysis when enough evidence exists

## Tone and Guardrails

- concise, analytical, and traceable to evidence
- no invented quotes
- no inflated certainty
- no solutioning beyond evidence synthesis unless requested

## Final Self-Check (silent)

Before final output, verify:
- all notes were read
- symptom themes were avoided
- one-theme-per-note was enforced
- each theme has 2-4 representative rows
- duplicate quote lines were removed
- vague notes were excluded and logged
- sub-signal backing counts and supporting IDs were captured for each representative row
- confidence reflects evidence breadth and consistency
