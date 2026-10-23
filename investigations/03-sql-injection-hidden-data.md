# Finding 03 — SQL Injection in Product Category Filter

## 1. Assessment Overview

**Target:** PortSwigger Web Security Academy — SQL injection vulnerability in WHERE clause allowing retrieval of hidden data  
**Assessment type:** Authorised web application security lab  
**Vulnerability category:** SQL Injection (SQLi)  
**Tools:** Burp Suite Community Edition, Proxy interception and request modification

This assessment examined whether user-controlled input in a product-category filter could alter the behaviour of the application's database query.

## 2. Objective

The objective was to test how the application handled a supplied category value and determine whether modifying the value could expose products that were not normally displayed.

## 3. Methodology

1. Opened the designated PortSwigger training lab.
2. Selected a product category to observe the application's normal request.
3. Intercepted the category request using Burp Suite.
4. Modified the category parameter using the test payload:

   ```sql
   '+OR+1=1--
   ```

5. Forwarded the modified request to the training application.
6. Observed the product listing and the lab's completion result.

All testing took place within the authorised training environment.

## 4. Finding and Evidence

### Observation

The original request filtered the displayed products by category.

After the category parameter was modified with the test payload, the application displayed all products and the training lab indicated that the challenge had been solved.

### Technical Interpretation

The payload attempts to alter the logic of a SQL condition by introducing an `OR` condition that evaluates as true and commenting out the remainder of the statement, depending on the database's SQL syntax and the way the input is processed.

The observed result is consistent with SQL injection in the category filter. The application appears to have allowed user-controlled input to influence the query's logic rather than treating the value strictly as data.

The database implementation and underlying source code were not independently examined.

### Expected Behaviour

The application should treat the supplied category as data, not executable SQL syntax. Users should only receive products permitted by the application's intended filtering and access-control rules.

## 5. Security Impact

SQL injection can allow an attacker to alter database query behaviour. Depending on the vulnerable query, database privileges and application design, possible consequences include unauthorised data disclosure, modification of records, or access to information that should remain hidden.

In this lab, the demonstrated outcome was the display of products that were otherwise hidden by the category filter.

The test did not establish access to other database tables, modification of data or compromise of the underlying server.

## 6. Risk Assessment

**Assessment:** Confirmed SQL injection behaviour in the training application.

The observed change in product visibility demonstrates that the input affected query behaviour. The wider severity in a real application would depend on the affected query, the data accessible through it, database privileges and the presence of other security controls.

No formal CVSS score has been assigned to this training exercise.

## 7. Recommended Remediation

- Use parameterised queries or prepared statements so user input cannot alter SQL syntax.
- Avoid constructing SQL queries by concatenating untrusted input.
- Validate category values against an allowlist of recognised categories.
- Use database accounts with only the permissions required by the application.
- Return generic error messages to users while recording useful diagnostic details securely.
- Add regression tests using unexpected input to verify that category filtering behaves safely.

Input validation is a useful additional control, but it is not a substitute for parameterised database queries.

## 8. Retest Criteria

After remediation:

1. Submit normal category filters and verify that products are filtered correctly.
2. Repeat the test in the authorised lab using the previously successful payload.
3. Confirm that the payload no longer changes the query's logic or exposes unintended products.
4. Verify that valid categories continue to work as expected.
5. Review server-side behaviour and logs where available.

## 9. Limitations

- Testing was restricted to the designated PortSwigger training lab.
- The underlying SQL query and database implementation were not directly inspected.
- The assessment confirmed the observed product-display behaviour, not unrestricted access to the database.
- The finding should not be treated as evidence that unrelated applications are vulnerable.
- Public screenshots must exclude session cookies, authentication tokens and other sensitive values.

## 10. Conclusion

The assessment demonstrated SQL injection behaviour in a product-category filter. Modifying the category request caused the application to display all products and completed the lab challenge.

The investigation documented the test method, observed outcome, potential impact and remediation recommendations. It demonstrates a practical approach to testing user-controlled input and reporting a validated vulnerability within an authorised environment.
