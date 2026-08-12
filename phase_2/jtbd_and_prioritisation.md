# JTBD and Prioritisation Template

## Step 1: Group the evidence

[Evidence theme summary](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=95382498#gid=95382498)

Theme confidence was calculated based on a [confidence rubric](confidence_rubric.csv) and the confidence of each individual stakeholder quote was determined by the theme confidence.

## Step 2: Build an evidence table

[Stakeholder evidence table](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1879132607#gid=1879132607)

This table captures representative stakeholder quotes mapped to each theme, with role, sub-signal, impact, confidence, and supporting note IDs.
Exact duplicates and vague/non-specific notes were excluded before final coding; see [Excluded notes](excluded_notes.csv).

## Step 3: Write JTBD statements

JTBD-01
When I need to understand an account's full recovery history across channels, I want one trusted record of status, actions, and ownership so that I can progress cases quickly and defend compliance decisions.

JTBD-02
When I manage follow-up commitments, I want callback dates, handoffs, and next actions enforced in workflow so that no recoverable case stalls or drops between shifts.

JTBD-03
When I review debt recovery performance, I want consistent activity and status data I can trust so that I can forecast accurately and make defensible governance decisions.

JTBD-04
When I need to resolve my debt, I want clear case status, balance information, and next-step options across self-serve and assisted paths so that I can complete resolution without repeated contact.

JTBD-05
When I triage a case, I want clear distinction between straightforward and vulnerable or high-risk situations so that I can route cases safely and apply the right level of specialist support.

JTBD-06
When new recovery processes are introduced, I want clear operational foundations, role clarity, and evidence of benefit so that teams adopt the change consistently and sustained improvements are realized.

JTBD-07
When I lead a collections team through operational change, I want clear sponsorship, escalation paths, and role expectations so that my team can adopt new workflows consistently without losing performance.

## JTBD table

[JTBD table](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1397865542#gid=1397865542)

### How portal relevance and priority were set

Portal relevance rubric:
- High: direct impact on portal-enabled outcomes (case visibility, contact flow, self-serve resolution, workflow enforcement).
- Medium: indirect/enabling impact (for example reporting trust or adoption readiness).

Priority rubric:
- Inputs: repeat backing count + theme confidence from theme_summary.csv, plus business impact/risk from stakeholder_evidence_table.csv.
- Frequency of evidence mapping (from evidence count): High = 8 or more SN tags, Medium = 5-7 SN tags, Low = 1-4 SN tags.
- High: strong repeated signal and confidence, with immediate operational, recovery, or compliance impact.
- Medium: meaningful impact, but lower urgency, narrower scope, or lower evidence strength than high items.
- Tie-break rule: for top-priority ties, rank portal relevance before evidence count. If portal relevance is equal, then rank by evidence count (deduplicated SN tags) in descending order.

## Step 4: Top 3 justification

Top 3 unmet jobs were selected from the [JTBD table](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1397865542#gid=1397865542) based on strongest combined ranking across frequency of evidence, business impact, and relevance to the portal.

### JTBD-01: single trusted account history
- Why it matters now: Agents spend material time reconstructing case history, slowing throughput and weakening compliance defensibility.
- Evidence: High-frequency signal from SN-008; SN-010; SN-015; SN-025; SN-027; SN-062; SN-066; SN-087; SN-096.
- Influence on Phase 1 scope: Prioritise a unified case timeline and status history as a core foundation capability.

### JTBD-02: enforced follow-up workflow
- Why it matters now: Missed or delayed follow-ups directly reduce recoveries and create avoidable leakage.
- Evidence: High-frequency signal from SN-007; SN-011; SN-040; SN-045; SN-049; SN-053; SN-067; SN-118.
- Influence on Phase 1 scope: Include callback-date control, ownership handoff rules, and exception alerts in the first release scope.

### JTBD-04: clear customer resolution journey
- Why it matters now: Repeat customer contact and unclear next steps increase friction, rework, and time-to-resolution.
- Evidence: Medium-frequency signal from SN-001; SN-002; SN-017; SN-028; SN-036; SN-047; SN-065.
- Influence on Phase 1 scope: Prioritise clear customer case visibility, next-step guidance, and clean self-serve-to-agent routing.

## Quality check

Ask yourself:
- Does this describe a need instead of a feature?
- Would the job still exist if the screen or tool changed?
- Can I point to real evidence behind the priority?
