---
name: build-roi-model-for-debt-recovery
description: 'Build an evidence-based ROI model for debt recovery improvement initiatives. Use when you have discovery data (stakeholder concerns, CSVs) and need to quantify business impact, prioritize opportunities, and make Phase 1 recommendations. Workflow: extract baseline metrics from CSVs → populate assumptions → evaluate opportunities → calculate ROI → rank & recommend. Produces: filled ROI model CSVs and prioritized roadmap.'
argument-hint: 'phase focus (e.g., "Phase 1 self-service") or "full model"'
---

# Build ROI Model for Debt Recovery Initiatives

A 6-step workflow for building an evidence-based ROI model grounded in operational data and stakeholder insights.

## When to Use

- You've completed discovery (stakeholder interviews, data analysis) and need to quantify business impact
- You're deciding which opportunities to prioritize in Phase 1
- You need to justify implementation costs and effort to finance/leadership
- You want to test assumptions and understand business case sensitivity

## Core Modelling Principles

**Golden Rule:** Always separate observed data from assumptions from formulas from recommendation logic. Never mix layers.

```
Data Layer      → Extracted from operational CSVs (observed, not assumed)
Assumption Layer → Estimated or derived values (justify source & confidence)
Formula Layer   → Calculations that convert assumptions into metrics
Recommendation → Business decision based on ROI, payback, effort
```

---

## Step 1: Document Baseline Metrics

Extract current state metrics from your operational CSVs. These are **observed**, not assumed.

### What to Extract

Use [02-baseline-metrics.csv](../templates/roi-model/02-baseline-metrics.csv) and populate:

| Metric | Data Source CSV | How to Extract | Example |
|--------|-----------------|-----------------|---------|
| **B-01: Total delinquent accounts** | delinquent_accounts_export.csv | COUNT of rows | 9,999 accounts |
| **B-02: Straightforward case volume/month** | delinquent_accounts_export.csv + recovery_activity_tracker.csv | COUNT WHERE delinquency_stage='early' ÷ months in data | 4,120 early-stage / 5 weeks = ~3,540/month |
| **B-03: Avg handling time per case** | recovery_activity_tracker.csv + finance_assumptions.csv | AVG(minutes_spent) grouped by activity_type | 7.2 min (observed); 18 min assumed in finance_assumptions |
| **B-04: Admin hours lost to reconciliation** | recovery_activity_tracker.csv | COUNT WHERE activity_type IN (status_check, spreadsheet_reconcile) × minutes_spent × 12 / 60 ÷ 252 working days | 22% duplicate checks + admin = ~1,155 hours/month |
| **B-05: Missed follow-up rate** | recovery_activity_tracker.csv | COUNT WHERE next_follow_up_date IS NULL ÷ total activities | 22% of activities missing follow-up dates |

### Quality Checklist

- ✓ Every metric has a data source (CSV name, specific column)
- ✓ Metric is observed, not estimated (count/sum/avg of actual data)
- ✓ Date range is documented (this is from 2026-01-03 to 2026-02-08, ~5 weeks)
- ✓ If projecting to annual, document multiplier (×12 for monthly, ÷52 for weekly)
- ✓ Confidence level is assigned (High if directly from data; Medium if aggregation required)

---

## Step 2: Establish Assumptions

Assumptions bridge observed data to opportunity impact. Every assumption must be justified.

### Using the Templates

Fill [01-assumptions.csv](../templates/roi-model/01-assumptions.csv) with:

| Assumption | Source | Confidence | Why This Matters |
|-----------|--------|------------|------------------|
| **A-01: Agent hourly cost** | finance_assumptions.csv: FA-01 | High | Cost multiplier for all time-savings benefits |
| **A-02: Straightforward case share** | finance_assumptions.csv: FA-03 | Medium | Segmentation for opportunity sizing |
| **A-03: Minutes saved per case (balance view)** | Estimated from stakeholder feedback | Medium | Assumes customer can self-serve instead of calling agent |
| **A-04: Minutes saved per case (promise capture)** | Estimated from process re-design | Low | Assumes digital promise capture replaces manual note |
| **A-05: Recovery uplift from payment plan** | finance_assumptions.csv: FA-07 | Low | Assumes better plan selection increases uptake |

### Assumption Sourcing Rules

| Source Type | Confidence Level | Examples | Use in Business Case? |
|---|---|---|---|
| **Observed data** | High | Direct CSV count, avg, or sum | ✓ Yes, primary evidence |
| **Industry/Finance estimate** | Medium | Agent cost from finance workbook, straightforward case % from ops leadership | ✓ Yes, with caveats |
| **Estimated/Scenario** | Low | "If we save X min per case, recovery uplift is Y%" | △ Only for sensitivity testing |
| **Untested assumption** | Very Low | "Portal adoption will be 80%" | ✗ No; mark for pilot testing |

