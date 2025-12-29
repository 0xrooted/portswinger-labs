# User Role Controlled by Request Paramter – DFIR Analysis

## Scenario
An access control vulnerability was identified where administrative
privileges were determined using a client-side cookie.

## Root Cause
The application trusted a client-controlled cookie to determine whether
a user had administrative privileges.

Instead of validating the user's role on the server-side using the session
context or database lookup, the application relied on a boolean cookie value.   

## Security Impact
This vulnerability allows a normal authenticated user to escalate privileges
by modifying a cookie value, resulting in unauthorized access to
administrative functionality.


## DFIR Perspective
From an incident response standpoint, this represents a privilege escalation
event where legitimate session identifiers are used to perform
unauthorized administrative actions.

## Evidence to Investigate
- HTTP access logs showing requests to administrative endpoints
- Session identifiers associated with non-admin users performing admin actions
- Absence of server-side role validation in backend logic
- Discrepancy between user role stored in database and role inferred from cookies

## Mitigation
- Do not store authorization decisions in client-side cookies
- Enforce role validation server-side using session identifiers
- Log all administrative actions with user identity and role
- Implement alerts for privilege escalation anomalies

## Notes
This writeup focuses on identifying the incident cause rather than
exploitation steps.


Lab Source: PortSwigger Web Security Academy (Access Control Vulnerability)