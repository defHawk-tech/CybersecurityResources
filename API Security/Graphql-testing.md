# GraphQL Testing Checklist

## 1. Information Gathering
- [ ] Identify the GraphQL endpoint.
- [ ] Check if introspection is enabled.
- [ ] Enumerate available queries and mutations.
- [ ] Document schema, types, and fields.
- [ ] Collect available queries and their parameters.

## 2. Authentication & Authorization
- [ ] Verify access control on each query/mutation.
- [ ] Test authenticated vs. unauthenticated access.
- [ ] Test role-based access (e.g., user, admin).
- [ ] Check for excessive data exposure.
- [ ] Test for authorization bypass through query manipulation.
- [ ] Ensure token validation on protected routes.

## 3. Input Validation
- [ ] Test input sanitization and validation.
- [ ] Attempt SQL injection through input fields.
- [ ] Try NoSQL injection if applicable.
- [ ] Test for Cross-Site Scripting (XSS).
- [ ] Test for malformed inputs and their effects.

## 4. Query & Mutation Testing
- [ ] Perform deep query nesting.
- [ ] Test for over-fetching (too much data).
- [ ] Test for under-fetching (too little data).
- [ ] Try unauthorized mutations.
- [ ] Validate mutation parameter types and values.

## 5. Query and Introspection Attacks
- [ ] Test for introspection abuse (exposing sensitive schema data).
- [ ] Manipulate queries to retrieve unauthorized data using introspection.
- [ ] Test for blind injection attacks using introspection.
- [ ] Attempt to exploit nested query capabilities for more information.

## 6. Field Manipulation
- [ ] Test for modification of query fields (fields that shouldn’t be queried).
- [ ] Attempt to access hidden fields or properties.
- [ ] Check if fields can be accessed inappropriately or with tampered input.

## 7. Batching and Rate Limiting Attacks
- [ ] Test for multiple query batching and the impact on the server.
- [ ] Check if the API properly limits batch size.
- [ ] Test for rate-limiting of queries and mutations.
- [ ] Attempt DoS attacks through large batch queries.

## 8. Authentication Bypass
- [ ] Test for flaws in token authentication (e.g., JWT).
- [ ] Attempt to bypass authentication by tampering with tokens.
- [ ] Test for weak or predictable session management.
- [ ] Check for missing CSRF protections.
  
## 9. SQL Injection
- [ ] Test for SQL injection through GraphQL queries and mutations.
- [ ] Check for unsafe handling of user inputs leading to SQL injection.
- [ ] Test for UNION-based SQL injection in GraphQL queries.
- [ ] Test for blind SQL injection by manipulating query parameters.

## 10. Insecure Direct Object References (IDOR)
- [ ] Check for access control flaws by modifying query parameters (e.g., IDs).
- [ ] Test for unauthorized access to data by manipulating object references.
- [ ] Attempt to access other users' data by tampering with query arguments.

## 11. Mutations and Data Tampering
- [ ] Test for improper validation in mutations (e.g., update/delete).
- [ ] Attempt unauthorized mutations (e.g., changing user roles, deleting records).
- [ ] Check if malicious users can tamper with data fields in mutations.
- [ ] Test for insufficient validation of input data in mutations.

## 12. Information Disclosure
- [ ] Ensure sensitive data is not exposed in query responses.
- [ ] Test for excessive information disclosure in error messages.
- [ ] Check for confidential data leakage (e.g., email addresses, personal data).
- [ ] Look for sensitive fields being exposed unintentionally.

## 13. Authorization Bypass
- [ ] Check for issues with access control for different user roles.
- [ ] Test for flaws in object-level access controls (e.g., user-specific data).
- [ ] Try to access data or perform actions that should be restricted based on the user role.
  
## 14. Tools for GraphQL Attacks
- [ ] **GraphiQL**: Use to explore the API and test queries.
- [ ] **Burp Suite**: Utilize the GraphQL plugin to test queries and mutations.
- [ ] **GraphQLMap**: Automated scanner to find security issues in GraphQL APIs.
- [ ] **GQLint**: Check for common GraphQL mistakes and vulnerabilities.
- [ ] **Apollo Client Devtools**: Explore schema and test queries directly.
- [ ] **SQLMap**: Use with GraphQL queries to check for SQL injection vulnerabilities.

## 15. Rate Limiting & Throttling
- [ ] Test for rate limits on the API.
- [ ] Check if queries are throttled appropriately.
- [ ] Attempt DoS attacks with large or complex queries.
- [ ] Test for user-specific rate-limiting mechanisms.

## 16. Error Handling
- [ ] Review error messages for sensitive information.
- [ ] Test for stack traces or detailed errors.
- [ ] Check error handling for invalid/malformed queries.
- [ ] Ensure errors do not reveal too much information about the backend structure.

## 17. Performance Testing
- [ ] Analyze query performance.
- [ ] Check for excessive processing times.
- [ ] Test GraphQL queries with large data sets.
- [ ] Monitor server load and response time during complex queries.

## 18. Security Headers
- [ ] Ensure security headers are properly set (CORS, CSP, etc.).
- [ ] Check for secure transport (HTTPS).
- [ ] Test for anti-CSRF protections on mutations.

---

## Additional Notes
- [ ] Document any specific business logic or custom implementations.
- [ ] Collaborate with developers for insights into complex queries and mutations.
- [ ] Regularly update the checklist based on new vulnerabilities and testing practices.
