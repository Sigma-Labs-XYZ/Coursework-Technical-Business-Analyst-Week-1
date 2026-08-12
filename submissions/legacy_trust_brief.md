## 1. Problem summary

Legacy Trust's debt recovery process is struggling to manage over 100,000 delinquent accounts across more than 50 agents. Agents rely on a 20-year-old collections database alongside spreadsheets, emails and individual workarounds to manage cases and follow-ups. This requires information to be manually checked and updated across different sources, leading to missed follow-ups, duplicate contact and inconsistent case statuses. The process is failing at scale because both straightforward and complex cases require significant agent involvement, despite around 38% of cases potentially being suitable for self-service. This wastes agent capacity, delays recovery activity and makes it difficult for leadership to accurately measure performance and lost revenue.

## 2. Stakeholder overview

| Stakeholder group | What they care about | How success is measured | Main worry | Evidence they will trust |
|---|---|---|---|---|
| Operations leadership | Where missed follow-ups (20% lost at shift handoff), duplicate contact, and wasted agent time occur | Process maps showing failure points; evidence of agent time savings; follow-up completion rate improvement | Assuming all cases can be automated when some require human judgement; that efficiency gains are real, not theoretical | Baseline handling times; missed follow-up audit; duplicate contact rate; agent time allocation data |
| Team leaders and agents | The As-Is process reflecting actual agent work with clear boundaries between automated and agent-led work; reduced manual work | Time spent hunting for information reduced; clear routing rules so cases don't get mixed in queues; acknowledgement of prior system issues | Complex cases pushed back onto agents without context; job security fears from automation; change fatigue from prior system update | Agent feedback from ride-alongs; realistic workflows; transparent handoff rules; escalation criteria |
| Finance | Measurable savings and improved recovery performance with transparent assumptions | ROI model with conservative/optimistic cases; proof agent time savings are real (not theoretical); credible recovery uplift | Financial benefits based on weak assumptions; shift of cost from operations to lost recovery; 15% loss needs breakdown | Transparent assumptions; sensitivity testing; baseline recovery rates; agent cost; reconciliation of activity data |
| Product and delivery | Discovery outputs realistic and usable for buildable requirements; full traceability from pain point to feature | Pain points and opportunities traceable to Phase 1 scope; process details captured; edge cases documented | Recommendations too vague to build; insufficient discovery detail; scope creep from unclear boundaries | Traceability matrix; documented process map; requirements linked to failures; clear Phase 1 scope |
| Customers | Straightforward path for suitable cases; transparent communication about what they owe; access to human support when needed | Completion rates for self-service; escalation rates; reduced repeat contacts; improved payment plan uptake | Self-service not meeting their circumstances; lack of awareness about digital options; dispute handling | Customer segmentation data; feature preference research; escalation/complaint rates; awareness audit |

## 3. Discovery questions

- Which debt-recovery cases are straightforward and rules-driven enough to be safely moved to self-service?
- Where do spreadsheets, emails and manual handoffs create the most duplicate work or missed follow-ups?
- How much agent time is currently spent searching for, reconciling and updating information across different sources?
- Why do cases remain in statuses such as pending callback without further action being taken?
- How can straightforward cases be separated from complex, vulnerable or specialist cases that require agent judgement?
- What are the current baseline measures for handling time, follow-up completion and recovery performance?
- What financial and operational improvement would Phase 1 need to demonstrate for leadership to consider it successful?

## 4. Traceability starter

| Priority JTBD | Stakeholder evidence (from interview notes) | Likely process area affected | Possible metric or evidence source | Likely later deliverables |
|---|---|---|---|---|
| JTBD-01: Clear balance and repayment options | SN-065, SN-002, SN-028, SN-036, SN-047 | Customer communication clarity and self-service guidance | Repeat contact rate; payment plan uptake; self-service completion rate; complaint rate on unclear balances | Customer-facing balance and options flow; content and communication standards; self-service journey map |
| JTBD-04: Clear and consistent customer guidance | SN-002, SN-028, SN-036, SN-047 | Contact guidance and next-step consistency | Repeat contact volume; first-contact resolution proxy; avoidable re-contact audit | Standardised guidance model; decision-tree content for customer journeys; handoff communication standards |
| JTBD-07: Complete and traceable audit trail | SN-008, SN-066, SN-060, SN-111, SN-047 | Audit trail integrity, compliance controls, and evidence capture | Audit evidence completeness rate; manual re-keying rate; compliance approval cycle time | Audit-trail requirements specification; compliance control points in To-Be process; case-history data model |

Priority rationale:
- These JTBDs are currently highest under the equally weighted model in [jtbd-statements](jtbd-statements.md): JTBD-01 (8), JTBD-04 (8), JTBD-07 (8).
- Each has broad independent stakeholder evidence and clear links to Phase 1 deliverables.

## 5. Final problem statement

Legacy Trust's debt recovery process relies on outdated systems, spreadsheets and manual workarounds to manage over 100,000 delinquent accounts across 50+ agents. This makes it difficult to consistently track case status, ownership and follow-ups, resulting in missed actions, duplicate effort and wasted agent capacity. Straightforward and complex cases also follow the same manual processes, limiting agents' ability to focus their time on cases that require human judgement. These inefficiencies are contributing to delayed recoveries and an estimated 15% revenue loss.
