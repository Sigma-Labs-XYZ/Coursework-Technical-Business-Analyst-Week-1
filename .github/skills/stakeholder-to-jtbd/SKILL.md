---
name: stakeholder-to-jtbd
description: 'Convert stakeholder interview quotes into Jobs to Be Done (JTBD) statements. Use when analyzing stakeholder_interview_notes.csv to build evidence-backed JTBD statements and prioritize them for business impact. Includes full workflow: grouping → evidence table → JTBD writing → prioritization.'
---

# Stakeholder Quotes to JTBD Statements

A guided workflow for converting stakeholder interview insights into actionable JTBD statements backed by evidence.

## When to Use

- You have stakeholder interview notes (CSV or notes) and need to extract Jobs to Be Done
- You're building a discovery brief or roadmap that requires evidence-backed prioritization
- You need to translate stakeholder pain points into user-centric, need-focused statements
- You want to ensure feature decisions are grounded in real stakeholder evidence

## Workflow Overview

This skill guides you through 4 steps:
1. **Group evidence** by theme
2. **Build an evidence table** linking quotes to themes and business impact
3. **Write JTBD statements** using the When/I want to/So that structure
4. **Prioritize and justify** your top 3 JTBDs

---

## Step 1: Group the Evidence by Theme

Read through your stakeholder notes and identify recurring themes. Use these suggested labels as a starting point, but add your own as needed:

- **duplicate work** – effort repeated across teams or systems
- **missed follow-up** – slipped actions, handoff failures
- **poor visibility** – lack of clarity or data access
- **customer friction** – processes that frustrate end users
- **financial credibility** – concerns about recovery, forecasting, or cost
- **change resistance** – skepticism about new tools or processes
- **system fragmentation** – data/processes split across multiple places

**Tip:** Print or export the stakeholder notes and mark each quote with its theme using color or labels.

---

## Step 2: Build an Evidence Table

Create a table that links each stakeholder quote to a theme, business impact, and confidence level.

Use [evidence-table-template.csv](./assets/evidence-table-template.csv) as your starting point, then fill in:

| Column | Description | Example |
|--------|-------------|---------|
| **Stakeholder** | Name or role | Amina Rahman, Compliance Liaison |
| **Quote or observation** | Direct quote from interview | "Customers respond well when they have control and transparency" |
| **Theme** | Grouping label from Step 1 | `customer friction` |
| **Business impact** | What happens if this is NOT solved | "Customers lose faith in recovery process; abandonment risk" |
| **Confidence** | High/Medium/Low based on how many sources mention it | High (mentioned by 5+ roles) |

**Quality check:**
- Does each quote map to exactly one primary theme?
- Did you capture the business impact (not just the symptom)?
- Is your confidence assessment based on frequency of mention?

---

## Step 3: Write JTBD Statements

Use the JTBD template structure:

```
When [situation or context]
I want to [action or capability]
So that [desired outcome or value]
```

### Core JTBD Principles

**1. Focus on Outcomes, Not Requested Features**

The "so that" clause is your outcome—the desired result or value. This is NOT a feature request.

| ❌ Feature-focused | ✅ Outcome-focused |
|---|---|
| "I want a self-service portal" | "I want to resolve my debt without waiting for an agent" |
| "I want email reminders" | "I want to be reminded about my payment at the right time" |
| "I want better reporting" | "I want reliable data so I can forecast recovery revenue accurately" |
| "I want a database that syncs" | "I want to avoid contacting customers twice for the same debt" |

**Why this matters:** Outcomes stay the same even if the solution changes. A portal, SMS, IVR, or call-back service could all achieve the outcome of "resolve debt without an agent." When you focus on the outcome, you're ready to evaluate multiple solutions.

**2. Separate Customer, Agent, Manager, and Finance Perspectives**

The same problem looks different from each vantage point. A customer wants clarity; an agent wants efficiency; a manager wants throughput; finance wants revenue predictability. Write separate JTBDs for each.

**3. Ground in Real Evidence**

Every JTBD must have at least one supporting quote from your stakeholder notes. List the evidence IDs (e.g., SN-001, SN-045).

**4. Job Permanence Test**

Would this job still exist if the entire solution changed? If your JTBD disappears just because you pick a different tool, you've described a feature, not a job.

### Minimum Coverage

Write at least **6 JTBD statements** covering:
- At least 2 from **customer** perspective
- At least 1 from **agent** perspective
- At least 1 from **operations manager** perspective
- At least 1 from **finance partner** perspective
- At least 1 cross-functional or compliance-related perspective

### Example JTBD Statements

