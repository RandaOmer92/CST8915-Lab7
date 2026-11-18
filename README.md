# CST8915 Lab 7: Introduction to Kubernetes Basics

**Student Name**: Randa Omer

**Student ID**: 041079985

**Course**: CST8915 Full-stack Cloud-native Development

**Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/47dvjuz682g?si=b0z9hqkPIhXjeZL7)

---

## RabbitMQ Analysis

### 1. Is RabbitMQ stateless or stateful application?

RabbitMQ is **stateful**. 

- A **stateless app does not keep important data. If it 
restarts, nothing is lost. Example: `product-service`.
- A **stateful** app keeps data that must not be lost. RabbitMQ keeps the **queues** and the **messages** (our orders) until someone reads them.

Kubernetes says StatefulSets are for apps that need **persistent storage** or a **stable, unique network identity** [5]. RabbitMQ needs both, so it is a stateful app.

### 2. What is the problem with running RabbitMQ without persistent storage?

In our YAML file, RabbitMQ runs as a normal **Deployment** with **no volume**. So RabbitMQ keeps its queues and messages **inside the pod**.

Storage inside the pod is **ephemeral**. Kubernetes says "ephemeral" means there is **no long-term guarantee** that the data will stay [2]. It is meant for temporary things like scratch space, cache and logs [2].

This means:
- **Orders can be lost.** If the pod goes away, the orders waiting in the queue go away too.
- **"Durable" does not help.** In my video the queue had the **D** (durable) label, but the order was still lost, because it was saved inside the pod.
- **The pod name changes.** RabbitMQ named itself after the pod (`rabbit@rabbitmq-5d4b559c94-59hlk`). The new pod got a new random name, and it started empty.

### 3. What happens when the RabbitMQ pod is deleted or restarted?


### 4. Possible solutions


### 5. Does Azure Service Bus solve these problems?

## Lessons Learned

## References

1. [Run a Single-Instance Stateful Application (Kubernetes docs)](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/)
2. [Local Ephemeral Storage (Kubernetes docs)](https://kubernetes.io/docs/concepts/storage/ephemeral-storage/)
3. [Persistent Volumes (Kubernetes docs)](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
4. [What is Azure Service Bus? (Microsoft Learn)](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)
5. [StatefulSets (Kubernetes docs)](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
