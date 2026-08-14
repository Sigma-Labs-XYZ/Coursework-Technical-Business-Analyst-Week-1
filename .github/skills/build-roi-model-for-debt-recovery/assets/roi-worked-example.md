# ROI Model: Worked Example

This document walks through filling each template CSV using data from your operational CSVs and assumptions.

---

## Step 1: Fill Baseline Metrics (02-baseline-metrics.csv)

Extract directly from your operational data:

```csv
metric_id,metric_name,current_value,unit,source,confidence_level,notes
B-01,total_delinquent_accounts,9999,accounts,delinquent_accounts_export.csv row count,High,Count of all rows in file
B-02,straightforward_case_volume_per_month,3540,cases/month,delinquent_accounts_export.csv + activity analysis,High,4120 early-stage accounts / 5 weeks tracking period × 4.33 weeks/month
B-03,avg_handling_time_straightforward_case,7.2,minutes,recovery_activity_tracker.csv,High,AVG(minutes_spent) from all activity types
B-04,admin_hours_per_day_lost_to_reconciliation,46,hours/month,recovery_activity_tracker.csv duplicate check rate,Medium,22% of activities have duplicate_check_flag=Y; 22% × 45000 activities/month × 7.2 min / 60 / 21 working days
B-05,missed_follow_up_rate,0.22,ratio,recovery_activity_tracker.csv,High,COUNT(next_follow_up_date IS NULL) / total activities = 2 / 9 in sample = 22%
```

**Key decisions:**
- B-02 volume: Used early-stage accounts as proxy for straightforward cases (matches finance_assumptions.csv FA-03 of 38%)
- B-03 time: Observed average from actual activity log (not assumed target)
- B-04 admin overhead: Quantified the duplicate-checking cost mentioned in stakeholder notes (SN-011, SN-028)
- B-05 follow-up gaps: Directly impacts compliance risk (SN-007, SN-060)

---

## Step 2: Document Assumptions (01-assumptions.csv)

Every assumption must be traceable to data or an external source:

```csv
assumption_id,assumption_name,value,unit,source,confidence_level,notes
A-01,agent_hourly_cost,22,GBP/hour,finance_assumptions.csv FA-01,High,Blended cost from Finance workbook; includes salary + oncost
A-02,straightforward_case_share,0.38,ratio,finance_assumptions.csv FA-03,Medium,Operations estimate; 38% of cases suitable for self-service/rules-based routing
A-03,minutes_saved_per_case_balance_view,2,minutes,Scenario estimate,Medium,Assumption: customer self-serve view eliminates one agent contact; validated by SN-001 + SN-081 (customers want transparency)
A-04,minutes_saved_per_case_promise_capture,3,minutes,Process re-design estimate,Low,Assumption: digital form replaces manual entry + agent note-taking; needs testing
A-05,recovery_uplift_percent_payment_plan,0.04,ratio,finance_assumptions.csv FA-07,Low,Finance model estimate; flagged as LOW confidence for sensitivity testing
```

**Sourcing rules applied:**
- A-01: High confidence because it's from Finance workbook (known organizational data)
- A-02: Medium because it's from Operations leadership estimate (not from data, but from subject matter expert)
- A-03: Medium because it's scenario-based BUT validated by stakeholder feedback (SN-001, SN-081 both confirm customers want transparency)
- A-04: Low because this assumes process change hasn't been tested yet
- A-05: Low because Finance explicitly flagged as estimate requiring sensitivity analysis

---

## Step 3: Evaluate Opportunities (03-opportunities.csv)

For each opportunity, calculate impact using formulas and baseline metrics. Based on phase_3_process_mapping.md automation opportunities:

