# MongoDB Schema Design for Versioned Documents

| Status   | Date       | Authors & Deciders |
| -------- | ---------- | ------------------ |
| Proposed | 2023-08-14 | Tyson Lawrie       |

## Context and Problem Statement

Prior to v4, the various documents used different mongodb strategies for the storage of versions documents i.e. Workflows, WorkflowTemplats, Task Templates, etc.

- Workflows and WorkflowTemplates (didn't exist in current structure) used a one-to-many approach / mulit document reference approach
- TaskTemplates used an embedded / single document / one-to-few approach

## Considered Options

The following considered objects are based on a number of references and pain points to consolidate down to a single design pattern for versioned objects.

### 1. Single Embedded Document

In this model we create a single document that has an array of the versioned elements.

This approach was used for TaskTemplates in v3, however it led to a lot of confusion in models and the Data Entity being stored ended up being the representation of that to the end user.

Ideally this works for one-to-few mappings however as Flow has matured we now know there are 10+ versions of some TaskTemplates and even 25+ versions of Workflows making it hard to limit size and also to query used the v4 Query APIs.

```json
{
    "_id" : ObjectId(""),
    "currentVersion" : NumberLong(1),
    "description" : "Get Incidents from ServiceNow with optional State",
    "lastModified" : ISODate("2020-04-30T22:54:03.745Z"),
    "name" : "Get Incidents",
    "category" : "ServiceNow",
    "nodetype" : "templateTask",
    "revisions" : [
        {
            "version" : 1,
            ...
            "changelog" : {
                "userId" : "",
                "reason" : "",
                "date" : ISODate("2020-04-30T22:54:03.745Z")
            }
        },
        {
            "version" : 2,
            ...
            "changelog" : {
                "userId" : "",
                "reason" : "",
                "date" : ISODate("2020-04-30T22:54:03.745Z")
            }
        }
    ],
    "status" : "active",
    "createdDate" : ISODate("2020-01-09T00:01:00.000Z"),
    "icon" : "API/HTTP call",
    "_class" : "net.boomerangplatform.model.FlowTaskTemplate",
    "verified" : true
}
```

### 2. Document per version

An additional option that we implemented initially in the beta for v4 is the document per version approach. This means that there are repeated fields in each document that are the same for multiple versions.

This is great for querying and sorting however it does become problematic in knowing what the latest state is across all versions i.e. the status element.

This reduces a little complexity as the Data Entity is the same as the Model used in the request.

```json
{
    "_id" : ObjectId(""),
    "version" : NumberLong(2),
    "description" : "Get Incidents from ServiceNow with optional State",
    "creationDate" : ISODate("2020-04-30T22:54:03.745Z"),
    "name" : "Get Incidents",
    "category" : "ServiceNow",
    "nodetype" : "templateTask",
    ...
    "changelog" : {
        "userId" : "",
        "reason" : "",
        "date" : ISODate("2020-04-30T22:54:03.745Z")
    },
    "status" : "active",
    "icon" : "API/HTTP call",
    "_class" : "net.boomerangplatform.model.FlowTaskTemplate",
    "verified" : true
}
```

### 3. Subset Pattern

A subset pattern is where you have a parent document that contains the common fields and then a child document that contains the versioned fields.

This allows you to retrieve all documents by parent and query relatively easily. This is useful in a one-to-many relationship (i.e. 25+ versions.)

This pattern requires a join to occur between two documents before returning a flattened model to the requestor.

```json
{
    "_id" : ObjectId(""),
    "name" : "get-incidents",
    "creationDate" : ISODate("2020-04-30T22:54:03.745Z"),
    "status" : "active",
    "verified" : true,
}
```

```json
{
    "_id" : ObjectId(""),
    "parent" : ObjectId(""),
    "displayName": "Get Incidents",
    "version" : NumberLong(2),
    "description" : "Get Incidents from ServiceNow with optional State",
    "category" : "ServiceNow",
    "nodetype" : "templateTask",
    ...
    "changelog" : {
        "userId" : "",
        "reason" : "",
        "date" : ISODate("2020-04-30T22:54:03.745Z")
    },
    "icon" : "API/HTTP call",
}
```

## Decision Outcome

_Proposed_ that we implement Option 3: Subset Pattern. While this is additional effort in the v4 migration (as we have already switched to Option 2) and will require us to ensure the Entity is defined differently to the model, it will allow greater control and querying capability as well as ability to increase the number of fields and expand the versioned fields in the future.

Yet to be explored, but considered, is that MongoDB doesn't create a new document for updates to documents that stay relatively similar in size between updates i.e. field replacements. Where as adding new embedded versions would vastly change the stored size and a new document (create operation) would need to occur regardless, so that overhead will always exist.

## Additional Context

- [MongoDB Building With Patterns The Subset Pattern](https://www.mongodb.com/blog/post/building-with-patterns-the-subset-pattern)
- [MongoDB Data Modeling](https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design)
- [DigitalOcean How To Design a Document Schema](https://www.digitalocean.com/community/tutorials/how-to-design-a-document-schema-in-mongodb)
