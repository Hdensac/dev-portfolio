---
title: "Construire une API REST prête pour la production avec Node.js et Express"
date: 2024-12-10
summary: "Guide pratique pour concevoir une API REST maintenable, sécurisée et bien documentée avec Node.js, Express, TypeScript et Prisma."
tags:
  - Node.js
  - Express
  - API REST
  - Backend
  - Tutoriel
authors:
  - me
featured: true
---

Créer une API REST semble simple au départ. La difficulté arrive quand il faut gérer l'authentification, la validation, les erreurs, la documentation, les tests et la sécurité. Voici une base solide pour construire une API exploitable en production.

## Points clés

1. Structurer le projet dès le départ
2. Valider les entrées avec un schéma clair
3. Centraliser la gestion des erreurs
4. Sécuriser l'accès avec JWT et des en-têtes adaptés
5. Documenter les routes avec OpenAPI
6. Tester les cas critiques

## Structure recommandée

```text
src/
├── config/
├── controllers/
├── middleware/
├── models/
├── routes/
├── services/
├── utils/
├── validators/
└── app.ts
```

Une structure lisible facilite la maintenance. Les contrôleurs doivent rester légers, les services portent la logique métier, et les middlewares gèrent les traitements transverses comme l'authentification ou la validation.

## Authentification

```typescript
export const authenticate = async (req, res, next) => {
  try {
    const token = req.headers.authorization?.split(' ')[1]

    if (!token) {
      return res.status(401).json({ error: 'Authentification requise' })
    }

    req.user = jwt.verify(token, process.env.JWT_SECRET!)
    next()
  } catch {
    res.status(401).json({ error: 'Jeton invalide ou expiré' })
  }
}
```

Le secret JWT doit rester dans les variables d'environnement. Il ne doit jamais être écrit en dur dans le code source.

## Validation

Zod permet de vérifier les entrées avant qu'elles atteignent la logique métier :

```typescript
const createUserSchema = z.object({
  body: z.object({
    email: z.string().email('Adresse e-mail invalide'),
    name: z.string().min(2, 'Le nom doit contenir au moins 2 caractères'),
    password: z.string().min(8, 'Le mot de passe doit contenir au moins 8 caractères')
  })
})
```

Cette approche réduit les erreurs silencieuses et rend les réponses API plus prévisibles.

## Sécurité

- Activer `helmet` pour les en-têtes HTTP sensibles
- Configurer CORS selon les domaines autorisés
- Limiter le nombre de requêtes avec un rate limiter
- Nettoyer les entrées utilisateur
- Ne jamais renvoyer les mots de passe ou secrets dans les réponses

## Tests

Les tests doivent couvrir les routes critiques : création de compte, connexion, refus des données invalides, accès protégé et erreurs serveur. Avec Jest et Supertest, on peut vérifier le comportement complet de l'API sans dépendre d'une interface graphique.

## Documentation

OpenAPI ou Swagger aide les consommateurs de l'API à comprendre les routes, les paramètres attendus et les formats de réponse. Une documentation vivante évite beaucoup de confusion entre backend et frontend.

## Conclusion

Une bonne API REST repose sur quelques principes simples : structure claire, validation systématique, gestion d'erreurs centralisée, sécurité par défaut, tests utiles et documentation à jour. Ce sont ces détails qui transforment une API qui fonctionne en API réellement exploitable.
