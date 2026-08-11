---
name: discovery-evidence-validation
description: |
  **USE WHEN:** Reviewing business analysis, discovery, or requirements documents to ensure findings are evidence-grounded, claims are traceable to sources, and facts/assumptions/recommendations are clearly distinguished.
  
  **PRODUCES:** Enhanced discovery brief with:
  - Each stakeholder concern linked to specific evidence quotes (e.g., SN-007, SN-040)
  - Identified gaps showing what's known vs. what's still uncertain
  - Clear distinction between observed facts, unstated assumptions, and forward-looking recommendations
  - Traceability matrix mapping pain points → metrics → deliverables
  
  **TYPICAL WORKFLOW:** Review case materials → identify gaps systematically → map evidence sources → enhance documents → surface blockers
---

# Evidence-Based Discovery Validation

Use this skill to audit business analysis, requirements, or discovery documents. Ensures every claim traces back to evidence, assumptions are explicit, and blockers are surfaced.

## When to Use This Skill

✅ **Use for:**
- Validating discovery briefs, problem statements, stakeholder analysis
- Ensuring requirements and recommendations are evidence-grounded
- Identifying gaps before moving to detailed design or delivery
- Distinguishing between observed facts (stakeholder quotes, data) vs. assumptions vs. recommendations
- Building traceability matrices for compliance, audit, or delivery handoff

❌ **Don't use for:**
- General content review or copyediting
- Creating discovery from scratch (use discovery templates directly)
- Technical feasibility assessment
- Solution design or architecture

## Step-by-Step Process

### Step 1: Gather Input Documents

**What you need:**
- Discovery brief or problem statement (draft or final)
- Source materials (interview transcripts, stakeholder notes, data exports)
- Any existing metrics or baseline data

**Questions to ask:**
- What's the discovery scope? (E.g., "debt recovery process," "customer onboarding flow")
- Do you have stakeholder interview quotes or notes?
- What data or metrics have been collected?

### Step 2: Systematic Gap Analysis

For each major claim or concern in the brief, audit:

| Element | What to Check | Example |
|---------|---|---|
| **Problem statement** | Is each issue sourced? Can you point to 2+ quotes showing it? | "Cases stuck in pending callback" — check SN-007, SN-053 |
| **Stakeholder concerns** | What does each stakeholder actually care about? What evidence would convince them? | Finance wants "transparent assumptions" — cite specific concerns about weak financial claims |
| **Discovery questions** | Is each question motivated by an evidence gap? | "Why are follow-ups lost?" — motivated by SN-040 (20% lost at handoff) |
| **Traceability** | Does each pain point map to a metric and a discoverable deliverable? | Missed follow-ups → handoff audit → As-Is process map with gaps highlighted |

### Step 3: Evidence Indexing

For each concern, build a table:

```
| Quote ID | Stakeholder | Quote | Theme | Confidence | Gap |
|---|---|---|---|---|---|
| SN-007 | Lawrence Bennett | "cases in 'awaiting callback' status for months..." | Missed follow-ups | HIGH | Who is responsible for enforcing callbacks? |
| SN-040 | Catherine Frost | "We lose at least 20% of follow-ups at shift handoff" | Missed follow-ups | HIGH | Why exactly 20%? What's the cost? |
```

**Mark evidence as:**
- **STRONG**: Direct quote from stakeholder experiencing the problem
- **PARTIAL**: Related observation but not direct evidence
- **MISSING**: Claim made but no evidence provided

### Step 4: Distinguish Facts, Assumptions, Recommendations

For each section of your document, clarify:

| Type | Definition | Example | How to Mark |
|------|-----------|---------|-----------|
| **FACT** | Observed data or direct quote from evidence | "20% of follow-ups lost at shift handoff" (SN-040) | Cite source: (SN-040) |
| **ASSUMPTION** | Unstated or inferred; treat as hypothesis | "Agents are slower because they use workarounds" (implied by SN-013, SN-072 but not measured) | Flag: *Assumption:* Handling time delay is caused by workarounds, not measured |
| **RECOMMENDATION** | Forward-looking action or design choice | "Process map should show compliance gates" (not yet observed, but needed) | Flag: *Recommendation:* Build risk mapping deliverable |

### Step 5: Identify Blockers

Surface concerns that could derail scope or feasibility:

