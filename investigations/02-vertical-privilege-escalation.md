# Finding 02 — Vertical Privilege Escalation Through User-Controlled Role Assignment

## 1. Assessment Overview

**Target:** PortSwigger Web Security Academy — User role can be modified in user profile  
**Assessment type:** Authorised web application security lab  
**Vulnerability category:** Broken Access Control / Privilege Escalation  
**Testing tools:** Burp Suite Community Edition, Repeater and web browser

This assessment examined whether a standard authenticated user could modify account-role information through a profile-update request and gain access to administrator functionality.

## 2. Objective

The objective was to determine whether the application enforced server-side authorisation when processing changes to a user's role.

## 3. Methodology

1. Opened the designated PortSwigger training lab and logged in as the supplied `wiener` test user.
2. Submitted a normal profile-update request.
3. Captured the request and sent it to Burp Suite Repeater.
4. Replayed the unmodified request to establish the normal response.
5. Added a `roleid` value of `2` to the profile-update request.
6. Sent the modified request and observed that the role change was accepted.
7. Accessed the lab's administrative endpoint and confirmed that the administrator panel loaded.
8. Completed the lab's intended task by deleting Carlos's test account.

All testing was conducted within the authorised, deliberately vulnerable training environment.

## 4. Finding and Evidence

### Observation

The application processed the modified profile-update request containing a client-supplied `roleid` value of `2`.

The role change was accepted, and the tester was subsequently able to access the administrative panel. Completing the lab's intended administrative action confirmed that the changed role provided elevated privileges within the training environment.

### Expected Behaviour

The server should determine a user's role from trusted server-side account data and enforce authorisation for privileged actions.

A standard user should not be able to grant themselves administrator privileges by modifying a profile-update request.

### Observed Behaviour

The application accepted a user-controlled role value, resulting in elevated access to administrator functionality.

This demonstrates a vertical privilege-escalation vulnerability caused by inadequate server-side role and authorisation controls.

## 5. Security Impact

In a real application, a similar vulnerability could allow a standard user to gain privileges intended only for administrators.

Depending on the application's functionality, an attacker might be able to access administrative data, modify other accounts, or perform unauthorised management actions.

In this training lab, the elevated role enabled access to the administrative panel and deletion of Carlos's test account.

These results demonstrate the impact within the lab, but do not establish the impact that an equivalent issue would have in a different application.

## 6. Risk Assessment

**Assessment:** Confirmed privilege escalation within the training application.

The issue is significant because a standard user could obtain administrative functionality by modifying a request field.

The severity of a real-world finding would depend on the privileges available through the administrator role, the sensitivity of affected data, and the potential for unauthorised changes. No formal CVSS score has been assigned to this training exercise.

## 7. Recommended Remediation

- Do not accept role assignments from ordinary user profile-update requests.
- Store and manage privileged role information using trusted server-side controls.
- Enforce authorisation checks for administrative functions on every request.
- Ensure that a user's permissions are checked independently of client-supplied parameters.
- Add automated tests confirming that standard users cannot modify their own privilege level.
- Log and monitor unauthorised role-change attempts and other unexpected privilege transitions.
- Retest both the role-update endpoint and administrative functionality after remediation.

Hiding an administrative page or changing the value in the browser is not a substitute for server-side authorisation.

## 8. Retest Criteria

After remediation:

1. Submit a normal profile-update request and verify that permitted profile fields can still be updated.
2. Attempt to include a modified role value while authenticated as a standard user.
3. Verify that the role cannot be changed through the ordinary profile-update endpoint.
4. Attempt to access administrative functionality as a standard user.
5. Confirm that the application denies unauthorised administrative actions and records relevant security events.

## 9. Limitations

- Testing was limited to the supplied PortSwigger training lab.
- The assessment covered the tested profile-update request and administrative endpoint.
- No production application or unrelated account was accessed.
- The findings do not establish that other applications are vulnerable.
- Any publicly shared screenshots must exclude session cookies, authentication tokens and API keys.

## 10. Conclusion

The test demonstrated vertical privilege escalation through a user-controlled role field. The application accepted the modified request, allowed the tester to access administrative functionality, and permitted completion of the lab's intended task.

The investigation demonstrates the use of Burp Suite Repeater to modify and replay HTTP requests, validate a security weakness, assess impact and formulate actionable remediation recommendations.

## 11. Evidence

### Evidence 02 — Role Modification Request

[View Burp Suite Repeater evidence](../evidence/02-roleid-repeater.png)

This screenshot supports the observation that the profile-update request included a user-supplied `roleid` value of `2` and that the application accepted the change. Sensitive session information must be redacted.

### Evidence 03 — Administrative Access

[View administrator-panel evidence](../evidence/03-admin-panel-access.png)

This screenshot supports the impact assessment by showing that the administrator panel was accessible after the role change in the authorised training lab.

The screenshots should be interpreted alongside the methodology, findings, limitations and remediation recommendations in this report.
