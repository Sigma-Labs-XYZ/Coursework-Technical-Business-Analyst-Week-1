# ROI Model Quick Reference

One-page reference for formulas, decisions, and checks while building your model.

---

## Formula Cheat Sheet

**Copy-paste these formulas into your ROI CSVs:**

### Annual Hours Saved
```
Annual Hours Saved = (Monthly Case Volume × Minutes Saved Per Case × 12 months) ÷ 60 minutes/hour
```
Example: (3,540 cases × 3 min × 12) ÷ 60 = 2,124 hours/year

### Annual Cost Saved
```
Annual Cost Saved = Annual Hours Saved × Hourly Agent Cost
```
Example: 2,124 hours × £22/hour = £46,728/year

### Total Annual Benefit
```
Total Benefit = Cost Saved + Revenue Uplift + Soft Benefits (if quantified)
```
Example: £46,728 + £200,000 = £246,728

### Net Benefit
```
Net Benefit = Total Benefit - Implementation Cost
```
Example: £246,728 - £25,000 = £221,728

### ROI Percentage
```
ROI % = (Net Benefit ÷ Implementation Cost) × 100
```
Example: (£221,728 ÷ £25,000) × 100 = 887%

### Payback Months
```
Payback Months = Implementation Cost ÷ (Monthly Benefit)
```
Where Monthly Benefit = Total Benefit ÷ 12

Example: £25,000 ÷ (£246,728 ÷ 12) = 1.4 months

### Effort Score (Lower is Better)
```
Effort Score = Implementation Cost ÷ Total Benefit
```
Example: £25,000 ÷ £246,728 = 0.10 (10% effort relative to benefit)

Interpretation:
- <20% = Low effort (good ROI-to-effort ratio)
- 20-50% = Medium effort
- >50% = High effort (not recommended unless strategic necessity)

---

## Decision Tree: Which CSV to Use?

### For Baseline Metrics (02-baseline-metrics.csv)

**Q: What's the current account volume?**
→ Source: delinquent_accounts_export.csv → COUNT rows

**Q: How many cases are straightforward?**
→ Source: delinquent_accounts_export.csv → COUNT WHERE delinquency_stage='early'

**Q: How long does an activity take?**
→ Source: recovery_activity_tracker.csv → AVG(minutes_spent)

**Q: What's the admin overhead?**
→ Source: recovery_activity_tracker.csv → COUNT WHERE duplicate_check_flag='Y' ÷ total

**Q: How many cases have missing follow-up dates?**
→ Source: recovery_activity_tracker.csv → COUNT WHERE next_follow_up_date IS NULL ÷ total

---

### For Assumptions (01-assumptions.csv)

**Q: What's the agent hourly cost?**
→ Source: finance_assumptions.csv (FA-01) → Copy value & mark confidence as "High"

**Q: What's the straightforward case percentage?**
→ Source: finance_assumptions.csv (FA-03) → Copy value & mark confidence as "Medium"

**Q: What time will be saved per case?**
→ Sources: (1) Current baseline (B-03) + (2) Process re-design estimate
→ Mark confidence as "Medium" if estimated; "High" if validated by pilot

**Q: What's the recovery uplift from this opportunity?**
→ Source: finance_assumptions.csv (FA-07, FA-08) → Copy & mark confidence as "Low"
→ **Decision:** Use in base case only if confidence is Medium+; use Low-confidence uplifts only in optimistic scenario

---

## Confidence Level Decision Matrix

**Use this to decide if an assumption goes in Base Case or only Optimistic Scenario:**

| Confidence | Definition | Base Case | Optimistic | Low-Risk Status |
|---|---|---|---|---|
| **High** | Observed data or Finance workbook; validated across sources | ✓ Yes | ✓ Yes | Safe to present to leadership |
| **Medium** | Operations estimate or stakeholder feedback; reasonable but not tested | ✓ Yes | ✓ Yes | Present but note dependency |
| **Low** | Scenario estimate; untested assumption; requires pilot validation | ✗ No | ✓ Yes | Use for sensitivity; plan to test |
| **Very Low** | Speculative; no evidence; requires major assumption | ✗ No | ✗ No | Do not use; mark for future pilot |

