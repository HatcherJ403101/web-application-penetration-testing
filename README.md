# Web Application Penetration Testing

## Project Overview

This project documents practical web application security testing in deliberately vulnerable PortSwigger Web Security Academy labs. It demonstrates a structured approach to identifying, validating and reporting vulnerabilities, assessing their potential impact, and recommending remediation.

The project forms part of a cybersecurity portfolio focused on developing practical penetration-testing methodology, HTTP request analysis and technical report writing.

## Objectives

- Inspect HTTP requests and responses.
- Test application access-control mechanisms.
- Identify insecure direct object references (IDOR).
- Investigate user-controlled role assignment and vertical privilege escalation.
- Use Burp Suite to intercept, modify and replay requests.
- Test user-controlled input for SQL injection.
- Record reproducible evidence for validated findings.
- Explain technical impact, limitations and remediation.
- Define retest criteria for validating security fixes.

## Assessments

### Assessment 01 — Insecure Direct Object Reference (IDOR)

**Status:** Completed

Tested an account endpoint in a PortSwigger training lab to determine whether a user could access another user's account information by changing a user identifier in the URL.

**Observed result:** Changing the identifier from `wiener` to `carlos` returned the other test user's account information, including an API key.

**Security significance:** The application returned another user's information without the expected authorisation check.

**Report:** [Read the IDOR investigation](investigations/01-idor-access-control.md)

**Evidence:** [View sanitised IDOR screenshot](evidence/01-idor-access-control.png)

### Assessment 02 — Vertical Privilege Escalation

**Status:** Completed

Used Burp Suite Repeater to inspect and modify a profile-update request in a separate PortSwigger training lab.

**Observed result:** The application accepted a user-supplied `roleid` value of `2`, allowing access to the lab's administrator panel and completion of the intended lab task.

**Security significance:** The result demonstrated that a standard user could obtain elevated privileges through a user-controlled role field.

**Report:** [Read the privilege-escalation investigation](investigations/02-vertical-privilege-escalation.md)

**Evidence:**
- [Role modification request](evidence/02-roleid-repeater.png)
- [Administrator-panel access](evidence/03-admin-panel-access.png)

### Assessment 03 — SQL Injection

**Status:** Completed

Intercepted a product-category request in a PortSwigger training lab and modified the category parameter using a SQL injection test payload.

**Observed result:** The application displayed all products after the modified request, and the lab reported successful completion.

**Security significance:** The behaviour was consistent with SQL injection affecting a product-category query.

**Report:** [Read the SQL injection investigation](investigations/03-sql-injection-hidden-data.md)

**Evidence:**
- [Hidden products and lab result](evidence/04-sql-injection-hidden-products.png)
- [Modified HTTP request](evidence/05-sql-injection-request.png)

## Tools and Techniques

- PortSwigger Web Security Academy
- Burp Suite Community Edition
- HTTP request and response analysis
- Burp Suite Repeater and Proxy interception
- URL parameter manipulation
- Access-control testing
- IDOR identification and validation
- Vertical privilege-escalation testing
- SQL injection testing
- Vulnerability impact assessment
- Remediation and retest planning
- GitHub and Markdown reporting

## Scope and Safety

Testing was restricted to the designated, intentionally vulnerable PortSwigger training labs. No unrelated public websites or production systems were tested.

Public evidence must not disclose API keys, session cookies, authentication tokens, credentials or other sensitive values. Screenshots are intended to demonstrate the testing process and observed results without exposing secrets.

The findings describe behaviour observed within the training environment. They do not establish that other applications contain the same vulnerabilities.

## Reporting Methodology

Each assessment documents:

1. Scope and objective
2. Testing methodology
3. Observed behaviour and supporting evidence
4. Vulnerability classification and potential impact
5. Risk assessment and limitations
6. Recommended remediation
7. Retest criteria and conclusion

Findings are reported based on observed behaviour, with limitations stated where the underlying implementation or wider impact has not been independently verified.

## Skills Demonstrated

- Manual web application security testing
- HTTP request interception and modification
- Access-control assessment
- IDOR testing
- Vertical privilege-escalation testing
- SQL injection validation
- Burp Suite request analysis
- Evidence collection and interpretation
- Vulnerability reporting and remediation
- Security-focused technical writing