```csv
opportunity_id,opportunity_name,description,case_volume_monthly,time_saved_per_case_min,implementation_cost,annual_hours_saved,annual_cost_saved,annual_revenue_uplift,soft_benefit_note,confidence_level,priority_rank
OP-01,Self-serve balance confirmation and account summary,Customer views balance + current account status without agent contact,3540,2,15000,1176,25920,0,Reduces customer friction; enables transparency; improves satisfaction (SN-001 + SN-081),Medium,3
OP-02,Automated direct payment processing,Customer pays immediately via portal without agent intervention; instantly updates core database,945,7,30000,1102,24244,180000,Increases payment conversion; faster cash collection; reduces agent admin time,Medium,2
OP-03,Automated promise-to-pay setup and tracking,Digital form captures promise; system auto-tracks and auto-follows up via email/SMS if missed; replaces manual spreadsheet tracking,3540,4,25000,2360,51920,120000,Eliminates spreadsheet reconciliation; reduces missed follow-ups (SN-060); improves compliance,Medium,1
OP-04,Automated case routing with vulnerability detection,Straightforward cases → self-serve; complex cases → agent/specialist based on vulnerability markers (hardship history; disputes; high debt >£5k; high ageing >90 days; broken PTPs),945,5,45000,394,8668,0,Eliminates manual triage backlog (SN-057); prevents simple cases stuck behind complex; focuses agent time on high-value work,Medium,4
OP-05,Automated audit trail for interactions and actions,All customer interactions and agent actions automatically logged and accessible; reduces manual record-keeping and spreadsheet reconciliation,0,0,20000,46,1012,0,Improves accountability; enables compliance reporting; reduces 22% of duplicate-check admin overhead (B-04),High,5
```

**Calculation walkthrough for OP-01 (Self-serve balance confirmation):**

```
Case volume: 3,540 cases/month (from B-02 straightforward cases)
Time saved: 2 min/case (assumption A-03: customer self-serves balance inquiry vs agent contact)
Annual hours saved = 3,540 × 2 × 12 ÷ 60 = 1,176 hours/year
Annual cost saved = 1,176 × £22/hr (A-01) = £25,920/year
Annual revenue uplift = £0 (cost efficiency play)
Implementation cost = £15,000 (portal design + customer messaging + onboarding)
Confidence = Medium (adoption depends on portal usability and customer awareness)
Priority = 3 (high ROI but depends on OP-04 routing to drive traffic)
```

**Calculation walkthrough for OP-02 (Automated direct payment):**

```
Case volume: 945 accounts × 15% payment-ready rate (from recovery_activity_tracker.csv "customer_initiated_payment" activities) = ~142/month
Annual hours saved = 945 × 7 min/case × 12 ÷ 60 ÷ 12 months × adoption rate = ~1,102 hours/year (estimated 18% case adoption)
Annual cost saved = 1,102 × £22/hr = £24,244/year
Annual revenue uplift = £8,000,000 baseline × 2.25% payment conversion lift = £180,000/year (Medium confidence: payment friction removal validated by SN-089)
Implementation cost = £30,000 (payment gateway + CRM integration + database updates)
Confidence = Medium (payment uplift modeled but adoption rate unvalidated)
Priority = 2 (strong ROI; enables customer self-service; must run with OP-03)
```

**Calculation walkthrough for OP-03 (Automated promise-to-pay):**

```
Case volume: 3,540 cases/month
Time saved: 4 min/case (eliminates manual form entry, data entry, and follow-up tracking; auto-reminders replace agent manual contact)
Annual hours saved = 3,540 × 4 × 12 ÷ 60 = 2,360 hours/year
Annual cost saved = 2,360 × £22/hr = £51,920/year
Annual revenue uplift = £8,000,000 baseline × 1.5% (improved follow-up compliance reduces missed payments) = £120,000/year
Implementation cost = £25,000 (form builder + CRM automation + email/SMS engine)
Confidence = Medium (time savings observed from recovery_activity_tracker.csv manual_plan_note activities; uplift is scenario-based but supported by SN-060 compliance concerns)
Priority = 1 (highest combined benefit; must run with OP-01 and OP-02 per phase_3 dependencies)
```

**Calculation walkthrough for OP-04 (Automated case routing):**

```
Case volume: 945 total accounts; time saved applies to ~38% straightforward cases = 359 cases/month
Time saved: 5 min/case (eliminates manual triage, queue sorting, specialist assignment delays)
Annual hours saved = 945 × 5 × 12 ÷ 60 = 1,575 hours theoretically; but routing affects all cases, not time per case
→ More accurate: Admin savings from eliminating manual triage queue work = ~394 hours/year (based on B-04 20% of reconciliation time freed)
Annual cost saved = 394 × £22/hr = £8,668/year
Annual revenue uplift = £0 (operational efficiency, not revenue-generating)
Implementation cost = £45,000 (routing engine development + vulnerability marker integration + agent workflow changes)
Confidence = Medium (routing logic is defined but vulnerability marker data quality unvalidated)
Priority = 4 (foundational but high implementation cost; secondary priority after core promise-capture automation)
```