### Key Assumption Decisions

**Decision 1: Which time-saving assumptions to use?**

Your data shows:
- Current avg handling time: 7.2 min (observed)
- Finance target: 10 min (assumed, low confidence)
- Opportunity: Reduce by automating admin overhead

**Recommendation:** Use conservative savings (e.g., -2 min, not -8 min) unless you have evidence that admin work will actually be eliminated.

**Decision 2: How to handle untested uplift assumptions?**

Your finance_assumptions.csv shows:
- Recovery uplift for plan selection: 4% (Low confidence)
- Recovery uplift for promise capture: 2.5% (Low confidence)

**Recommendation:** Create conservative case (use 1.5%) and optimistic case (use 4-5%). Never use untested uplift as the primary business case.

---

## Step 3: Baseline Metrics → Opportunity Impact

For each opportunity, calculate the impact using:

```
Annual Hours Saved = monthly case volume × minutes saved per case × 12 ÷ 60
Annual Cost Saved = annual hours saved × hourly cost (A-01)
Annual Revenue Uplift = monthly recovery baseline × uplift % × 12
```

### Populate Opportunities CSV

Use [03-opportunities.csv](../templates/roi-model/03-opportunities.csv):

| OP ID | Opportunity | Case Volume | Time Saved | Annual Cost Saved | Revenue Uplift | Implementation Cost | Effort | Confidence |
|-------|---|---|---|---|---|---|---|---|
| **OP-01** | Self-serve balance & arrears view | 3,540/month (straightforward cases eligible for portal) | 2 min/case (customer views self instead of calling) | 3,540 × 2 × 12 ÷ 60 × £22 = £25.1K | 0 (cost saved, not revenue) | £15K (portal UX + messaging) | Medium | Medium |
| **OP-02** | Digital promise-to-pay capture | 3,540/month | 3 min/case (digital form vs agent manual entry) | 3,540 × 3 × 12 ÷ 60 × £22 = £37.7K | 2.5% uplift on £8M baseline = £20K/month = £240K/year | £25K (form + CRM integration) | Medium | Low |
| **OP-03** | Eligible payment-plan selection | 3,540/month | 1 min/case (rules engine guides instead of agent decides) | 3,540 × 1 × 12 ÷ 60 × £22 = £12.6K | 4% uplift on £8M baseline = £32K/month = £384K/year | £35K (rules config) | Low | Low |
| **OP-04** | Contact detail update request | 2,500/month (non-straightforward; estimated) | 4 min/case (customer confirms vs agent re-verifies) | 2,500 × 4 × 12 ÷ 60 × £22 = £22K | 0 | £10K (simple form) | Low | Medium |
| **OP-05** | Rules-based routing | 9,999/month (all cases) | 5 min/case (system routes vs ops team manually) | 9,999 × 5 × 12 ÷ 60 × £22 = £110K | 0 (efficiency, not revenue) | £45K (rules engine + training) | High | Medium |

### Benefit Type Classification

For each opportunity, separate:

- **Hard Savings:** Annual cost saved (direct agent time reduction)
  - Example OP-01: £25.1K saved agent time
  
- **Revenue Uplift:** New recovery revenue (improved outcomes)
  - Example OP-02: £240K additional recovery
  
- **Soft Benefits:** Value that's real but harder to quantify
  - Example: "Reduced compliance risk," "Faster case closure," "Better customer satisfaction"
  - Note in CSV; don't include in ROI formula

---

## Step 4: Calculate ROI Metrics

Populate [04-roi-summary.csv](../templates/roi-model/04-roi-summary.csv) using formulas:

### Formulas

```
Total Benefit = Annual Cost Saved + Annual Revenue Uplift
Net Benefit = Total Benefit - Implementation Cost
ROI % = (Net Benefit / Implementation Cost) × 100
Payback Months = Implementation Cost / (Monthly Benefit)
Effort Score = (Implementation Cost + Training + Change Mgmt) / Expected Benefit
```

### Example Calculations

**OP-01: Self-serve account summary**
```
Total Benefit = £25.1K (cost saved) + £0 (revenue) = £25.1K
Net Benefit = £25.1K - £15K = £10.1K
ROI % = (£10.1K / £15K) × 100 = 67%
Payback Months = £15K / (£25.1K/12) = 7.2 months
Effort Score = (£15K cost + £5K training) / £25.1K = 80%
Confidence = Medium (untested portal assumptions)
→ Recommendation: Quick-win; good fit for Phase 1
```

