# DataMigrations

## V3 to V4

# Flow v3 to v4 Model Changes

As part of v3 to v4, a data migration exercise is needed for the collections.

> Note: we are **not** fully migrating the Workflow Activity.

## Task Templates

- Collection: `task_templates`

> Note: Task Templates have been flattened so there is no array of revisions, there is now a Document (Task Template) per version.

| v3              | v4           | Change                                                                                                              |
| --------------- | ------------ | ------------------------------------------------------------------------------------------------------------------- |
| id              | id           | no change                                                                                                           |
| name            | name         | limited to alphanumer, lower case, and -                                                                            |
| -               | displayName  | added                                                                                                               |
| status          | status       | no change                                                                                                           |
| description     | description  | no change                                                                                                           |
| -               | labels       | new `Map<String, String>`                                                                                           |
| -               | annotations  | new `Map<String, Object>`                                                                                           |
| createdDate     | creationDate | changed element name                                                                                                |
| lastModified    | -            | removed                                                                                                             |
| -               | version      | added                                                                                                               |
| -               | changelog    | Previously on the revision                                                                                          |
| category        | category     | no change                                                                                                           |
| icon            | icon         | no change                                                                                                           |
| verified        | verified     | no change                                                                                                           |
| scope           | scope        | no change - set to global for all loader templates                                                                  |
| flowTeamId      | -            | removed - now implemeneted via relationships on teams                                                               |
| nodeType        | type         | changed name and values - templateTask now template and customTask now custom                                       |
| enableLifecycle | -            | removed                                                                                                             |
| revisions       | spec         | changed - see below model table of changes                                                                          |
| -               | config       | a version of what was on the revision for the UI detail of params. This is the AbstractConfigurationProperty model. |

### Task Template Spec

> Note: previously `List<TaskTemplateRevision>`. The Documents have been flattened.

| v3         | v4         | Change                                                                                                                                |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| arguments  | arguments  | no change                                                                                                                             |
| changelog  | -          | moved to TaskTemplate                                                                                                                 |
| command    | command    | no change                                                                                                                             |
| config     | params     | changed element name - further changes to be made to the inputs to store UI related details in labels, rather than in with the params |
| envs       | envs       | no change                                                                                                                             |
| image      | image      | no change                                                                                                                             |
| results    | results    | no change                                                                                                                             |
| script     | script     | no change                                                                                                                             |
| version    | -          | moved to TaskTemplate                                                                                                                 |
| workingDir | workingDir | no change                                                                                                                             |

## Workflows

- Collection: `workflows`

| v3               | v4               | Change                                                             |
| ---------------- | ---------------- | ------------------------------------------------------------------ |
| id               | id               | no change                                                          |
| name             | name             | no change                                                          |
| -                | creationDate     | added                                                              |
| shortDescription | shortDescription | no change                                                          |
| description      | description      | no change                                                          |
| icon             | icon             | no change                                                          |
| status           | status           | no change                                                          |
| triggers         | triggers         | no change for now                                                  |
| tokens           | tokens           | no change                                                          |
| labels           | labels           | changed storage from `List<KeyValuePair>` to `Map<String, String>` |
| -                | annotations      | added                                                              |
| storage          | -                | removed - now workspaces on `workflow_revisions`                   |
| scope            | scope            | no change - may be removed                                         |
| properties       | -                | removed - now params and config on `workflow_revisions`            |
| flowTeamId       | -                | removed - now implemeneted via relationships on teams              |
| ownerUserId      | -                | removed - now implemented via relationships on user                |

### Triggers

> Note: need to come back to. For now leaving as is.

## Workflow Revisions

- Collection: `workflow_revisions` (previously `workflows_revisions`)

| v3         | v4          | Change                                                                                                                         |
| ---------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------ |
| id         | id          | no change                                                                                                                      |
| version    | version     | Integer instead of long                                                                                                        |
| workFlowId | workflowRef | changed name                                                                                                                   |
| changelog  | changelog   | no change                                                                                                                      |
| markdown   | markdown    | no change                                                                                                                      |
| -          | workspaces  | previously on the `workflows` (not the revision) - model also changed                                                          |
| -          | params      | properties were previously a part of `workflows` (not the revision) - model also changed                                       |
| dag        | tasks       | different underlying DAGTask vs Task model and name                                                                            |
| -          | config      | a version of what was on the workflow properties for the UI detail of params. This is the AbstractConfigurationProperty model. |

### Workspaces

> Note: Moved from fixed objects to a List of generic Workspaces