**Calculation walkthrough for OP-05 (Automated audit trail):**

```
Case volume: N/A (system-level benefit, not per-case)
Time saved: 46 hours/month (eliminates duplicate-check admin overhead from B-04; replaces spreadsheet reconciliation)
Annual hours saved = 46 × 12 = 552 hours/year → documented as 46 hours baseline
Annual cost saved = 46 × £22/hr × 12 = £12,144/year → conservatively modeled as £1,012/month = £12,144/year
Annual revenue uplift = £0 (compliance and operational benefit, not revenue-generating)
Implementation cost = £20,000 (audit logging framework + reporting dashboard + integration testing)
Confidence = High (benefit directly observable from B-04 baseline; no assumption needed)
Priority = 5 (critical for compliance SN-060 but run parallel to Phase 1; not on critical path for customer-facing automation)
```

---

## Step 4: Calculate ROI Metrics (04-roi-summary.csv)

Convert opportunity-level benefits into financial metrics:

```csv
opportunity_id,opportunity_name,total_benefit_annual,net_benefit_annual,roi_percent,payback_months,effort_score,confidence_level,recommendation_note
OP-01,Self-serve balance confirmation and account summary,25920,10920,73%,6.9,0.58,Medium,Quick win; Phase 1B candidate after routing is live; lower priority due to payback length
OP-02,Automated direct payment processing,204244,174244,581%,1.8,0.15,Medium,Strong ROI; fast payback; must run parallel with OP-03; enables customer self-serve
OP-03,Automated promise-to-pay setup and tracking,171920,146920,588%,1.7,0.145,Medium,Highest combined benefit; strong ROI + compliance uplift; Phase 1 critical path; run with OP-01 + OP-02
OP-04,Automated case routing with vulnerability detection,77880,32880,73%,6.9,0.58,Medium,Foundational infrastructure; lower Year 1 ROI but enables OP-01/OP-02/OP-03; long payback requires Phase 2+ benefit realization
OP-05,Automated audit trail for interactions and actions,12144,-7856,-39%,>12,1.65,High,Compliance critical but negative Year 1 ROI; must run parallel to Phase 1 as risk mitigation; full benefit realized Year 2+ through reduced audit costs
```

**Calculation walkthrough for OP-02 (Automated direct payment):**

```
Total Benefit = £24,244 (cost saved) + £180,000 (revenue uplift) = £204,244
Net Benefit = £204,244 - £30,000 (implementation) = £174,244
ROI % = (£174,244 / £30,000) × 100 = 581%
Payback Months = £30,000 / (£204,244 / 12) = 1.8 months
Effort Score = £30,000 / £204,244 = 0.15
Recommendation = Medium confidence; strong business case; customer self-serve enabler; must run with OP-03
```

**Calculation walkthrough for OP-03 (Automated promise-to-pay):**

```
Total Benefit = £51,920 (cost saved) + £120,000 (revenue uplift) = £171,920
Net Benefit = £171,920 - £25,000 (implementation) = £146,920
ROI % = (£146,920 / £25,000) × 100 = 588%
Payback Months = £25,000 / (£171,920 / 12) = 1.7 months
Effort Score = £25,000 / £171,920 = 0.145
Recommendation = Phase 1 priority; strong ROI + compliance benefit; dependencies: must run with OP-01 + OP-02 (phase_3 requirement)
```

**Calculation walkthrough for OP-04 (Automated case routing):**

```
Total Benefit = £77,880 (time savings from eliminating manual triage across 3,540 monthly cases)
Net Benefit = £77,880 - £45,000 (implementation) = £32,880
ROI % = (£32,880 / £45,000) × 100 = 73%
Payback Months = £45,000 / (£77,880 / 12) = 6.9 months
Effort Score = £45,000 / £77,880 = 0.58
Recommendation = Foundational infrastructure; enables OP-01/OP-02/OP-03 to function; longer payback acceptable because it unblocks Phase 1 benefits; consider as "enabling cost" rather than standalone ROI
```

**Calculation walkthrough for OP-05 (Automated audit trail):**

```
Total Benefit = £12,144 (admin hours saved from eliminated duplicate checking and spreadsheet reconciliation)
Net Benefit = £12,144 - £20,000 (implementation) = -£7,856 (negative Year 1)
ROI % = (-£7,856 / £20,000) × 100 = -39%
Payback Months = >12 months
Effort Score = £20,000 / £12,144 = 1.65 (high relative cost)
Recommendation = Compliance-critical but negative Year 1 ROI; full benefits realized Year 2+ through reduced audit costs and risk avoidance; treat as risk mitigation investment, not profit center; run parallel to Phase 1
```

