# Docker Overview

## Definition
Docker is an open-source platform for containerizing applications. It packages code, runtimes, system tools, and libraries into a single standard unit called a container.

## Why it exists
To solve the "It works on my machine!" problem. Instead of an integration engineer spending 3 days configuring Java 1.8, TomCat, and specific environment variables on a new server, Docker allows them to run the application exactly as it ran on their laptop, completely isolated from the host OS.

## Commands
- `docker build -t my_app .`: Build an Image using the `Dockerfile` in the current folder.
- `docker run -d -p 8080:80 my_app`: Run the image in detached mode (`-d`), mapping port 8080 on the host to port 80 in the container.
- `docker ps`: List active running containers.
- `docker exec -it <container_id> /bin/sh`: Drop into a terminal shell inside the running container (crucial for debugging).
- `docker logs -f <container_id>`: Tail the application logs.
- `docker system prune -a`: Delete all unused images/containers to save disk space.

## Architecture
- **Image**: The read-only blueprint (e.g., Ubuntu + Java + Your App). Similar to an OOP Class.
- **Container**: The running instance of an Image. Similar to an OOP Object.
- **Volumes**: Storage. If a container dies, all internal data is destroyed. Volumes map a folder inside the container to the host machine for persistence.
- **Networks**: Containers run on isolated bridge networks and communicate via internal DNS.

## Interview Questions
**Q: "Your containerized API works locally but fails to connect to the database in production. Why?"**
*Answer*: The app is likely hardcoded to connect to `localhost`. Inside a Docker container, `localhost` refers to the container itself, not the host machine or the database server. Applications must be parameterized to use environment variables (e.g., `DB_HOST`) so that Docker-Compose or Kubernetes can inject the correct service name at runtime.

**Q: "What is the difference between Virtual Machines (VMs) and Containers?"**
*Answer*: VMs virtualize the hardware. Every VM runs a full, heavy operating system (Guest OS), which eats up massive amounts of RAM. Containers virtualize the OS. They share the host's Kernel, making them incredibly lightweight—spinning up in milliseconds rather than minutes.

## Cheat Sheet (Dockerfile)
| Keyword | Purpose |
| :--- | :--- |
| `FROM` | Base image (e.g., `FROM openjdk:11`) |
| `WORKDIR` | Sets the working directory inside the container |
| `COPY` | Copies files from your laptop into the container |
| `RUN` | Executes a shell command during the *build* phase |
| `ENV` | Sets environment variables |
| `EXPOSE` | Documents which port the app listens on |
| `CMD` | The command that runs when the container *starts* |
