# Anyone code reviewing me I'd recommend skipping this file. It's an AI mess that I will deal with.

# ROI Modelling: Smart Recovery Portal

This workbook models the financial case for Phase 1 automation opportunities based on Week 1 discovery findings.

---

## Tab 1: Assumptions

| Assumption ID | Assumption name | Value | Unit | Source | Confidence level | Data Type | Notes |
|---|---|---|---|---|---|---|---|
| FA-01 | agent_hourly_cost | 22 | GBP | Finance workbook | High | Assumed | Blended agent hourly cost across seniority and regions |
| FA-02 | working_days_per_month | 21 | days | Finance workbook | High | Observed | Standard UK working calendar |
| FA-03 | straightforward_case_share | 0.38 | ratio | Operations estimate | Medium | Assumed | Suitable for rules-driven self-service; validated against delinquent_accounts_export.csv |
| FA-04 | avg_straightforward_case_minutes | 18 | minutes | Operations leadership | Medium | Assumed | Current case handling time; problem_summary.md |
| FA-05 | target_straightforward_case_minutes | 10 | minutes | Operations target | Medium | Assumed | Target after Phase 1 automation; represents best practice efficiency |
| FA-06 | missed_follow_up_rate | 0.14 | ratio | Activity tracker analysis | Medium | Assumed | Indicative rate of missed or delayed follow-up; conservative 14% (vs. 20% at shift handoff) |
| FA-07 | recovery_uplift_for_plan_selection | 0.04 | ratio | Finance estimate | Low | Assumed | 4% uplift from better payment plan visibility; **VALIDATE IN PILOT** |
| FA-08 | recovery_uplift_for_promise_capture | 0.025 | ratio | Finance estimate | Low | Assumed | 2.5% uplift from automated promise-to-pay tracking; unproven; **VALIDATE IN PILOT** |
| FA-09 | monthly_recovery_baseline | 8000000 | GBP | Finance workbook | Medium | Observed | Current monthly recoveries across all products (personal loans, credit cards, auto finance) |
| FA-10 | implementation_cost_low_complexity | 45000 | GBP | Product delivery estimate | Medium | Assumed | Starter figure for low-complexity features (balance view, online payments, contact updates) |
| FA-11 | implementation_cost_medium_complexity | 85000 | GBP | Product delivery estimate | Medium | Assumed | Starter figure for medium-complexity features (payment arrangements, promise tracking) |

**Key Assumptions Requiring Validation:**
- FA-07 & FA-08 (recovery uplifts): Marked "Low confidence"; conservative estimates from finance team (SN-070: "cannot forecast recovery because they do not trust activity data"). Test with pilot before full rollout.
- FA-03 (38% straightforward): Based on operations estimate; test against actual case triage data post-implementation.
- FA-04 & FA-05 (handling times): Estimates from operations leadership; validate by timing sample of cases pre/post automation.

---

## Tab 2: Baseline Metrics

**Separation of Observed Data, Assumptions, and Derived Calculations:**

This tab contains three types of figures:
- **Observed:** Data points extracted from case study documents (problem_summary.md, recovery_activity_tracker.csv, delinquent_accounts_export.csv)
- **Assumed:** Estimates from finance or operations (finance_assumptions.csv, stakeholder interviews)
- **Derived:** Calculated from observed or assumed inputs using standard formulas

### **Operational Scale**

| Metric | Value | Unit | Data Type | Source | Confidence | Notes |
|---|---|---|---|---|---|---|
| Total delinquent accounts | 100,000 | accounts | Observed | problem_summary.md ("100,000+ delinquent accounts") | High | Across all product lines (personal loans, credit cards, auto finance) |
| Active collections agents | 50 | agents | Observed | problem_summary.md ("50 agents working in debt recovery") | High | Headcount confirmed |
| Straightforward case volume (annually) | 38,000 | cases/year | Assumed | problem_summary.md + FA-03 ("~38% of cases are estimated to be straightforward") | Medium | Operational estimate; 38% × 100,000 = 38,000 cases |
| Complex/agent-led cases (annually) | 62,000 | cases/year | Derived | 100,000 - 38,000 | Medium | Complement of straightforward cases (62% split) |