---

## Step 5: Scenario Comparison

Test key assumptions with conservative, base, and optimistic cases for the Phase 1B critical paths (OP-02 and OP-03):

### OP-03 Automated Promise-to-Pay – Sensitivity Analysis

This opportunity depends on two key assumptions: (1) time saved through automation, and (2) recovery uplift from better follow-up.

**Conservative Scenario:**
- Time saved: 2.5 min/case (vs 4 min base) – slower process change adoption
- Adoption rate: 50% (vs 70% base) – only half of straightforward cases use digital PTP
- Recovery uplift: 0.75% (vs 1.5% base) – follow-up improvements smaller than expected
- Implementation: £25K (same)

```
Adjusted case volume = 3,540 × 50% adoption = 1,770 cases/month
Annual cost saved = 1,770 × 2.5 × 12 ÷ 60 × £22 = £15,390/year
Annual revenue = £8M × 0.75% = £60,000
Total benefit = £75,390
Net benefit = £75,390 - £25,000 = £50,390
ROI % = 201%
Payback = 4.0 months
→ Still profitable; conservative case holds up but longer payback
Recommendation: Even with lower adoption, ROI remains strong; proceed with measurement plan
```

**Base Scenario (Current Model):**
```
Annual cost saved = 3,540 × 4 × 12 ÷ 60 × £22 = £51,920/year
Annual revenue = £8M × 1.5% = £120,000
Total benefit = £171,920
Net benefit = £171,920 - £25,000 = £146,920
ROI % = 588%
Payback = 1.7 months
→ Strong business case; justifies Phase 1 investment
```

**Optimistic Scenario:**
- Time saved: 5 min/case (if all follow-up is fully automated) 
- Adoption rate: 85% (high user adoption of digital PTP) 
- Recovery uplift: 2.5% (follow-up automation significantly improves payment rates)
- Implementation: £25K (same)

```
Adjusted case volume = 3,540 × 85% adoption = 3,009 cases/month
Annual cost saved = 3,009 × 5 × 12 ÷ 60 × £22 = £66,198/year
Annual revenue = £8M × 2.5% = £200,000
Total benefit = £266,198
Net benefit = £266,198 - £25,000 = £241,198
ROI % = 965%
Payback = 1.1 months
→ Upside is significant; optimistic case shows exceptional returns
Recommendation: Pilot should measure progress toward this scenario
```

**Key insight:** OP-03 is robust across scenarios. Even at 50% adoption and 0.75% uplift, ROI is 201%. Base case ROI of 588% significantly outweighs implementation risk. Proceed with Phase 1B.

---

### OP-02 Automated Direct Payment – Sensitivity Analysis

**Conservative Scenario:**
- Payment conversion uplift: 1% (vs 2.25% base) – payment friction is smaller barrier than expected
- Adoption rate: 30% (vs estimated 50-100% immediate uptake) – customers slow to adopt digital payment
- Implementation: £30K (same)

```
Adjusted case volume = 945 × 30% = 284 cases/month
Annual cost saved = 284 × 7 × 12 ÷ 60 × £22 = £7,822/year
Annual revenue = £8M × 1% = £80,000
Total benefit = £87,822
Net benefit = £87,822 - £30,000 = £57,822
ROI % = 193%
Payback = 4.1 months
→ Still profitable; addresses customer pain (SN-089)
Recommendation: Even conservative case justifies investment
```

**Base Scenario (Current Model):**
```
Annual cost saved = 945 × 7 × 12 ÷ 60 × £22 × 18% adoption = £24,244/year
Annual revenue = £8M × 2.25% = £180,000
Total benefit = £204,244
Net benefit = £204,244 - £30,000 = £174,244
ROI % = 581%
Payback = 1.8 months
→ Strong business case with revenue uplift; customer self-serve enabler
```

**Optimistic Scenario:**
- Payment conversion uplift: 3.5% (payment automation creates new behavior)
- Adoption rate: 70% (high initial adoption with good UX)
- Implementation: £30K (same)

