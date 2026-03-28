# Docker Concepts Notes — Week 5 Monday

---

## Why Docker Matters for Cloud Jobs

Containers are now standard in cloud operations. Engineers who understand Docker resolve deployment incidents faster and are more competitive in the 2026 job market. You need to know what containers are, why they exist, and how to use basic commands.

---

## What is a Container?

A container is a **lightweight, isolated environment** that packages an application and everything it needs to run — code, runtime, libraries, config files — into one portable unit.

The container runs identically on any machine — your laptop, a test server, or an Azure VM — because the environment is packaged with the application.

**The problem containers solve:**
> "It works on my machine but not in production"

With containers this problem disappears because the environment is always the same.

---

## Docker vs Virtual Machine

Most common interview question — know this cold.

| | Virtual Machine | Docker Container |
|---|---|---|
| **Includes** | Full operating system + app | App + dependencies only |
| **Size** | Gigabytes | Megabytes |
| **Startup time** | Minutes | Seconds |
| **Resource usage** | Heavy — each VM needs its own OS | Light — containers share host OS kernel |
| **Isolation** | Complete separate OS | Process-level, shared kernel |

**Simple analogy:**
- VM = a separate house with its own foundation, plumbing, electricity
- Container = an apartment — shares the building infrastructure but has its own private space

---

## Docker Image vs Container

These two are the most confused terms in Docker. Know the difference.

### Docker Image
- A **read-only template** used to create containers
- Cannot be changed after it is built
- Like a **class** in programming — defines the blueprint
- Stored on Docker Hub or a private registry
- Examples: `nginx`, `python:3.12`, `ubuntu:22.04`

### Docker Container
- A **running instance** of an image
- Like an **object** created from a class
- Can be started, stopped, deleted
- Many containers can run from the same image at the same time

**Analogy:**
- Image = a recipe
- Container = the dish made from the recipe
- You can make many dishes from one recipe

---

## Core Docker Concepts

### Dockerfile
A text file with step-by-step instructions for building a Docker image.

```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

- `FROM` — which base image to start from
- `COPY` — copy files from your machine into the image
- `EXPOSE` — which port the app uses inside the container

### Docker Hub
The public registry where Docker images are stored. Free official images include `nginx`, `python`, `ubuntu`, `mysql`. Pull any image with `docker pull`.

### Port Mapping
Connects a port on your host machine to a port inside the container.

```
-p 8080:80
```

Host port 8080 → Container port 80. Open browser at `localhost:8080` and traffic reaches the container's port 80.

---

## Essential Docker Commands

```bash
# Download an image
docker pull nginx

# Run a container
docker run -d -p 8080:80 --name my-container nginx
# -d = run in background (detached mode)
# -p = port mapping host:container
# --name = give the container a name

# See running containers
docker ps

# See all containers including stopped
docker ps -a

# See downloaded images
docker images

# View container logs
docker logs my-container

# Stop a container
docker stop my-container

# Remove a container
docker rm my-container

# Remove an image
docker rmi nginx

# Build image from Dockerfile
docker build -t my-app .
# -t = tag (name) the image
# . = use Dockerfile in current directory

# Inspect container details
docker inspect my-container
```

---

## Running Your First Container

```bash
# Pull nginx image
docker pull nginx

# Run it
docker run -d -p 8080:80 --name my-first-container nginx

# Open browser → localhost:8080
# You should see the nginx welcome page

# Confirm it is running
docker ps

# Stop and clean up
docker stop my-first-container
docker rm my-first-container
```

---

## Building Your Own Image

```bash
# Create project folder
mkdir my-portfolio
cd my-portfolio
```

Create `index.html`:
```html
<h1>My Cloud Portfolio — Afaq Tahir</h1>
```

Create `Dockerfile`:
```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

```bash
# Build the image
docker build -t my-portfolio .

# Run it
docker run -d -p 8081:80 my-portfolio

# Open browser → localhost:8081
```

---

## Docker Troubleshooting

### Container keeps restarting
```bash
docker logs my-container
```
Read the error output. Common causes: app crash on startup, missing config, port already in use.

### App not reachable from browser
1. Check container is running: `docker ps`
2. Check port mapping is correct in your `docker run` command
3. Check if another process uses that host port: `netstat -an | findstr 8080` on Windows

### Image not found
```bash
docker images          # Check if image exists locally
docker pull nginx      # Pull from Docker Hub if missing
```

---

## How to Answer Docker Questions in Interviews

**Q: What is Docker and why do we use it?**
Docker packages an application and all its dependencies into a container. The container runs identically on any machine — development laptop, test server, or cloud VM. This eliminates the classic "it works on my machine" problem because the environment is always the same.

**Q: What is the difference between a container and a VM?**
A VM includes a full operating system — heavy, takes minutes to start, uses gigabytes. A container shares the host OS kernel — lightweight, starts in seconds, uses megabytes. You can run hundreds of containers where you might only run a few VMs on the same hardware.

**Q: What is a Docker image vs a container?**
An image is a read-only template — like a recipe. A container is a running instance of that image — like the dish made from the recipe. Many containers can run from the same image simultaneously.

**Q: Have you worked with Docker?**
Yes — I built and ran Docker containers as part of my cloud learning portfolio. I created a Dockerfile for a static web application, built the image, and ran it with port mapping. My container portfolio is visible at my GitHub repository.

---

## Docker vs Kubernetes — One Paragraph

Docker runs containers on a **single host**. When you need to manage hundreds of containers across many servers automatically, you need Kubernetes. Kubernetes orchestrates containers — it restarts failed containers, distributes load, rolls out updates without downtime, and scales up or down based on demand. Docker is one driver. Kubernetes is the traffic management system for thousands of drivers across an entire city.

---

## Key Terms Summary

| Term | Meaning |
|---|---|
| Container | Isolated running environment for an application |
| Image | Read-only template used to create containers |
| Dockerfile | Instructions file for building an image |
| Docker Hub | Public registry storing Docker images |
| Port mapping `-p` | Connects host port to container port |
| `docker ps` | Shows running containers |
| `docker images` | Shows downloaded images |
| `docker logs` | Shows container output |
| `docker build` | Creates image from Dockerfile |
| `docker run` | Creates and starts a container |