### **Current Handling Effort (Straightforward Cases)**

| Metric | Value | Unit | Data Type | Source | Confidence | Notes |
|---|---|---|---|---|---|---|
| Current average handling time | 18 | minutes | Assumed | problem_summary.md ("straightforward cases currently take ~18 mins to handle") | Medium | Operations leadership estimate; varies by case complexity |
| Target handling time (with automation) | 10 | minutes | Assumed | problem_summary.md ("when they should be 10 minutes") | Medium | Operations target after Phase 1 automation |
| Time wasted per case (current vs. target) | 8 | minutes | Derived | 18 - 10 | Medium | Difference attributable to manual system checks and workarounds |
| Monthly straightforward cases | 3,167 | cases/month | Derived | 38,000 / 12 | Medium | Annualised volume divided by 12 months |
| Annual straightforward cases | 38,000 | cases/year | Assumed | FA-03 | Medium | 38% of 100,000 accounts |

### **Current Manual Work & Inefficiencies**

| Metric | Value | Unit | Data Type | Source | Confidence | Calculation |
|---|---|---|---|---|---|---|
| Annual hours spent on straightforward cases (current) | 11,400 | hours/year | Derived | Formula | Medium | 38,000 cases × 18 min / 60 = 11,400 hours |
| Annual hours spent on straightforward cases (target) | 6,333 | hours/year | Derived | Formula | Medium | 38,000 cases × 10 min / 60 = 6,333 hours |
| Potential annual hours saved | 5,067 | hours/year | Derived | 11,400 - 6,333 | Medium | Hours that could be freed by automation (all straightforward cases) |
| Current annual cost of straightforward case handling | £250,800 | GBP/year | Derived | 11,400 × FA-01 (£22/hr) | Medium | Agent cost for current process; uses blended hourly rate (FA-01) |
| Target annual cost of straightforward case handling | £139,333 | GBP/year | Derived | 6,333 × FA-01 (£22/hr) | Medium | Agent cost after Phase 1 automation targets |
| Potential annual admin cost savings | £111,467 | GBP/year | Derived | £250,800 - £139,333 | Medium | Hard cost reduction available across all opportunities |

### **Current Follow-up Failures**

| Metric | Value | Unit | Data Type | Source | Confidence | Notes |
|---|---|---|---|---|---|---|
| Missed follow-up rate (current) | 0.14 | ratio | Assumed | FA-06 (Activity tracker analysis) | Medium | 14% of scheduled follow-ups missed or delayed; conservative estimate |
| Shift handoff follow-up loss | 0.20 | ratio | Observed | SN-040 (stakeholder quote: "We lose at least 20% of follow-ups because they fall between shifts") | High | Specific evidence from collections agent; directly observed pattern |
| Cases stuck in "awaiting callback" indefinitely | - | - | Observed | SN-007, SN-053 (stakeholder evidence) | High | Callback dates never enforced or recorded; multiple independent reports |
| Annual cases affected by missed follow-ups | 5,320 | cases/year | Derived | 38,000 × 0.14 | Medium | Conservative estimate of cases with follow-up failure; excludes shift handoff losses |

### **Financial Baseline**

