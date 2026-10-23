# Web Application Penetration Testing

## Project Overview

This project documents practical web application security testing using intentionally vulnerable training labs. It follows a structured assessment process: understand normal application behaviour, test security controls, validate findings, assess potential impact and recommend remediation.

The project is being developed as a cybersecurity portfolio to demonstrate foundational penetration-testing skills and technical report writing.

## Objectives

- Understand HTTP requests, responses and application parameters.
- Identify and validate access-control weaknesses.
- Practise manual testing in authorised training environments.
- Record reproducible evidence for confirmed findings.
- Explain potential technical and business impact.
- Recommend remediation and define retest criteria.
- Produce clear, evidence-based security reports.

## Assessments

### Assessment 01 — Insecure Direct Object Reference (IDOR)

**Status:** Completed

Tested an account endpoint in a PortSwigger Web Security Academy training lab to determine whether a user could access another user's account information by changing an identifier in the request.

**Key observation:** Changing the account identifier from `wiener` to `carlos` returned the other test user's account information, including an API key. This demonstrated an access-control weakness in the training application.

**Report:** [Read the IDOR investigation](investigations/01-idor-access-control.md)

**Evidence:** [View sanitised assessment screenshot](evidence/01-idor-access-control.png)

The published evidence must not reveal the API key or other sensitive values.

## Tools and Techniques

- PortSwigger Web Security Academy
- Browser-based testing
- HTTP request and response analysis
- URL and parameter manipulation
- Access-control testing
- Vulnerability validation
- Risk and impact assessment
- Remediation and retest planning
- GitHub and Markdown reporting

## Scope and Safety

Testing is restricted to authorised training labs and intentionally vulnerable applications. No unrelated public websites or systems are tested.

Sensitive values, including API keys, session cookies, credentials and authentication tokens, must be excluded or redacted from public reports and screenshots.

## Reporting Methodology

Each assessment aims to document:

1. Scope and objective
2. Test methodology
3. Observed behaviour and evidence
4. Confirmed vulnerability and potential impact
5. Risk assessment and limitations
6. Recommended remediation
7. Retest criteria and conclusion

Only findings supported by observed evidence are described as confirmed vulnerabilities.
