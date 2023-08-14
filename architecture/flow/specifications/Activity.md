# Activity Feature Specification.

## Summary

Activity allows end users to search and view an overview of activities by a combination of: Team, Workflow, and Labels. You can also view the detailed execution of a particular activity, allowing end users to view task level execution, logs, results as well as the workflow level exeuction and results.

## Background

This screen is the main way of viewing and finding the individual executions. An execution can be linked to directly from the Run if the user selects Run and View.

Labels allow an abstract way of finding workflows and activities based on arbitrary data added by a user to a Workflow or from an external interaction such as a label of eventId (if the workflow was trigger by a CloudEvent)

## Requirements

- A listing screen used as the landing page when navigating to Activity
    - Show a snapshot of the days stats
    - Be able to filter by status
    - Be able to filter by Team, Workflow, Trigger, and Label and Start / End date
    - A table view with sortable headers showing: Team, Scope, Workflow, Trigger, Initiated By, Start Time, Duration, Status
- An Activity Detail view
    - Metda about the Workflow: Team, Version, Initiated By, Trigger, Start Time
    - Advanced Detail to get to debug commands and labels
    - Visual read-only view of the workflow depicting status and path taken
    - An ability to see Result Parameters for the Workflow
    - An ability to see overall workflow status
    - A log view of the tasks and their status with actions
        - Show Task Status
        - Name, Start Time, Duration
        - View Log
        - View Result Parameters
        - View Error

### Non Functional

- TBA

## Impacts

- The Activity Detail (i.e. a specific activity) can be gotten to direction from the Run and View in the Workflows screen.
- The Activity screen can be navigated to and pre-filtered from the Workflows screen

## Dependencies

- TBA

## Relevant Information

- TBA

## Acceptance Criteria

| Feature | Given | When | Then
| --- | --- | --- | --- |
| - | - | - | - |

## Technical Detail

- TBA