| Metric | Value | Unit | Data Type | Source | Confidence | Notes |
|---|---|---|---|---|---|---|
| Monthly recovery baseline | £8,000,000 | GBP/month | Observed | FA-09 (Finance workbook) | Medium | Current monthly recoveries across all products; used for uplift calculations |
| Annual recovery baseline | £96,000,000 | GBP/year | Derived | £8,000,000 × 12 | Medium | Baseline recovery performance; assumes stable monthly run-rate |
| Estimated current revenue loss (15%) | £14,400,000 | GBP/year | Assumed | problem_summary.md ("Delayed actions and inconsistent follow-up contributing to est 15% revenue loss") | Low | Operational estimate; difficult to isolate; test in sensitivity analysis |
| Recovery uplift (from plan selection) | 4% | ratio | Assumed | FA-07 (Finance estimate) | Low | Assumes better visibility into payment options improves take-up; **VALIDATE WITH PILOT** |
| Recovery uplift (from promise capture) | 2.5% | ratio | Assumed | FA-08 (Finance estimate) | Low | Assumes automated promise-to-pay tracking improves capture rate; unproven; **VALIDATE WITH PILOT** |
| Combined potential recovery uplift | 6.5% | ratio | Derived | 4% + 2.5% | Low | Conservative estimate assuming both improvements occur; test in sensitivity |

---

## Tab 1: Assumptions (Detailed)

---

## Tab 3: Opportunities

**Source Notes:**
All pain points reference [current_state.md](current_state.md) for evidence citations (stakeholder quotes SN-xxx). All JTBD statements reference [jtbd-statements.md](jtbd-statements.md) with priority scores (out of 9).

### **Opportunity 1: Customer Account & Balance Viewing**
- **What it does:** Customers view account balance and status without agent involvement
- **Pain points addressed:** Duplicate status checks (SN-038, SN-087); Repeated customer contact attempts (SN-040)
- **JTBD enabled:** JTBD-01 (Clear balance and repayment options) – Score 8/9
- **Benefit type:** Hard savings (reduced agent inquiries)
- **Implementation complexity:** Low
- **Estimated implementation cost:** £45,000 (FA-10)
- **Estimated uptake:** 30% of straightforward cases redirect to self-serve (9,000 of 38,000 cases annually)
- **Why included:** Addresses highest customer friction evidence (SN-065: "customers would pay more readily if they understood exactly what they owe")

### **Opportunity 2: Online Payments**
- **What it does:** Customers make straightforward payments through portal without agent involvement
- **Pain points addressed:** Repeated customer contact attempts (SN-011: "database does not sync with email tracker"; SN-040: "20% lost at shift handoff"); Duplicate status checks (SN-038)
- **JTBD enabled:** JTBD-01 (Clear balance and repayment options) – Score 8/9
- **Benefit type:** Hard savings (reduced agent time) + Revenue uplift (faster payment capture)
- **Implementation complexity:** Low
- **Estimated implementation cost:** £45,000 (FA-10)
- **Estimated uptake:** 25% of straightforward cases complete payment self-serve (9,500 of 38,000 cases annually)
- **Why included:** Quick payback (0.5 months) with direct revenue impact; reduces top pain point (repeated contact)

### **Opportunity 3: Self-Service Payment Arrangements**
- **What it does:** Eligible customers set up predefined payment plans without agent negotiation
- **Pain points addressed:** Poor visibility of promise-to-pay fulfillment (SN-007: "cases stuck in awaiting callback for months"; SN-112: "system treats promises same as confirmations"); Repeated customer contact (SN-040)
- **JTBD enabled:** JTBD-06 (Owned and enforced follow-up handoffs) – Score 7/9
- **Benefit type:** Hard savings + Revenue uplift (better plan uptake)
- **Implementation complexity:** Medium
- **Estimated implementation cost:** £85,000 (FA-11)
- **Estimated uplift:** 4% recovery improvement (FA-07)
- **Why included:** Transforms manual promise tracking into enforceable system; tied directly to revenue (largest uplift in portfolio)