| v3  | v4       | Change |
| --- | -------- | ------ |
| -   | name     | new    |
| -   | type     | new    |
| -   | optional | new    |
| -   | spec     | new    |

**V3**

```json
{
    "activity" : {
        "enabled" : true,
        "size" : NumberInt(1),
        "mountPath" : "/workspace/activity"
    },
    "workflow" : {
        "enabled" : false,
        "size" : NumberInt(1),
        "mountPath" : "/workspace/workflow"
    }
}
```

**V4**

> Note: will only be created if `enabled: true` in v3

```json
[
    {
      "name": "activity",
      "type": "workflow",
      "optional": false,
      "spec": {
        "size" : NumberInt(1),
        "mountPath" : "/workspace/activity",
        "class" : "",
        "accessMode" : ""
      }
    },
    {
      "name": "workflow",
      "type": "workflowRun",
      "optional": false,
      "spec": {
        "size" : NumberInt(1),
        "mountPath" : "/workspace/workflow",
        "class" : "",
        "accessMode" : ""
       }
    }
  ]
```

### Tasks

> Note: extremely complex migration. Needs large testing datasets.

| v3              | v4              | Change                                                   |
| --------------- | --------------- | -------------------------------------------------------- |
| taskId          | -               | removed                                                  |
| label           | name            | changed element name                                     |
| type            | type            | Types may have changed                                   |
| templateId      | templateRef     | changed from template's ID to name                       |
| templateVersion | templateVersion | no change                                                |
| results         | results         | no change                                                |
| -               | labels          | added                                                    |
| -               | annotations     | added                                                    |
| properties      | params          | KeyValuePair to Map                                      |
| dependencies    | dependencies    | model change                                             |
| metadata        | -               | removed. Added as an annotation. `boomerang.io/position` |

#### Dependencies

| v3                    | v4                 | Change                                                 |
| --------------------- | ------------------ | ------------------------------------------------------ |
| conditionalExecution  | -                  | removed                                                |
| taskId                | taskRef            | element name change                                    |
| executionCondition    | executionCondition | same                                                   |
| switchCondition       | decisionCondition  | element name change                                    |
| additionalPropertieis | -                  | removed                                                |
| metadata              | -                  | removed. Added as an annotation. `boomerang.io/points` |

### Config

| v3                   | v4  | Change                                                  |
| -------------------- | --- | ------------------------------------------------------- |
| type                 | -   | removed                                                 |
| inputs               | -   | removed                                                 |
| nodeId               | -   | removed. Added as an annotation. `boomerang.io/nodeId`. |
| taskId               | -   | removed                                                 |
| taskVersion          | -   | removed                                                 |
| outputs              | -   | removed                                                 |
| additionalProperties | -   | removed                                                 |

## Workflow Runs

- Collection: `workflow_runs` (previously `workflows_activity`)

| v3                  | v4                  | Change                                                     |
| ------------------- | ------------------- | ---------------------------------------------------------- |
| id                  | id                  | no change                                                  |
| labels              | labels              | changed to `Map<String, String>`                           |
| -                   | annotations         | new element                                                |
| initiatedByUserId   | -                   | removed - now `initiatedByRef`                             |
| initiatedByUserName | -                   | removed - now `initiatedByRef`                             |
| -                   | initiatedByRef      | new                                                        |
| creationDate        | creationDate        | no change                                                  |
| duration            | duration            | Long to long                                               |
| -                   | startTime           | new - set to creationDate                                  |
| status              | status              | Types have changed                                         |
| -                   | phase               | new - set to final phase                                   |
| statusOverride      | statusOverride      | changed types - copy only if set - map to new status types |
| statusMessage       | statusMessage       | no change - copy only if set                               |
| isAwaitingApproval  | isAwaitingApproval  | no change - copy only if set                               |
| error               | ???                 | _TBD_                                                      |
| teamId              | -                   | removed - now retrieved via relationships                  |
| userId              | -                   | removed - now retrieved via relationships                  |
| workflowId          | workflowRef         | changed element name                                       |
| workflowRevisionid  | workflowRevisionRef | changed element name                                       |
| trigger             | trigger             | no change                                                  |
| properties          | params              | changed model                                              |
| outputProperties    | results             | changed model                                              |
| switchValue         | -                   | removed                                                    |
| Workspaces          | ???                 | _TBD_                                                      |

## Task Runs

- Collection: `task_runs` (previously: `workflows_activity_task`)

> Note: this collection is not being migrated

