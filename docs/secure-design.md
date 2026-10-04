# NEXUS Secure Session Design

This document defines the intended secure reference behavior for the session-management laboratory.

## Session Identifier

Use a cryptographically secure random generator.

Requirements:

- unpredictable,
- sufficient entropy,
- no sequential structure,
- no user identifiers,
- no timestamps or other guessable fields,
- server-side validation.

## Authentication Rotation

On successful authentication:

1. validate credentials,
2. establish the authenticated identity,
3. rotate the session identifier,
4. associate the new session with the authenticated user,
5. invalidate the pre-authentication session state.

This prevents session fixation.

## Logout

Logout must invalidate the server-side session and expire the client cookie.

A copied old identifier must no longer authenticate after logout.

## Expiration

Use controlled idle and absolute lifetimes appropriate for the application.

Long-lived sessions should require explicit justification.

## Cookie Attributes

Production-safe cookies should use appropriate protections including:

- `HttpOnly`
- `Secure` when HTTPS is used
- an appropriate `SameSite` policy
- a narrow cookie scope

The exact settings should match the deployment architecture.

## Authorization

Authentication establishes identity. Authorization independently checks whether the identity may perform the requested action.

Never infer administrator privileges from possession of a session identifier alone.

## Sensitive Events

Consider session invalidation or re-authentication after:

- password changes,
- account recovery,
- privilege changes,
- security-sensitive account updates.

## Secure Reference Profile

The secure laboratory profile should disable the intentionally vulnerable switches and provide behavior suitable for comparison against the vulnerable profiles.

The secure profile is a reference implementation for training, not a guarantee that every production security requirement has been addressed.