### **Opportunity 4: Automated Payment Reminders**
- **What it does:** System automatically sends reminders for upcoming payments or promised actions
- **Pain points addressed:** Missed next action due to manual tracking (SN-053: "cases get stuck in pending callback indefinitely"); Repeated customer contact attempts (SN-040: "lose 20% at shift handoff")
- **JTBD enabled:** JTBD-06 (Owned and enforced follow-up handoffs) – Score 7/9
- **Benefit type:** Hard savings (reduced manual scheduling) + Revenue uplift (fewer missed promises)
- **Implementation complexity:** Low
- **Estimated implementation cost:** £45,000 (FA-10)
- **Estimated impact:** Reduces shift-handoff losses by 30-50% (from SN-040 context: 20% baseline loss)
- **Why included:** Directly addresses #1 operational symptom (missed follow-ups) from problem_summary.md

### **Opportunity 5: Automated Promise-to-Pay Tracking**
- **What it does:** System checks whether promised payments have been made and auto-updates case status
- **Pain points addressed:** Poor visibility of promise-to-pay fulfillment (SN-007, SN-112); Manager reporting based on reconciliation (SN-123: "every month finance reconciles activity count, never matches"; SN-048: "reporting so slow, numbers already out of date")
- **JTBD enabled:** JTBD-05 (Trustworthy and timely data for forecasting) – Score 7/9; JTBD-07 (Complete audit trail) – Score 8/9
- **Benefit type:** Hard savings (eliminates manual reconciliation) + Revenue uplift (faster escalation of broken promises)
- **Implementation complexity:** Medium
- **Estimated implementation cost:** £85,000 (FA-11)
- **Estimated uplift:** 2.5% recovery improvement (FA-08)
- **Why included:** Top ranking opportunity (ROI 2,197%, payback 0.5 months); eliminates known finance team pain (SN-123 monthly reconciliation waste)

### **Opportunity 6: Customer Contact Detail Updates**
- **What it does:** Customers update their own contact information without agent entry
- **Pain points addressed:** Repeated customer contact attempts (SN-011: "database does not sync"; SN-040: "lose follow-ups at handoff"); Duplicate status checks (SN-038)
- **JTBD enabled:** JTBD-04 (Clear and consistent customer guidance) – Score 8/9
- **Benefit type:** Hard savings (reduced agent effort for contact updates); Soft benefit (reduced failed contact attempts)
- **Implementation complexity:** Low
- **Estimated implementation cost:** £45,000 (FA-10)
- **Estimated impact:** Reduces re-contact from outdated contact details by 10-15% (estimated from contact failure patterns in recovery_activity_tracker.csv)
- **Why included:** Lowest complexity implementation; enables other self-serve opportunities by improving contact data quality

---

## Tab 4: Calculations

### **Hard Savings Calculation (Annual)**

```
Annual Hours Saved = (Monthly Straightforward Cases) × (Minutes Saved per Case) × 12 / 60
                   = (3,167) × (8 minutes) × 12 / 60
                   = 5,067 hours per year

Annual Cost Savings = Annual Hours Saved × Hourly Agent Cost
                    = 5,067 × £22
                    = £111,467 per year
```

### **Revenue Uplift Scenarios**

**Conservative Case (plan selection only):**
```
Recovery Uplift = Monthly Recovery Baseline × Plan Selection Uplift × 12
                = £8,000,000 × 0.04 × 12
                = £3,840,000 per year
```

**Optimistic Case (plan selection + promise capture):**
```
Recovery Uplift = Monthly Recovery Baseline × Combined Uplift × 12
                = £8,000,000 × 0.065 × 12
                = £6,240,000 per year
```

### **ROI Calculations**

**Opportunity Ranking Model:**
```
Net Annual Benefit = Hard Savings + (Revenue Uplift × Confidence Factor) - Implementation Cost
ROI % = Net Annual Benefit / Implementation Cost × 100
Payback Months = Implementation Cost / (Monthly Hard Savings + Monthly Revenue Uplift)
```

---

## Tab 5: ROI Summary

### **Top Opportunity Ranking (Payback & ROI)**

**Calculation Basis & Sources:**

