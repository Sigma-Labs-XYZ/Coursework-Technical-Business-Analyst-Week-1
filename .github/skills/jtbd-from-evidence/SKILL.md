---
name: jtbd-from-evidence
description: |
  **USE WHEN:** Turning stakeholder interview quotes or observations into evidence-grounded Jobs-to-be-Done (JTBD) statements for discovery, prioritisation, and requirements work.

  **PRODUCES:** For each input: stakeholder, original quote/observation, underlying need, JTBD statement, and assumptions/uncertainties.

  **METHOD:** Extract context + need + desired outcome from evidence, keep solution-agnostic language, avoid feature rewording, flag low-evidence cases, and deduplicate overlapping jobs across quotes.
argument-hint: "Paste one or more stakeholder quotes and optional context"
user-invocable: true
---

# JTBD From Stakeholder Evidence

Use this skill to convert stakeholder evidence into concise, traceable, solution-agnostic JTBD statements.

Core rule: a JTBD must describe the underlying job, not the tool someone asked for.

## What This Skill Produces

For each input quote or observation, return:

1. Stakeholder
2. Original quote or observation
3. Underlying need
4. JTBD statement
5. Any assumptions or uncertainties

JTBD format:

When [situation/context], I want to [underlying job or need], so that [desired outcome].

## When to Use

Use for:
- Interview note analysis
- Discovery synthesis
- Building JTBD backlogs
- Preparing evidence-backed prioritisation

Do not use for:
- Writing solution requirements
- Defining product features
- Creating benefits claims without evidence

## Step-by-Step Workflow

### Step 1: Parse The Evidence Input

Capture the raw input exactly:
- Stakeholder name and role (if available)
- Quote or observation text
- Any nearby context (process stage, customer segment, metric)

If stakeholder is missing, label as Unknown stakeholder.

### Step 2: Separate Signal From Suggested Solution

Identify whether the quote includes a proposed tool or feature.

If the quote says "I need a dashboard" (or similar), do not use dashboard as the job. Extract the real job behind it (for example: reliable workload visibility to manage team decisions accurately).

Examples of solution language to strip from the job:
- dashboard
- portal
- spreadsheet
- automation
- system update

Rewrite mentally as need language:
- visibility
- control
- timely follow-up
- reliable records
- confident forecasting

### Step 3: Extract JTBD Components

For each quote, extract three parts:
- Situation/context: What condition triggers the need?
- Underlying job: What is the stakeholder trying to get done?
- Desired outcome: Why it matters in business terms?

Keep each component anchored to evidence from the quote/context.

### Step 4: Check Evidence Strength Before Finalising

Rate confidence using these checks:
- Source consistency: repeated by multiple stakeholders or only one?
- Specificity: concrete details/numbers or generic frustration?
- Directness: directly observed experience or inferred/secondhand?

If evidence is weak, still provide a draft JTBD but clearly flag assumptions/uncertainties.

### Step 5: Build The JTBD Statement

Use the exact pattern:

When [situation/context], I want to [underlying job or need], so that [desired outcome].

Quality rules:
- Use concise business language.
- Keep solution-agnostic wording.
- Do not make the job about implementing a specific tool.
- Do not invent outcomes not present or reasonably implied by evidence.
- If the statement still names a tool as the job, rewrite it before returning output.

### Step 6: Deduplicate Across Multiple Quotes

When processing multiple quotes:
- Merge quotes into one JTBD if they express the same underlying job.
- Keep separate JTBDs only when context, need, or outcome materially differs.
- Reference supporting quote IDs or stakeholders under assumptions/uncertainties.

## Output Format

Use this structure for each item:

- Stakeholder: <name/role>
- Original quote or observation: <verbatim or near-verbatim>
- Underlying need: <plain-language need>
- JTBD statement: When ..., I want to ..., so that ...
- Assumptions or uncertainties: <none, or explicit gaps needing validation>

## Decision Rules And Branching

- If quote is feature-request-heavy:
  - Translate to need language first.
  - Reject feature wording in final JTBD.

