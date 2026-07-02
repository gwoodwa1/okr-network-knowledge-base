---
type: API Reference
title: REST API
description: Client integration reference covering JWT authentication, core endpoints, errors, and rate limits.
resource: urn:api:rest_api_doc
tags: [api, rest, jwt, authentication, pagination]
timestamp: 2024-01-20T00:00:00Z
owner: API Team
status: example
version: "1.0"
---

# Authentication

Send a JWT with every request:

```http
Authorization: Bearer <your-jwt-token>
```

# Endpoints

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/api/users/register` | Register a user account. |
| `POST` | `/api/users/login` | Authenticate and obtain a JWT. |
| `GET` | `/api/data/items` | Retrieve a paginated item list. |
| `POST` | `/api/data/items` | Create an item. |

# Error model

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [{"field": "email", "message": "Invalid email format"}]
  }
}
```

# Rate limiting

The example limit is 1,000 requests per user per hour. Responses expose the limit, remaining request count, and reset time through `X-RateLimit-*` headers.
