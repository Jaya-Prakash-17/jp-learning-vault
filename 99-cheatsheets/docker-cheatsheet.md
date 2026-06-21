# Docker Cheat Sheet

### Core Concepts
- **Image**: Read-only blueprint/template (Code + OS + Runtime). Like an OOP Class.
- **Container**: Running instance of an Image. Like an OOP Object.
- **Volume**: Persistent storage mapping. Containers are ephemeral (when they die, data dies). Volumes save data to the host.
- **Docker Compose**: Tool to orchestrate multiple containers at once (API + DB).

### Daily Commands (Must Know)
| Command | Action |
| :--- | :--- |
| `docker build -t app .` | Build an image from the local Dockerfile. |
| `docker run -d -p 80:80 app` | Run container in background, mapping HostPort:ContainerPort. |
| `docker ps` | List active containers. |
| `docker stop <id>` | Gracefully shut down a container. |
| `docker logs -f <id>` | Tail application logs inside container. |

### Advanced Troubleshooting
| Command | Action |
| :--- | :--- |
| `docker exec -it <id> /bin/sh` | Drop into a terminal inside the running container. |
| `docker system prune -a` | Delete unused images/containers to free disk space. |
| `docker inspect <id>` | View internal JSON metadata (IPs, mounts, env vars). |

### Dockerfile Keywords
- `FROM`: Base OS/Runtime (e.g., `openjdk:11`).
- `COPY`: Move files from laptop to container image.
- `RUN`: Execute a command *during the build process*.
- `ENV`: Define an environment variable.
- `CMD`: The command executed *when the container starts*.

### Interview Triggers
- 🚨 **"VM vs Container"** ➡️ Trigger: VMs virtualize the hardware (heavy, slow). Containers virtualize the OS and share the host Kernel (lightweight, ms startup).
- 🚨 **"Container fails to connect to Production DB"** ➡️ Trigger: Don't use `localhost`. In Docker, `localhost` = the container itself. Use injected Environment Variables (`DB_HOST`) relying on Docker's internal DNS.
