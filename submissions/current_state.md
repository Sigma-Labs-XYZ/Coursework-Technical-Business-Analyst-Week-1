# Current State

## Main Actors and Systems

- Customer
- Collections agent
- Team leader/manager
- Spreadsheet tracker
- Email/manual communication
- Legacy collections system/database

## Pain points

- Duplicate status checks
    - Step: Agent cross-checks spreadsheet or email history
    - Evidence: Stakeholder quote (SN-038: "The biggest win will be when agents stop checking whether work was already done"); Stakeholder quote (SN-087: "We are paying agents to hunt for information that should already be on the screen"); Operational observation from recovery_activity_tracker showing duplicate_check_flag=Y across 15+ activities

- Repeated customer contact attempts
    - Step: Customer reached? → Record attempt → Schedule follow-up → loops back to Agent contacts customer
    - Evidence: Stakeholder quote (SN-040: "We lose at least 20% of follow-ups because they fall between shifts and no one owns the handoff"); Stakeholder quote (SN-011: "The collections database does not sync with the email tracker, so agents often re-contact customers who were already promised callbacks"); Operational observation from recovery_activity_tracker showing multiple call_attempt and email_sent activities on same accounts within days

- Poor visibility of promise-to-pay fulfillment
    - Step: Promise or next action is tracked manually
    - Evidence: Stakeholder quote (SN-007: "We have cases sitting in 'awaiting callback' status for months because the promised date was never recorded"); Stakeholder quote (SN-112 from evidence table: "The current system treats payment promises the same as payment confirmations, which creates confusion"); Operational observation from delinquent_accounts_export showing multiple cases in 'promise_due' status with no recorded follow-up dates

- Missed next action due to manual tracking
    - Step: Follow-up is scheduled manually
    - Evidence: Stakeholder quote (SN-053: "Cases get stuck in 'pending callback' status indefinitely because the callback date is never enforced"); Source dataset recovery_activity_tracker showing next_follow_up_date field is empty in 15+ records; Operational observation showing cases remain in 'awaiting_follow_up' status without progression

- Manager reporting based on reconciliation rather than live reporting
    - Step: Managers reconcile status for reporting
    - Evidence: Stakeholder quote (SN-123: "Every month the finance team has to reconcile our activity count with the database, and they never match"); Stakeholder quote (SN-048: "Reporting takes so long that by the time we see the numbers, they are already out of date"); Operational observation that recovery_activity_tracker requires manual reconciliation across multiple activity types and source_systems

## Current Process

Customer: The current process can feel slow and repetitive. Customers may experience repeated contact attempts or delays in follow-ups because actions are tracked manually, giving them limited visibility over what is happening with their account.

Agent: The process can feel inefficient and difficult to manage. Agents have to check multiple systems, spreadsheets and emails, manually record outcomes and keep track of future actions, increasing their workload and the risk of something being missed.

Team leader/manager: The process can feel difficult to oversee. Managers do not have a single live view of account statuses and therefore have to reconcile information from the legacy system and spreadsheets before they can confidently understand or report on performance.

## Self-service suitability test

| Current process activity | High-volume | Repeatable | Rules-driven | Lower-risk | Self-service candidate? |
|---|---|---|---|---|---|
| Check account/balance | Yes | Yes | Yes | Yes | Yes |
| Make a payment | Yes | Yes | Yes | Yes | Yes |
| Set up a straightforward payment arrangement | Yes | Yes | Yes | Mostly | Yes, with rules |
| Payment reminders | Yes | Yes | Yes | Yes | Yes |
| Promise-to-pay tracking | Yes | Yes | Yes | Mostly | Yes |
| Update customer contact details | Yes | Yes | Yes | Yes | Yes |

## Automation Opportunities
- Customer account and balance viewing – customers can view their account information without contacting an agent.
- Online payments – customers can make straightforward payments through the portal.
- Self-service payment arrangements – eligible customers can set up predefined payment arrangements.
- Automated payment reminders – customers automatically receive reminders about upcoming payments or agreed actions.
- Automated promise-to-pay tracking – the system checks whether promised payments have been made and updates/flags the status.
- Customer contact detail updates – customers can update their own contact information.

## Keep agent-led if the step is:
Complex cases, disputes, exceptions and escalations should remain agent-led because they may require human judgement, investigation or consideration of individual customer circumstances.

Payment arrangements that fall outside predefined self-service rules should also remain agent-led, as these may require negotiation or a more detailed assessment of the customer's circumstances.
