# Jobs-to-be-Done (JTBD) Statements From Stakeholder Evidence

This document contains evidence-grounded JTBD statements generated from stakeholder interview notes.

## JTBD Set

| JTBD ID | Mapped theme | Primary actor | Underlying need | JTBD statement | Source quote or observation | Assumptions or uncertainties |
|---|---|---|---|---|---|---|
| JTBD-01 | customer friction | Customer | Clear balance and repayment options | When I am trying to resolve overdue debt, I want to clearly understand what I owe and what options I have, so that I can act quickly and make a payment I can commit to. | Dr Lynda Smith (Operations Analyst): [SN-065](../docs/stakeholder_interview_notes.csv#L66) | Customer need is inferred from operational observation, not a direct customer quote. |
| JTBD-02 | duplicated work | Collections agent | Reliable record of prior contact actions | When I pick up a case, I want to see whether contact already happened and what was agreed, so that I do not repeat work or give conflicting messages. | Christopher Richards (Collections Agent): [SN-011](../docs/stakeholder_interview_notes.csv#L12) | Assumes contact duplication is mainly caused by disconnected systems; validate with system audit. |
| JTBD-03 | poor account-status visibility | Operations manager | Consistent case status definitions across teams | When I review case progress across teams, I want each status to mean the same thing everywhere, so that I can make reliable decisions and avoid misrouting work. | Jacqueline Norris (Operations Analyst): [SN-085](../docs/stakeholder_interview_notes.csv#L86), Dr Louis Sinclair (Service Design Lead): [SN-122](../docs/stakeholder_interview_notes.csv#L123) | Primary actor set to operations manager based on decision accountability; source quotes come from analyst/design roles. |
| JTBD-04 | customer friction | Finance partner | Confidence in customer communication outcomes | When I review recovery operations, I want confidence that customers receive clear and consistent guidance, so that repeat contact demand and avoidable cost are reduced. | Daniel Okoye (Finance Business Partner): [SN-002](../docs/stakeholder_interview_notes.csv#L3) | Outcome links to cost reduction are reasonable but not quantified in this quote. |
| JTBD-05 | low confidence in reporting and forecasting | Finance analyst | Trustworthy and timely data for forecasting | When I forecast recovery revenue, I want activity data that is current and reliable, so that plans and financial commitments are credible. | Daniel Farmer (Finance Analyst): [SN-070](../docs/stakeholder_interview_notes.csv#L71), [SN-048](../docs/stakeholder_interview_notes.csv#L49) | Supported by two quotes from same stakeholder; validate with additional finance stakeholders if needed. |
| JTBD-06 | delayed or missed followup | Operations team lead | Owned and enforced follow-up handoffs | When a follow-up moves across shifts, I want clear ownership and enforced callback dates, so that cases do not stall and recovery opportunities are not lost. | Catherine Frost (Data Analyst): [SN-040](../docs/stakeholder_interview_notes.csv#L41), Lawrence Bennett (Finance Analyst): [SN-007](../docs/stakeholder_interview_notes.csv#L8) | Actor generalised to team lead based on cross-role evidence. |
| JTBD-07 | compliance and audit trail gaps | Compliance officer | Complete and traceable case history | When I review a case for compliance, I want one complete and traceable audit trail of contacts and status changes, so that I can evidence decisions and approve process changes safely. | Andrea Hunt (Operations Manager): [SN-008](../docs/stakeholder_interview_notes.csv#L9), Jacqueline Norris (Operations Analyst): [SN-066](../docs/stakeholder_interview_notes.csv#L67) | Assumes a single evidence trail is feasible in the target process; validate control design constraints. |

## Coverage Check

- customer friction: JTBD-01, JTBD-04
- duplicated work: JTBD-02
- poor account-status visibility: JTBD-03
- low confidence in reporting and forecasting: JTBD-05
- delayed or missed followup: JTBD-06
- compliance and audit trail gaps: JTBD-07

- Customer actor: JTBD-01
- Agent actor: JTBD-02
- Operations manager actor: JTBD-03
- Finance partner actor: JTBD-04
- Additional actors: Finance analyst (JTBD-05), Operations team lead (JTBD-06), Compliance officer (JTBD-07)

## Independent Evidence Count Per JTBD

Counting method used:
- Scope: all relevant notes in the mapped theme from [docs/stakeholder-evidence-tables.md](../docs/stakeholder-evidence-tables.md).
- Independent evidence: unique stakeholder names only (strict exact-name matching).
- Repeated mentions by the same stakeholder increase note count, but not independent evidence count.
- Blank stakeholder names are treated as separate unknown records by note ID.

Frequency rating methodology:
- Rating is based on independent stakeholder count (not raw mentions).
- High: 5 or more independent stakeholders.
- Medium: 3 to 4 independent stakeholders.
- Low: 1 to 2 independent stakeholders.

Business impact rating methodology:
- High: directly affects revenue/recoveries, significant costs, compliance/risk, or ability to operate effectively.
- Medium: causes meaningful wasted time, inefficiency, delays, or customer problems, but does not have a strong/direct link to major business outcomes.
- Low: mostly inconvenience or minor friction, with limited effect on cost, revenue, risk, or performance.

Portal implementation relevance methodology:
- High: the portal would directly address the JTBD through its core functionality.
- Medium: the portal would partially support the JTBD, but other systems/process changes would also be needed.
- Low: the JTBD is mostly outside the portal's scope and would need a different solution.

Equally weighted prioritisation scoring system:
- Purpose: identify the most important JTBDs using a consistent, simple scoring approach.
- Inputs used (equal weight): Frequency rating, Business impact rating, Portal implementation relevance.
- Score conversion: High = 3, Medium = 2, Low = 1.
- Total priority score: Frequency score + Business impact score + Portal relevance score.
- Maximum possible score: 9.

| JTBD ID | Mapped theme | Independent stakeholders (count) | Frequency rating | Business impact rating | Portal implementation relevance | Total priority score (max 9) |
|---|---|---:|---|---|---|---:|
| JTBD-01 | customer friction | 4 | Medium | High | High | 8 |
| JTBD-02 | duplicated work | 5 | High | Medium | Medium | 7 |
| JTBD-03 | poor account-status visibility | 7 | High | Medium | Medium | 7 |
| JTBD-04 | customer friction | 4 | Medium | High | High | 8 |
| JTBD-05 | low confidence in reporting and forecasting | 4 | Medium | High | Low | 6 |
| JTBD-06 | delayed or missed followup | 4 | Medium | High | Medium | 7 |
| JTBD-07 | compliance and audit trail gaps | 5 | High | High | Medium | 8 |

Interpretation note:
- JTBD-01 – Clear balance and repayment options (Score: 8/9)
This job matters because unclear balances and repayment options create friction for customers trying to resolve their debt and may delay recovery. It is supported by evidence from 4 independent stakeholders, including SN-065, which identifies customer difficulty in understanding balances and repayment options. For Phase 1, this could prioritise functionality that allows customers to view their outstanding balance and understand available repayment options.

- JTBD-04 – Clear and consistent customer guidance — 8/9
This job matters because unclear or inconsistent guidance can drive repeat customer contact, increasing handling time and operational costs. It is supported by evidence from 4 independent stakeholders, including SN-002, which links customer communication issues to repeat contact and avoidable cost. For Phase 1, this could prioritise clear, standardised guidance that allows customers to understand and complete their next steps without contacting an agent.

- JTBD-07 – Complete and traceable audit trail — 8/9
This job matters because incomplete case histories make it difficult to evidence decisions and create compliance and governance risk. It is supported by evidence from 5 independent stakeholders, including SN-008 and SN-066, which highlight the need for greater traceability in recovery activity. For Phase 1, this could require customer interactions and status changes made through the portal to be consistently recorded and traceable.