---

## Scenario Testing Decision Tree

**When to test Conservative vs. Optimistic:**

```
┌─ Is the opportunity dependent on an UNTESTED assumption?
│
├─ YES (e.g., "recovery uplift = 4%")
│  ├─ Build 3 scenarios: Conservative, Base, Optimistic
│  └─ Show range to Finance & Compliance
│
└─ NO (e.g., "time saved = 2 min" where we measured baseline at 7.2 min)
   └─ Build 2 scenarios: Base, Optimistic
      (Conservative = do nothing; not interesting)
```

### For Each Scenario, What Changes?

| Scenario | Time Saved | Uplift | Implementation | Notes |
|----------|-----------|--------|---|---|
| **Conservative** | -30% from base | -50% from base | Same cost | Realistic if adoption is low |
| **Base** | As estimated | As estimated | As planned | Most likely outcome |
| **Optimistic** | +30% from base | +50% from base | Same cost | Best case if execution is excellent |

---

## Benefit Type Classification Checklist

Before finalizing your opportunity, mark each benefit:

**Hard Savings (Cost Reduction):**
- ✓ Include in ROI formula
- ✓ Directly from time × cost calculation
- Examples: Agent time saved, admin overhead eliminated, training cost avoided

**Revenue Uplift (New Money):**
- ✓ Include in ROI formula
- ✓ Usually from improved collection rate or faster case resolution
- ⚠ Mark confidence carefully (is uplift tested?)
- Examples: 2.5% recovery uplift on £8M baseline = £200K/year

**Soft Benefits (Real but Hard to Quantify):**
- △ Mention but don't include in ROI formula (unless you can quantify)
- ✓ Note in "soft_benefit_note" column
- Examples: "Better compliance audit trail," "Reduced customer friction," "Faster case closure," "Improved staff satisfaction"
- 💡 Tip: If Finance pushes back on revenue uplift, you can fall back on hard savings only

---

## Prioritization Scoring Checklist

Before finalizing your ranking, ask:

**ROI Score – Does this opportunity deliver financial return?**
- [ ] 3 pts: ROI > 100% (more than 1:1 return on investment)
- [ ] 2 pts: ROI 50-100% (reasonable return but slower payoff)
- [ ] 1 pt: ROI < 50% (low return; consider if strategic necessity)

**Payback Score – Will we see cash back quickly?**
- [ ] 3 pts: Payback < 3 months (fast cash recovery)
- [ ] 2 pts: Payback 3-6 months (medium-term return)
- [ ] 1 pt: Payback > 6 months (slow; requires patience or strategic commitment)

**Confidence Score – How sure are we this will work?**
- [ ] 3 pts: High confidence (all assumptions Medium+ confidence)
- [ ] 2 pts: Medium confidence (mix of High/Medium assumptions)
- [ ] 1 pt: Low confidence (multiple Low-confidence assumptions; requires testing)

**Effort Score – Can we implement this without breaking other work?**
- [ ] 3 pts: Low effort (implementation cost < 20% of benefit)
- [ ] 2 pts: Medium effort (implementation cost 20-50% of benefit)
- [ ] 1 pt: High effort (implementation cost > 50% of benefit; risky)

**Total Weighted Score:**
(ROI × 0.35) + (Payback × 0.25) + (Confidence × 0.25) + (Effort × 0.15)

Target: Score > 2.0 for Phase 1

---

## Common Traps & How to Avoid

