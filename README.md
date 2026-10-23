# Web Application Penetration Testing

## Project Overview

This project documents practical web application security testing conducted in intentionally vulnerable PortSwigger Web Security Academy labs. It demonstrates a structured approach to identifying, validating and reporting access-control weaknesses, assessing their impact, and recommending remediation.

The project is part of a cybersecurity portfolio focused on developing practical penetration-testing methodology and professional technical reporting.

## Objectives

- Inspect HTTP requests and responses.
- Test application access-control mechanisms.
- Identify insecure direct object references (IDOR).
- Investigate user-controlled role assignment and privilege escalation.
- Use Burp Suite Repeater to modify and replay requests.
- Validate vulnerabilities using observable application behaviour.
- Document evidence, impact, limitations and remediation.
- Define retest criteria for validating security fixes.

## Assessments

### Assessment 01 — Insecure Direct Object Reference (IDOR)

**Status:** Completed

Tested an account endpoint in a PortSwigger training lab to determine whether a user could access another user's account information by changing an identifier in the URL.

**Observed result:** Changing the identifier from `wiener` to `carlos` returned the other test user's account information, including an API key.

**Security significance:** The result demonstrated an access-control weakness in the training application because the requested account information was returned without the expected authorisation check.

**Report:** [Read the IDOR investigation](investigations/01-idor-access-control.md)

**Evidence:** [View sanitised IDOR evidence](evidence/01-idor-access-control.png)

### Assessment 02 — Vertical Privilege Escalation

**Status:** Completed

Used Burp Suite Repeater to inspect and modify a profile-update request in a separate PortSwigger training lab.

**Observed result:** The application accepted a user-supplied `roleid` value of `2`. The changed role then allowed access to the lab's administrator panel, and the intended lab task was completed.

**Security significance:** The result demonstrated that a standard user could elevate privileges by modifying a role field that should have been controlled and authorised by the server.

**Report:** [Read the privilege-escalation investigation](investigations/02-vertical-privilege-escalation.md)

**Evidence:**
- [Role modification request](evidence/02-roleid-repeater.png)
- [Administrator-panel access](evidence/03-admin-panel-access.png)

## Tools and Techniques

- PortSwigger Web Security Academy
- Burp Suite Community Edition
- HTTP request and response analysis
- Burp Suite Repeater
- URL parameter manipulation
- Access-control testing
- User-role and privilege-escalation testing
- Vulnerability validation
- Risk and impact assessment
- Remediation and retest planning
- GitHub and Markdown reporting

## Scope and Safety

Testing was restricted to the designated, intentionally vulnerable training labs. No unrelated public websites or production systems were tested.

Public evidence must not disclose API keys, session cookies, authentication tokens, credentials or other sensitive values. Screenshots are intended to demonstrate the testing process and observed outcomes without exposing secrets.

## Reporting Methodology

Each assessment aims to document:

1. Scope and objective
2. Test methodology
3. Observed behaviour and evidence
4. Vulnerability classification and potential impact
5. Risk assessment and limitations
6. Recommended remediation
7. Retest criteria and conclusion

Findings are based on observed behaviour in the training environment. The results should not be interpreted as evidence that other applications have the same vulnerabilities.

## Skills Demonstrated

- Manual web application testing
- HTTP request manipulation
- Access-control assessment
- IDOR identification and validation
- Vertical privilege-escalation testing
- Burp Suite Repeater
- Evidence collection and analysis
- Vulnerability reporting
- Remediation recommendations
- Security-focused technical writing
