# Kubernetes (K8s) Overview

## Definition
Kubernetes is an open-source container orchestration platform originally developed by Google. 

## Why it exists
Docker is great for running one container on one laptop. But if you have an enterprise app with 50 microservices running across 10 different servers, Docker alone cannot handle load balancing, self-healing, scaling, or rolling updates. Kubernetes acts as the "operating system" for a cluster of servers, managing where and how containers run.

## Commands
- `kubectl get pods`: List all pods in the default namespace.
- `kubectl describe pod <pod_name>`: View detailed events and status of a specific pod (crucial for debugging `CrashLoopBackOff`).
- `kubectl logs -f <pod_name>`: View the logs of the container inside the pod.
- `kubectl apply -f deployment.yaml`: Deploy or update resources based on a YAML file.
- `kubectl get services`: View load balancers and internal IPs.

## Architecture
- **Control Plane (The Brain)**: 
  - *API Server*: The front door. Everything talks to this.
  - *etcd*: The highly available database storing cluster state.
  - *Scheduler*: Decides which Worker Node should run a new pod.
- **Worker Nodes (The Muscle)**: 
  - *Kubelet*: The agent on each node that talks to the API Server.
  - *Pod*: The smallest deployable unit. Usually contains one Docker container.
- **Resources**:
  - *Deployment*: Manages replicas (e.g., "Ensure exactly 3 copies of my API are always running").
  - *Service*: Provides a stable IP address and load balances traffic across the pods.

## Interview Questions
**Q: "What is the difference between a Pod, a Deployment, and a Service?"**
*Answer*: A **Pod** is the actual running container. Pods are mortal—they die and get replaced constantly, getting a new IP address every time. A **Deployment** is the manager that ensures the desired number of Pods are running. A **Service** is the stable networking layer; it sits in front of the Pods, providing a permanent IP address and load-balancing traffic to the Pods even as they die and respawn.

**Q: "Your pod is stuck in a `CrashLoopBackOff` state. How do you troubleshoot it?"**
*Answer*: First, I run `kubectl describe pod <pod_name>` to see if it's failing a readiness/liveness probe or if there is an image pull error. Next, I run `kubectl logs <pod_name> --previous` to see the actual application stack trace right before the container crashed. Usually, it's a missing environment variable causing the app to fail on startup.

## Cheat Sheet
| Concept | Explanation |
| :--- | :--- |
| **Namespace** | Virtual clusters. A way to divide a cluster into "Dev", "Test", and "Prod". |
| **ConfigMap** | Stores non-sensitive configuration data (like URLs) separately from the image. |
| **Secret** | Stores sensitive data (like DB passwords) encoded in Base64. |
| **Ingress** | The HTTP/HTTPS router that exposes Services to the outside internet. |
