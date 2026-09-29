# Recommendation

## Ranked Opportunities

| Rank | Opportunity | Effort | Conservative ROI | Optimistic ROI | Phase 1 |
| --- | --- | --- | --- | --- | --- |
| 1 | OP-01 Self-serve account summary | 3 | 170% | 449% | Yes |
| 2 | OP-05 Automated payment status check | 2 | 70% | 1,313% | Yes |
| 3 | OP-04 Rules-based routing and claiming | 4 | 80% | 266% | Yes |
| 4 | OP-02 Digital promise-to-pay capture | 4 | 35% | 1,304% | Defer |
| 5 | OP-03 Automated follow-up and reminders | 2 | −15% | 2,206% | Defer |

Ranked on the conservative case. The optimistic column is shown to make the swing visible. OP-03 moves from last to first on one unvalidated assumption, which is why it is not driving the ranking.

## Recommendation Summary

Phase 1 should take OP-01, OP-05 and OP-04. There is also a prerequisite that blocks any self-service routing. SN-070 says vulnerable customers are not flagged differently, and no field in the export identifies them, so the routing rule cannot exclude them today. All three pay back inside twelve months in the conservative case, without relying on any revenue uplift. OP-01 has the strongest return of the three and needs only a read-only screen. OP-05 is the cheapest thing on the list and removes a check nobody should be doing by hand. OP-04 has the best evidence behind it — `duplicate_check_flag = Y` on 20.4% of activity rows is counted, not estimated — and it fixes the cause of duplicate outreach rather than the symptom, which is what Gareth asked for. OP-04 carries higher effort than its return alone would justify, and it is included because the evidence is the firmest and the problem is structural.

OP-02 and OP-03 are deferred, but not dropped. Both look extraordinary in the optimistic case and neither stands up in the conservative one. OP-03 is negative on its own numbers while being the mechanism that would deliver OP-02's uplift, so they only make sense scoped together. Before either enters a build, finance needs to say how the 2.5% uplift was arrived at. For Week 2 this means scope is set by the three conservative winners, and the first analysis task is closing the two open questions: the straightforward-share disagreement with Amina, and the basis for A-08 with Daniel.