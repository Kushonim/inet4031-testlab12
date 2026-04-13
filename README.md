# INET 4031 Test Lab 12 — Docker Full Stack Ticket System
## Author: Austin Lee | Kushonim
## Date Last Modified: 4/13/2026

## Overview
This project is a containerized full-stack ticket management system built using Docker Compose. It includes a Flask API, a MariaDB database, and an Apache web server acting as a frontend proxy.

The system supports:
- Viewing tickets via API and web UI
- Creating new tickets
- Persistent database storage
- Health checks for service monitoring

---

## Architecture

The stack contains three services:

- **db (MariaDB 11.4)**  
  Stores ticket data in a persistent volume.

- **app (Flask API)**  
  Handles REST API requests and communicates with the database.

- **web (Apache)**  
  Serves the frontend and proxies requests to the Flask API.

---

## How to Run the Stack

### Build and start all services:
```bash
docker compose up --build
