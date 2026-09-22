---
title: "Déployer une application avec Docker : du développement à la production"
date: 2024-10-15
summary: "Guide pratique pour conteneuriser une application, optimiser les images Docker et préparer un déploiement plus fiable."
tags:
  - Docker
  - DevOps
  - Déploiement
  - Tutoriel
authors:
  - me
featured: false
---

Docker facilite le déploiement en emballant une application avec ses dépendances. L'objectif est simple : obtenir un environnement reproductible, proche de la production, et plus facile à déplacer d'une machine à l'autre.

## Pourquoi Docker ?

Docker aide à résoudre plusieurs problèmes classiques :

- L'application fonctionne sur une machine mais pas sur une autre
- Les dépendances sont difficiles à reproduire
- Les environnements de développement et de production divergent
- Le déploiement devient trop manuel

## Dockerfile de base

Exemple minimal pour une application Node.js :

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000
CMD ["node", "server.js"]
```

Construction et lancement :

```bash
docker build -t my-app .
docker run -p 3000:3000 my-app
```

## Optimiser avec le multi-stage build

Le multi-stage build permet de garder les outils de compilation dans une étape séparée et de ne copier que le résultat final dans l'image de production.

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

Cette technique réduit souvent fortement la taille de l'image.

## Docker Compose en local

`docker-compose.yml` permet de lancer l'application avec ses dépendances :

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

## Bonnes pratiques

- Ajouter un fichier `.dockerignore`
- Utiliser une image de base légère et versionnée
- Exécuter l'application avec un utilisateur non root
- Ne jamais écrire les secrets dans l'image
- Activer un health check
- Scanner les images contre les vulnérabilités
- Taguer les images avec une version claire

## Checklist avant production

- Variables d'environnement configurées
- Migrations de base de données exécutées
- Logs exploitables
- Health check disponible
- Sauvegarde et restauration prévues
- Image testée dans un environnement de préproduction

## Conclusion

Docker rend les déploiements plus reproductibles, mais il ne remplace pas les bonnes pratiques d'exploitation. Une image propre, légère, sécurisée et testée reste la base d'une mise en production fiable.
