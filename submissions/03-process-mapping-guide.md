# Process Mapping Guide

Use this guide when you build the As-Is process map.

## Minimum actors and systems to include

- customer
- collections representative
- team leader or manager
- spreadsheet tracker
- email or manual communication channel
- legacy collections database

## Suggested As-Is flow

1. Account enters delinquency queue
2. Representative creates or receives worklist
3. Representative checks legacy account status
4. Representative cross-checks spreadsheet or email history
5. Representative contacts customer
6. Outcome is captured manually
7. Promise or next action is tracked manually
8. Follow-up is scheduled manually
9. Exceptions are escalated
10. Managers reconcile status for reporting

## Pain points to mark on the flow

Mark at least five directly on the map:
- duplicate status checks
- spreadsheet version or ownership conflict
- missed next action due to manual tracking
- repeated customer contact attempts
- poor visibility of promise-to-pay fulfilment
- manager reporting based on reconciliation rather than live status

## Self-service suitability test

A step is a better Phase 1 candidate if it is:
- high-volume
- repeatable
- rules-driven
- low to medium risk
- understandable for customers

## Keep representative-led if the step is:
- high-risk
- specialist-controlled
- judgment-heavy
- dependent on negotiation or exception handling

## Deliverables to produce from the map

- As-Is process map
- pain-point overlay
- short current-state summary
- first-pass automation candidate list


Based on the As-Is diagram the processes that can and should be automation led are:
1. When the representative cross checks the account details on the database with the information on the spreadsheet tracker and in emails, because this is a mundane process, takes long and has scope for human error.
2. When the representative logs the contact attempt they have to update this in the database, email threads and spreadsheets. This makes the process so much longer than necessary, and can be automated to save time and errors.
3. When the representative is updating customer records with their payment plans, they could easily make a mistake because they have to update in in several places.
4. The representative has to manually flag an account once it has been contacted to avoid the customer being called again about the same thing. This is a process that should be automated because if the representative forgets to flag the account then there would be inconsistency issues.
5. The representative not only has to manually check if the customer has paid into their account but they also have to remember to check at the due date because there is no automatic trigger or alert sent to them. This is a huge are of concern because it means that deadlines can be missed which affects the whole company.


The processes that should not be automated on the other hand include negotiation of the payment plans with the customer, because the ideal case is that the customer pays upfront. The most likely case for this is by having a human to human conversation in which the representative can explain the payment plan options and suggest the best method. People are more likely to comply when they speak to a person as opposed to speaking to a bot.

The other process is the escalation to the manager. This is a human decision that should e taken to decide whether it is necessary for a case to be escalated to the manager especially because the manager will be busy and doesn't have time to deal with more accounts than necessary. In this case, the representative needs to make an informed decision about whether this escalation is actually necessary.