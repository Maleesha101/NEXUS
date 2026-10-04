# NEXUS Architecture

## 1. System Overview

NEXUS models an emergency fleet-dispatch platform used by a fictional logistics organization.

The platform contains four primary roles:

| Role | Purpose |
|---|---|
| DRIVER | View assigned vehicle and shift information |
| DISPATCHER | Manage dispatch operations and emergency orders |
| SUPERVISOR | Coordinate shifts and supervise dispatch activity |
| ADMIN | Manage the platform and inspect security events |

The application is designed around normal business workflows so that session-management weaknesses can be tested through realistic API interactions.

## 2. Planned Components

```text
+---------------------+
| Browser / Burp      |
+----------+----------+
           |
           | HTTP
           v
+---------------------+
| Nginx               |
| Reverse Proxy       |
+----------+----------+
           |
           v
+---------------------+
| Laravel Application |
|                     |
| Auth API            |
| Session Manager     |
| Dispatch Services   |
| Shift Services      |
| Security Events     |
+----------+----------+
           |
           v
+---------------------+
| PostgreSQL          |
+---------------------+
```

Docker Compose will provide the isolated laboratory environment.

## 3. Application Domains

### Authentication

Responsible for:

- login,
- logout,
- authenticated identity lookup,
- password changes,
- authentication-related session transitions.

### Session Management

Responsible for:

- session identifier generation,
- session creation,
- session lookup,
- session rotation,
- expiration,
- revocation,
- cookie handling.

The session layer is the main security-testing target.

### Fleet Operations

Responsible for:

- vehicles,
- dispatch orders,
- emergency dispatch,
- current shifts,
- shift handover.

### Security Events

Records security-relevant application events for investigation and lab visibility.

## 4. Trust Boundaries

The main trust boundaries are:

1. Unauthenticated browser → authentication API
2. Authenticated browser → session-protected API
3. Session identity → authorization layer
4. Laravel application → PostgreSQL
5. Dockerized laboratory components → host environment

The lab must not treat possession of a session identifier as equivalent to authorization for arbitrary roles. A compromised dispatcher session should only provide dispatcher privileges unless a separate authorization weakness is intentionally introduced.

## 5. Security Design Goal

NEXUS intentionally contains session-management weaknesses in controlled profiles. The same application should also support a secure configuration that can be used as a reference implementation and comparison target.
