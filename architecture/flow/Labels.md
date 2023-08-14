# Labels

Labels are key/value pairs that are intended to be used to specify identifying attributes that are meaningful and relevant.

It provides a way to overlay custom mappings/structures in a loosely coupled fashion, without requiring clients to store these mappings. It provides a level of extensibility for a number of use cases that don't require the code to continually be updated with new storage mechanisms and mappings.

## Use Cases

Labels could provide end users and systems the ability to:

- collate Workflows together with the same label, such as a category.
- attach identifying attributes to a Workflow Activity such as meaningful information as to how it was triggered
- attach organizationally relevant information to Users such as externally relevant Feature Flags such as whether to send emails or notificaitons, or Workflow specific logic deciders.

## Implementation

The syntax for creating a label key-value pair is in the format `<prefix>/<name>=<value>`. The prefix is optional and must be a valid DNS subdomain (such as "company.com")

### Data Structure
```
"labels": {
    "key1" : "value1",
    "key2" : "value2"
  }
```

### Label Prefixing

Label prefixing makes it easier to manage shared labels. Labels without a prefix are private to users. The shared prefix ensures that shared labels do not interfere with custom user labels.

For example, `io.boomerang.event/` is found on Workflow Activity that has been triggered by an Event

| Key | Description | Example |
| --- | --- | --- |
| `io.boomerang.event/id` | The unique Cloud Event ID of the event that triggered the Workflow | `io.boomerang.event/id=A234-1234-1234` |
| `io.boomerang.event/source` | Specific to the object type or path for the sending source system | `io.boomerang.event/source=/catalog/services/cloud-object-storage/mybucket` |
| `io.boomerang.event/subject` | Message subject with contextually relavent information for processing the Cloud Event | `io.boomerang.event/subject=/<workflowId>/<workflowActivityId>/<topic>` |
| `io.boomerang.event/initiatorid` | A unique, and optional extension, that assists in identifying the source sender by ID. Usually a 16-digit HEX string. | `io.boomerang.event/time=4bf92f3577b34da6` |
| `io.boomerang.event/initiatorcontext` | An optional extension that may contain more information about the app that initiated the Cloud Event. | `io.boomerang.event/time=context description of the initiating app` |

### Strict Convention

Strict labeling conventions are a best practice for a reason. Loose label naming significantly increases the time and difficulty of querying the information you're looking for.

However there is no enforcement of any convention.

## Support for Labels

### Workflows

Users can manage (create, update, delete) the labels attached to a workflow via the UI and the v1 API.

_Future:_
1. Ability to filter Workflows in the UI via labels.

### Activity

Users can query the Workflow Activity via the v1 API based on Workflow labels.

_Future:_ 
1. ability to filter Workflow Activity in the UI via labels.

### Teams

Admins can manage (create, update, delete) labels attached to a team  via the UI and the v1 API. Admins can also filter Teams in the v1 API by labels.

### Users

Admins can manage (create, update, delete) labels attached to a user via the UI and the v1 API. Admins can also filter Users in the v1 API by labels.

1. Ability to filter Users in the UI via labels.