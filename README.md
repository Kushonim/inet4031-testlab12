# INET 4031 Test Lab 12 — Docker Full Stack Ticket System
## Author: Austin Lee | Kushonim
## Date Last Modified: 4/13/2026

## Overview
This project is a containerized full-stack ticket system built with Docker Compose. It includes:
- Flask API backend
- MariaDB database
- Apache web server frontend/proxy

The application allows users to view and create support tickets through both a web interface and a REST API.

---

## System Architecture
- **db (MariaDB)**: Stores ticket data with persistent storage using Docker volumes  
- **app (Flask API)**: Handles API requests and database operations  
- **web (Apache)**: Serves frontend and routes API requests to Flask  

---

## How to Start the System

```bash
docker compose up --build
```

## Verify Containers
```bash
docker compose ps
```

Expected:

- db → healthy
- app → healthy
- web → running

## API Endpoints
**Health Check**
```bash
curl http://localhost/health
```

Expected:
```bash
{"database":"connected","status":"healthy"}
```

## Get Tickets
```bash
curl http://localhost/api/tickets
```
Returns a JSON array of tickets.

## Create Ticket
```bash
curl -X POST http://localhost/api/tickets \
  -H "Content-Type: application/json" \
  -d '{"title":"Test Ticket","description":"API test"}'
```

Expected:
```bash
{"id": 12, "message": "Ticket created successfully"}
```

## Web Interface

Open in browser:

```bash
http://<VM-IP>:80
```
Expected:

- Ticket dashboard loads
- “API healthy” indicator is green
- Tickets are visible
- New tickets can be created from the form

## Data Persistence

Tickets persist using a Docker volume.

Test persistence:
```bash
docker compose stop db
docker compose start db
curl http://localhost/api/tickets
```

## Port Requirements

Port 80 must be free on the host machine.

If needed:
```bash
sudo systemctl stop apache2
```

## Verification Script

Run:
```bash
chmod +x check-lab.sh
./check-lab.sh
```
Expected:
```bash
Results: 9 passed, 0 failed
All checks passed
```
