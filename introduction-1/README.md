# API

Welcome to the **Monopoly SDK REST API** — a JSON-over-HTTPS interface designed to power multiplayer Monopoly game sessions as part of the Monopoly SDK. This API is primarily used behind the scenes by the client-side SDK, but it can also be integrated directly for custom orchestration, analytics, or admin tooling.

***

## Key Concepts

* **Sessions**: Represent an individual Monopoly game instance.
* **Players**: Unique participants in a session.
* **Turns**: Each player's game actions, such as rolling dice.
* **Snapshots**: Serializable representations of session state for recovery or audit.

***

## Base URL

```
Production: https://api.monopoly.io/v1
Sandbox:    https://sandbox.monopoly.io/v1
```

All responses are JSON. All endpoints require authentication unless stated otherwise.

***

## Authentication

The API uses **Bearer tokens (JWTs)** issued via the `/auth/token` endpoint. These tokens are short-lived (≤30 minutes) and must be included in the `Authorization` header of each request.

```http
Authorization: Bearer <jwt>
```

For certain administrative operations, you may also provide an API key via:

```http
X-API-KEY: <your-api-key>
```

You can refresh expired tokens using `/auth/refresh`.

***

## Common Headers

```http
Content-Type: application/json
Authorization: Bearer <your-jwt-token>
```

***

## Error Handling

All errors follow a consistent structure:

```json
{
  "code": "ERR_INVALID_SECRET",
  "message": "Secret token is invalid or expired"
}
```

HTTP status codes reflect the nature of the error:

* `400 Bad Request`: Invalid input or schema
* `401 Unauthorized`: Missing or invalid token
* `403 Forbidden`: Valid token, insufficient permissions
* `404 Not Found`: Invalid path or resource
* `409 Conflict`: Invalid game state transition

***

## Quick Start Flow

1. Obtain a token:

```http
POST /auth/token
{
  "tenantId": "...",
  "secret": "..."
}
```

2. Create a session:

```http
POST /sessions
{
  "players": [ { "id": "u1", "name": "Alice" }, ... ]
}
```

3. Start the session:

```http
POST /sessions/{sessionId}/start
```

4. Submit a turn:

```http
POST /sessions/{sessionId}/turns
```

5. Retrieve the game state:

```http
GET /sessions/{sessionId}/state
```

***

## Tools & SDKs

* **Official JavaScript SDK**: `@monopoly/sdk`
* **Postman Collection**: [Download](https://docs.monopoly.io/postman.json)
* **OpenAPI Spec**: [View YAML](../API/monopoly-sdk-openapi.yaml)

***

## Rate Limiting

Default rate limit: **60 requests/minute per tenant**. Contact support to increase limits for high-volume or enterprise usage.

***

## Support

For questions, bugs, or feature requests, visit:

* 🧾 [API Docs](https://docs.monopoly.io)
* 🐛 [GitHub Issues](https://github.com/monopoly/monopoly-sdk/issues)
* 💬 [Discord](https://discord.gg/monopoly-sdk)

***

Let's get rolling 🎲
