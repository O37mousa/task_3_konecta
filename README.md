# Task_3 KONECTA 

## 🐧1️⃣ Running Ubuntu Container with Docker

This guide explains how to run an Ubuntu container using Docker, why it may exit immediately, and how to keep it running.

---

###  Run Ubuntu Container

To run an Ubuntu container:

```bash
# Basic run command
docker run ubuntu

# If permission is denied, use sudo
sudo docker run ubuntu
```

### Check Running Containers

To check all containers (including stopped ones):

```bash
sudo docker ps -a
```

### ❓ Why Can't You See the Container?
The Ubuntu container exits immediately because there's no running process inside it.
By default, Docker starts the container, runs the default command (bash), and exits if there's no interaction or ongoing task.

### How to Keep the Container Running
Use the interactive mode to keep the container alive:
```bash
sudo docker run -it ubuntu
```

---

## 2. Create a Dockerfile for the Flask Application

# ⚙️ Docker Compose Summary – Flask + PostgreSQL

This setup defines two services using Docker Compose:

---

## 🖥️ `web` (Flask App)
- **Builds** from local `Dockerfile`
- **Environment Variables**:
  - `FLASK_APP`, `FLASK_RUN_HOST`, `FLASK_ENV`
  - `DATABASE_URL` for PostgreSQL connection
- **Ports**: Maps `5000` (host) to `5000` (container)
- **Depends on**: `db` service (PostgreSQL)

---

## 🗄️ `db` (PostgreSQL)
- **Uses** the official `postgres:latest` image
- **Environment Variables**:
  - `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`
- **Volume**: Persists data using `db_data`

---

## 💾 Volume
- `db_data`: Stores PostgreSQL data persistently

---

## 🚀 Usage
- Start services: `docker-compose up --build`
- Stop: `docker-compose down`

