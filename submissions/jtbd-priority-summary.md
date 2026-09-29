# Stakeholder Unmet Needs Rating Matrix & Justification Analysis
**Smart-Recovery Initiative — Legacy Trust Bank**

---

## 1. Stakeholder Unmet Needs Rating Matrix

The matrix below evaluates the key stakeholder roles, their primary unmet jobs/needs, and rates them across **Frequency of Evidence**, **Business Impact**, and **Relevance to the Portal** (High / Medium / Low), establishing the priority order for Phase 1 release.

| JTBD ID | Stakeholder Role | Primary Unmet Need / Job | Frequency of Evidence | Business Impact | Relevance to Portal | Priority Level |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: |
| **JTBD-01** | **Customer (Debtor)** | **Self-Service Balance Confirmation & Repayment Setup** | **High**<br>(8 notes, 2,507 candidate accounts [77.2%]) | **High**<br>(+4% recovery uplift, £300k annual benefit) | **High**<br>(Core primary portal workflow) | **Top Priority (#1)** |
| **JTBD-02** | **Collections Agent** | **Automated Cross-Channel Sync & Duplication Elimination** | **High**<br>(18 notes, 2,020 duplicate activities [20.4%]) | **High**<br>(Saves 230.1 agent hours, £5k lost labor/sample) | **High**<br>(Automated real-time event updates) | **Top Priority (#2)** |
| **JTBD-03** | **Operations Manager** | **Automated Case Triage & Queue Escalation** | **High**<br>(11 notes, 1,742 early-stage accounts [53.7%]) | **High**<br>(Reduces handling time 18 $\to$ 10 mins) | **High**<br>(Pre-agent digital filtering layer) | **Top Priority (#3)**|
| **JTBD-04** | **Finance Partner** | **Digital PTP Capture & Multi-Channel Written Confirmation** | **Medium**<br>(2 notes, 1,231 portal agent fallbacks) | **High**<br>(+2.5% PTP recovery uplift, £115k benefit) | **High**<br>(Automated SMS/email receipt generator) | **High** |
| **JTBD-05** | **Compliance Liaison** | **Tamper-Proof Centralized Audit Logging** | **High**<br>(15 notes, 4 disconnected channel systems) | **Medium**<br>(Mitigates regulatory fines & QA audit overhead) | **Medium**<br>(Backend audit log dependency) | **Medium** |
| **JTBD-06** | **Service Design Lead** | **Unified Customer MDM & API System Integration** | **Medium**<br>(16 notes, £500k estimated annual lost recovery) | **Medium**<br>(Fixes long-term data architecture debt) | **Medium**<br>(Enabling infrastructure foundation) | **Medium** |

---

## 2. Justification Analysis for Top 3 Unmet Jobs

### Unmet Job #1: Customer Self-Service Balance Confirmation & Repayment Setup (Customer / Debtor)
* **Why it Matters Now:**  
  Over **53.67% of delinquent accounts (1,742 accounts)** sit in early-stage delinquency (£14.26M balance exposure), where fast digital nudges prevent default escalation. Currently, **48.45% of portal users (1,231 journeys)** drop back to human agents because the portal lacks custom payment arrangement options.
* **Supporting Evidence:**  
  * `delinquent_accounts_export.csv`: **2,507 accounts (77.23% of delinquent volume)** are qualified self-service candidates (`self_service_candidate = 'Y'`).
  * `finance_assumptions.csv`: Assumption `FA-07` establishes a **+4.0% recovery uplift** on self-service plan selection, generating **£300,000 in gross annual benefit** (£215,000 net 12M P&L impact).
* **Phase 1 Scope Influence:**  
  Must be the **core primary feature** in Phase 1 (Rank #1 in Excel ROI model with a 3.4-month payback period).

---

### Unmet Job #2: Automated Cross-Channel Sync & Duplication Elimination (Collections Agent)
* **Why it Matters Now:**  
  Frontline collections capacity is severely throttled by manual spreadsheet re-keying and status checks. Agents waste **20.42% of their time on redundant administrative tasks**, driving agent burnout and causing customers to be called repeatedly regarding promised callbacks.
* **Supporting Evidence:**  
  * `recovery_activity_tracker.csv`: Confirms **2,020 duplicate activities** consuming **13,806 agent minutes (230.1 hours)**.
  * Task Analysis: **100% of all duplicate activity** comes from `spreadsheet_reconcile` (72.29% duplicate rate) and `status_check` (69.00% duplicate rate).
* **Phase 1 Scope Influence:**  
  The Phase 1 portal must incorporate an **automated real-time status update engine** that writes directly to the core database upon portal action, completely removing manual spreadsheet reconciliation from agent workflows.

---

### Unmet Job #3: Digital Promise-to-Pay (PTP) Capture & Written Plan Confirmation (Finance Partner / Customer)
* **Why it Matters Now:**  
Without automated priority logic, straightforward cases and complex hardship situations are dumped into unified manual queues, causing simple tasks that should take minutes to stall for days. This queue clogging directly impacts **1,742 early-stage accounts (53.67% of the portfolio)** representing **£14.26 million in balance exposure**, delaying initial customer outreach and driving preventable default escalations.

**Supporting Evidence:**
* `stakeholder_interview_notes.csv`: Operations Manager Priya Nair observes that *"Simple cases that could be resolved in minutes take days because they get stuck in the wrong queue,"* while Operations Analyst Barry Skinner notes that *"Straightforward cases get delayed because they are queued behind complex ones with no priority logic."*
* `delinquent_accounts_export.csv`: Identifies **1,742 accounts (53.67%)** in Early-Stage Delinquency (1–30 DPD) and **2,507 accounts (77.23%)** as qualified self-service candidates.
* `finance_assumptions.csv`: Assumption `FA-03` estimates a **38.0% straightforward case share** suitable for rules-driven self-service. Assumptions `FA-04` and `FA-05` demonstrate that automated triage and self-service support reduce average case handling time from **18.0 minutes to 10.0 minutes** (saving **8 minutes per case**, a 44.4% handling time reduction).
* `recovery_activity_tracker.csv`: Logs **1,423 manual escalations**, **1,275 tasks** ending in `next_action_unclear`, and **1,233 tasks** flagged as `awaiting_review`.
* `smart_recovery_portal_events.csv`: Shows **1,231 out of 2,541 portal journeys (48.45%)** falling back to human agents due to the absence of automated pre-agent triage.

**Phase 1 Scope Influence:**
Must be embedded into the Phase 1 portal architecture as a **pre-agent digital filtering and rules-based routing layer**. By automatically validating customer eligibility (`FA-03`) and enabling self-service resolution for early-stage accounts, the portal offloads high-volume routine queries. This ensures specialist agents handle only complex, high-empathy hardship negotiations, reducing average handling time by **8 minutes per straightforward case** and unlocking significant operational capacity across the recovery team.