- If quote has low direct evidence:
  - Add explicit uncertainty note.
  - Mark what validation is needed.

- If multiple quotes overlap:
  - Produce one JTBD with multiple supporting references.
  - Do not create duplicate JTBD entries.

## Quality Checklist

- Is the JTBD grounded in the provided evidence?
- Is it written in the required When/I want/so that structure?
- Is it solution-agnostic?
- Does it capture need, not requested feature?
- Are assumptions clearly flagged where evidence is thin?
- Have overlapping quotes been merged where appropriate?
- If the quote mentions a tool, did we translate to the deeper job before writing the JTBD?

## Example Inputs And Outputs

### Example 1: Single quote with implied need

Input:
- Stakeholder: Lawrence Bennett (Collections Agent)
- Quote: We have cases sitting in pending callback for months because the callback date was never enforced.

Output:
- Stakeholder: Lawrence Bennett (Collections Agent)
- Original quote or observation: We have cases sitting in pending callback for months because the callback date was never enforced.
- Underlying need: Reliable follow-up ownership and callback control.
- JTBD statement: When callbacks are scheduled across shifts, I want clear ownership and enforced callback dates, so that cases do not stall and recoveries are not delayed.
- Assumptions or uncertainties: Assumes handoff control is a main cause of delay; validate with shift-level handoff data.

### Example 2: Quote includes requested solution

Input:
- Stakeholder: Daniel Farmer (Finance Analyst)
- Quote: We need a dashboard so I can trust the numbers and forecast recovery revenue.

Output:
- Stakeholder: Daniel Farmer (Finance Analyst)
- Original quote or observation: We need a dashboard so I can trust the numbers and forecast recovery revenue.
- Underlying need: Timely and reliable performance data for planning.
- JTBD statement: When planning recovery performance, I want reliable and up-to-date activity data, so that I can forecast revenue with confidence.
- Assumptions or uncertainties: Dashboard request treated as proposed solution, not the job itself.

### Example 4: Dashboard request mapped to deeper job

Input:
- Stakeholder: Operations Manager
- Quote: I need a dashboard so I can see self-serve and agent-routed work.

Output:
- Stakeholder: Operations Manager
- Original quote or observation: I need a dashboard so I can see self-serve and agent-routed work.
- Underlying need: Reliable visibility of workload split and flow.
- JTBD statement: When I review team workload, I want reliable visibility of self-serve and agent-routed cases, so that I can manage the team accurately.
- Assumptions or uncertainties: Assumes current visibility is fragmented; validate by checking current reporting latency and completeness.

### Example 3: Multiple quotes support one job

Input:
- Stakeholder A: Jacqueline Norris (Operations Analyst)
- Quote A: There is no standard definition of what each status means.
- Stakeholder B: Sarah Mitchell (Collections Agent)
- Quote B: Different teams use statuses differently.

Output:
- Stakeholder: Jacqueline Norris (Operations Analyst), Sarah Mitchell (Collections Agent)
- Original quote or observation: There is no standard definition of what each status means. Different teams use statuses differently.
- Underlying need: Shared status definitions across teams.
- JTBD statement: When managing cases across teams, I want a shared and consistent meaning for each status, so that handoffs, reporting, and decisions are accurate.
- Assumptions or uncertainties: Combined into one JTBD because both quotes indicate the same underlying job.

## Example Prompts To Trigger This Skill

- Turn these interview notes into evidence-grounded JTBD statements and flag weak assumptions.
- Convert these 10 stakeholder quotes into deduplicated JTBDs with uncertainties.
- From these discovery notes, extract underlying needs and write solution-agnostic JTBDs.

## Related Skills To Create Next

- JTBD Prioritisation Scoring: Impact, urgency, and frequency scoring of JTBD backlog.
- JTBD-to-Requirements Mapper: Convert validated JTBDs into testable requirement statements.
- Assumption Validation Planner: Create validation tests for low-confidence JTBD assumptions.
