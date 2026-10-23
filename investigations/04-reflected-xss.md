# Finding 04 — Reflected Cross-Site Scripting (XSS)

## 1. Assessment Overview

**Target:** PortSwigger Web Security Academy — Reflected XSS, HTML context with nothing encoded  
**Assessment type:** Authorised web application security lab  
**Vulnerability category:** Cross-Site Scripting (XSS)  
**Testing tools:** Web browser, Burp Suite Community Edition

This assessment examined whether user-controlled search input was reflected into a web page in a way that allowed the browser to interpret it as executable JavaScript.

## 2. Objective

The objective was to establish how the application handled search input and determine whether untrusted input could be executed as script in the browser.

## 3. Methodology

1. Opened the designated PortSwigger training lab.
2. Submitted a normal search term to establish the application's baseline behaviour.
3. Inspected the response and observed that the search term appeared in the search-results message.
4. Submitted the following proof-of-concept payload in the authorised lab:

   ```html
   <script>alert(1)</script>
   ```

5. Observed that a JavaScript alert displaying `1` appeared in the browser.
6. Captured screenshots of the alert and the relevant request/response evidence.

All testing was conducted within the designated training environment.

## 4. Finding and Evidence

### Observation

The application displayed a search-results message that incorporated the user-supplied search term.

When the test payload was submitted, the browser displayed a JavaScript alert containing `1`.

### Expected Behaviour

User-controlled input should be treated as untrusted data and safely encoded for its output context. It should not be interpreted as executable script merely because it is included in a search-results page.

### Observed Behaviour

The browser executed the submitted script payload after the application reflected the input into the page.

This confirms reflected XSS behaviour in the training lab.

### Evidence

- **Evidence 06 — Browser alert:** `evidence/06-reflected-xss-alert.png`
- **Evidence 07 — Request and response:** `evidence/07-reflected-xss-request-response.png`

The screenshots should be reviewed alongside the test methodology and limitations. Any authentication cookies, session tokens or other sensitive values must be redacted.

## 5. Security Impact

Reflected XSS occurs when an application includes untrusted request data in a response in a way that allows a browser to execute it as script.

In a real application, an attacker could attempt to persuade a victim to follow a crafted link or submit a crafted request. If the vulnerable page executes the injected script in the application's origin, possible impact may include actions performed in the victim's authenticated context or access to information available to that script.

The actual impact depends on the application's design, browser protections, session controls and the data or actions available to the affected user.

This test demonstrated script execution through a browser alert. It did not test cookie theft, credential collection, account compromise or other follow-on impact.

## 6. Risk Assessment

**Assessment:** Confirmed reflected XSS behaviour in the training application.

The successful alert demonstrates that the input was interpreted as executable JavaScript in the browser. The severity of an equivalent issue in a real application would depend on the affected page, potential victims, available privileges and the actions the injected script could perform.

No formal CVSS score has been assigned to this training exercise.

## 7. Recommended Remediation

- Apply context-aware output encoding to untrusted data before rendering it into HTML.
- Use safe templating mechanisms that encode output by default.
- Avoid placing untrusted input into executable JavaScript, event-handler attributes or other dangerous contexts.
- Validate input where appropriate, while recognising that validation alone is not a substitute for safe output encoding.
- Consider a restrictive Content Security Policy as a defence-in-depth measure, not as the primary fix.
- Add regression tests to confirm that search terms are rendered as text rather than executable markup.

## 8. Retest Criteria

After remediation:

1. Submit ordinary search terms and confirm search continues to work.
2. Repeat the authorised test using the original proof-of-concept payload.
3. Confirm that the browser no longer executes the injected script.
4. Verify that the payload is safely encoded or treated as text in the returned page.
5. Review relevant output contexts to ensure the fix is not limited to one displayed message.

## 9. Limitations

- Testing was restricted to the designated PortSwigger training lab.
- The assessment covered the reflected search-input behaviour that was observed.
- No attempt was made to steal cookies, obtain credentials or affect another user's account.
- The finding does not establish that other applications are vulnerable.
- Published screenshots must not disclose session cookies, authentication tokens or other sensitive values.

## 10. Conclusion

The assessment demonstrated reflected XSS in the training application. A controlled test payload was reflected in a way that caused the browser to execute JavaScript and display an alert.

The investigation recorded the reproduction method, observed result, potential impact, remediation guidance and retest criteria. It demonstrates a structured approach to validating a web application vulnerability and documenting the result without claiming impact that was not tested.
