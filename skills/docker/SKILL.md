---
name: docker
description: |
  Docker container management standards. Usare per gestione container,
  docker-compose, creazione nuovi container, troubleshooting Docker.
---

## Directory Structure

```
/docker/
  <project-name>/
    docker-compose.yaml
    data/
      <service-name>/
```

## User & Group Configuration

- Tutti i container run as `docker` user (UID 1001, GID 110)
- Use `user: "1001:110"` in docker-compose.yaml
- Mai run come root unless esplicito

## Compose File Requirements

1. Define `user: "1001:110"` at service level
2. Use bind mounts for ALL persistent data (no volumes: with anonymous or named volumes)
3. Use relative paths per bind mounts
4. Specifica container names espliciti

## Data Storage

- **ALLOWED:** Bind mounts (`./data/...`)
- **FORBIDDEN:** Docker volumes

## Quick Reference

```yaml
volumes:
  - ./data/postgres:/var/lib/postgresql/data  # CORRETTO
  - postgres_data:/var/lib/postgresql/data    # FORBIDDEN

services:
  myapp:
    user: "1001:110"
```

## New Container Checklist

1. Create directory: `mkdir -p /docker/<project>/data/<service>`
2. Create docker-compose.yaml
3. Pre-create data directories
4. Test con `docker-compose up`