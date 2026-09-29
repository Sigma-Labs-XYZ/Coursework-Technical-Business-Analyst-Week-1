---
name: analyze-csv-as-business-analyst
description: 'Analyze CSVs from a business analyst perspective: profile key metrics, assess data quality, extract evidence-backed findings, and link insights to business problems. Use when summarizing delinquent_accounts_export.csv, finance_assumptions.csv, recovery_activity_tracker.csv, smart_recovery_portal_events.csv, or stakeholder_interview_notes.csv. Produces: key points, critical evidence, business impact assessment.'
argument-hint: 'CSV filename or "all five datasets"'
---

# Analyze CSVs as a Business Analyst

A structured workflow to analyze operational data and extract evidence-backed business insights.

## When to Use

- You need to summarize findings from operational CSVs for a discovery brief, business case, or roadmap
- You want to identify what the data confirms (or contradicts) about stakeholder concerns
- You need to ground business impact claims in actual data evidence
- You're building an ROI model or identifying quick-win opportunities

## Key Principle

**Every finding must be grounded in data.** Not "Agents are busy" but "Agents spend avg 7.2 min per activity + 34% duplicate checks = 9.7 min effective per activity."

---

## Step 1: Profile the Dataset

For each CSV, document the fundamentals:

| Element | What to look for | Why it matters |
|---------|------------------|----------------|
| **Volume** | Row count, date range, coverage period | Is this a representative sample? |
| **Granularity** | What does each row represent? (account, activity, event?) | Can you aggregate/segment the data? |
| **Time range** | Earliest and latest date in the data | Is this recent? Does it cover seasonal patterns? |
| **Key columns** | The 3-5 most important fields for business analysis | What can you actually measure/compare? |
| **Coverage gaps** | Missing values, empty fields | How much data can you trust? |

### Example Profiling Questions

**For delinquent_accounts_export.csv:**
- How many accounts? What's the date range? (volume & recency)
- What delinquency stages are present? (risk distribution)
- Which accounts have self_service_candidate = Y vs N? (segmentation for portal roadmap)
- How many accounts have missing email or mobile? (limiting factor for outreach channels)

**For recovery_activity_tracker.csv:**
- How many activities total? Average per account? (activity density)
- What activity types dominate? (process insight)
- Date range vs account creation dates (is tracking complete?)
- How many duplicate_check_flag = Y? (process inefficiency measure)

**For smart_recovery_portal_events.csv:**
- How many portal journeys? Completion rate? (adoption metric)
- Which event steps have failures or low progression? (UX issue identification)
- Time between events (are there drop-offs at specific steps?)
- What's the ineligibility rate? (process design feedback)

---

## Step 2: Assess Data Quality & Consistency

Identify issues that affect your findings' credibility:

| Quality Issue | What to check | Business implication |
|---------------|---------------|----------------------|
| **Missing data** | Null/blank/empty cells per column | Can you trust aggregations? Are certain customer segments underrepresented? |
| **Date inconsistencies** | Format differences (2026-01-01 vs 01/01/2026), future dates | Will your analysis require data cleaning? |
| **Duplicates** | Same activity_id or account_id appearing multiple times | Are you double-counting? |
| **Outliers** | Unusual values (e.g., 999 minutes per activity) | Data entry error or rare legitimate case? |
| **Cross-reference issues** | Do account_ids in activity log match delinquent_accounts? | Is there data leakage or misalignment? |

**Document findings as:**
- ✓ **Data Quality Score: [High/Medium/Low]** – [reason]
- **Key clean-up needed:** [specific steps if any]

---

## Step 3: Extract Key Findings (Metrics + Evidence)

For each CSV, identify 3-5 key findings following this format:

```
**Finding:** [Business insight statement]
**Evidence:** [Specific number, percentage, count, or example]
  - Data: [Value from CSV with column source]
  - Sample: [1-2 concrete examples with row references]
**Business impact:** [What this means for the problem we're solving]
**Confidence:** [High/Medium/Low based on sample size and data quality]
```

### Finding Types (Choose relevant ones)

**Volume & Scale:**
- "X accounts in [stage] across Y date range, representing £Z total value"
- Evidence: Count of rows + SUM of balances + date range

**Segmentation & Targeting:**
- "X% of accounts are [trait], Y% are [other trait]"
- Evidence: COUNT WHERE criteria / TOTAL COUNT

**Efficiency/Friction Points:**
- "Activities on same account average X per month; Y% have duplicate checks flagged"
- Evidence: Activity count per account (avg/median) + COUNT WHERE duplicate_check_flag=Y

**Channel Adoption:**
- "X% of customers accessed portal, Y% completed journey, Z% had ineligibility reasons"
- Evidence: COUNT DISTINCT journeys / total accounts invited, completion rates per step

**Cost/Time Drivers:**
- "Average time per activity is X minutes; straightforward cases estimated at Y minutes"
- Evidence: AVG(minutes_spent) from activity tracker + assumptions from finance_assumptions.csv

**Risk Concentration:**
- "X% of balance is in Y accounts with risk_flag=Z; concentrated in [segment]"
- Evidence: SUM WHERE risk_flag / TOTAL balance, top 10 account analysis