**OP-02: Digital promise-to-pay capture**
```
Total Benefit = £37.7K (cost saved) + £240K (revenue) = £277.7K
Net Benefit = £277.7K - £25K = £252.7K
ROI % = (£252.7K / £25K) × 100 = 1,011%
Payback Months = £25K / (£277.7K/12) = 1.1 months
Effort Score = £25K / £277.7K = 9%
Confidence = Low (uplift assumption untested)
→ Recommendation: High upside but risky; pilot test first
```

**OP-05: Rules-based routing**
```
Total Benefit = £110K (cost saved) + £0 (revenue) = £110K
Net Benefit = £110K - £45K = £65K
ROI % = (£65K / £45K) × 100 = 144%
Payback Months = £45K / (£110K/12) = 4.9 months
Effort Score = £45K / £110K = 41%
Confidence = Medium (operational complexity; high change effort)
→ Recommendation: Strong ROI but needs change management; Phase 1b candidate
```

---

## Step 5: Scenario Testing (Conservative vs. Optimistic)

Build at minimum two scenarios for each opportunity:

### Conservative Case
- Use lower time-saving estimates (e.g., -1 min instead of -3 min)
- Use lower adoption rates (e.g., 50% instead of 75%)
- Use lower uplift (e.g., 1.5% instead of 4%)
- **Purpose:** What's the worst reasonable outcome?

### Optimistic Case
- Use higher time-saving estimates (justified by process re-design)
- Use higher adoption (if pilot data supports it)
- Use higher uplift (if industry benchmarks support it)
- **Purpose:** What's the upside if execution is excellent?

### Example: OP-02 Promise Capture - Scenario Sensitivity

| Scenario | Cost Saved | Revenue Uplift | Implementation | Net Benefit | ROI % | Payback |
|----------|-----------|---|---|---|---|---|
| Conservative (1.5% uplift, 1 min saved) | £12.6K | £144K | £25K | £131.6K | 526% | 2.1 mo |
| Base Case (2.5% uplift, 3 min saved) | £37.7K | £240K | £25K | £252.7K | 1,011% | 1.1 mo |
| Optimistic (4% uplift, 4 min saved) | £50.3K | £384K | £25K | £409.3K | 1,637% | 0.8 mo |

**Key insight:** Even conservative case has 526% ROI. Opportunity is robust across scenarios.

---

## Step 6: Rank Opportunities & Recommend Phase 1

### Ranking Framework

Score each opportunity across 4 dimensions:

| Dimension | Scoring | Weight | Why It Matters |
|-----------|---------|--------|---|
| **ROI** | High: >100%; Medium: 50-100%; Low: <50% | 35% | Direct financial return |
| **Payback** | High: <3 months; Medium: 3-6 months; Low: >6 months | 25% | Cash flow & business pressure timing |
| **Confidence** | High (Medium+ confidence in assumptions); Medium (1-2 Low assumptions); Low (untested uplifts) | 25% | Risk of not delivering expected benefit |
| **Effort** | High: <20% effort score; Medium: 20-50%; Low: >50% | 15% | Implementation complexity & resource constraint |

### Example Ranking

| Opportunity | ROI | Payback | Confidence | Effort | Weighted Score | Recommendation |
|---|---|---|---|---|---|---|
| OP-01 Self-serve | Medium (67%) | High (7.2 mo) | Medium | High (80%) | 61 | Phase 1B (after data fix) |
| OP-02 Promise capture | High (1,011%) | High (1.1 mo) | Low | High (9%) | 82 | Phase 1 Pilot (with measurement) |
| OP-03 Payment plan | High (>100%) | Medium (5 mo) | Low | Medium (30%) | 70 | Phase 2 (depends on OP-05) |
| OP-04 Contact update | Medium (73%) | High (5.5 mo) | Medium | High (91%) | 55 | Phase 2 (low priority) |
| OP-05 Routing | High (144%) | Medium (4.9 mo) | Medium | Medium (41%) | 79 | Phase 1 (foundational) |

---

## Step 7: Write Phase 1 Recommendation

Document your recommendation (1-2 paragraphs as per ROI guide):

### Template

