# NEXUS Security Laboratory Guide

## Purpose

This guide will provide the hands-on exercises for testing session-management vulnerabilities in the NEXUS fleet-dispatch application.

The application is intentionally vulnerable when a vulnerable laboratory profile is enabled.

## Laboratory Safety

Run NEXUS only in an isolated environment that you control.

Do not expose the vulnerable application to the public internet or use the techniques against systems you do not own or have explicit authorization to test.

## Planned Exercises

| ID | Vulnerability | Main Evidence |
|---|---|---|
| SM-01 | Predictable Session ID | Session identifiers can be predicted or enumerated |
| SM-02 | Session Fixation | Known pre-authentication session survives login |
| SM-03 | Missing Session Rotation | Authentication does not establish a fresh identifier |
| SM-04 | Logout Invalidation Failure | Old session remains usable after logout |
| SM-05 | Excessive Session Lifetime | Session remains valid beyond the intended window |
| SM-06 | Missing HttpOnly | Client-side script can access the session cookie |
| SM-07 | Weak SameSite Policy | Cookie cross-site protection is intentionally weakened |

## Primary Chain

The main exercise will combine:

1. Session reconnaissance
2. Identification of predictable session behavior
3. Candidate session discovery
4. Session replay
5. Dispatcher identity compromise
6. Fictional emergency-dispatch action

The goal is to demonstrate how a seemingly small session-management weakness can become a business-impacting compromise.

## Testing Tools

Recommended:

- Browser developer tools
- Burp Suite Proxy
- Burp Suite Repeater
- Burp Suite HTTP history
- curl for repeatable HTTP requests

## Evidence

For each exercise, record:

- request and response,
- relevant cookie attributes,
- session identifier behavior,
- authenticated identity,
- authorization result,
- vulnerable behavior,
- secure behavior,
- remediation.

Detailed instructions will be added as the application implementation is completed.
