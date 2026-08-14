# Process Mapping Guide

## As-Is process map with pain points
[As-Is process map with pain points](/As_Is_process_map.png)


## Short comparison of how the current process feels for a customer, agent and manager
- Customer: Process feels slow and entirely out of their control. They are often asked to repeat themselves and wait for updates, which causes frustration and dissatisfaction. They are forced to wait for an agent to call them and if missed, they get pushed back into a repetitive contact cycle.
- Agent: Process feels inefficient and frustrating. They are forced to spend time reconciling spreadsheets and email trails, which takes time away from judgement-based case work. The lack of a single source of truth means they are often unsure if they have the latest information, which causes duplicated effort and missed follow-ups.
- Manager: Process feels opaque and unmanageable. They have no visibility of which follow-ups have happened, which means they cannot accurately forecast or report on performance. They are forced to rely on reconciled spreadsheets and email trails, which is time-consuming and error-prone. They are unable to identify which cases are stuck and why, which means they cannot intervene to prevent missed follow-ups.

## Self-service suitability test

A step is a better Phase 1 candidate if it is:
- high-volume
- repeatable
- rules-driven
- low to medium risk
- understandable for customers

## 5 automation opportunities
1. Self-serve portal for customers to confirm balances and get their current account information/summary.
2. Automated direct payment processing for customers who want to pay their debt on their own schedule/immediately, without waiting for an agent. It should instantly update the core database.
3. Automated "Promise-to-Pay" setup and tracking, so customers can select a future date to make a payment. The system automatically tracks this date and automatically follows up if the payment is missed via email or SMS. Removes the need for a spreadsheet to track promises and reduces agent time spent on follow-up.
4. Automated case routing, so that straightforward cases are automatically routed to the self-service portal and complex cases are routed to the appropriate agent or specialist. In terms of complex cases, it should consider vulnerability markers such as history of financial hardship, previous active disputes, high debt (over £5k) or high ageing of more than 90 days past due and multiple broken PTPs. This removes the need for manual triage and reduces the risk of simple cases getting stuck behind complex ones.
5. Automated audit trail, so that all customer interactions and agent actions are automatically logged and easily accessible for review. This reduces the need for manual record-keeping and improves accountability.

Dependencies: 1, 2 and 3 must be implemented together to ensure that the self-service portal is effective and that customers can resolve their cases without an agent. 4 and 5 can be implemented independently, but will enhance the effectiveness of the self-service portal and improve operational efficiency.


## Agent led steps: agent works with the automated system so they have a clear role in the new process.

Automation step 4, if the routing logic detects a vulnerability marker, or if a customer self-identifies as vulnerable on the portal, the automated routing stops instantly and the case is routed to an agent for manual triage. The agent will then determine the appropriate next step, which may include routing to a specialist or providing additional support to the customer.

Automation step 3, if the customer replies to an automated PTP reminder with a complex query or if they break multiple automated PTPs in a row, the system is directed to an agent for manual follow-up. The agent will then determine the appropriate next step, which may include providing additional support to the customer or escalating the case to a specialist.

