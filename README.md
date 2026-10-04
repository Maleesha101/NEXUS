# NEXUS Fleet Operations — Session Management Security Lab

NEXUS is an intentionally vulnerable fleet-dispatch platform designed for hands-on application security training focused on **session management vulnerabilities and chained attacks**.

The lab models an emergency logistics operation where authenticated users manage vehicles, shifts, dispatch orders, and emergency operations. Session weaknesses can be combined to move from session analysis to session replay and, depending on the compromised identity, unauthorized operational actions.

## Security Focus

Primary vulnerabilities include:

- Predictable session identifiers
- Session fixation
- Missing session rotation after authentication
- Session invalidation failures during logout
- Excessive session lifetime
- Insecure session-cookie attributes

The lab emphasizes realistic workflows rather than isolated payload demonstrations.

## Intended Attack Narrative

A learner should be able to investigate a realistic application, understand its session lifecycle, identify weaknesses, and demonstrate an attack chain such as:

`session reconnaissance → predictable identifier discovery → session replay → identity compromise → privileged dispatch action`

The exact chain depends on the active laboratory configuration.

## Planned Technology Stack

- Laravel / PHP
- PostgreSQL
- Nginx
- Docker Compose
- REST API
- Lightweight web interface
- PHPUnit/Pest for automated validation
- Burp Suite for manual security testing

## Safety

NEXUS is intentionally vulnerable. Run it only in an isolated local or dedicated laboratory environment. Do not deploy the vulnerable configuration to production or expose it to untrusted networks.

## Documentation

The repository documentation will cover:

- Architecture and trust boundaries
- Threat model
- Session lifecycle
- Vulnerability profiles
- Attack chains
- Secure design and remediation
- Manual Burp Suite testing
- Automated validation
- Laboratory reset procedures

> **Status:** Documentation and laboratory foundation are being built incrementally. The repository is not yet the completed application.