| JTBD ID | Actor | Statement | Evidence | Priority | Impact |
|---------|-------|-----------|----------|----------|--------|
| JTBD-001 | **Customer** | When I receive a debt notice, I want to see exactly what I owe, why I owe it, and my payment options, so that I can make an informed decision and take action | SN-001, SN-065, SN-017 | High | Increases engagement & recovery |
| JTBD-002 | **Customer** | When I want to pay my debt, I want to do it on my own timeline without waiting for an agent, so that I can resolve this quickly and move on | SN-005, SN-081, SN-099 | High | Reduces call volume & improves satisfaction |
| JTBD-003 | **Agent** | When I take a customer call, I want to see their complete contact history and all prior commitments, so that I don't repeat questions or break promises | SN-002, SN-011, SN-087 | High | Reduces re-contact; prevents compliance violations |
| JTBD-004 | **Operations Manager** | When a case arrives, I want to instantly classify it as straightforward or complex, so that I can route it efficiently and keep simple cases moving | SN-003, SN-029, SN-039 | High | Improves case resolution time |
| JTBD-005 | **Finance Partner** | When I forecast recovery revenue, I want to trust the activity data and understand what's actually in the pipeline, so that I can provide leadership with realistic projections | SN-026, SN-070, SN-080 | Medium-High | Enables credible financial planning |
| JTBD-006 | **Compliance/Audit** | When I need to prove what happened to a case, I want access to a complete, unified audit trail across all systems, so that I can meet compliance requirements without manual research | SN-008, SN-066, SN-062 | High | Reduces compliance risk & audit cost |

See [jtbd-example.md](./assets/jtbd-example.md) for detailed explanations of each JTBD with business impact assessment.

---

## Step 4: Prioritize by Business Impact & Evidence Strength

From your 6+ JTBD statements, select the top 3 that have:
1. **Highest business impact** – financial loss, compliance risk, revenue opportunity, operational cost savings
2. **Strongest evidence** – mentioned by multiple stakeholder roles, multiple evidence IDs (SN-xxx)

### Prioritization Framework

For each candidate JTBD, score it:

| Criterion | Scoring | Example |
|-----------|---------|---------|
| **Business Impact** | Financial impact in £ or % of recovery | JTBD-001: 5% recovery uplift = £500k/year → Score: High |
| **Evidence Strength** | Number of distinct stakeholder roles mentioning it | JTBD-003: 5 roles (agent, manager, compliance, ops, finance) → Score: High |
| **Frequency** | How many evidence links (SN-xxx) support it? | JTBD-004: 4+ evidence links → Score: High |
| **Blocking Factor** | Does this JTBD block other work or improvements? | JTBD-006: Audit trail blocks compliance approval → Score: High |
| **Urgency** | Time sensitivity (compliance deadline, volume crisis, turnover risk) | JTBD-002: Reducing call volume urgent due to scale crisis → Score: High |

**Scoring guide:**
- Score High: 5+ evidence links, 4+ distinct roles, quantifiable impact > £100k or regulatory risk, or blocks other work
- Score Medium: 3-4 evidence links, 2-3 roles, impact £50-100k, or nice-to-have improvement
- Score Low: 1-2 evidence links, 1 role, impact < £50k, or low urgency

### Justification Template

For your top 3 JTBDs, document:

**Why it matters now:**
- What happens if we don't solve this? (financial loss, compliance violation, team attrition, customer churn)
- Is this blocking other roadmap items?
- What's the time window? (urgency)

**Which evidence supports it:**
- List all supporting quotes: SN-001, SN-045, SN-065
- Which stakeholder roles raised this? (Finance said X, Operations said Y, Compliance said Z)
- Is there consensus or conflict?

**How it should influence Phase 1:**
- What capability or change must happen FIRST to address this JTBD?
- Does this JTBD depend on solving another problem first? (dependencies)
- Is this a quick-win, foundational work, or multi-phase effort?
- How will you measure success? (outcome metrics, not output metrics)

---

## Quality Checklist

Before finalizing your JTBD statements, verify:

- ✓ **Outcome-focused, not feature-focused?**
  - ❌ Bad: "I want a self-service portal"
  - ✅ Good: "I want to resolve my debt without waiting for an agent, so I can move on"
  - ❌ Bad: "I want a better database"
  - ✅ Good: "I want to know instantly if a customer was already contacted, so I don't re-contact them"

- ✓ **Is the "so that" clause the real value, not just a restatement?**
  - ❌ Bad: "...so that I can see their history" (that's the feature, not the outcome)
  - ✅ Good: "...so that I don't repeat questions and I keep my promises" (that's the business value)

- ✓ **Job Permanence Test: Would this job exist if the solution tool changed?**
  - ❌ Bad: "I want email reminders" (disappears if you use SMS instead)
  - ✅ Good: "I want to be reminded at the right time" (still true regardless of channel)
  - ❌ Bad: "I want a portal login" (specific to portals)
  - ✅ Good: "I want control over my account" (portal, SMS, chatbot, or agent could deliver this)

- ✓ **Grounded in real evidence?**
  - ❌ Bad: "Agents need better tools" (no source)
  - ✅ Good: "Agents waste 2+ hours daily proving what they did (SN-027); I want to record work automatically so audits are effortless"

- ✓ **Covered all critical actor perspectives?**
  - Customer (at least 2), Agent, Operations Manager, Finance Partner, plus 1 cross-functional perspective

- ✓ **Is this about the actor's job, or is it about your solution?**
  - ❌ Bad: "I want the recovery team to use our new system"
  - ✅ Good: "I want to resolve cases quickly without hunting for information"

---

## Files in This Skill

- [evidence-table-template.csv](./assets/evidence-table-template.csv) – Start here to build your evidence table
- [jtbd-example.md](./assets/jtbd-example.md) – Complete example JTBD statements with formatting
