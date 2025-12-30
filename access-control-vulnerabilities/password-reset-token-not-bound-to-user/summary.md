# Password Reset Token Not Bound to User – DFIR Analysis

## Scenario
A password reset functionality was found to be vulnerable due to improper
validation of reset tokens. The application allowed a password reset token
to be reused across different user accounts.

## Root Cause
The password reset token was not uniquely bound to a specific user account.
The server trusted user-identifying parameters (such as username) supplied
in the password reset request instead of associating the token with a
single user on the server side.

## Security Impact
This vulnerability enables an attacker to reset the password of another
user by reusing a valid reset token and modifying the username parameter.
This results in full account takeover.


## DFIR Perspective
From a digital forensics and incident response perspective, this issue
represents an Account Takeover (ATO) incident caused by flawed authentication
logic rather than credential compromise.


## Evidence to Investigate
- Password reset requests reusing the same token for different user accounts
- Reset requests for one user originating from sessions or IP addresses
associated with another user
- Successful password resets without corresponding email verification
- Login events from new IP addresses immediately after password reset

## Incident Classification
Account Takeover (ATO)  

## Mitigation
- Bind password reset tokens to a specific user account on the server side
- Invalidate reset tokens immediately after a single successful use
- Do not trust username or email parameters supplied by the client
- Implement short expiration times for reset tokens
- Log and alert on abnormal password reset and login behavior

## Notes
This analysis focuses on identifying the authentication logic flaw and its
forensic implications rather than demonstrating exploitation steps.


Lab Source: PortSwigger Web Security Academy (Access Control Vulnerability)