**BLOCKER indicators:**
- "I cannot recommend X until..." (e.g., SN-019: cannot recommend automating until risks are mapped)
- "The team says they won't..." (resistance signals)
- "We have no way to..." (foundational missing capability)
- Compliance or regulatory gaps
- Prior change failure with trauma signals

**Action:** Create "Unresolved blockers" section in brief or discovery doc

### Step 6: Enhance Discovery Document

Update your brief or document with:

1. **Stakeholder table enhancements:**
   - Add specific evidence links (e.g., "What they care about: (SN-007, SN-040, SN-053)")
   - Add "Evidence they will trust" specifics

2. **Discovery questions with context:**
   - Add gap motivation for each question
   - Flag URGENT vs. HIGH vs. MEDIUM based on impact

3. **Traceability matrix:**
   - Link each pain point to evidence sources
   - Map to specific metrics (not just "handling time" but "average handling time by case type")
   - Specify deliverables (not just "process map" but "As-Is process map with callback enforcement gap highlighted")

4. **Assumption register:**
   - Explicit list of assumptions (especially in financial model)
   - Confidence levels for each

5. **Blockers section:**
   - What must be resolved before Phase 1 can proceed?
   - Who owns each blocker?

## Quality Checklist

✓ Does every stakeholder concern cite 2+ evidence sources?  
✓ Are "facts" sourced (quotes, data)?  
✓ Are "assumptions" explicitly labeled?  
✓ Are "recommendations" forward-looking, not disguised facts?  
✓ Does the traceability matrix show concrete metrics (not vague "time savings")?  
✓ Are compliance/risk gaps surfaced and mapped?  
✓ Are blockers named with owner and resolution path?  
✓ Would a skeptical stakeholder find this credible?  

## Example: Before & After

### BEFORE (Generic):
> **Stakeholder:** Operations leadership  
> **Concern:** Missed follow-ups  
> **Success measure:** Evidence of where automation can save agent time  

### AFTER (Evidence-grounded):
> **Stakeholder:** Operations leadership (Amina, Priya)  
> **Concern:** Missed follow-ups and callback enforcement (20% lost at shift handoff per SN-040, SN-105)  
> **Success measure:** Process maps showing failure points; shift handoff audit; follow-up completion rate baseline; evidence of automation savings in agent time  
> **What they will trust:** Baseline handling times; missed follow-up audit data; shift handoff documentation; agent time allocation breakdown  
> **Blocker:** SN-040/SN-105 quantify loss but don't explain root cause — need discovery on "why do callbacks get lost?"

## Common Gaps Found & How to Fix

| Gap Found | Why It Matters | How to Fix |
|-----------|---|---|
| Claims without evidence | Stakeholders won't believe it; wastes discovery time | Cite source or move to "assumptions" and add to discovery questions |
| Vague metrics | Can't measure success or validate Phase 1 | Replace "handling time" with "average handling time by case type (baseline: 18 min vs. 10-min target)" |
| Missing compliance layer | Risk of Phase 1 failing or introducing new problems | Add compliance stakeholder; map edge cases; create risk deliverable |
| Unexplained stakeholder tensions | Can cause scope creep or hidden resistance | Surface contradictions (e.g., "Daniel wants financial ROI, but Gareth fears complexity increases") |
| Assumptions in disguise | Financial model becomes unreliable; delivery delays | Flag assumptions with confidence levels; add sensitivity testing |
| No blockers identified | Phase 1 fails when hidden risks surface | Review stakeholder "main worry" column; look for "I cannot..." language |

## Example Prompts to Trigger This Skill

- "Review my discovery brief for evidence gaps. Show me what's sourced vs. assumed."
- "Check that each stakeholder concern in my brief is grounded in at least one interview quote."
- "Build a traceability matrix showing how my pain points map to metrics and deliverables."
- "Identify assumptions in my ROI model and create a sensitivity analysis structure."
- "Surface blockers in my discovery that could derail Phase 1 scope."
- "Validate that my problem statement is specific enough to build requirements from."

## Related Skills & Customizations to Create

- **TBA JTBD Prioritization** — Convert evidence-grounded pain points to Jobs-to-be-Done
- **Process Gap Analysis** — Map current state (As-Is) to problems; surface failure points
- **Financial Model Validation** — Ensure ROI model separates data, assumptions, formulas
- **Stakeholder Tension Mapping** — Identify conflicting priorities and resolution paths
- **Change Readiness Assessment** — Audit for adoption risks and prior change trauma signals