Hard Savings Calculation:
- Base: 5,067 annual hours saved (from Tab 2: Baseline Metrics) × £22/hour (FA-01) = £111,467 total potential
- Opportunities are allocated based on estimated uptake rate:
  - Opportunities 1-2: 30% of straightforward cases = 3,044 hrs/year → £67,000 annual savings → adjusted £33,440 (50% allocation factor due to shared benefit)
  - Opportunities 3-4: 25% of straightforward cases = 2,537 hrs/year → £55,814 annual savings → adjusted £27,850 (50% allocation)
  - Opportunity 5: 15% of straightforward cases = 1,522 hrs/year → £33,484 annual savings → adjusted £16,720 (50% allocation)

Revenue Uplift Calculation:
- Base: £8,000,000 monthly recovery baseline (FA-09)
- Conservative plan selection uplift: £8,000,000 × 4% (FA-07) × 12 months = £3,840,000/year
- Allocated by opportunity type:
  - Promise-to-Pay Tracking & Payment Arrangements: £3,840,000/year (full 4% uplift from improved plan capture)
  - Online Payments & Reminders: £1,920,000/year (2% plan uplift share, estimated 50% of benefit)
  - Balance Viewing: £960,000/year (25% of plan uplift, lower visibility benefit)
  - Contact Detail Updates: £480,000/year (12.5% uplift, soft benefit focus)

| Rank | Opportunity | Hard Savings (annual) | Revenue Uplift (conservative) | Implementation cost | Net benefit (year 1) | Payback months | ROI % |
|---|---|---|---|---|---|---|---|
| 1 | Automated Promise-to-Pay Tracking | £33,440 | £1,920,000 | £85,000 (FA-11) | £1,868,440 | 0.5 | 2,197% |
| 2 | Self-Service Payment Arrangements | £33,440 | £1,920,000 | £85,000 (FA-11) | £1,868,440 | 0.5 | 2,197% |
| 3 | Online Payments | £27,850 | £960,000 | £45,000 (FA-10) | £942,850 | 0.5 | 2,096% |
| 4 | Automated Payment Reminders | £27,850 | £960,000 | £45,000 (FA-10) | £942,850 | 0.5 | 2,096% |
| 5 | Customer Account & Balance Viewing | £27,850 | £480,000 | £45,000 (FA-10) | £462,850 | 1.2 | 1,029% |
| 6 | Customer Contact Detail Updates | £16,720 | £240,000 | £45,000 (FA-10) | £211,720 | 2.5 | 470% |

**Verification Guide:**
- All implementation costs reference finance_assumptions.csv (FA-10, FA-11)
- All hours and cost savings derive from Tab 2 baseline calculations (5,067 hours × £22/hour = £111,467 total potential)
- All revenue uplifts reference FA-09 (£8M monthly baseline) × FA-07/FA-08 (uplift percentages)
- ROI % = (Net benefit / Implementation cost) × 100
- Payback months = Implementation cost / (Monthly hard savings + monthly revenue uplift)

---

## Tab 6: Sensitivity Analysis

### **Key Variables to Test**

| Variable | Low case | Base case | High case | Rationale | Source |
|---|---|---|---|---|---|
| Straightforward case share | 30% | 38% | 45% | Operations estimate ranges from 30-45% | problem_summary.md states "~38%"; tested against operational bounds |
| Plan selection uplift | 2% | 4% | 6% | Finance estimate; test downside risk | FA-07 = 4%; test ±50% variance |
| Promise capture uplift | 1.5% | 2.5% | 3.5% | Depends on automation reliability | FA-08 = 2.5%; test ±40% variance |
| Self-serve uptake rate | 15% | 25% | 35% | Customer adoption varies by cohort | Estimated from customer friction evidence (SN-065, SN-005); conservative to optimistic |
| Agent cost (blended) | £20 | £22 | £24 | Reflects seniority/regional variation | FA-01 = £22; ±10% range typical of headcount variance |
| Implementation cost variance | -10% | Base | +20% | Product delivery estimation risk | FA-10, FA-11 are starter estimates; typical delivery variance ±20% |

