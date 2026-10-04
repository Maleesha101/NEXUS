# NEXUS Agent Instructions

## Purpose

NEXUS is an intentionally vulnerable application-security laboratory. Development must preserve the educational purpose of the lab while keeping the vulnerable behavior isolated and reproducible.

## Core Rules

1. Treat the repository as a security laboratory, not a production application.
2. Vulnerabilities must be intentional, documented, configurable, and testable.
3. Prefer realistic business workflows over artificial `/vulnerable` endpoints.
4. Keep authentication, session management, and authorization as separate concepts.
5. Never add real credentials, API keys, private keys, tokens, or production secrets.
6. Vulnerable defaults must never be presented as production-safe configuration.
7. Every vulnerability should have:
   - a clear implementation boundary,
   - a reproducible test path,
   - expected vulnerable behavior,
   - secure behavior,
   - remediation guidance.
8. Keep attack impact inside the fictional NEXUS domain. Do not add functionality intended to affect real infrastructure.
9. Use deterministic seed data where practical so manual Burp testing is reproducible.
10. Run relevant tests and validation before claiming a feature is complete.

## Git Workflow

Work incrementally. Do not combine unrelated phases into one commit.

Before committing:

- inspect `git status`,
- inspect the relevant diff,
- verify no secrets are staged,
- run appropriate tests or documentation checks.

Use focused conventional commits such as:

- `docs: ...`
- `feat: ...`
- `test: ...`
- `fix: ...`

Do not blindly stage the entire repository when unrelated files may be present.

## Security-Lab Principle

The vulnerable implementation and secure reference implementation should remain easy to compare. Avoid hiding the vulnerability behind unnecessary abstraction or making exploitation depend on undocumented behavior.

## Documentation Principle

If behavior changes, update the relevant documentation in the same development phase or in a clearly related follow-up commit.
