# Sibers Project - Full Stack Deployment

Full stack application combining backend (ASP.NET Core + SQLite) and frontend (Vue 3 + Vite) using Docker Compose.

## Structure

- **Backend**: ASP.NET Core Web API with SQLite database
- **Frontend**: Vue 3 application with Vite, Pinia, and Vue Router
- **Database**: SQLite (persistent volume)

## Prerequisites

- Docker
- Docker Compose

## Quick Start

```bash
# Clone the repository
git clone git@github.com:noitorraa/web-app-deploy.git
# Build and start all services
docker-compose up -d --build
```

## Services

| Service  | Port | Description       |
| -------- | ---- | ----------------- |
| Frontend | 3000 | Vue 3 application |
| Backend  | 8080 | ASP.NET Core API  |

## Access

- **Frontend**: <http://localhost:3000>
- **Backend API**: <http://localhost:8080> (also accessible via /api proxy from frontend)

## Management

```bash
# View logs
docker-compose logs -f

# Stop all services
docker-compose down

# Stop and remove volumes (clean slate)
docker-compose down -v

# Rebuild and restart
docker-compose up -d --build --force-recreate
```

## Architecture

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Browser    │───▶│   Nginx     │───▶│  Backend    │
└─────────────┘    │ (Frontend)  │    │ (ASP.NET)   │
                    └─────────────┘    └─────────────┘
                         │                     │
                         ▼                     ▼
                    ┌─────────────┐    ┌─────────────┐
                    │   Static    │    │   SQLite    │
                    │   Files     │    │   Database  │
                    └─────────────┘    └─────────────┘
```

The frontend makes API requests to `/api` which are proxied by Nginx to the backend service within the Docker network.
