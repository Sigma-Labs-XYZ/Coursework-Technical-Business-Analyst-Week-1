# ROI Modelling Guide

## ROI model spreadsheet
[ROI model](https://docs.google.com/spreadsheets/d/13X9shDs3kk0TCBXhh22O_8N7N4BIemz1xmRbUKPmzqY/edit?usp=sharing)

## How the model is built
The model is built on observed operational data and structured financial parameters to ensure full traceability and defensibility. It is designed to be flexible, so you can test different assumptions and scenarios to see how they affect the ROI. Baseline metrics are derived from the recovery_activity_tracker.csv and delinquent_accounts_export.csv. Assumptions are supplied by Finance in the finance_assumptions.csv or derived from the observed data, each mapped with a clear source and confidence level.

### Formulas used:

- Annual hours saved = monthly case volume x minutes saved per case x 12 / 60
- Annual cost saved = annual hours saved x hourly cost
- Net benefit = annual total benefit - implementation cost
- ROI % = net benefit / implementation cost x 100
- Payback months = implementation cost / (annual total benefit / 12)

## Scenario testing

### Optimistic scenario
Under the baseline model using 100% of the Finance team's target recovery uplift rates (4% for plan section and 2.5% for promise capture) alongside full labour cost savings, the initiative delivers £6.29M in total annual benefit. Against a combined £175K implementation cost, this generates a 3495% 12-month ROI and a payback period of 0.33 months (~10 days).

### Conservative scenario
The top line recovery-uplift carries lower confidence because it relies on external customer adoption. Therefore, a conservative scenario helps stress-test the model by applying a 90% reduction to the recovery-uplift assumptions (counting on 10% realisation). Even under these cautious assumptions, the Self-Service Portal bundle alone delivers over £640K in total annual benefit, maintaining a 653% ROI and a payback period of just 1.6 months. This proves the business case remains overwhelmingly positive and low-risk for Phase 1, even if initial customer adoption is far slower than anticipated.


## Recommendations

Phase 1 should proceed with OPP-01 (Self-Serve Account Summary), OPP-05 (Automated Audit Trail) and OPP-04 (Automated Case Routing). All 3 pay back in under 1.6 months in the conservative scenario, without relying on speculative revenue uplift.

OPP-01 has the strongest return of the 3 as it delivered over £640k in conservative annual benefit and achieving full payback in 1.6 months on its £85k implementation cost. OPP-05 is is the cheapest item on the list with its implementation cost of £45k and eliminates 3.31 daily hours per agent spent on manual spreadsheet reconciliation and status-checking. Moreover, OPP-05 reduces audit exposure as the transition from manual spreadsheet reconciliation to an automated audit trail removes the worry behind regulatory vulnerability. OPP-04 is the most complex to implement, but it has the strongest operational evidence as the recovery_activity_tracker.csv shows 3.10 daily hours lost to manual triage waste. OPP-04 fixes the root cause of duplicate outreach rather than the symptom, creating the explicit hand-off rules that Gareth asked for to keep complex, high-balance or vulnerable accounts from blocking straightforward cases. It also enables the self-service portal to work effectively, so it is a critical enabler for Phase 1.

OPP-02 (Direct Payment Processing) and OPP-03 (Automated Promise-to-Pay) look good on paper under optimistic adoption rates, but they are more speculative because they rely on customer adoption. OPP-03 relies on OPP-01 to work effectively so we shouldn't treat them as separate, standalone builds. Instead, we bundle them into the core OPP-01 portal build, which is why the ROI model shows them as a single line item. OPP-02 is a nice-to-have, but it is not essential to Phase 1 and can be deferred until Phase 2.
