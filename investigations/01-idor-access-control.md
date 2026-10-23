# Finding 01 — Insecure Direct Object Reference (IDOR)

## 1. Assessment Overview

**Target:** PortSwigger Web Security Academy — User ID controlled by request parameter  
**Assessment type:** Authorised web application security lab  
**Vulnerability category:** Broken Access Control / IDOR  
**Testing approach:** Manual testing of an authenticated account endpoint

This investigation assessed whether the application enforced authorisation when retrieving account information belonging to a particular user.

## 2. Objective

The objective was to determine whether an authenticated user could alter an account identifier in a request and access another user's account information without appropriate authorisation.

## 3. Methodology

1. Opened the designated PortSwigger training lab.
2. Authenticated using the lab-provided `wiener` test account.
3. Visited the account page and observed that the URL contained a user identifier parameter.
4. Changed the identifier from `wiener` to `carlos`.
5. Inspected the resulting page to determine whether the application enforced access control.

All testing took place within the authorised training environment.

## 4. Finding and Evidence

### Observation

The account page used a URL parameter to identify the account being requested.

After changing the identifier from `wiener` to `carlos`, the application displayed Carlos's username and an API key.

The application returned another user's account information without requiring the tester to authenticate as that user.

### Expected Behaviour

The server should verify that the authenticated user is authorised to access the requested account or object. Changing an identifier must not bypass this check.

### Observed Behaviour

The server returned account information for the altered identifier. This demonstrates that the relevant request did not enforce the expected account-level authorisation.

**Evidence:** See `evidence/01-idor-access-control.png`. The published screenshot must have the API key fully redacted.

## 5. Security Impact

An attacker with access to a valid account could potentially manipulate the identifier to access information belonging to other users.

The observed disclosure included an API key. The key's permissions and potential use were not investigated, so the wider impact cannot be determined from this test alone.

Depending on the information exposed and the privileges associated with the key, the impact could include unauthorised disclosure of account data or further access to application functionality.

## 6. Risk Assessment

**Assessment:** Confirmed access-control weakness in the training application.

The issue allows account information to be retrieved by changing a user identifier without the required authorisation check.

The practical severity in a real application would depend on the sensitivity of the exposed information, the number of affected users, and the permissions associated with the exposed API key. No formal CVSS score has been assigned in this exercise.

## 7. Recommended Remediation

- Enforce authorisation checks on the server for every request that retrieves account-specific information.
- Derive the current user's identity from the authenticated session where appropriate, rather than trusting a client-supplied identifier.
- Verify that the requesting user has permission to access the requested object.
- Avoid exposing API keys or other secrets unnecessarily in account pages.
- Ensure API keys have limited permissions and can be rotated or revoked if exposed.
- Add automated tests that confirm one user cannot access another user's data by changing an identifier.

Changing an identifier to an unpredictable value is not a substitute for server-side authorisation.

## 8. Retest Criteria

After remediation, repeat the original request while authenticated as the test user.

Verify that:
- The user can access their own authorised account information.
- Changing the identifier to another user's account does not disclose that user's data.
- The server rejects or appropriately denies unauthorised access.
- No sensitive account details or API keys are returned as a result of the unauthorised request.

## 9. Limitations

- Testing was confined to a deliberately vulnerable training lab.
- Only the observed account endpoint and identifier manipulation were assessed.
- The permissions of the returned API key were not examined.
- The result does not establish that another application has the same vulnerability.
- The screenshot must not disclose the API key in the public repository.

## 10. Conclusion

The test demonstrated an IDOR-style access-control weakness. Changing the account identifier caused the application to return another user's account information without the expected authorisation check.

The investigation documented the reproduction method, observed impact, remediation recommendations and retest criteria. It demonstrates a structured approach to validating a web application vulnerability and communicating its significance.
