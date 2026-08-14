# ROI Modelling

## Workbook

All tabs live in `TBA W1 Data`. CSV exports are committed in `phase_4/tables` so the figures are readable without the Sheet.

| Tab | What it holds |
| --- | --- |
| [Assumptions](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=75137262#gid=75137262) | Every input not counted from data, with source and confidence |
| [Baseline Metrics](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=664448429#gid=664448429) | Values counted from the sample datasets |
| [Conservative Opportunities](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1844585565#gid=1844585565) | Opportunity inputs, hard savings only |
| [Optimistic Opportunities](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1552544905#gid=1552544905) | Opportunity inputs including revenue uplift |
| [Conservative ROI Summary](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=1686948848#gid=1686948848) | Ranked output, conservative case |
| [Optimistic ROI Summary](https://docs.google.com/spreadsheets/d/1s_VAkF6BfqbuDBFMO-3JWp2epwHLnhYLYTk04nKr3CY/edit?gid=467308915#gid=467308915) | Ranked output, optimistic case |

## How the model is built

Anything in Baseline Metrics was counted from `recovery_activity_tracker` or `delinquent_accounts_export`. Anything in Assumptions was supplied by finance or derived by me, and carries a source and a confidence level.

Formulas used:

- Annual hours saved = monthly case volume × straightforward share × minutes saved per case × 12 ÷ 60
- Annual cost saved = annual hours saved × agent hourly cost (A-01)
- Annual revenue uplift = monthly recovery baseline × 12 × uplift rate × attribution share
- Net benefit = annual total benefit − implementation cost
- 12-month ROI = net benefit ÷ implementation cost
- Payback months = implementation cost ÷ (annual total benefit ÷ 12)

Effort scale:

1. Configuration only, no new interface
2. Single rule or scheduled job reading existing data
3. New customer-facing screen, read-only
4. Customer-facing write-back, or new routing logic in the legacy system
5. Multi-system change requiring compliance sign-off

## Things worth flagging

The straightforward-case share is contested:
Finance assumed 0.38 (A-03). The accounts export flags 77.4% of accounts as `self_service_candidate = Y` with `risk_flag = N` (A-04). That is a factor of two on the input that drives every volume figure. Both are carried through as the conservative and optimistic levers rather than picking one. 

Missed follow-up rate is where estimate and observation agree: Finance held 0.14; the data gives 0.148 (B-05). That corroboration is what makes the rest of the model credible, and it is why the disagreement above reads as a finding rather than as bad data.

Everything counted is sample-scale:
3,246 accounts against a stated population of more than 100,000, so a scaling factor of 30.8 (A-13). Scaled, B-04 becomes roughly 216 admin hours per day, which against 50-plus agents is over half of all capacity. Treat that figure as an upper bound until the sample is confirmed representative.

Monthly case volume is the weakest input:
A-12 (45,700) is derived from 3,214 distinct accounts over 66 days, then scaled. Two inference steps, Low confidence, and every hours-saved figure depends on it.

Some baseline metrics support pain points rather than the model:
B-06 sizes PP-003, B-07 sizes PP-006, B-08 sizes PP-001. They are evidence for the Phase 3 overlay, not ROI inputs.

## Scenario testing

Two levers change between the cases. The method is identical in both.

| Lever | Conservative | Optimistic |
| --- | --- | --- |
| Straightforward case share | 0.38 (finance estimate) | 0.774 (observed) |
| Promise-capture uplift | 0 | 0.025 (finance estimate) |

The conservative case counts hard savings only - agent time removed, priced at A-01. No revenue uplift is claimed. The optimistic case adds the uplift and splits it 40/40/20 across OP-02, OP-03 and OP-05, because capture, enforcement and detection are one chain and none delivers the benefit alone.

| | Conservative ROI | Optimistic ROI |
| --- | --- | --- |
| OP-01 Self-serve account summary | 170% | 449% |
| OP-02 Digital promise-to-pay capture | 35% | 1,304% |
| OP-03 Automated follow-up and reminders | −15% | 2,206% |
| OP-04 Rules-based routing and claiming | 80% | 266% |
| OP-05 Automated payment status check | 70% | 1,313% |

The ranking inverts:
OP-03 is worst in one case and best in the other, on no new evidence. — the entire swing comes from one Low-confidence assumption. OP-01 and OP-04 pay back in both cases, and their returns rest on counted figures.

That is the useful result. It separates opportunities that are worth doing regardless from opportunities that are only worth doing if finance's uplift estimate holds.

## Recommendation

Phase 1 should take OP-01, OP-05 and OP-04. All three pay back inside twelve months in the conservative case, without relying on any revenue uplift. OP-01 has the strongest return of the three and needs only a read-only screen. OP-05 is the cheapest thing on the list and removes a check nobody should be doing by hand. OP-04 has the best evidence behind it — `duplicate_check_flag = Y` on 20.4% of activity rows is counted, not estimated — and it fixes the cause of duplicate outreach rather than the symptom, which is what Gareth asked for. OP-04 carries higher effort than its return alone would justify, and it is included because the evidence is the firmest and the problem is structural.

OP-02 and OP-03 are deferred, but not dropped. Both look extraordinary in the optimistic case and neither stands up in the conservative one. OP-03 is negative on its own numbers while being the mechanism that would deliver OP-02's uplift, so they only make sense scoped together. Before either enters a build, finance needs to say how the 2.5% uplift was arrived at. For Week 2 this means scope is set by the three conservative winners, and the first analysis task is closing the two open questions: the straightforward-share disagreement with Amina, and the basis for A-08 with Daniel. There is also a prerequisite that blocks any self-service routing — SN-070 says vulnerable customers are not flagged differently, and no field in the export identifies them, so the routing rule cannot exclude them today.