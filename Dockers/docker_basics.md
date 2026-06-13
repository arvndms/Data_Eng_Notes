# Docker Notes for Data Engineering Beginners

## What Problem Does Docker Solve?

Without Docker, an application depends on:

- Operating system settings
- Programming language versions
- Libraries/packages
- Environment variables
- Databases and other services

This often leads to:

> "It works on my machine."

Docker packages everything needed to run an application so it behaves consistently across different machines.

---

# Core Concepts

## Docker Image

An image is a blueprint or snapshot containing:

- Application code
- Dependencies
- Runtime (Python, Java, Node.js, etc.)
- Configuration
- Startup instructions

Think of it as:

```text
Recipe
Blueprint
Template
```

Example:

```text
Docker Image
├── Ubuntu/Linux
├── Python 3.12
├── Required Libraries
└── My Application
```

---

## Docker Container

A container is a running instance of an image.

Think:

```text
Class  → Object
Image  → Container
```

or

```text
Blueprint → House
Image     → Container
```

Example:

```bash
docker run my-app
```

Result:

```text
Image
  ↓
Container
  ↓
Running Application
```

---

# Docker Workflow

## Step 1: Write Application

```text
My App
```

## Step 2: Create Dockerfile

```dockerfile
FROM python:3.12

COPY . /app

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

## Step 3: Build Image

```bash
docker build -t my-app .
```

Creates:

```text
Docker Image
```

## Step 4: Run Container

```bash
docker run my-app
```

Creates:

```text
Running Container
```

---

# Why Not Just Run Code Directly?

You absolutely can:

```bash
python app.py
```

The issue is consistency.

Example:

### Your Laptop

```text
Python 3.12
Redis 7
```

### Server

```text
Python 3.10
Redis 6
```

Unexpected bugs may appear.

Docker ensures:

```text
Same Environment
Same Dependencies
Same Versions
```

everywhere.

---

# Why Run Docker Locally?

Common beginner question:

> "If Docker is for other people, why do I need it?"

Answer:

Docker is for YOU too.

Benefits:

### 1. Test the Deployment Environment

The same image you deploy is the one you test locally.

```text
Local
  ↓
Docker Image
  ↓
Production
```

### 2. Rebuild Environment Easily

New laptop?

Instead of reinstalling everything:

```text
Python
Database
Redis
Packages
Settings
```

Just run:

```bash
docker compose up
```

### 3. Avoid Team Conflicts

Without Docker:

```text
You      → Python 3.12
Teammate → Python 3.10
```

With Docker:

```text
You      → Same Image
Teammate → Same Image
```

---

# Registry

A registry stores Docker images.

Think:

```text
GitHub stores code

Docker Registry stores images
```

Workflow:

```text
Build Image
    ↓
Push to Registry
    ↓
Others Pull Image
    ↓
Run Container
```

Example:

```bash
docker push myuser/my-app
```

Someone else:

```bash
docker pull myuser/my-app
docker run myuser/my-app
```

---

# Can My Docker Run Other People's Containers?

Yes.

Docker is a platform for running containers.

Examples:

```bash
docker run nginx
docker run postgres
docker run redis
```

Your machine can run:

```text
Docker Engine
│
├── My App
├── PostgreSQL
├── Redis
├── Nginx
└── Other People's Apps
```

---

# Docker vs Virtual Machine

## Virtual Machine

```text
Hardware
  ↓
Host OS
  ↓
Hypervisor
  ↓
Guest OS
  ↓
Application
```

Each VM contains a full operating system.

---

## Docker Container

```text
Hardware
  ↓
Host OS
  ↓
Docker Engine
  ↓
Container
  ↓
Application
```

Containers share the host OS kernel.

Benefits:

- Faster startup
- Less memory
- Lightweight
- Easier scaling

---

# Why Docker Matters for Data Engineering

Data Engineering tools often require multiple services.

Example stack:

- Airflow
- PostgreSQL
- Redis
- Kafka
- Spark
- MinIO

Installing everything manually is difficult.

Docker allows:

```bash
docker compose up
```

to start an entire stack.

---

# Example: Airflow

Without Docker:

```text
Install Python
Install Airflow
Install PostgreSQL
Configure Airflow
Create Users
Debug Version Issues
```

With Docker:

```bash
docker compose up
```

Everything starts automatically.

---

# Isolation

Project A:

```text
Spark 3.5
Java 17
```

Project B:

```text
Spark 3.3
Java 11
```

Without Docker:

Potential conflicts.

With Docker:

```text
Container A
├── Spark 3.5
└── Java 17

Container B
├── Spark 3.3
└── Java 11
```

No conflicts.

---

# Typical Data Engineering Local Environment

```text
Docker
│
├── Airflow
├── PostgreSQL
├── Kafka
├── Spark
└── MinIO
```

Started with:

```bash
docker compose up
```

---

# Essential Commands

## Check Docker Version

```bash
docker --version
```

## List Running Containers

```bash
docker ps
```

## List All Containers

```bash
docker ps -a
```

## Pull Image

```bash
docker pull nginx
```

## Run Container

```bash
docker run nginx
```

## Stop Container

```bash
docker stop <container_id>
```

## Build Image

```bash
docker build -t my-app .
```

## Start Multi-Service Setup

```bash
docker compose up
```

## Stop Multi-Service Setup

```bash
docker compose down
```

---

# Key Takeaways

1. Docker is not primarily about running apps.
2. Docker is about running apps consistently everywhere.
3. Image = Blueprint.
4. Container = Running instance of an image.
5. Registries store images.
6. Docker helps both you and other developers.
7. Data Engineers use Docker heavily for Airflow, Spark, Kafka, databases, and local development environments.
8. A major benefit is reproducing production environments locally.
9. Docker containers are lighter than virtual machines.
10. Learning basic Docker is a valuable skill for modern Data Engineering.