| v3                        | v4              | Change                                        |
| ------------------------- | --------------- | --------------------------------------------- |
| id                        | id              | no change                                     |
| nodeId                    | -               | removed                                       |
| order                     | -               | removed                                       |
| taskName                  | name            | added - I think - needs to be confirmed       |
| type                      | type            | no change                                     |
| -                         | labels          | added                                         |
| -                         | annotations     | added                                         |
| -                         | creationDate    | added                                         |
| startTime                 | startTime       | added                                         |
| duration                  | duration        | no change                                     |
| status                    | status          | altered status'                               |
| -                         | phase           | added                                         |
| -                         | statusMessage   | added                                         |
| error                     | -               | ? should this be available                    |
| -                         | params          | added - used to be on the `workflow_revision` |
| outputs                   | templateResults | altered structure                             |
| outputProperties          | results         | altered structure                             |
| preApproved               | preApproved     | no change                                     |
| switchValue               | decisionValue   | changed name                                  |
| -                         | dependencies    | added - used to be on the `workflow_revision` |
| workflowId                | workflowRef     | changed name                                  |
| template                  | templateRef     | changed name                                  |
| templateRevision          | templateVersion | changedName                                   |
| activityId                | workflowRunRef  | changedName                                   |
| runWorkflowActivityId     | ?               | not sure                                      |
| runWorkflowId             | ?               | not sure                                      |
| runWorkflowActivityStatus | ?               | not sure                                      |
| -                         | workflowResults | added                                         |
| approval                  | ?               | not yet known                                 |

## Task Locks

- Collection: `locks` (previously: `tasks_locks`)

Model is the same, however have introduced support for Azure CosmosDB API for MongoDB which means the TTL and indexes are slightly different depending on MongoDB implementation.

## Actions

- Collection: `actions` (previously: `workflows_activity_approval`)

| v3                | v4                | Change                                                                                                      |
| ----------------- | ----------------- | ----------------------------------------------------------------------------------------------------------- |
| id                | id                | no change                                                                                                   |
| workflowId        | workflowRef       | name change                                                                                                 |
| activityId        | workflowRunRef    | name change                                                                                                 |
| taskActivityId    | taskRunRef        | name change                                                                                                 |
| teamId            | -                 | moved to team relationship                                                                                  |
| actioners         | actioners         | no change                                                                                                   |
| status            | status            | Underlying object name change from ApprovalStatus to ActionStatus                                           |
| type              | type              | Underlying object name change from ManualType to ActionType. Enum task is now manual. Approval is the same. |
| creationDate      | creationDate      | no change                                                                                                   |
| numberOfApprovers | numberOfApprovers | no change                                                                                                   |
| approverGroupId   | approverGroupId   | no change                                                                                                   |

## Teams

- Collection: `teams`

| v3                  | v4           | Change                                                             |
| ------------------- | ------------ | ------------------------------------------------------------------ |
| id                  | id           | no change                                                          |
| name                | name         | no change                                                          |
| -                   | creationDate | added                                                              |
| isActive            | status       | migrated to Enum of active, inactive                               |
| higherLevelGroupId  | externalRef  | renamed                                                            |
| labels              | labels       | changed storage from `List<KeyValuePair>` to `Map<String, String>` |
| ApproverGroups      | -            | removed - now separate in `approver_groups`                        |
| settings.properties | parameters   | renamed. was under settings, bumped up a level                     |
| settings            | settings     | empty. future functionality                                        |
| quotas              | quotas       | no change                                                          |

## ApproverGroups

- Collection: `approver_groups`

| v3        | v4           | Change                              |
| --------- | ------------ | ----------------------------------- |
| id        | id           | no change                           |
| name      | name         | no change                           |
| -         | creationDate | added                               |
| approvers | approverRefs | changed model to a list of User Ids |

## Relationship

- Collection: `relationships`

> Note: New to v4. Replaces the refs on objects

| v3  | v4           | Change |
| --- | ------------ | ------ |
| -   | id           | added  |
| -   | creationDate | added  |
| -   | relationship | added  |
| -   | fromType     | added  |
| -   | fromRef      | added  |
| -   | toType       | added  |

## Supporting Models

### RunStatus

| v3         | v4         | Change       |
| ---------- | ---------- | ------------ |
| notstarted | notstarted | no change    |
| -          | ready      | new          |
| inProgress | running    | changed name |
| waiting    | waiting    | no change    |
| completed  | succeeded  | changed name |
| failure    | failed     | changed name |
| invalid    | invalid    | no change    |
| skipped    | skipped    | no change    |
| cancelled  | cancelled  | no change    |

### TeamStatus

| v3  | v4       | Change |
| --- | -------- | ------ |
| -   | active   | new    |
| -   | inactive | new    |
