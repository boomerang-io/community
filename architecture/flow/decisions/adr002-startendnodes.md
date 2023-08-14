# Start and End Nodes

- **Status:** Proposed
- **Deciders:** Tyson Lawrie, Marcus Roy, _tbd_
- **Date:** 2022-10-08 (proposed)

## Context and Problem Statement

Prior to v4, the Workflow contained start and end nodes as part of the stored Workflow revision document. These nodes are used in conjunction with the dependencies to determine the direction and ordering of the task nodes in the graph as well as ensuring that a path is not executed if it doesn't eventually hit the end of the graph tree (i.e. the end node).

Moving to the ability to create via an API, the start and end node are an interesting dilemna for end users to have to add into the task list.

## Considered Options

### 1. New Mode

In async, Workflows and Tasks would have to be manually moved from Queued to Started to Completed.

In Syncrhonous mode, Workflows and Tasks would automatically move from Queued to Started and a synchronous outbound call from the engine would be made.

### 2. Synchronous Polling

An Executor, would continuously poll every x seconds to determine if there are any queued Workflows or Tasks that need processing.

### 3. Synchronous Event

An Executor, would listen for a Workflow / Task status event to determine if there are any queued Workflows or Tasks that need processing.

## Decision Outcome

_Proposed_ that we implement option 2 or 3 (or both as necessary if eventing is still a feature flag in its own right).

## Additional Context

![v4 Architecture](./BoomerangFlow-v4-Architecture.drawio.png)
