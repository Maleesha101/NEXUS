# NEXUS Attack Chains

NEXUS is designed around multi-step attack chains rather than isolated payloads.

## Primary Chain — Predictable Session to Dispatch

```text
Application reconnaissance
        |
        v
Session behavior analysis
        |
        v
Predictable session identifiers
        |
        v
Session identifier discovery/replay
        |
        v
Dispatcher identity
        |
        v
Emergency dispatch action
```

### Step 1 — Reconnaissance

The learner identifies normal authentication and protected API behavior using the browser and Burp Suite.

### Step 2 — Session Analysis

The learner records session identifiers across multiple login cycles and identifies sequential or otherwise predictable values in the vulnerable profile.

### Step 3 — Session Discovery

Using only the laboratory's own seeded users and normal authenticated endpoints, the learner determines whether a candidate identifier maps to a live session.

The application must not provide a purpose-built session enumeration endpoint.

### Step 4 — Session Replay

A discovered valid session identifier is replayed against a protected endpoint such as the authenticated identity endpoint.

### Step 5 — Business Impact

If the compromised identity is a dispatcher, the learner can demonstrate the effect through the fictional emergency-dispatch workflow.

The action must remain inside the NEXUS database-backed simulation.

## Secondary Chain — Fixation

```text
Obtain pre-auth session
        |
        v
Victim authenticates
        |
        v
Session identifier remains unchanged
        |
        v
Reuse known identifier
        |
        v
Authenticated session
```

The secure configuration must rotate the session identifier after authentication.

## Secondary Chain — Logout Replay

```text
Authenticated session
        |
        v
Copy session identifier
        |
        v
Victim logs out
        |
        v
Server fails to revoke session
        |
        v
Replay old identifier
```

The secure configuration must reject the old identifier after logout.

## Chain Design Rules

- Every step should use normal application behavior.
- Do not expose a debug endpoint that directly returns another user's session.
- Do not embed real credentials or external infrastructure access.
- Keep authorization separate from session management.
- Document both vulnerable and secure outcomes.
