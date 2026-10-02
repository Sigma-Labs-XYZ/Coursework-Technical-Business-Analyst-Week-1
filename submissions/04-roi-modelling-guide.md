# ROI Modelling Guide

This guide helps you turn Week 1 discovery into a value-ranked opportunity model.


Workbook: https://docs.google.com/spreadsheets/d/17-aPlFpUJFySb_8Vu_5VZOmI08mEghXmzWSRNRgF4ug/edit?gid=0#gid=0

## Recommended workbook tabs

1. Assumptions
2. Baseline Metrics
3. Opportunities
4. Calculations
5. ROI Summary
6. Sensitivity Analysis

## Core modelling rule

Always separate:
- observed data
- assumptions
- formulas
- recommendation logic

## Opportunity ideas you can model

- self-serve balance and arrears view
- contact detail confirmation or update request
- digital promise-to-pay capture
- eligible payment-plan selection
- rules-based routing to representatives
- portal interaction history for representatives
- automated follow-up reminders

## Simple formulas

- Annual hours saved = monthly case volume x minutes saved per case x 12 / 60
- Annual cost saved = annual hours saved x hourly cost
- Net benefit = annual total benefit - implementation cost
- ROI % = net benefit / implementation cost
- Payback months = implementation cost / monthly benefit

## Benefit types to keep separate

| Benefit type | What it means | Example |
|---|---|---|
| Hard savings | More directly reducible cost | reduced admin effort |
| Revenue uplift | Improved collections performance | better promise capture or plan uptake |
| Soft benefit | Useful but less cashable | better visibility, lower friction |

## Scenario testing

At minimum, create:
- conservative case
- optimistic case

## Final recommendation prompt

Which Opportunities Best Suit Phase 1 & Why They Rank Highly:

The opportunities that best suit Phase 1 are Self-Service Balance Lookup (OPP-01), Automated Payment Plan Selection (OP-02), and Promise-to-Pay Confirmation (OP-03), powered by Automated Queue Triage (OP-04). These items rank at the top because they solve the biggest daily headaches for both customers and staff while keeping the technology simple. Balance lookup and payment plan setup target the 38% of accounts that are simple and early-stage. They give customers an easy way to check what they owe and pay online without waiting on hold, which immediately takes thousands of phone calls off the team. Meanwhile, queue triage acts as the brain in the background, automatically steering these simple cases to the portal so representatives only have to handle complex or sensitive cases.
From a practical perspective, this combination satisfies all key stakeholders. For Priya, the technology is feasible and cheap to build, with low starter costs (£45,000 to £85,000 per tool). For Amina, it removes the heavy admin work, like checking three different sheets to see if a customer was called, so her team can focus on helping people who genuinely need human support. For Daniel in Finance, the financial return is safe. Even in our conservative scenario where fewer customers use the portal than expected, the time saved by staff pays back the setup costs in under two months, meaning the bank does not have to rely on risky guesses about extra revenue to justify the spend.   

Which Lower-Ranked Items to Defer:

We should defer Automated Shift Handoff & Audit Trail Logging (OP-05) to a later phase for 2 main reasons:
1. OP-05 is an internal back-office improvement. While it helps with team organization and audit compliance, it does not directly reduce incoming customer call volumes or help customers pay off their debt online.
2. In Phase 1, the bank's main goal is to reduce representative handling time and cut call queues using customer self-service. Therefore, OP-05 is deferred to Phase 2 so the team can focus on getting the core customer portal right first.  

What the Results Imply for Week 2 Scope:

These findings show that our Week 2 project scope must focus tightly on the customer portal experience and basic background routing. We do not need to build a complicated system that tries to automate every single customer situation. Instead, Week 2 design work should concentrate on three core deliverables: building a simple digital interface for balance checks and payment plans, setting up automated SMS and email reminders for promise dates, and creating clear safety rules that instantly transfer hardship or disputed cases to a human agent. Keeping Week 2 focused on these core tools guarantees a quick, safe, and profitable rollout.