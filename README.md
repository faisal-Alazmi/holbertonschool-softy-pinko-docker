# Softy Pinko Docker Project

A containerized web application infrastructure built with Docker, featuring a reverse proxy, load balancer, two API servers, and a front-end static server.

---

## Architecture

```
Client
  ↓
[Proxy Server - Port 80]  ← Single entry point (Nginx)
  ↓              ↓
[Front-end]    [Load Balancer]
  Port 9000       ↓        ↓
            [API Server 1] [API Server 2]
              Port 5252     Port 5252
```

---

## Requirements

- [Docker Desktop](https://www.docker.com/)
- Git Bash (Windows users)

---

## Tasks

### Task 0 — First Docker Image
Build a basic Ubuntu image that prints `Hello, World!`

```bash
docker build -f ./Dockerfile -t softy-pinko:task0 .
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
```

---

### Task 1 — Back-end
Flask API server with one endpoint `/api/hello` running on port 5252.

```bash
docker build -f ./Dockerfile -t softy-pinko:task1 .
docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
```

---

### Task 2 — Front-end
Nginx static server serving the Softy Pinko website on port 9000.

```bash
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
```

---

### Task 3 — Connecting Front-end and Back-end
Front-end fetches dynamic data from the back-end API using AJAX.  
Run both containers simultaneously in separate terminals.

**Terminal 1:**
```bash
docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3
```

**Terminal 2:**
```bash
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task3 softy-pinko-front-end:task3
```

---

### Task 4 — Docker Compose
Spin up both front-end and back-end with a single command using `docker-compose.yml`.

```bash
docker-compose build
docker-compose up
```

---

### Task 5 — Proxy Server
Add an Nginx reverse proxy as the single entry point on port 80.  
All traffic routes through the proxy to either the front-end or back-end.

```bash
docker-compose build
docker-compose up
```

Visit: `http://localhost:80`

---

### Task 6 — Horizontal Scaling
Scale the API to 2 servers with Round Robin load balancing via Nginx.

```bash
docker-compose up --scale back-end=2
```

---

## Technologies

| Tool | Purpose |
|------|---------|
| Docker | Containerization |
| Ubuntu | Base image |
| Python / Flask | Back-end API |
| Nginx | Front-end server & Reverse proxy |
| Docker Compose | Multi-container orchestration |

---

احفظه في **root المشروع** باسم `README.md` (مو داخل أي task).
