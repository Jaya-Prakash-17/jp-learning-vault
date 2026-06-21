# Kubernetes (K8s) Cheat Sheet

### Core Architecture
**Control Plane (The Brain):**
- **API Server**: Front door for all `kubectl` commands.
- **etcd**: Key-value datastore of cluster state.
- **Scheduler**: Assigns Pods to Worker Nodes.

**Worker Nodes (The Muscle):**
- **Kubelet**: Agent that talks to the API server.
- **Pod**: Smallest unit. Wraps 1+ Docker containers.

### K8s Resources
| Resource | Purpose |
| :--- | :--- |
| **Pod** | The mortal, running container. Dies frequently. |
| **Deployment** | The manager. Ensures *X* replicas of a Pod are always running. |
| **Service** | The network router. Gives a stable IP/DNS to volatile Pods. |
| **Ingress** | Exposes HTTP/HTTPS routes from outside the cluster to Services. |
| **ConfigMap** | Stores non-sensitive variables/URLs separately from the image. |
| **Secret** | Stores Base64 encoded passwords/keys. |

### Daily Commands (Must Know)
| Command | Action |
| :--- | :--- |
| `kubectl get pods -n <namespace>` | List pods in a namespace. |
| `kubectl apply -f app.yaml` | Deploy/Update resources declaratively. |
| `kubectl delete pod <name>` | Kill a pod (Deployment will recreate it). |

### Advanced Troubleshooting
| Command | Action |
| :--- | :--- |
| `kubectl describe pod <name>` | View pod events. Find why it's pending/crashing. |
| `kubectl logs -f <name>` | View container stdout logs. |
| `kubectl logs <name> --previous`| View logs of the *previously* crashed container. |
| `kubectl exec -it <name> -- sh` | Drop into shell inside the pod. |

### Interview Triggers
- 🚨 **"Pod vs Deployment vs Service"** ➡️ Trigger: Pod = Mortal Container. Deployment = Immortal Manager. Service = Stable IP Router.
- 🚨 **"CrashLoopBackOff Error"** ➡️ Trigger: `describe pod` to check Readiness/Liveness probes or ImagePullBackOff. `logs --previous` to find the Java stack trace that killed the container.
