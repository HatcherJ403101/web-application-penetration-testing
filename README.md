# Web Application Penetration Testing

## Project Overview

This project documents practical web application security testing in intentionally vulnerable PortSwigger Web Security Academy labs. It demonstrates a structured approach to identifying, validating and reporting vulnerabilities, assessing potential impact, and recommending remediation.

The project is part of a cybersecurity portfolio focused on developing practical penetration-testing methodology, HTTP request analysis and technical reporting.

## Objectives

- Inspect HTTP requests and responses.
- Test application access-control mechanisms.
- Identify insecure direct object references (IDOR).
- Investigate vertical privilege escalation.
- Test user-controlled input for SQL injection and cross-site scripting.
- Use Burp Suite to intercept, modify and replay HTTP requests.
- Record evidence for validated findings.
- Assess impact and recommend remediation.
- Define retest criteria for validating security fixes.

## Assessments

### Assessment 01 — Insecure Direct Object Reference (IDOR)

**Status:** Completed

Tested an account endpoint to determine whether a user could retrieve another user's account information by changing an identifier in the URL.

**Observed result:** Changing the identifier from `wiener` to `carlos` returned the other test user's account information, including an API key.

**Report:** [Read the IDOR investigation](investigations/01-idor-access-control.md)

**Evidence:** [View sanitised IDOR screenshot](evidence/01-idor-access-control.png)

### Assessment 02 — Vertical Privilege Escalation

**Status:** Completed

Used Burp Suite Repeater to modify a profile-update request in a separate training lab.

**Observed result:** The application accepted a user-supplied `roleid` value of `2`, allowing access to the administrator panel and completion of the intended lab task.

**Report:** [Read the privilege-escalation investigation](investigations/02-vertical-privilege-escalation.md)

**Evidence:**
- [Role modification request](evidence/02-roleid-repeater.png)
- [Administrator-panel access](evidence/03-admin-panel-access.png)

### Assessment 03 — SQL Injection

**Status:** Completed

Intercepted a product-category request and modified the category parameter using a SQL injection test payload.

**Observed result:** The application displayed all products and the training lab reported successful completion.

**Report:** [Read the SQL injection investigation](investigations/03-sql-injection-hidden-data.md)

**Evidence:**
- [Hidden products and lab result](evidence/04-sql-injection-hidden-products.png)
- [Modified HTTP request](evidence/05-sql-injection-request.png)

### Assessment 04 — Reflected Cross-Site Scripting (XSS)

**Status:** Completed

Tested a search function using a controlled proof-of-concept payload in the authorised training lab.

**Observed result:** The browser executed the reflected script and displayed a JavaScript alert.

**Report:** [Read the reflected XSS investigation](investigations/04-reflected-xss.md)

**Evidence:**
- [Reflected XSS browser alert](evidence/06-reflected-xss-alert.png)
- [XSS request and response](evidence/07-reflected-xss-request-response.png)

## Tools and Techniques

- PortSwigger Web Security Academy
- Burp Suite Community Edition
- HTTP request and response analysis
- Proxy interception and Repeater
- URL and parameter manipulation
- IDOR and access-control testing
- Vertical privilege-escalation testing
- SQL injection testing
- Reflected XSS testing
- Vulnerability validation and impact assessment
- Remediation recommendations and retest planning
- GitHub and Markdown reporting

## Scope and Safety

Testing was restricted to the designated, intentionally vulnerable training labs. No unrelated public websites or production systems were tested.

Public evidence must not disclose API keys, session cookies, authentication tokens, credentials or other sensitive values. Screenshots are intended to demonstrate the testing process and observed outcomes without exposing secrets.

The findings describe behaviour observed within the training environment. They do not establish that other applications have the same vulnerabilities.

## Reporting Methodology

Each assessment aims to document:

1. Scope and objective
2. Testing methodology
3. Observed behaviour and supporting evidence
4. Vulnerability classification and potential impact
5. Risk assessment and limitations
6. Recommended remediation
7. Retest criteria and conclusion

Findings are based on observed behaviour. Limitations are stated wherever the underlying implementation or wider impact has not been independently verified.

## Skills Demonstrated

- Manual web application security testing
- HTTP request interception and modification
- Access-control assessment
- IDOR testing
- Vertical privilege-escalation testing
- SQL injection validation
- Reflected XSS testing
- Burp Suite request analysis
- Evidence collection and interpretation
- Vulnerability reporting and remediation
- Security-focused technical writing
