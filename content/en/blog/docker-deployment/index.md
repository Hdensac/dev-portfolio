---
title: "Deploying an Application with Docker: From Development to Production"
date: 2024-10-15
summary: "A practical guide to containerizing an application, optimizing Docker images, and preparing a more reliable deployment."
tags:
  - Docker
  - DevOps
  - Deployment
  - Tutorial
authors:
  - me
featured: false
---

Docker simplifies deployment by packaging an application with its dependencies. The goal is simple: get a reproducible environment that stays close to production and is easier to move from one machine to another.

## Why Docker?

Docker helps solve several common problems:

- The application works on one machine but not another
- Dependencies are hard to reproduce
- Development and production environments drift apart
- Deployment becomes too manual

## Basic Dockerfile

Minimal example for a Node.js application:

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000
CMD ["node", "server.js"]
```

Build and run:

```bash
docker build -t my-app .
docker run -p 3000:3000 my-app
```

## Optimize with multi-stage builds

Multi-stage builds keep compilation tools in a separate stage and copy only the final output into the production image.

```dockerfile
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:18-alpine

WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

EXPOSE 3000
CMD ["node", "dist/server.js"]
```

This technique often reduces image size significantly.

## Docker Compose locally

`docker-compose.yml` can run the application with its dependencies:

```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb
```

## Best practices

- Add a `.dockerignore` file
- Use a lightweight and versioned base image
- Run the application as a non-root user
- Never write secrets into the image
- Add a health check
- Scan images for vulnerabilities
- Tag images with clear versions

## Pre-production checklist

- Environment variables configured
- Database migrations applied
- Usable logs available
- Health check available
- Backup and restore planned
- Image tested in a staging environment

## Conclusion

Docker makes deployments more reproducible, but it does not replace good operations practices. A clean, lightweight, secure, and tested image remains the foundation of a reliable production deployment.
