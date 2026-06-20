Before learning Kubernetes, understand **why Kubernetes exists**.

Kubernetes is not just another tool. It was created to solve the limitations of running containers with Docker alone.

Prerequisite:

* Docker
* Container fundamentals
* Namespaces
* Container isolation
* Multi-stage builds
* Container networking

---

# Docker vs Kubernetes

## Docker

Docker is a container platform.

It helps:

* Build containers
* Run containers
* Package applications

However, Docker alone is not sufficient for large-scale production environments.

## Kubernetes

Kubernetes is a **container orchestration platform**.

Its job is to:

* Manage containers
* Scale containers
* Heal failed containers
* Handle production workloads

---

# Why Kubernetes?

As organizations moved towards microservices, the number of containers increased significantly.

Running a few containers with Docker is easy.

Running thousands of containers in production becomes difficult.

Kubernetes solves these challenges.

---

# Problem 1: Single Host Dependency

## Docker Scenario

```text
Host
 └── Docker
      ├── Container 1
      ├── Container 2
      ├── Container 3
      └── Container N
```

All containers run on a single machine.

If:

* Host fails
* Memory becomes exhausted
* CPU becomes overloaded

Applications are affected.

### Limitation

Docker primarily operates on a single host.

---

## Kubernetes Solution

Kubernetes works as a Cluster.

```text
Cluster
 ├── Node 1
 ├── Node 2
 ├── Node 3
 └── Node N
```

If one node becomes unhealthy:

* Workloads can move to another node.
* Applications remain available.

Key takeaway:

> Kubernetes is cluster-based, not single-host based.

---

# Problem 2: Auto Healing

## Docker Scenario

Suppose a container crashes.

```bash
docker ps
```

A DevOps Engineer must:

* Identify failure
* Restart container manually

Example:

```bash
docker restart container-id
```

This is not practical when managing thousands of containers.

---

## Kubernetes Solution

Kubernetes automatically detects failures.

If a container or pod crashes:

* Kubernetes recreates it automatically.
* User intervention is not required.

This behavior is called:

### Auto Healing

Key takeaway:

> Kubernetes constantly tries to maintain the desired state.

---

# Problem 3: Auto Scaling

## Scenario

Normal traffic:

```text
10,000 Users
```

Festival season or movie release:

```text
100,000+ Users
```

One container may not be enough.

---

## Docker Limitation

Scaling is mostly manual.

Engineer must:

* Create additional containers
* Configure traffic routing

---

## Kubernetes Solution

Kubernetes can automatically:

* Increase replicas
* Decrease replicas

Based on:

* CPU usage
* Memory usage
* Traffic load

This feature is called:

### Auto Scaling

Key takeaway:

> More traffic → More Pods

> Less traffic → Fewer Pods

---

# Problem 4: Load Balancing

When multiple container instances exist:

```text
Container 1
Container 2
Container 3
Container 4
```

Traffic must be distributed evenly.

---

## Kubernetes Solution

Kubernetes provides built-in load balancing.

```text
Users
   ↓
Load Balancer
   ↓
Pods
```

Traffic gets distributed automatically.

---

# Problem 5: Enterprise-Level Support

Large organizations require:

* Load Balancers
* Firewalls
* Scaling
* High Availability
* Auto Healing
* API Gateways
* Security Controls

Docker alone does not provide these capabilities out of the box.

Kubernetes supports enterprise-grade deployments.

Examples mentioned:

* Netflix
* Large-scale production systems

---

# Kubernetes Cluster Concept

Kubernetes is usually deployed as a Cluster.

```text
Master Node
      |
--------------------
|        |         |
Node1   Node2    Node3
```

Benefits:

* High Availability
* Better Resource Utilization
* Fault Tolerance

---

# Interview Question

## What problem does Kubernetes solve?

Kubernetes solves:

1. Single-host dependency
2. Auto healing
3. Auto scaling
4. Load balancing
5. Enterprise-level production requirements

---

# Important Definitions

## Container Orchestration

Managing containers automatically at scale.

Examples:

* Deployment
* Scaling
* Monitoring
* Recovery

---

## Auto Healing

Automatic recovery of failed containers or pods.

---

## Auto Scaling

Automatic increase or decrease of application instances based on demand.

---

## Cluster

A group of machines working together to run applications.
---

