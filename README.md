# :wave: Welcome to the Boomerang community 

The Boomerang community, roadmap, and planning repository. This is where you can find information on joining, contributing, governance, releases and roadmap.

Boomerang is a collection of open source, cloud-native projects for CI/CD and automation. You can find more [here](https://useboomerang.io)

## Roadmap

The following are our high level roadmap items that we are aiming for in 2022, see [planning](#planning) for the detailed release / iteration breakdown.

| Goal | Description |
| --- | --- |
| Enhanced Architecture | A new architecture based on lessons learnt. The Eventing / Webhook Listener service will be merged into the API service which in turn will be split out from the Workflow service. The Workflow service will focus on being the backend to the front end and performing CRUD operations. The executor engine will be split from the Workflow service and merged with the Controller service. See [enhancement request](https://github.com/boomerang-io/roadmap/issues/201) for more information.
| API Driven | Expand the APIs to cover all endpoints and drive powerful integrations. Every action should be able to be done through the API. |
| Non blocking execution | Utilize NATS queues for non blocking task execution to do a better balanced job of handling high load. |
| Seperation of execution concern | Add an installation option where a namespace per team can be used for separation as well as node labels for running team tasks on different kubernetes nodes. |
| Looping | As Tekton finalizes looping support, add the capability to Flow via the drag and drop UI |
| Greater Activity detail | Activity is only recorded once you get to execution of the workflow. Add in greater visibility to workflow errors even prior to execution. |
| Labels | Greater support for labels through the UI and ability to search on labels. |
| Enhanced Triggering | New user experience for creating triggers, including the ability to enable through button click integration for popular integrations |

## Planning

We use [GitHub Issues Projects](https://github.com/features/issues) _beta_ for our release management, if you want to take a look at the active release or the roadmap:

- [Boomerang Flow GitHub Issues Project](https://github.com/orgs/boomerang-io/projects/4/views/1)
- [Boomerang Bosun GitHub Issues Project](https://github.com/orgs/boomerang-io/projects/5)

## Governance

The following documentation will help guide us all as we strive to create a community working together to build open source tools.

- [Maintainers](https://github.com/boomerang-io/roadmap/blob/main/MAINTAINERS.md)
- [Code of Conduct](https://github.com/boomerang-io/roadmap/blob/main/CODE_OF_CONDUCT.md)

### Community Meeting

A community meeting will be held every two weeks on Tuesday at 3:00pm US Central Timezone
  - [Agenda](https://docs.google.com/document/d/1298K1t36f5jl9VwEipp3KHgmdj-vRHHA5YlnMaS2n0A/edit?usp=sharing)
  - [Google Meet](https://meet.google.com/thh-dpwr-ynv)
  - [Add to Calendar](https://calendar.google.com/event?action=TEMPLATE&tmeid=NHNzZmVpaDRxdGh0MTM5MjQ1aGUzdDhoY3ZfMjAyMTA3MTNUMjAwMDAwWiB0eXNvbkBsYXdyaWUuY29tLmF1&tmsrc=tyson%40lawrie.com.au&scp=ALL)

> To get access to this meeting and the agenda, please [join the Boomerang IO google group](https://groups.google.com/g/boomerang-io)

## Documentation & Presentation

- [Docs](https://www.useboomerang.io/docs/boomerang-flow/introduction/overview)
- [Presentation](https://docs.google.com/presentation/d/1id1qePshOm3YRbLay47Ny6WvkrbxIOHEJtVXsM8PmGI/edit?usp=sharing)
- [YouTube](https://youtu.be/erBEQdBHFJU)

## Want to get involved?

We welcome all contributions to the project and you can reach out to us via [slack](https://join.slack.com/t/boomerang-io/shared_invite/zt-pxo2yw2o-c3~6YvWkKNrKIwhIBAKhaw) or through GitHub.

### How to Contribute
Like any good development project, we use Pull Requests (PRs) to track code changes. We recommend that if you want to contrubute and implement a fix, change, or enhancement, you do so by linking the PR with an Issue.

Typically this is achieved by forking the repository and create a PR to be able to link this to the parent repository and request a merge.

### GitHub Issue Types

There are 5 types of issues that we have added to the issue templates. Epic and Task are generally reserved for the active development team and related to implementing a Change or Enhancemnet

| Type |	Purpose |
| --- | --- |
| 🐛 Bug Report |	Create a report to help us improve if something isn't working as expected. |
| ✨ Change or Enhancement |	A change or improvement suggestion. |
| 💬 Support or Inquiry |	When help is needed or to track questions. |
| 🚀 Epic | A theme of work that is required to complete the larger goal |
| 🔨 Task | Steps to implement a feature |

### Commit Messages

The commit message should state the change in 72 characters or less. Additionally we recommend, and require in some repositories, the usage of a commit lint and conventional commit so that we can map these to Release Notes.
