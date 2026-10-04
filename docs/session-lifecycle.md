# NEXUS Session Lifecycle

## Overview

A NEXUS session represents the authenticated browser context used to access protected application resources.

The lifecycle should be understandable in both vulnerable and secure laboratory profiles.

## Normal Lifecycle

```text
Anonymous
   |
   | login
   v
Pre-authentication state
   |
   | successful authentication
   v
Authenticated session
   |
   +---- request protected resource
   |
   +---- password/security change
   |
   +---- logout
   v
Revoked / expired session
```

## Session Creation

A session identifier is generated when a browser establishes a session.

The laboratory provides a configurable identifier generator so that vulnerable and secure behaviors can be compared.

### Vulnerable Example

A predictable profile may generate identifiers resembling:

`nexus-session-000001`

`nexus-session-000002`

`nexus-session-000003`

The exact sequence is laboratory data, not a production recommendation.

### Secure Example

The secure profile should use a cryptographically secure random identifier with sufficient entropy and no meaningful sequence information.

## Authentication Transition

After successful authentication, the secure lifecycle should rotate the session identifier.

This prevents a known pre-authentication identifier from becoming the authenticated identifier.

## Authorization

The authenticated session identifies the user. The authorization layer then determines which actions that user may perform.

Session management must not be responsible for granting arbitrary role privileges.

## Logout

A secure logout operation should:

1. identify the current server-side session,
2. revoke or invalidate it,
3. expire the browser cookie,
4. prevent subsequent reuse of the old session identifier.

The vulnerable logout profile may intentionally omit server-side invalidation to demonstrate replay.

## Expiration

Sessions should have a controlled lifetime.

The vulnerable long-lived profile demonstrates how an extended lifetime increases replay exposure.

## Password and Security Changes

Sensitive account changes should invalidate appropriate existing sessions or otherwise require re-authentication.

The final implementation will document exactly which session transitions occur for password changes and other security-sensitive operations.

## Testing Principle

For every lifecycle transition, manual testing should answer:

- What identifier exists before the transition?
- Does the identifier change?
- Is the old identifier still valid?
- Which identity does the identifier represent?
- What authorization does that identity receive?
- What happens after logout or expiration?

These questions form the basis of the Burp Suite laboratory exercises.
