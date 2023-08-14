# Dashboard Feature Specification.

## Summary

Dashboard is the landing page and is where users get high level insights and summaries of their various policies and violations.

## Background

The dashboard is the current snapshot of the state of things. We want it to be an instant view of whats been happening but also a place to action the top 5 or 10 items for each object.

## Requirements

- Landing with ability to refine / filter the team and a time period
    - Default to all teams
        - Allow to filter to a team
    - Default to 3 month time period
        - Allow time period to be selected but not custom range
- Insights as cards
    - How many policies exist (potentially add number of definitions / rules)
    - How many pass / warnings / fails (maybe as a pie graph)
    - How many validations have been performed
    - Activity over time as graph
    - Latest policies or most used as list card
        - With Call to Action for View Policies
    - Latest activity as list
        - With Call to Action for View Activity
- Future considerations
    - ‘Wastage’ type widget / card that would identify policies that are always passed. This would help give really good feedback to a user to either clean up a policy or make it stricter. Or we could go the reverse, find policies that are never passed.

### Non Functional

- TBA

## Impacts

TBA

## Dependencies

- TBA

## Relevant Information

- [Boomerang CICD Dashboard concept](https://ibm.invisionapp.com/d/main#/console/15357849/319430086/preview)
    - Probably closer to this one with a team filter otherwise pull data from all teams you have access to
- [IBM Services Essentials Core Insights](https://ibm.invisionapp.com/d/main#/console/15364384/319615391/preview)
    - We dont want the ribbon at the top for this dashboard / language page

## Acceptance Criteria

| Feature | Given | When | Then
| --- | --- | --- | --- |
| - | - | - | - |

## Technical Detail

- TBA