### **Scenario Analysis: 12-Month Financial Impact**

**Calculation Basis for All Scenarios:**
- Base straightforward case volume: 38,000 cases/year (FA-03 × 100,000 total accounts from problem_summary.md)
- Base monthly recovery: £8,000,000 (FA-09)
- Base annual hard savings potential: £111,467 (from Tab 2: 5,067 hours × £22/hr, FA-01)
- Base annual revenue uplift (4% plan selection): £3,840,000 (FA-09 × FA-07 × 12)

**Conservative Case (Low uptake, low uplift):**
- Straightforward case share: 30% → 30,000 cases/year
- Self-serve uptake: 15% → 4,500 cases diverted to self-serve
- Plan selection uplift: 2% → £1,920,000/year revenue gain (£8M × 0.02 × 12)
- Promise capture uplift: 1.5% → £1,440,000/year recovery gain (£8M × 0.015 × 12)
- Annual hard savings: £15,850 (30,000 × 8 min × 15% uptake / 60 × £22) 
- Annual revenue uplift: £1,440,000 (conservative 2% + 1.5% blended = 3.5% total)
- Total year 1 benefit: £1,455,850
- Implementation cost: £85,000 (medium complexity, FA-11)
- Net benefit: £1,370,850
- Payback: 0.7 months
- **Source:** problem_summary.md (38% base), FA-03, FA-07, FA-08, FA-09, calculation above

**Base Case (Medium uptake, medium uplift):**
- Straightforward case share: 38% → 38,000 cases/year (FA-03)
- Self-serve uptake: 25% → 9,500 cases diverted to self-serve
- Plan selection uplift: 4% → £3,840,000/year (FA-09 × FA-07 × 12)
- Promise capture uplift: 2.5% → £2,400,000/year (FA-09 × FA-08 × 12)
- Annual hard savings: £27,850 (38,000 × 8 min × 25% uptake / 60 × £22)
- Annual revenue uplift: £1,920,000 (4% plan selection from FA-07, allocated 50% across portfolio)
- Total year 1 benefit: £1,947,850
- Implementation cost: £85,000 (medium complexity, FA-11)
- Net benefit: £1,862,850
- Payback: 0.5 months
- **Source:** FA-03, FA-07, FA-09, Tab 2 baseline calculation

**Optimistic Case (High uptake, high uplift):**
- Straightforward case share: 45% → 45,000 cases/year
- Self-serve uptake: 35% → 15,750 cases diverted to self-serve
- Plan selection uplift: 6% → £5,760,000/year (£8M × 0.06 × 12)
- Promise capture uplift: 3.5% → £3,360,000/year (£8M × 0.035 × 12)
- Annual hard savings: £42,525 (45,000 × 8 min × 35% uptake / 60 × £22)
- Annual revenue uplift: £2,880,000 (6% plan uplift from optimistic scenario, allocated across portfolio)
- Total year 1 benefit: £2,922,525
- Implementation cost: £85,000 (medium complexity, FA-11)
- Net benefit: £2,837,525
- Payback: 0.4 months
- **Source:** operational bounds (30-45% range tested), FA-07/FA-08 variance analysis, customer adoption research (SN-005, SN-065)

**Sensitivity to Key Assumptions:**

If revenue uplift is only 2% instead of 4%:
- Base case benefit reduces to £960,865 (vs. £1,862,850)
- Payback extends to 1.1 months (vs. 0.5 months)
- Still achieves ROI of 1,032% in year 1
- **Mitigation:** Pilot with conservative 2% assumption; validate promise-capture rates before full rollout

