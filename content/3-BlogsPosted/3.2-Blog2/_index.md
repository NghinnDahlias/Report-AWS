---
title: "Blog 2"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
**Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report.
{{% /notice %}}

# WHY IS REST API NOT ALWAYS THE BEST CHOICE? THE POWER OF PUB/SUB AND MQTT IN DISTRIBUTED SYSTEMS

When designing communication between services, clients, or devices, REST APIs over HTTP are often the default choice. A client sends a request, the server processes it, and then returns a response. This model is familiar, easy to implement, and suitable for many traditional applications.

However, as systems scale, especially when they need to process real-time data from many devices or integrate multiple independent services, the request/response model begins to show its limitations.

Pub/Sub and MQTT provide a better approach for problems that require asynchronous communication, loose coupling between components, and event-driven scaling.

## 1. Limitations of the synchronous HTTP/REST model

In a REST-based model, the client usually has to actively send requests to the server. If it wants to check whether new data or commands are available, it may need to poll continuously.

Common issues include:

* Requests may timeout when the network is unstable.
* Continuous polling increases the number of requests and bandwidth usage.
* Clients and servers depend directly on each other's runtime status.
* When one service fails, services calling it directly may fail as well.
* Adding more consumers often requires changing the current logic.

This model is still effective for tasks such as data queries, authentication, form submission, or actions that require an immediate response. But it is not always the best fit for telemetry data or continuously generated event streams.

## 2. How do Pub/Sub and MQTT solve these problems?

In a Publish/Subscribe model, a broker sits between publishers and subscribers.

### Publisher

A publisher only needs to send messages to a specific topic. It does not need to know:

* how many subscribers exist
* where the subscribers are running
* how the subscribers process the data

### Subscriber

Subscribers register for a topic. When the broker receives a new message, it delivers that message to all matching subscribers.

```text
Publisher
-> Topic
-> Message Broker
-> Subscriber
```

This structure creates strong decoupling between components:

```text
The publisher does not call the subscriber directly
The subscriber does not need to know the exact publisher
The broker handles message distribution
```

MQTT was designed with this model in mind and is especially suitable for constrained devices or unstable networks. Its payload and header overhead are usually lighter than more traditional application-layer protocols, which helps reduce transmission costs.

## 3. Event-driven architecture on AWS

Pub/Sub is not only useful for IoT devices. It also works well in backend and distributed-system designs.

Several AWS services commonly support this style:

### AWS IoT Core

AWS IoT Core provides a managed MQTT broker that supports secure device connectivity using certificates and routes messages through the AWS IoT Rules Engine.

### Amazon SNS

Amazon Simple Notification Service supports the Pub/Sub and fan-out model. A single message can be delivered to multiple subscribers such as SQS, Lambda, HTTP endpoints, or email.

### Amazon EventBridge

Amazon EventBridge provides an event bus for connecting AWS services, custom applications, and some SaaS platforms through events.

These services are all related to event-driven architecture, but they serve different scopes:

```text
AWS IoT Core
-> Device connectivity and message routing

Amazon SNS
-> Notification Pub/Sub and fan-out

Amazon EventBridge
-> Event routing between services and applications
```

## 4. Example of an IoT data flow

A typical telemetry flow can be designed like this:

```text
MQTT Gateway
-> AWS IoT Core
-> AWS IoT Rules Engine
-> Amazon Data Firehose
-> Amazon S3
```

Processing steps:

1. The gateway sends telemetry to AWS IoT Core over MQTT.
2. The AWS IoT Rules Engine receives messages based on the configured topic.
3. The rule forwards the data to Amazon Data Firehose.
4. Firehose buffers multiple records and stores them in Amazon S3.
5. Another rule or branch can invoke Lambda when the data exceeds a threshold.

Alert example:

```text
Telemetry Event
-> Rule checks conditions
-> AWS Lambda
-> Notification service
```

In this architecture, the gateway does not need to write directly to a database or alerting system. Components are triggered through events and can scale more independently.

## 5. When should you use REST, and when should you use Pub/Sub?

### REST is a good fit when

* the client needs an immediate response
* the action is clearly a query or command
* the communication is simple request/response
* the number of participating components is still limited
* the caller needs an immediate success or failure result

### Pub/Sub is a better fit when

* data is produced continuously
* multiple consumers need the same event
* components should operate independently
* the system needs asynchronous processing
* you want to add more consumers without changing the publisher
* you are building an event-driven architecture

REST and Pub/Sub do not replace each other. A real system can use REST for user-facing APIs and Pub/Sub for internal event processing.

## Conclusion

REST APIs remain a strong choice for many traditional client-server patterns. But in IoT, distributed gateways, telemetry pipelines, and microservices, synchronous communication can create tighter coupling than necessary.

Pub/Sub and MQTT help systems:

* reduce tight coupling
* process data asynchronously
* scale by adding more subscribers
* work better with constrained devices and unreliable networks
* support event-driven architecture

The important point is not to replace REST completely. It is to choose the right communication model for each type of workload.

## References

* [What is AWS IoT Core?](https://docs.aws.amazon.com/iot/latest/developerguide/what-is-aws-iot.html)
* [MQTT topics](https://docs.aws.amazon.com/iot/latest/developerguide/topics.html)
* [AWS IoT Rules](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html)
* [What is Amazon SNS?](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
* [What is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
* [Amazon Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
