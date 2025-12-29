# Unprotected Admin Functionality – DFIR Analysis

## Scenario
The application exposed an administrative endpoint that could be accessed
without authentication.

## Root Cause
The application failed to enforce authentication and authorization checks
on administrative functionality. Security relied entirely on the assumption
that users would not discover the admin endpoint.

## Security Impact
Any unauthenticated user could access administrative features such as
user management. This allows account deletion or modification without
proper identity verification.

## DFIR Perspective
From an incident response standpoint, such actions may not generate
authentication logs, making it difficult to attribute malicious activity
to a specific user.

## Evidence to Investigate
- Web server access logs showing requests to administrative endpoints
- Absence of authentication or session validation logs
- Timeline correlation between suspicious HTTP requests and user deletion events

## Mitigation
- Enforce authentication and role-based access control on all admin endpoints
- Validate user roles on the server side
- Log all administrative actions with user identity and timestamps

## Notes
This writeup focuses on identifying the incident cause rather than
exploitation steps.


Lab Source: PortSwigger Web Security Academy (Access Control Vulnerability)