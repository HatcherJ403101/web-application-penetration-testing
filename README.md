# Web Application Penetration Testing

## Project Overview

This project documents practical web application security testing using intentionally vulnerable training applications. The objective is to develop a structured penetration-testing methodology: understand application behaviour, identify potential vulnerabilities, validate findings, assess their impact and recommend remediation.

The project will focus initially on access control and authorisation, then expand into additional web application security topics as testing progresses.

## Objectives

- Understand web application requests and responses.
- Identify and assess access-control weaknesses.
- Practise manual testing using browser developer tools and Burp Suite Community Edition.
- Record reproducible evidence for validated findings.
- Explain technical risk and potential business impact.
- Recommend practical remediation and describe how fixes should be retested.
- Produce clear reports suitable for a technical security audience.

## Planned Assessments

### Assessment 01 — Access Control and IDOR

Investigate whether a training application enforces authorisation when a user requests an object or resource.

Planned activities include:
- Establishing expected behaviour and test conditions.
- Reviewing relevant requests and responses.
- Testing access controls within the authorised lab.
- Recording evidence and assessing any confirmed issue.
- Documenting remediation and retesting considerations.

Additional assessments will be documented as they are completed.

## Tools

- PortSwigger Web Security Academy
- Burp Suite Community Edition
- Web browser developer tools
- Markdown for technical reporting
- GitHub for version control and evidence documentation

## Scope and Safety

Testing is restricted to intentionally vulnerable training labs and systems for which permission has been granted. No unrelated public websites, accounts or services will be tested.

Session cookies, authentication tokens, credentials and personal data must be excluded or redacted from public evidence.

## Reporting Methodology

Each assessment will document:
1. Scope and objective
2. Test approach and expected behaviour
3. Observations and supporting evidence
4. Validated findings and potential impact
5. Risk assessment and limitations
6. Recommended remediation
7. Retest approach and conclusion

Only findings supported by observed evidence will be reported as confirmed vulnerabilities.
