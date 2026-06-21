# Docker & Containerization

## 1. Architecture & The Need
- **The Need**: Solving the "It works on my machine" problem. An integration app might work locally because you have Java 11 installed, but fail in production because the server has Java 8. Docker packages the code *and* the environment together.
- **Architecture**: Unlike Virtual Machines which require a full heavy operating system for every app, Docker uses lightweight Containers that share the host machine's OS kernel but isolate the application processes, networking, and file systems.

## 2. Core Concepts
- **Image**: The read-only blueprint or template (e.g., an Ubuntu image with Java 11 and your compiled `.jar` file). Think of it like a Class in OOP.
- **Container**: The active, running instance of an Image. Think of it like an Object.
- **Volumes**: Persistent storage. If a container dies, all internal data is lost forever. Volumes map a folder inside the container to a folder on the host machine to save data.

## 3. Basic Daily Usage (Must-Know Commands)
- `docker build -t my_app .`: Read the Dockerfile in the current directory and build an Image named `my_app`.
- `docker run -d -p 8080:80 my_app`: Run the image as a container in the background (`-d`), mapping port 8080 on your laptop to port 80 inside the container.
- `docker ps`: List all running containers.
- `docker stop <container_id>`: Stop a running container gracefully.
- `docker logs -f <container_id>`: Watch the application logs inside the container.

## 4. Advanced Commands & Usage
- `docker exec -it <container_id> /bin/sh`: Open an interactive terminal session *inside* the running container to debug.
- `docker-compose up -d`: Orchestrate multiple containers at once (e.g., starting an API container AND a PostgreSQL database container together).
- `docker network inspect <network_name>`: Debug internal DNS and see which IP addresses Docker assigned to which containers.
- `docker system prune -a`: Delete all unused images, stopped containers, and networks to free up massive amounts of disk space.

---

## Interview Question Deep Dive

### Q: "Your containerized integration app works locally but fails to connect to the database in the production cluster. Why?"

**30-Second Answer**: It is almost always a networking or environment variable issue. The container in production is likely trying to hit `localhost` (which points to itself inside the container) instead of the actual database service name or IP address.

**2-Minute Answer**: When an app runs locally, the database might actually be on `localhost:5432`. But inside a Docker container, `localhost` means the container's own internal loopback interface. 

To fix this, the application code must never hardcode database URLs. It should read from environment variables (e.g., `DB_HOST`). Locally, I might pass `-e DB_HOST=localhost`, but in production via `docker-compose` or Kubernetes, I would pass `-e DB_HOST=database_service_name`. Docker's internal DNS will automatically resolve the service name to the correct container IP.

**Deep Dive Answer**: To troubleshoot this live, I wouldn't just guess. I would run `docker exec -it <container_id> /bin/sh` to drop into the running container's terminal. From there, I would run `env` to verify the environment variables were injected correctly. Then, I would use `ping` or `curl -v` to manually test network connectivity to the database service to see if it's a DNS resolution issue or a firewall blocking the port.

**Real Example**: I focus heavily on Docker to isolate environments. When writing complex Groovy scripts for Edifecs, ensuring the local development environment matches the exact Java runtime version of the production server is critical. Docker allows me to package the runtime and the code together.

**Follow-up Questions**:
- *Interviewer*: "If a container crashes and restarts, what happens to the data written inside it?" (Answer: It is lost forever, unless you mapped a volume using `-v` to persist data to the host machine).