| Trap | Example | How to Avoid |
|------|---------|---|
| **Mixing data + assumptions** | "Agents save 5 min per case" (doesn't say: 2 min measured, 3 min assumed) | Separate B-03 (observed 7.2 min) from A-04 (assumed 3 min savings) |
| **Using untested uplift in base case** | Recovery uplift 4% (Low confidence) in primary ROI | Put Low-confidence uplifts in Optimistic scenario only; base case uses 1% or £0 |
| **Ignoring implementation reality** | ROI says £500K benefit but doesn't account for 6-month integration delay | Calculate payback starting from actual go-live date, not day 1 |
| **All opportunities in Phase 1** | "All 5 have positive ROI, let's do all" | Sequence by dependencies; do foundational (OP-05) before dependent (OP-01) |
| **No sensitivity testing** | One ROI model, submitted to Finance as fact | Always test Conservative & Optimistic; show what assumptions matter most |
| **Vague soft benefits** | "Better compliance" (not quantified) | Either quantify (e.g., "£50K audit cost saved") or exclude from ROI; acknowledge separately in recommendation |
| **Ignoring pilot risk** | Promise capture assumed to have 4% uplift from day 1 | Run as supervised pilot; measure first; scale after validation |

---

## Phase 1 Readiness Checklist

Before submitting your ROI model to Finance, confirm:

**Data & Assumptions:**
- [ ] Every baseline metric (B-01 through B-05) is sourced from an operational CSV
- [ ] Every assumption (A-01 through A-05) has a confidence level and justification
- [ ] High-confidence assumptions are from Finance workbook or observed data
- [ ] Low-confidence assumptions are marked for pilot testing

**Opportunity Evaluation:**
- [ ] All 5 opportunities have been evaluated (or documented why not applicable)
- [ ] Time savings are calculated using B-03 baseline or justified differently
- [ ] Cost savings are calculated using A-01 agent cost (£22/hr)
- [ ] Revenue uplifts are sourced from finance_assumptions.csv or marked as scenario-only

**ROI Calculations:**
- [ ] ROI % formula is consistent across all opportunities
- [ ] Payback months are calculated from monthly benefit (not annual)
- [ ] Effort scores are calculated and range makes sense (0.10 = low, 0.80 = high)
- [ ] Conservative AND Optimistic scenarios exist for high-risk opportunities

**Prioritization:**
- [ ] Weighted scoring is applied consistently (35% ROI + 25% Payback + 25% Confidence + 15% Effort)
- [ ] Top 3 opportunities are clearly marked for Phase 1
- [ ] Dependencies are documented (e.g., "OP-01 depends on OP-05 completion")
- [ ] Soft benefits are mentioned (even if not in ROI formula)

**Recommendation:**
- [ ] Recommendation explains which opportunities are Phase 1 and why
- [ ] Recommendation acknowledges risks and what will be measured to test assumptions
- [ ] Recommendation identifies which deferred opportunities are Phase 2
- [ ] Recommendation explains Week 2 scope: budget, timeline, success metrics

---

## Links to Resources

- **Baseline Metrics Template:** [02-baseline-metrics.csv](../templates/roi-model/02-baseline-metrics.csv)
- **Assumptions Template:** [01-assumptions.csv](../templates/roi-model/01-assumptions.csv)
- **Opportunities Template:** [03-opportunities.csv](../templates/roi-model/03-opportunities.csv)
- **ROI Summary Template:** [04-roi-summary.csv](../templates/roi-model/04-roi-summary.csv)

- **Operational Data Sources:**
  - [data/delinquent_accounts_export.csv](../../data/delinquent_accounts_export.csv) – Account volume
  - [data/finance_assumptions.csv](../../data/finance_assumptions.csv) – Costs & assumptions
  - [data/recovery_activity_tracker.csv](../../data/recovery_activity_tracker.csv) – Activity times & duplicates
  - [data/smart_recovery_portal_events.csv](../../data/smart_recovery_portal_events.csv) – Portal adoption
  - [data/stakeholder_interview_notes.csv](../../data/stakeholder_interview_notes.csv) – Pain points & priorities

- **Discovery Guides:**
  - [/stakeholder-to-jtbd skill](../skills/stakeholder-to-jtbd/SKILL.md) – How to identify JTBD statements
  - [/analyze-csv-as-business-analyst skill](../skills/analyze-csv-as-business-analyst/SKILL.md) – How to extract data insights
