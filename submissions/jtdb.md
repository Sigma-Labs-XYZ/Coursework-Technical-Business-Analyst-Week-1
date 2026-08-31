## 1. Stakeholder Frustration to Jobs-to-be-Done (JTBD) Framework

Qualitative analysis of 126 stakeholder interview notes across 17 roles reveals widespread operational friction. The **Jobs-to-be-Done (JTBD)** framework translates qualitative complaints into structured, human-centered requirements:

> *"When [Situation], I want to [Motivation/Action], so that [Expected Outcome]."*

### Core Jobs-to-be-Done (JTBD) Statements

#### 1. Customer (Debtor)
* **Stakeholder Quote:** *"Customers respond well when they have control and transparency about what they owe."* — Amina Rahman, Compliance Liaison
* **JTBD Statement:** 
  > **When** I fall behind on my loan or credit card payments, **I want** to securely log into a private 24/7 digital portal to view my outstanding balance and select an affordable repayment plan, **so that** I can resolve my debt on my own terms without feeling embarrassed or waiting on hold to speak with an agent.
* **Target Capability:** Self-service identity verification, real-time balance lookup, and digital payment plan setup.

#### 2. Collections Agent
* **Stakeholder Quote:** *"The collections database does not sync with the email tracker, so agents often re-contact customers who were already promised callbacks."* — Christopher Richards, Collections Agent
* **JTBD Statement:** 
  > **When** I open an assigned delinquent account, **I want** a single, automatically synchronized history of all past emails, calls, and portal interactions, **so that** I can immediately understand the case context and avoid calling a customer who has already arranged a callback or payment.
* **Target Capability:** Single Customer View (SCV), real-time cross-channel event synchronization, and centralized activity logging.

#### 3. Operations Manager
* **Stakeholder Quote:** *"Simple cases that could be resolved in minutes take days because they get stuck in the wrong queue."* — Priya Nair, Operations Manager
* **JTBD Statement:** 
  > **When** new delinquent accounts enter the recovery pipeline, **I want** automated rules-based triage to offload straightforward cases to digital self-service, **so that** my specialist agents spend their time exclusively on complex, high-empathy negotiations.
* **Target Capability:** Automated queue triage, eligibility engine (`FA-03`: 38% straightforward case share), and skill-based agent routing.

#### 4. Finance Partner
* **Stakeholder Quote:** *"Customers call back three times because they do not remember what they were told on the first call."* — Daniel Okoye, Finance Business Partner
* **JTBD Statement:** 
  > **When** an agreed payment plan or Promise-to-Pay (PTP) is created, **I want** the system to instantly generate and send an automated written confirmation via SMS and email, **so that** inbound re-verification calls drop and cash flow predictability improves.
* **Target Capability:** Automated written confirmations, schedule tracking, and automated payment reminders.

#### 5. Compliance Liaison
* **Stakeholder Quote:** *"The audit trail is scattered across email, spreadsheets, and the legacy database, making compliance reviews a nightmare."* — Andrea Hunt, Operations Manager
* **JTBD Statement:** 
  > **When** regulatory audits or quality reviews occur, **I want** an immutable, centralized event log capturing every status update and customer consent step, **so that** I can prove regulatory compliance without manually auditing offline spreadsheets.
* **Target Capability:** Tamper-proof digital event logging, standardized account state definitions, and automated QA reporting.

#### 6. Service Design & Delivery Lead
* **Stakeholder Quote:** *"A single customer can have five separate records in the system from different entry points."* — Mr Philip Stone, Service Design Lead
* **JTBD Statement:** 
  > **When** designing the target debt recovery platform, **I want** unified customer record matching and automated system integration, **so that** we eliminate duplicate data entry, prevent contradictory outreach, and ensure seamless portal-to-agent handoffs.
* **Target Capability:** Core banking API integration, master data management (MDM) record merging, and omnichannel workflow routing.