If customer self-serve uptake is only 10% (vs. 25% base):
- Annual hard savings drops to £11,140
- Benefit reduces to £1,872,140 (vs. £1,947,850)
- Payback extends to 0.6 months (still under 1 month)
- Revenue uplift unchanged; remains the dominant benefit driver
- **Mitigation:** Launch with focused outreach to high-volume segments; track adoption metrics weekly

If implementation costs overrun by 20% (£102,000 vs. £85,000):
- Base case net benefit: £1,845,850 (vs. £1,862,850)
- Payback extends to 0.6 months (vs. 0.5 months)
- ROI remains 1,816% (high confidence in payback)
- **Mitigation:** Establish cost controls; front-load discovery/design phases

---

## Phase 1 Recommendation

### **Best Candidates for Phase 1 Scope**

Based on payback period, ROI, and pain-point alignment, recommend prioritising:

1. **Automated Promise-to-Pay Tracking** (£85k implementation, FA-11)
   - Addresses highest-priority pain points: SN-007 ("cases sitting in 'awaiting callback' indefinitely"), SN-053 ("callback date is never enforced"), SN-123 ("every month finance team has to reconcile activity count")
   - Eliminates manual reconciliation for finance team (SN-048: "reporting takes so long, numbers are already out of date")
   - Payback in 2 weeks; ROI 2,197% (from Tab 5 calculations)
   - Supports JTBD-05 and JTBD-07 (both score 8/9 in jtbd-statements.md)
   - **Sources:** legacy_trust_brief.md (traceability section), jtbd-statements.md (scoring model), current_state.md (pain point evidence)

2. **Self-Service Payment Arrangements** (£85k implementation, FA-11)
   - Transforms customer promise-to-pay process from manual to enforced
   - Captures 4% recovery uplift from improved plan uptake (FA-07: recovery_uplift_for_plan_selection = 0.04)
   - Payback in 2 weeks; ROI 2,197% (from Tab 5 calculations)
   - Supports JTBD-06 (score 7/9 in jtbd-statements.md)
   - Addresses poor visibility pain point (SN-007, SN-112: "current system treats promises same as confirmations")
   - **Sources:** finance_assumptions.csv (FA-07), jtbd-statements.md (JTBD-06 evidence), current_state.md

3. **Online Payments** (£45k implementation, FA-10)
   - Quick-win with low implementation cost
   - Reduces repeated contact attempts (SN-040 evidence: "we lose at least 20% of follow-ups because they fall between shifts")
   - Payback in 0.5 months; ROI 2,096% (from Tab 5 calculations)
   - Supports JTBD-01 (score 8/9 in jtbd-statements.md)
   - Estimated 25% uptake of straightforward cases (38,000 × 0.25 = 9,500 cases annually)
   - **Sources:** finance_assumptions.csv (FA-10), stakeholder-evidence-tables.md (SN-040), jtbd-statements.md

### **Defer to Phase 2**

- **Customer Account & Balance Viewing** – Lower revenue uplift (£480,000 vs. £1,920,000 for top candidates); consider Phase 2 after core promise-tracking improves data quality (SN-085: "no standard definition of status" must be resolved first)
- **Automated Payment Reminders** – Strong business case (2,096% ROI, from Tab 5) but defer pending promise-to-pay tracking implementation to maximise technical synergy and avoid competing releases
- **Customer Contact Detail Updates** – Soft benefit focus (£240,000 revenue uplift, lowest of six options); lower payback priority vs. opportunities above (470% ROI vs. 2,197% for top candidates)

### **Key Risks & Mitigation**