---

## Step 4: Cross-Reference with Stakeholder Evidence

Link your data findings to stakeholder concerns from stakeholder_interview_notes.csv:

| Stakeholder Concern | Data Evidence | Match? | Notes |
|-------------------|----------------|--------|-------|
| "Agents re-contact customers unnecessarily" | duplicate_check_flag=Y rate in recovery_activity_tracker | ✓ Confirmed: X% flagged | This directly validates agent frustration about system fragmentation |
| "Portal doesn't work for self-service" | ineligibility_result=ineligible rate in portal_events | ? Partial: Y% marked ineligible; need to understand *why* | Suggests process design, not portal capability, is limiting factor |
| "We can't track cases between systems" | Missing field rates in recovery_activity_tracker.csv | ? Suspected: Z% of rows missing next_follow_up_date | Data isolation issue confirmed; can't reliably trace handoffs |

**Why this matters:** You're proving or disproving what stakeholders said by showing actual data patterns.

---

## Step 5: Summarize What the CSV Shows (Business Analyst Summary)

For each CSV, write a 2-3 sentence business summary answering:
- **What is this dataset telling us about the business problem?**
- **What capability gap or opportunity does it reveal?**
- **Which stakeholder concerns does it validate or contradict?**

### Example Summaries

**delinquent_accounts_export.csv:**
"We have [X] accounts across [stages], with [Y]% self-service candidates available but [Z]% missing contact channels (email/mobile). Risk is concentrated in [segment], representing [£amount]. The data shows we have capacity for agent-light strategies, but contact channel gaps and risk flags reveal why current agent-led approach is under stress."

**recovery_activity_tracker.csv:**
"Average [X] activities per account over [timeframe], with [Y]% activities flagged for duplicate checking. Activity type distribution reveals [Z]% are manual_plan_notes and status_checks—high-touch admin work. Time-per-activity averaging [W] minutes suggests process overhead (system hunting, manual reconciliation) not core contact work. High duplicate rates confirm stakeholder frustration about system fragmentation."

**smart_recovery_portal_events.csv:**
"[X] portal journeys initiated via [channels]; [Y]% complete flow end-to-end. Ineligibility rate is [Z]%; highest drop-off occurs at [step]. Data suggests portal capability works for those who reach it, but eligibility gatekeeping and multi-channel outreach limitations explain low adoption vs [percentage] of self-service candidates."

---

## Step 6: Prioritize Findings by Evidence Strength

Rank your findings by credibility using this framework:

| Confidence Level | Criteria | Example |
|------------------|----------|---------|
| **High** | 100+ observations, <5% missing data, clear pattern, validated across multiple CSVs | "38% of straightforward-stage accounts accessed portal" (from both accounts export AND portal events data) |
| **Medium** | 20-100 observations, <15% missing data, single-source validation, qualifies with caveats | "Average 7.2 min per activity" (from activity tracker alone; sample size 2,000+ but time field may be incomplete) |
| **Low** | <20 observations, >15% missing data, unsourced, contradicts other data | "Duplicate rate suggests X problem" (only 5 duplicates in 1,000 rows; pattern unclear) |

**Report only High + Medium confidence findings in your summary.**

---

## Step 7: Business Impact Assessment

For each key finding, document the impact:

| Impact Dimension | Questions | Example |
|------------------|-----------|---------|
| **Financial** | Does this affect revenue, cost, or recovery rate? By how much? | Finding: 34% duplicate activities → Impact: ~£450k wasted agent time/year at £22/hr |
| **Operational** | Does this affect throughput, quality, or scale capacity? | Finding: Avg 9.7 min effective per activity (7.2 base + 2.5 duplicate check) → Impact: Can't scale to 100K+ accounts with current staffing |
| **Customer** | Does this affect satisfaction, friction, or outcomes? | Finding: 40% portal-ineligible despite self-service candidates → Impact: Frustration; forced agent contact increases handling time |
| **Compliance** | Does this affect audit trails, data consistency, or regulatory risk? | Finding: next_follow_up_date missing in 22% of activities → Impact: Can't enforce promised callbacks; FCA compliance risk |

---

## Quality Checklist for Your Summary

Before finalizing, verify:

- ✓ **Every key point has a number attached** (not "many" or "most"; say "67%")
- ✓ **Every finding cites the CSV and specific column/range** (not just "the data shows")
- ✓ **Findings are grounded in data, not interpretation** 
  - ❌ Bad: "Agents are too busy and unhappy"
  - ✅ Good: "Agents log 7.2 min/activity + 34% duplicate checks = 9.7 effective min. At 21 workdays × 8 hrs/day, max throughput is 109 cases/month/agent, below our 120 target."
- ✓ **Stakeholder concerns are validated or contradicted by specific evidence**
- ✓ **Business impact is quantified** (£cost, % efficiency gain, compliance risk)
- ✓ **Confidence levels are assigned** (High/Medium/Low with reasons)

---

## Files & References

Use [analysis-template.csv](./assets/analysis-template.csv) to structure your findings in a table format you can export.

See [example-summary.md](./assets/example-summary.md) for a complete worked example of CSV analysis with all 5 datasets.
