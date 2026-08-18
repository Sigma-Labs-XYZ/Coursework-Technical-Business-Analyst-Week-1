# Example JTBD Statements (Six Complete Examples)

This document shows realistic JTBD statements derived from your stakeholder notes. Each example:
- Separates customer, agent, manager, and finance perspectives
- Focuses on **outcomes, not features** (notice the "so that" clauses)
- Grounds in real stakeholder evidence with multiple sources
- Includes prioritization scoring

---

## JTBD-001: Customer – Account Transparency

| Field | Value |
|-------|-------|
| **Actor** | Customer with delinquent account |
| **JTBD Statement** | **When** I receive a debt recovery notice, **I want to** understand exactly what I owe, why, and my payment options, **so that** I can make an informed decision and take action (or know I can't) |
| **Why this is outcome-focused** | Not "I want a portal" or "I want an email" – the outcome is *understanding and agency*. Portal, SMS, letter, or call could deliver this. |
| **Evidence links** | SN-001, SN-065, SN-017 (4+ roles mention transparency barriers) |
| **Business impact** | Improves engagement rate; increases recovery rate; reduces "don't understand" complaints |
| **Priority Score** | **High** (5+ evidence, 4 roles: customer, ops, compliance, finance) |

---

## JTBD-002: Customer – Self-Service Access

| Field | Value |
|-------|-------|
| **Actor** | Customer who wants to resolve debt independently |
| **JTBD Statement** | **When** I want to pay my debt, **I want to** do it on my own schedule without waiting for an agent, **so that** I can resolve this quickly and stop worrying about it |
| **Why this is outcome-focused** | Not "I want a self-service portal" – the outcome is *autonomy and speed*. Could be portal, SMS payment link, IVR, or agent callback. |
| **Evidence links** | SN-005 (customers will do anything if given chance), SN-081 (portal works because it gives control), SN-099 (40% of customers want self-resolution) |
| **Business impact** | Reduces agent workload by ~40%; increases satisfaction for independent customers; frees capacity for complex cases |
| **Priority Score** | **High** (4+ evidence, 3 roles: customer, ops, finance) |

---

## JTBD-003: Agent – Complete Context Access

| Field | Value |
|-------|-------|
| **Actor** | Collections agent (inbound/outbound) |
| **JTBD Statement** | **When** I take a customer call, **I want to** instantly see their full history—prior contact, promises made, payment attempts, current status—**so that** I don't repeat questions and I keep promises I make |
| **Why this is outcome-focused** | Not "I want a better database" or "I want the systems to sync" – the outcome is *accuracy and trustworthiness*. The underlying data sync is the enabler, not the job. |
| **Evidence links** | SN-002 (customers call 3x; don't remember first call), SN-011 (agents re-contact due to sync failures), SN-028 (customers re-contact because we re-contact them), SN-087 (agents waste time hunting info) |
| **Business impact** | Prevents duplicate contact (regulatory risk + wasted time); improves customer satisfaction; reduces re-contact rate by ~50% |
| **Priority Score** | **High** (5+ evidence, 5 roles: agent, operations, customer, compliance, finance) |

---

## JTBD-004: Operations Manager – Intelligent Case Routing

| Field | Value |
|-------|-------|
| **Actor** | Operations manager or supervisor |
| **JTBD Statement** | **When** a case arrives, **I want to** instantly know whether it's straightforward or requires specialist handling, **so that** I can route it efficiently and prevent simple cases from getting stuck behind complex ones |
| **Why this is outcome-focused** | Not "I want a classification system" – the outcome is *throughput and efficiency*. Could be algorithmic classification, manual triage tool, or AI scoring. |
| **Evidence links** | SN-003 (simple cases stuck for days in wrong queue), SN-029 (straightforward cases delayed behind complex), SN-039 (no way to identify straightforward), SN-057 (complex and simple mixed in same queue) |
| **Business impact** | Improves case resolution time for 60% of cases by 40%+; reduces queue complexity; enables tiered routing strategy |
| **Priority Score** | **High** (4+ evidence, 4 roles: ops, customer, agent, finance) |

---

## JTBD-005: Finance – Revenue Forecasting Credibility

| Field | Value |
|-------|-------|
| **Actor** | Finance partner/forecaster |
| **JTBD Statement** | **When** I forecast recovery revenue for leadership, **I want to** trust that the activity data is complete and accurate, so I understand what's actually in the pipeline, **so that** I can provide realistic projections and measure improvement |
| **Why this is outcome-focused** | Not "I want better reporting" or "I want a data warehouse" – the outcome is *credibility and measurable improvement*. Data infrastructure is the enabler. |
| **Evidence links** | SN-026 (never measured how often cases come back), SN-070 (finance doesn't trust activity data), SN-048 (reporting takes too long; data is stale), SN-080 (no visibility into pipeline or case duration) |
| **Business impact** | Enables accurate ROI modeling for improvements; builds leadership confidence; unlocks ability to measure self-service impact |
| **Priority Score** | **Medium-High** (4 evidence, 2 roles: finance + ops; high urgency due to roadmap business case needs) |

---

## JTBD-006: Compliance/Audit – Unified Audit Trail

| Field | Value |
|-------|-------|
| **Actor** | Compliance analyst or auditor |
| **JTBD Statement** | **When** I need to demonstrate what happened to a case or prove we followed regulations, **I want to** access a complete, unified audit trail across all systems in one place, **so that** I can respond to audits quickly and without manual data hunting |
| **Why this is outcome-focused** | Not "I want a centralized database" – the outcome is *compliance confidence and audit efficiency*. Could be achieved through API aggregation, data lake, or system consolidation. |
| **Evidence links** | SN-008 (audit trail scattered; makes compliance reviews a nightmare), SN-066 (audit trails across multiple systems make it nearly impossible), SN-062 (each new tool adds another place data gets out of sync), SN-015 (same case shows different status in different systems) |
| **Business impact** | Eliminates manual audit preparation; reduces compliance risk and audit costs; enables process quality measurement |
| **Priority Score** | **High** (4+ evidence, 3 roles: compliance, audit, ops; regulatory blocking factor: audit trail gaps = compliance risk) |

---

## Prioritization Summary

| JTBD | Actor | Priority | Impact | Evidence | Decision |
|------|-------|----------|--------|----------|----------|
| JTBD-001 | Customer | High | ~5% recovery uplift | 5 roles, 3+ quotes | **Top 3** – immediate impact on recovery |
| JTBD-002 | Customer | High | ~40% agent capacity freed | 3 roles, 3+ quotes | **Top 3** – enables self-service roadmap |
| JTBD-003 | Agent | High | ~50% re-contact reduction | 5 roles, 5+ quotes | **Top 3** – highest evidence; compliance risk |
| JTBD-004 | Ops | High | ~40% faster case resolution | 4 roles, 4+ quotes | High priority; Phase 2 (depends on data cleanup) |
| JTBD-005 | Finance | Medium-High | Enables credible ROI modeling | 2 roles, 4 quotes | Medium (foundational for business case validation) |
| JTBD-006 | Compliance | High | Audit efficiency + risk reduction | 3 roles, 4+ quotes | High (blocking approval); Phase 1 parallel track |

---

## What Makes These Outcomes, Not Features?

Notice what's **NOT** in these JTBDs:
- "I want a self-service portal" ← This is a feature. ✅ We have: "I want autonomy" (outcome; portal is one solution)
- "I want better reporting" ← This is a feature. ✅ We have: "I want to trust the data" (outcome; reporting is one solution)
- "I want a database sync" ← This is a feature. ✅ We have: "I want to keep promises and avoid re-contact" (outcome; sync is one enabler)
- "I want email reminders" ← This is a feature. ✅ Better: "I want to be contacted at the right time" (outcome; channel is flexible)

The **"so that" clause is your outcome.** If it disappears when you change tools, you're describing the feature, not the job.

---

## How to Use This Template

1. **Copy the JTBD structure** for each of your statements – include the "Why this is outcome-focused" row to force yourself to think about solutions separately
2. **Map evidence carefully** – link every JTBD to 3+ quotes with multiple roles represented
3. **Score prioritization** – use the priority score table above: count evidence, count roles, assess business impact
4. **Justify your top 3** – write the full case (why it matters now, who supports it, how it influences Phase 1) for your top 3 only
5. **Test for outcome-focus** – for each JTBD, ask: "Would this job still exist if we changed the solution tool?" If no, rewrite the "so that"
