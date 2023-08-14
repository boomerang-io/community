# Eventing

As we mature and scales, eventing will become an important implementation, not just in triggering Workflows but also how we queue and execute Workflows. A majority of the detail can be found in our [public architecture documentation](https://www.useboomerang.io/docs/boomerang-flow/architecture/eventing-architecture)

## Implementation

We use [CloudEvents](cloudevents.io) and [NATS](nats.io) as the default implementaiton. CloudEvents provides the generic specification, and NATS Streaming is our queuing mechanism.

Eventing is currently an optional inclusion, if disabled, we fall back on sending the events received from the listener to the workflow services via HTTP.

## Sample Object

```
{
    "specversion" : "1.0",
    "type" : "io.boomerang.eventing.custom",
    "source" : "/github/actions",
    "id" : "C234-1234-1234",
    "time" : "2020-04-05T17:31:00Z",
    "subject" : "/5f74d0293979cd04c7f8afa1"
    "datacontenttype" : "application/json",
    "data" : {
        "event" : "request_success",
        "inputs" : {
          "key": "value"
        }
    }
}
```

## Authorization

We check for the authorization token prior to processing any requests. If the Workflow ID is valid but the token is not, we will log an activity against the Workflow with a Workflow level failure.

## Roadmap

As we grow and mature in our eventing approach, we may move to a Distributed Application Runtime / Application Mesh to satisfy our microservice dependencies (broader than eventing). At this point in time the indication would be [dapr](dapr.io).

This will allow us to utilize the framework for many different aspects but also abstract the implementation from a particular eventing middleware / implementation.

## References

- [Boomerang Flow Listener](https://github.com/boomerang-io/flow.service.listener) the inital implementation with Boomerang Flow.

- [CloudEvents](https://cloudevents.io/) is a generic event specification with frameworks for easily translating event objects.