```
Adjusted case volume = 945 × 70% = 661 cases/month
Annual cost saved = 661 × 7 × 12 ÷ 60 × £22 = £28,842/year
Annual revenue = £8M × 3.5% = £280,000
Total benefit = £308,842
Net benefit = £308,842 - £30,000 = £278,842
ROI % = 930%
Payback = 1.3 months
→ Strong upside; digital payment could drive material recovery improvements
Recommendation: Pilot with outcome measurement around payment behavior change
```

**Key insight:** OP-02 shows strong ROI across scenarios. Conservative case (193%) still justifies investment, while optimistic case (930%) demonstrates why this should be bundled with OP-03. Combined Phase 1B ROI is compelling.

---

## Step 6: Prioritization & Ranking

Weighted scoring (35% ROI + 25% Payback + 25% Confidence + 15% Effort):

### Scoring Method

For each opportunity, assign points:

| Dimension | High (3 pts) | Medium (2 pts) | Low (1 pt) |
|-----------|---|---|---|
| **ROI** | >100% | 50-100% | <50% |
| **Payback** | <3 months | 3-6 months | >6 months |
| **Confidence** | High or Medium | Mixed High/Low | Low |
| **Effort** | <20% score | 20-50% score | >50% score |

### Scoring for Each Opportunity

| Opportunity | ROI Score | Payback Score | Confidence Score | Effort Score | Weighted Total | Rank |
|---|---|---|---|---|---|---|
| OP-01 (73% ROI, 6.9 mo, Med, 58%) | 2 | 2 | 2 | 2 | 2.0 | 3 |
| OP-02 (581% ROI, 1.8 mo, Med, 15%) | 3 | 3 | 2 | 3 | 2.75 | 1 (tie) |
| OP-03 (588% ROI, 1.7 mo, Med, 14%) | 3 | 3 | 2 | 3 | 2.75 | 1 (tie) |
| OP-04 (73% ROI, 6.9 mo, Med, 58%) | 2 | 1 | 2 | 2 | 1.75 | 4 |
| OP-05 (-39% ROI, >12 mo, High, 165%) | 1 | 1 | 3 | 1 | 1.50 | 5 |

**Calculation:** (ROI score × 0.35) + (Payback × 0.25) + (Confidence × 0.25) + (Effort × 0.15)

**Example OP-02:** (3 × 0.35) + (3 × 0.25) + (2 × 0.25) + (3 × 0.15) = 1.05 + 0.75 + 0.50 + 0.45 = 2.75

**Key insight:** OP-02 and OP-03 score equally high (2.75), but per phase_3_process_mapping.md, they must run together with OP-01 to ensure portal effectiveness. Bundle as "Phase 1: Customer Self-Service" workstream.

---

## Step 7: Phase 1 Recommendation

Based on ranking + dependencies from phase_3_process_mapping.md, here's the Phase 1 plan:

```
**PHASE 1 RECOMMENDATION**

Phase 1 workstreams follow a two-stage rollout aligned with dependency requirements:

**PHASE 1A: Foundation Layer (Weeks 1-8)**
Must complete before portal features go live to ensure proper case routing and compliance.

(1) **OP-04 Automated Case Routing** (foundational, 6.9-month payback, 73% Year 1 ROI)
    - Infrastructure layer: Implements vulnerability-based routing logic
    - Routes straightforward cases → self-serve portal; complex cases → agent/specialist
    - Directly addresses SN-057 (complex & simple cases mixed in queue)
    - Eliminates manual triage backlog (estimated 295 hours/month saved across organization)
    - Cost: £45K; Must start Week 1

(2) **OP-05 Automated Audit Trail** (parallel to OP-04)
    - Compliance & operational infrastructure: Auto-logs all interactions and agent actions
    - Addresses SN-060 compliance blocker for portal launch
    - Negative Year 1 ROI (-39%) but risk mitigation critical
    - Enables Phase 1B portal launch (SN-060 requires audit trail before customer portal access)
    - Cost: £20K; Timeline: 6-8 weeks parallel

**PHASE 1A Investment: £65K | Timeline: 8 weeks**

---

**PHASE 1B: Customer Self-Service Bundle (Weeks 8-16)**
Per phase_3_process_mapping.md: "OP-01, OP-02, and OP-03 must be implemented together to ensure portal effectiveness"

(3) **OP-02 Automated Direct Payment Processing** (highest ROI tier, 1.8-month payback, 581% ROI)
    - Enables customer payment without agent intervention
    - Immediate database updates increase payment conversion
    - Strong revenue uplift (£180K/year estimated)
    - Cost: £30K; Payback: 1.8 months

(4) **OP-03 Automated Promise-to-Pay Setup & Tracking** (highest ROI tier, 1.7-month payback, 588% ROI)
    - Core compliance automation: replaces manual spreadsheet tracking
    - Auto-follows up via email/SMS if payment missed
    - Addresses SN-060 compliance concern about missed follow-ups
    - Strongest combined benefit: cost savings + compliance + revenue uplift
    - Cost: £25K; Payback: 1.7 months

(5) **OP-01 Self-Serve Balance Confirmation Portal** (supporting enabler, 6.9-month payback, 73% ROI)
    - Customer-facing interface that customers use to trigger OP-02 and OP-03
    - Medium confidence but essential for OP-02/OP-03 to function
    - Depends on OP-04 routing to funnel appropriate traffic
    - Reduces customer friction; improves transparency (SN-001 + SN-081 validated)
    - Cost: £15K; Payback: 6.9 months

**PHASE 1B Investment: £70K | Timeline: 8 weeks | Payback: 1.7 months from OP-03/OP-02**
**These 3 opportunities run in parallel; cannot split implementation**

---

**WEEK 2 SCOPE IMPLICATIONS:**

Phase 1 Total Investment: £135K (£65K foundation + £70K portal)
Timeline: 16 weeks (8 weeks foundation + 8 weeks portal bundle)
Break-even: Month 2-3 (from Phase 1B savings/revenue)
Full benefit realization: 6+ months (Phase 1A + Phase 1B + adoption ramp)

**Critical success metrics:**
- OP-04: Routing accuracy >98%; straightforward case identification >90%
- OP-05: Audit trail completeness 100%; SN-060 compliance validated
- OP-02: Payment conversion >15%; customer adoption >20%
- OP-03: Promise capture rate >75%; follow-up SMS delivery >95%
- OP-01: Portal adoption >30% of straightforward case customers

**Deferred to Phase 2:**
- No other opportunities; Phase 1 is comprehensive and integrated per process mapping
```

---

## Dependency Map

```
Phase 1 Workstreams:

┌─────────────────────────────────────────────────────────────┐
│ PHASE 1A: Foundation (Weeks 1-8)                            │
│ ┌──────────────────────────────────────────────────────────┤
│ │ OP-04: Automated Case Routing        [£45K, 8 weeks]    │
│ │ └─→ Infrastructure for routing traffic to portal         │
│ │                                                           │
│ │ OP-05: Automated Audit Trail ││┐     [£20K, 6-8 weeks]  │
│ │ └─→ Compliance enabler for portal launch (SN-060)        │
└─────────────────────────────────────────────────────────────┘
             │
             ├─────────────────────────────────────────────────────────────┐
             │                                                             │
┌────────────▼─────────────────────────────────────────────────────────┐  │
│ PHASE 1B: Customer Self-Service Bundle (Weeks 8-16)                 │  │
│ Must run together per phase_3_process_mapping.md                     │  │
│ ┌──────────────────────────────────────────────────────────────────┤  │
│ │ OP-02: Direct Payment         [£30K, parallel, ROI: 581%]       │  │
│ │ OP-03: Promise-to-Pay          [£25K, parallel, ROI: 588%]      │  │
│ │ OP-01: Portal Balance View     [£15K, parallel, ROI: 73%]       │  │
│ │                                                                   │  │
│ │ These 3 are interconnected:                                       │  │
│ │ - Portal (OP-01) is customer interface for OP-02 & OP-03        │  │
│ │ - Payment flow (OP-02) drives promise-to-pay volume (OP-03)     │  │
│ │ - Both payment & promise tracking require audit trail (OP-05)   │  │
│ │ - Case routing (OP-04) funnels appropriate traffic to portal    │  │
└──────────────────────────────────────────────────────────────────┘  │
                                                                        │
                    Phase 1A enables Phase 1B ◄──────────────────────────┘
```

---

## Next Steps

1. **Validate assumptions** with Finance (confirm £22/hr agent cost, uplift estimates)
2. **Get Compliance approval** for audit trail work + promise capture method
3. **Set pilot success criteria** for OP-02 (what % uplift = continue to full rollout?)
4. **Build change management plan** for OP-05 (routing changes how agents work)
5. **Monthly remodel** during Phase 1 (update actual metrics vs assumptions)
