# Boomerang Roadmap

## Flow

A project view of community roadmap items can be found [here](https://github.com/orgs/boomerang-io/projects/4/views/1)

### 2023

The main goal for 2023 is a major refactor of the Flow service to support a new architecture. This will include a new UI and API. The new architecture will be based on lessons learnt from the current architecture and will be more API driven.

- API driven implementation
  - v1 - v3 were UI driven with separate APIs bolted on after the fact for integration and as such we aim to consolidate to a single set of APIs that the UI leverages
  - Re-think our approach to authentication and authorization to make this possible
    - introduce new tokens at Global, Team, Workflow, User, and Session levels.
    - Tokens will have permissions made up of scopes and actions
- Separate the Execution Engine from the Workflow service
- Adjust the method of integration between the new Execution Engine and the Controller (renamed to Handler) to be based on an event-sink that allows different Handlers to be swapped in, i.e. Tekton Handler, Kubernetes Jobs Handler, etc.
- Re-imagine the UI to support this new architecture
  - Consolidate everything to be Team based as the primary grouping mechanism
  - Make team management more intuitive
  - Remove Personal and System workflows (as they never had the full functionality in missing parameters and custom task templates, as well as never having proper quota management)
  - Migrate to ReactFlow as the DAG modeling framework

### 2022

| Goal                            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Enhanced Architecture           | A new architecture based on lessons learnt. The Eventing / Webhook Listener service will be merged into the API service which in turn will be split out from the Workflow service. The Workflow service will focus on being the backend to the front end and performing CRUD operations. The executor engine will be split from the Workflow service and merged with the Controller service. See [enhancement request](https://github.com/boomerang-io/roadmap/issues/201) for more information. |
| API Driven                      | Expand the APIs to cover all endpoints and drive powerful integrations. Every action should be able to be done through the API.                                                                                                                                                                                                                                                                                                                                                                  |
| Non blocking execution          | Utilize NATS queues for non blocking task execution to do a better balanced job of handling high load.                                                                                                                                                                                                                                                                                                                                                                                           |
| Seperation of execution concern | Add an installation option where a namespace per team can be used for separation as well as node labels for running team tasks on different kubernetes nodes.                                                                                                                                                                                                                                                                                                                                    |
| Looping                         | As Tekton finalizes looping support, add the capability to Flow via the drag and drop UI                                                                                                                                                                                                                                                                                                                                                                                                         |
| Greater Activity detail         | Activity is only recorded once you get to execution of the workflow. Add in greater visibility to workflow errors even prior to execution.                                                                                                                                                                                                                                                                                                                                                       |
| Labels                          | Greater support for labels through the UI and ability to search on labels.                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Enhanced Triggering             | New user experience for creating triggers, including the ability to enable through button click integration for popular integrations                                                                                                                                                                                                                                                                                                                                                             |
