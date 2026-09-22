---
title: "Building a Production-Ready REST API with Node.js and Express"
date: 2024-12-10
summary: "A practical guide to designing a maintainable, secure, and well-documented REST API with Node.js, Express, TypeScript, and Prisma."
tags:
  - Node.js
  - Express
  - REST API
  - Backend
  - Tutorial
authors:
  - me
featured: true
---

Creating a REST API feels simple at first. The real challenge starts when authentication, validation, error handling, documentation, tests, and security all become part of the same production system.

## Key points

1. Structure the project from the beginning
2. Validate inputs with clear schemas
3. Centralize error handling
4. Secure access with JWT and proper headers
5. Document routes with OpenAPI
6. Test critical flows

## Recommended structure

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

A readable structure makes maintenance easier. Controllers should stay light, services should carry business logic, and middleware should handle cross-cutting concerns such as authentication and validation.

## Authentication

```typescript
export const authenticate = async (req, res, next) => {
  try {
    const token = req.headers.authorization?.split(' ')[1]

    if (!token) {
      return res.status(401).json({ error: 'Authentication required' })
    }

    req.user = jwt.verify(token, process.env.JWT_SECRET!)
    next()
  } catch {
    res.status(401).json({ error: 'Invalid or expired token' })
  }
}
```

JWT secrets must stay in environment variables. They should never be hardcoded in the source code.

## Validation

Zod helps validate inputs before they reach business logic:

```typescript
const createUserSchema = z.object({
  body: z.object({
    email: z.string().email('Invalid email address'),
    name: z.string().min(2, 'Name must be at least 2 characters'),
    password: z.string().min(8, 'Password must be at least 8 characters')
  })
})
```

This approach reduces silent failures and makes API responses more predictable.

## Security

- Enable `helmet` for sensitive HTTP headers
- Configure CORS for trusted domains
- Add rate limiting
- Sanitize user input
- Never return passwords or secrets in responses

## Tests

Tests should cover critical routes: account creation, login, invalid data rejection, protected access, and server errors. With Jest and Supertest, it is possible to verify API behavior without depending on a graphical interface.

## Documentation

OpenAPI or Swagger helps API consumers understand routes, expected parameters, and response formats. Living documentation avoids a lot of confusion between backend and frontend work.

## Conclusion

A strong REST API is built on clear structure, systematic validation, centralized errors, secure defaults, useful tests, and up-to-date documentation. Those details turn a working API into a production-ready API.
