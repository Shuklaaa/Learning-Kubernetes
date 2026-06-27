# Kubernetes Clusters, Contexts, and Minikube Profiles

## Understanding the Terminology

One of the most confusing topics for beginners is the difference between:

* Cluster
* Context
* Namespace
* Minikube Profile

This guide explains each concept and the commands used to manage them.

---

# 1. What is a Cluster?

A **Cluster** is a complete Kubernetes environment.

It consists of:

* Control Plane
* Worker Node(s)
* API Server
* etcd
* Scheduler
* kube-proxy
* kubelet

Example:

```text
My Laptop

│

├── Cluster 1 (minikube)

│     ├── Node
│     ├── Pods
│     ├── Services
│     └── Deployments

│

└── Cluster 2 (dev-cluster)

      ├── Node
      ├── Pods
      ├── Services
      └── Deployments
```

With Minikube, each **profile** represents a separate Kubernetes cluster.

---

# 2. Check All Minikube Clusters (Profiles)

```bash
minikube profile list
```

Example output:

```text
PROFILE         DRIVER    STATUS
minikube        docker    Running
dev-cluster     docker    Stopped
```

Here you have **two Kubernetes clusters**.

---

# 3. Start a Specific Cluster

```bash
minikube start -p minikube
```

or

```bash
minikube start -p dev-cluster
```

The `-p` flag specifies the Minikube profile (cluster).

---

# 4. Stop a Cluster

```bash
minikube stop -p minikube
```

or

```bash
minikube stop -p dev-cluster
```

---

# 5. Delete a Cluster

Delete a specific cluster:

```bash
minikube delete -p dev-cluster
```

Delete all clusters:

```bash
minikube delete --all
```

---

# 6. What is a Context?

A **Context** tells `kubectl`:

* Which cluster to connect to
* Which user credentials to use
* Which namespace to use by default

Think of it as a shortcut.

```text
Context

├── Cluster
├── User
└── Namespace
```

When you execute a `kubectl` command, it uses the current context.

---

# 7. Check Current Context

```bash
kubectl config current-context
```

Example:

```text
minikube
```

This means all `kubectl` commands are currently talking to the **minikube** cluster.

---

# 8. List All Contexts

```bash
kubectl config get-contexts
```

Example:

```text
CURRENT   NAME
*         minikube
          dev-cluster
```

The `*` indicates the active context.

---

# 9. Switch Between Contexts

Switch to another cluster:

```bash
kubectl config use-context dev-cluster
```

Switch back:

```bash
kubectl config use-context minikube
```

---

# 10. List All Clusters in kubeconfig

```bash
kubectl config get-clusters
```

Example:

```text
NAME
minikube
dev-cluster
```

---

# 11. View Complete kubeconfig

```bash
kubectl config view
```

This displays:

* Clusters
* Users
* Contexts
* Certificates

---

# 12. Check Cluster Information

```bash
kubectl cluster-info
```

Example:

```text
Kubernetes control plane is running at https://127.0.0.1:xxxxx
CoreDNS is running at ...
```

---

# 13. Check Nodes

```bash
kubectl get nodes
```

Example:

```text
NAME       STATUS    ROLES
minikube   Ready     control-plane
```

---

# 14. Update Minikube Context

Sometimes after restarting Minikube, update the kubeconfig:

```bash
minikube update-context
```

---

# Relationship Between Cluster, Context, and Namespace

```text
                    kubeconfig

                         │

               Current Context

                         │

      ┌──────────────────┴──────────────────┐

      │                                     │

   Cluster                           User Credentials

      │

Default Namespace

      │

Pods, Services, Deployments
```

A context simply points `kubectl` to:

* A cluster
* A user
* A default namespace

---

# Cluster vs Context

| Cluster                        | Context                                |
| ------------------------------ | -------------------------------------- |
| Actual Kubernetes environment  | Configuration used by kubectl          |
| Contains Nodes, Pods, Services | Points to a Cluster + User + Namespace |
| Runs workloads                 | Decides where kubectl sends commands   |

---

# Minikube Profiles vs Kubernetes Contexts

| Minikube Profile             | Kubernetes Context            |
| ---------------------------- | ----------------------------- |
| Creates a Kubernetes cluster | Connects kubectl to a cluster |
| Example: `minikube`          | Example: `minikube`           |
| Example: `dev-cluster`       | Example: `dev-cluster`        |

In Minikube, a profile usually has a corresponding context with the same name.

---

# Common Workflow

### Check available clusters

```bash
minikube profile list
```

### Check current context

```bash
kubectl config current-context
```

### List contexts

```bash
kubectl config get-contexts
```

### Switch context

```bash
kubectl config use-context dev-cluster
```

### Verify cluster

```bash
kubectl cluster-info
```

### Check nodes

```bash
kubectl get nodes
```

---

# Frequently Used Commands

```bash
# List Minikube clusters (profiles)
minikube profile list

# Start a cluster
minikube start -p <profile-name>

# Stop a cluster
minikube stop -p <profile-name>

# Delete a cluster
minikube delete -p <profile-name>

# Show current Kubernetes context
kubectl config current-context

# List all contexts
kubectl config get-contexts

# Switch context
kubectl config use-context <context-name>

# List clusters in kubeconfig
kubectl config get-clusters

# View kubeconfig
kubectl config view

# Display cluster information
kubectl cluster-info

# List nodes
kubectl get nodes

# Refresh Minikube context
minikube update-context
```

---

# Interview Questions

### 1. What is the difference between a Cluster and a Context?

A **Cluster** is the actual Kubernetes environment where workloads run.

A **Context** is a kubeconfig entry that tells `kubectl` which cluster, user, and namespace to use.

---

### 2. What is a Minikube Profile?

A Minikube profile is an independent local Kubernetes cluster. Each profile has its own nodes, resources, and kubeconfig context.

---

### 3. How do you switch between Kubernetes clusters?

```bash
kubectl config use-context <context-name>
```

---

### 4. How do you list all available clusters?

```bash
kubectl config get-clusters
```

For Minikube profiles:

```bash
minikube profile list
```

---

# Key Takeaways

* A **Cluster** is a Kubernetes environment.
* A **Minikube Profile** creates and manages a local Kubernetes cluster.
* A **Context** tells `kubectl` which cluster, user, and namespace to use.
* Most `kubectl` issues in multi-cluster setups are caused by being connected to the wrong context.
* Always verify the current context before deploying resources using:

```bash
kubectl config current-context
```