```
**Phase 1 Recommendation**

Phase 1 should prioritize [OP-05: Rules-based routing] and [OP-02: Digital promise capture pilot], 
based on ROI ranking and implementation dependencies. 

OP-05 (routing) is foundational—it eliminates the 22% duplicate-checking overhead (£305K/year) 
and enables downstream opportunities like self-serve. With 144% ROI and 4.9-month payback, 
it justifies Phase 1 effort. OP-02 (promise capture) offers 1,011% upside ROI in base case 
and 526% even conservatively, but depends on testing the 2.5% uplift assumption; run as 
supervised pilot (6-8 weeks) to validate. 

OP-01 (self-serve) is deferred to Phase 1B pending audit trail fix (SN-060 compliance concern); 
once data integrity is proven, portal scaling follows. OP-03 (payment plan) and OP-04 
(contact update) are Phase 2, ranked lower by confidence and effort.

**Week 2 Scope Implication:** Phase 1 requires:
- Data integration work (audit trail fix)
- Rules engine implementation (routing)
- Digital capture form + CRM sync (promise capture)
- Estimated budget: £85K; payback: 4-5 months on conservative assumptions.
```

---

## Files & Templates

All templates are in [templates/roi-model/](../templates/roi-model/):

- [01-assumptions.csv](../templates/roi-model/01-assumptions.csv) – Start here; link to finance_assumptions.csv + your estimates
- [02-baseline-metrics.csv](../templates/roi-model/02-baseline-metrics.csv) – Extract from data CSVs
- [03-opportunities.csv](../templates/roi-model/03-opportunities.csv) – Evaluate each opportunity
- [04-roi-summary.csv](../templates/roi-model/04-roi-summary.csv) – Calculate ROI & payback for each

---

## Operational Data Sources

Reference these CSVs in [data/](../data/) to populate templates:

| CSV | Useful For | Columns to Use |
|-----|-----------|-----------------|
| delinquent_accounts_export.csv | Account volume, segmentation, self-service candidates | account_id, delinquency_stage, self_service_candidate, overdue_amount |
| finance_assumptions.csv | Agent cost, baseline recovery, assumption confidence | value, unit, confidence_level for FA-01, FA-02, FA-03, FA-09 |
| recovery_activity_tracker.csv | Activity volume, time per activity, duplicate rates, follow-up tracking | activity_type, minutes_spent, duplicate_check_flag, next_follow_up_date |
| smart_recovery_portal_events.csv | Portal adoption, journey completion, ineligibility patterns | journey_id, event_step, event_status, eligibility_result |
| stakeholder_interview_notes.csv | Pain points, business priorities, stakeholder consensus | quote_or_observation (link findings to SN-XXX references) |

---

## Quality Checklist

Before finalizing your ROI model, verify:

- ✓ **Every baseline metric is sourced from an operational CSV** (not assumed)
- ✓ **Every assumption has a confidence level and justification** (High/Medium/Low with reason)
- ✓ **Formulas are documented** (show the calculation, not just the result)
- ✓ **Scenarios exist** (conservative and optimistic cases for high-risk opportunities)
- ✓ **ROI calculations are consistent** (same formula for all opportunities)
- ✓ **Benefit types are separated** (hard savings ≠ revenue uplift ≠ soft benefits)
- ✓ **Ranking weights reflect business priorities** (ROI 35%, payback 25%, confidence 25%, effort 15%)
- ✓ **Phase 1 recommendation explains dependencies** (why OP-X before OP-Y?)
- ✓ **Soft benefits are acknowledged** (even if not in ROI calc) – e.g., compliance risk reduction, team satisfaction

---

## Common Pitfalls & How to Avoid

| Pitfall | Example | Fix |
|---------|---------|-----|
| **Mixing data + assumptions** | "Agents save 5 minutes per case" without noting that 2 min is observed, 3 min is estimated | Separate baseline time (observed) from "time saved if we change process" (assumed) |
| **Using untested uplifts in base case** | "Portal will increase recovery by 4%" (confidence: Low) as primary business case | Use Low-confidence uplifts only in optimistic scenario; base case uses conservative estimate or 0% |
| **Ignoring implementation reality** | ROI calc shows 200% but doesn't account for 6-month integration, training, and adoption ramp | Add effort score & payback; be honest about timeline and change management cost |
| **Treating all opportunities equally** | "All 5 opportunities have positive ROI, so we'll do all of them in Phase 1" | Rank by weighted score; sequence by dependencies (foundational items first) |
| **No sensitivity testing** | One ROI model, no variation | Always test conservative & optimistic; show what assumption changes ROI most |
| **Vague soft benefits** | "Better compliance" (not quantified) | Either quantify (£50K audit cost saved) or explicitly exclude from ROI; acknowledge separately |

---

## Next Steps After Building Model

1. **Share with Finance & Compliance** – Validate assumptions; identify which ones need executive approval
2. **Identify pilot metrics** – What will you measure during Phase 1 to test assumptions? (e.g., actual promise capture rate, portal completion %)
3. **Build Phase 2 roadmap** – Which deferred opportunities unlock once Phase 1 is stable?
4. **Schedule review cadence** – Monthly ROI tracking during implementation; remodel if assumptions change