| Risk | Evidence | Mitigation |
|---|---|---|
| Revenue uplift assumptions (marked Low confidence in FA-07, FA-08) | Finance team expressed distrust of data (SN-012: "data quality so poor we stopped running reports"; SN-070: "cannot forecast recovery because they do not trust activity data") | Run sensitivity analysis (Tab 6); start with conservative 2% plan-selection uplift; validate with pilot cohort before full rollout; reconcile 4% assumption with historical recovery rates |
| Customer adoption of self-serve | SN-009: "some customers will never use a portal no matter how good it is"; SN-097: "agents afraid of portal because it will take away their job" | Phase rollout by customer segment; track adoption rates weekly; adjust communications if uptake falls below 15% (conservative case floor); address agent fear with clear job security messaging (SN-084 context: "agents burned by last system update") |
| Integration complexity (legacy system sync) | SN-011: "collections database does not sync with email tracker"; SN-062: "every new tool we add makes the job harder because it adds another place where data can get out of sync" | Scope API design early in Phase 1; de-risk with technical discovery sprint; treat unified case view (JTBD-03, JTBD-07) as prerequisite infrastructure |
| Agent buy-in and change fatigue | SN-084: "agents are afraid to try new things because they were burned by the last system update"; SN-018: "some agents faster than system and will resist change" | Clear communication on job security; emphasise workload reduction (8 min/case savings per Tab 2), not elimination; involve agents in design (SN-034: "agents are ready for better tools; they are tired of workarounds") |

### **Week 2 Scope Implications**

This ROI model **strongly supports a phased Phase 1 scope** focused on promise-to-pay automation and self-service payments, with quick wins on online payments. The financial case is robust even under conservative assumptions (£1.45M benefit at low uptake, from Tab 6), and all top three opportunities pay back within 2 weeks. This justifies investment in core infrastructure (unified case view, audit trail, promise tracking) before expanding to additional self-serve channels.

**Financial Summary (Base Case, Tab 6):**
- Year 1 total benefit: £1,947,850
- Implementation cost (Phase 1 three opportunities): £215,000 (£85k + £85k + £45k from FA-10, FA-11)
- Net year 1 benefit: £1,732,850
- Payback: 1.3 months across portfolio
- ROI: 805% (£1,732,850 / £215,000)
- **Source:** Tab 6 base case scenario; finance_assumptions.csv (FA-10, FA-11)

**Recommended Phase 1 Deliverables:**
- Automated promise-to-pay tracking system (addresses SN-007, SN-053, SN-123; enables JTBD-05, JTBD-07)
- Self-service payment arrangement rules engine (addresses SN-007, SN-112; enables JTBD-06)
- Online payment portal interface (addresses SN-040; enables JTBD-01)
- Audit trail and reporting dashboard for finance (JTBD-07, SN-008, SN-066 evidence)
- Customer guidance and communication standards (JTBD-04, SN-002 evidence)
- **Underlying infrastructure:** Unified case view, consolidated activity log, data reconciliation rules (prerequisite for SN-011 resolution and SN-085 status standardisation)

**Phase 2 candidates** (post-Phase 1 validation):
- Expanded self-service balance view (JTBD-01; depends on data quality improvement from Phase 1)
- Additional payment reminder channels (SMS, email automation; supports JTBD-06)
- Customer contact detail update portal (lower priority ROI at 470%, from Tab 5)
- Proactive outreach routing (SN-045: "contact strategy is reactive"; SN-077: "reach out in random order rather than strategic sequence")

**Assumptions to Validate in Phase 1 Pilot:**
1. Self-serve adoption reaches 15%+ (conservative case floor from Tab 6)
2. Promise-to-pay capture rate improves to at least 2% uplift (conservative downside test)
3. Agent handle time reduction achieves 6+ minutes per straightforward case (vs. 8 min target from Tab 2; testing friction)
4. Data reconciliation effort reduces by 50%+ for finance team (SN-123, SN-048 context)

**Dependencies & Pre-Requisites:**
- SN-085 status standardisation across teams (prerequisite for JTBD-03; affects data quality trust)
- Compliance sign-off on audit trail design (SN-060: "compliance team cannot approve anything until they see future process mapped out"; SN-066: "audit trails make it nearly impossible to demonstrate what happened")
- Agent communication plan addressing job security (SN-084, SN-097 mitigation)
