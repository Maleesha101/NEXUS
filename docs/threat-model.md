# NEXUS Threat Model

## Scope

This threat model covers the intentionally vulnerable NEXUS fleet-dispatch application running inside the local laboratory environment.

The primary security objective is to demonstrate how session-management weaknesses can become meaningful application-level compromises.

## Assets

| Asset | Security Property | Example Impact |
|---|---|---|
| User session | Confidentiality / integrity | Account impersonation |
| Dispatcher identity | Integrity | Unauthorized dispatch actions |
| Shift state | Integrity | Incorrect handover or operational state |
| Dispatch orders | Integrity | Unauthorized emergency order creation |
| Security events | Integrity | Loss of investigation evidence |
| User credentials | Confidentiality | Account compromise |

## Actors

### Unauthenticated User

Can access public application functionality and authentication endpoints.

### Authenticated User

Can access resources permitted by their role.

### Malicious Lab User

Represents an attacker who can interact with the application and inspect their own traffic using Burp Suite.

The attacker is expected to discover weaknesses through normal application behavior rather than privileged debugging endpoints.

## Primary Threats

### T1 — Predictable Session Identifier

If session identifiers follow an enumerable pattern, an attacker may be able to predict or test identifiers belonging to other active sessions.

### T2 — Session Fixation

If a pre-authentication session identifier survives authentication, an attacker who knows that identifier may be able to reuse the authenticated session.

### T3 — Missing Session Rotation

Authentication should establish a new authenticated session identifier. Failure to rotate the identifier increases the impact of session fixation and stolen pre-authentication state.

### T4 — Logout Revocation Failure

If logout only removes the browser cookie but leaves the server-side session valid, a previously copied session identifier can remain usable.

### T5 — Excessive Session Lifetime

Long-lived sessions increase the window in which a stolen session identifier can be replayed.

### T6 — Weak Cookie Protection

Missing or weak cookie attributes can make session identifiers easier to expose through client-side or cross-site conditions.

## Attack Preconditions

The laboratory does not assume compromise of the host operating system or PostgreSQL server.

Testing should be possible using:

- normal application responses,
- browser cookies,
- Burp Suite,
- multiple seeded accounts,
- documented laboratory configuration.

## Security Boundary

A session compromise must not automatically bypass authorization.

For example:

`dispatcher session compromise → dispatcher privileges`

does not become:

`dispatcher session compromise → admin privileges`

unless an independent authorization flaw is deliberately introduced.

## Risk Demonstration

The main educational chain is:

`session reconnaissance → identifier weakness → session replay → identity compromise → unauthorized fleet operation`

The business impact remains fictional and database-backed. No real fleet, vehicle, emergency service, or external control system is connected to NEXUS.
