# Introduction

> Access level: **Authenticated Developers Only**\
> Audience: Platform engineers, backend integrators, infrastructure teams and more

Welcome to the internal API documentation for Monopoly SDK. These docs cover authenticated endpoints, developer tooling, deployment targets, and internal implementation details **not** exposed through the public API surface.

Use this section if you're:

* Building custom backend integrations
* Implementing auth workflows (token exchange, key rotation)
* Deploying SDK microservices in self-hosted environments
* Writing internal analytics or moderation tooling



| A1 | B1 | B1 |
| -- | -- | -- |
| A2 | B2 | C2 |
| A3 | B3 | C3 |

***

## Access Requirements

To access these APIs and documents, you need:

* A valid **tenant ID**
* A **client secret** with internal API scopes
* (Optional) **Admin API key** for elevated routes

Contact your account representative or the infra team to request access.

***

## Topics Covered

| Section                                              | Description                                                          |
| ---------------------------------------------------- | -------------------------------------------------------------------- |
| 🔐 [Authentication](auth-internal.md)                | How to authenticate internal services using secrets or signed tokens |
| 🧠 [Session Orchestration](session-orchestration.md) | Hooks for controlling turn order, rule overrides, and arbitration    |
| 🗃️ [Data Exports](data-exports.md)                  | Snapshots, diffs, and replay logs for sessions                       |
| 📡 [Webhooks](webhooks.md)                           | Subscribing to internal event streams for monitoring                 |
| 🧩 [Plugin System](plugin-api.md)                    | Registering server-side plugins (anti-cheat, moderation, logging)    |
| 📈 [Metrics](metrics.md)                             | Prometheus-ready endpoints and usage aggregation                     |

***

## Authentication Models

We support multiple internal auth strategies:

1. **Signed JWTs** with scoped `aud=internal.monopoly.io`
2. **API key headers** (for trusted services)
3. **mTLS client certificates** (enterprise-only)

For most tenants, we recommend JWT + rotating refresh tokens for service-to-service use.

***

## Support & Escalation

To report bugs or request higher quotas:

* 📮 File an issue in the private GitHub repo
* 💬 Reach out on `#api-core-internal` Slack channel
* ✉️ Email `infra@monopoly.io`

> Note: Internal docs are versioned separately from public docs. Breaking changes will be communicated via changelog and engineering syncs.

***

## Next Up

Start with [Authentication Internals](auth-internal.md) or [Session Orchestration](session-orchestration.md) to understand the mechanics of the internal control plane.
