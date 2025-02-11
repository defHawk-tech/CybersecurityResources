# GraphQL Testing Checklist

## 1. Information Gathering
- [ ] Identify the GraphQL endpoint.
- [ ] Check if introspection is enabled.
- [ ] Enumerate available queries and mutations.
- [ ] Document schema, types, and fields.
- [ ] Collect available queries and their parameters.
- [ ] Check for versioning in the GraphQL API (e.g., `/v1/graphql` vs. `/v2/graphql`).
- [ ] Identify deprecated fields or queries.

## 2. Authentication & Authorization
- [ ] Verify access control on each query/mutation.
- [ ] Test authenticated vs. unauthenticated access.
- [ ] Test role-based access (e.g., user, admin).
- [ ] Check for excessive data exposure.
- [ ] Test for authorization bypass through query manipulation.
- [ ] Ensure token validation on protected routes.
- [ ] Test for token expiration and renewal mechanisms.
- [ ] Check for replay attacks using expired tokens.

## 3. Input Validation
- [ ] Test input sanitization and validation.
- [ ] Attempt SQL injection through input fields.
- [ ] Try NoSQL injection if applicable.
- [ ] Test for Cross-Site Scripting (XSS).
- [ ] Test for malformed inputs and their effects.
- [ ] Test for buffer overflows or integer overflows in input fields.
- [ ] Check for proper handling of file uploads (if applicable).

## 4. Query & Mutation Testing
- [ ] Perform deep query nesting.
- [ ] Test for over-fetching (too much data).
- [ ] Test for under-fetching (too little data).
- [ ] Try unauthorized mutations.
- [ ] Validate mutation parameter types and values.
- [ ] Test for query aliasing abuse (e.g., requesting the same field multiple times with different aliases).
- [ ] Check for proper handling of pagination (e.g., `first`, `last`, `after`, `before`).

## 5. Query and Introspection Attacks
- [ ] Test for introspection abuse (exposing sensitive schema data).
- [ ] Manipulate queries to retrieve unauthorized data using introspection.
- [ ] Test for blind injection attacks using introspection.
- [ ] Attempt to exploit nested query capabilities for more information.
- [ ] Test for introspection queries that reveal sensitive information (e.g., deprecated fields, internal types).

## 6. Field Manipulation
- [ ] Test for modification of query fields (fields that shouldn’t be queried).
- [ ] Attempt to access hidden fields or properties.
- [ ] Check if fields can be accessed inappropriately or with tampered input.
- [ ] Test for field name collisions (e.g., aliasing fields to override existing ones).

## 7. Batching and Rate Limiting Attacks
- [ ] Test for multiple query batching and the impact on the server.
- [ ] Check if the API properly limits batch size.
- [ ] Test for rate-limiting of queries and mutations.
- [ ] Attempt DoS attacks through large batch queries.
- [ ] Test for query batching with mixed queries (e.g., combining read and write operations).

## 8. Authentication Bypass
- [ ] Test for flaws in token authentication (e.g., JWT).
- [ ] Attempt to bypass authentication by tampering with tokens.
- [ ] Test for weak or predictable session management.
- [ ] Check for missing CSRF protections.
- [ ] Test for weak JWT secrets or predictable token generation.

## 9. SQL Injection
- [ ] Test for SQL injection through GraphQL queries and mutations.
- [ ] Check for unsafe handling of user inputs leading to SQL injection.
- [ ] Test for UNION-based SQL injection in GraphQL queries.
- [ ] Test for blind SQL injection by manipulating query parameters.
- [ ] Test for ORM-based SQL injection (e.g., Sequelize, TypeORM).

## 10. Insecure Direct Object References (IDOR)
- [ ] Check for access control flaws by modifying query parameters (e.g., IDs).
- [ ] Test for unauthorized access to data by manipulating object references.
- [ ] Attempt to access other users' data by tampering with query arguments.
- [ ] Test for IDOR in nested objects or relationships.

## 11. Mutations and Data Tampering
- [ ] Test for improper validation in mutations (e.g., update/delete).
- [ ] Attempt unauthorized mutations (e.g., changing user roles, deleting records).
- [ ] Check if malicious users can tamper with data fields in mutations.
- [ ] Test for insufficient validation of input data in mutations.
- [ ] Test for race conditions in mutations (e.g., updating the same record simultaneously).

## 12. Information Disclosure
- [ ] Ensure sensitive data is not exposed in query responses.
- [ ] Test for excessive information disclosure in error messages.
- [ ] Check for confidential data leakage (e.g., email addresses, personal data).
- [ ] Look for sensitive fields being exposed unintentionally.
- [ ] Test for information disclosure in GraphQL subscriptions.

## 13. Authorization Bypass
- [ ] Check for issues with access control for different user roles.
- [ ] Test for flaws in object-level access controls (e.g., user-specific data).
- [ ] Try to access data or perform actions that should be restricted based on the user role.
- [ ] Test for authorization bypass in nested queries or relationships.

## 14. Tools for GraphQL Attacks
- [ ] **GraphiQL**: Use to explore the API and test queries.
- [ ] **Burp Suite**: Utilize the GraphQL plugin to test queries and mutations.
- [ ] **GraphQLMap**: Automated scanner to find security issues in GraphQL APIs.
- [ ] **GQLint**: Check for common GraphQL mistakes and vulnerabilities.
- [ ] **Apollo Client Devtools**: Explore schema and test queries directly.
- [ ] **SQLMap**: Use with GraphQL queries to check for SQL injection vulnerabilities.
- [ ] **InQL (Burp Suite Extension)**: Use for automated GraphQL schema analysis and query generation.
- [ ] **GraphQL Playground**: Test queries and mutations interactively.
- [ ] **Postman**: Use for automated testing of GraphQL APIs with collections.
- [ ] **OWASP ZAP**: Test for common vulnerabilities like XSS, CSRF, and injection.
- [ ] **GraphQL Cop**: Automated security testing tool for GraphQL APIs.
- [ ] **Altair GraphQL Client**: Test and debug GraphQL queries.

## 15. Rate Limiting & Throttling
- [ ] Test for rate limits on the API.
- [ ] Check if queries are throttled appropriately.
- [ ] Attempt DoS attacks with large or complex queries.
- [ ] Test for user-specific rate-limiting mechanisms.
- [ ] Test for rate-limiting bypass techniques (e.g., IP rotation, token reuse).
- [ ] Check if rate limits are applied consistently across different query types (e.g., queries vs. mutations).
- [ ] Test for query complexity-based rate limiting (e.g., depth, number of fields).

## 16. Error Handling
- [ ] Review error messages for sensitive information.
- [ ] Test for stack traces or detailed errors.
- [ ] Check error handling for invalid/malformed queries.
- [ ] Ensure errors do not reveal too much information about the backend structure.
- [ ] Test for consistent error responses (e.g., HTTP status codes, GraphQL error formats).
- [ ] Check if error messages are user-friendly but not overly verbose.
- [ ] Test for error handling in edge cases (e.g., null values, empty arrays).

## 17. Performance Testing
- [ ] Analyze query performance.
- [ ] Check for excessive processing times.
- [ ] Test GraphQL queries with large data sets.
- [ ] Monitor server load and response time during complex queries.
- [ ] Test for performance issues in subscriptions (e.g., too many active subscriptions).

## 18. Security Headers
- [ ] Ensure security headers are properly set (CORS, CSP, etc.).
- [ ] Check for secure transport (HTTPS).
- [ ] Test for anti-CSRF protections on mutations.
- [ ] Test for HSTS (HTTP Strict Transport Security) headers.

## 19. Business Logic Testing
- [ ] Test for business logic flaws (e.g., bypassing payment flows, manipulating pricing, or access to premium features).
- [ ] Validate that custom resolvers or middleware enforce business rules.
- [ ] Test for race conditions in mutations (e.g., double-spending, inventory overselling).

## 20. Caching and Data Consistency
- [ ] Test for caching mechanisms (e.g., CDN, server-side caching) and their impact on data consistency.
- [ ] Check if cached data is properly invalidated after mutations.
- [ ] Test for stale data exposure due to improper caching.

## 21. Third-Party Integrations
- [ ] Test for vulnerabilities in third-party services or APIs called by the GraphQL API.
- [ ] Check for proper error handling when third-party services fail.
- [ ] Test for data leakage through third-party integrations.

## 22. Schema Design Review
- [ ] Review schema design for potential security issues (e.g., exposing sensitive fields).
- [ ] Check for proper use of directives (e.g., `@deprecated`, `@auth`).
- [ ] Ensure schema follows best practices (e.g., avoiding overly complex types).

## 23. Monitoring and Logging
- [ ] Test if sensitive data is logged in server logs.
- [ ] Check if query and mutation execution is properly monitored.
- [ ] Ensure logging does not expose sensitive information (e.g., tokens, PII).

## 24. Compliance
- [ ] Test for compliance with data protection regulations (e.g., GDPR, CCPA).
- [ ] Check if sensitive data is properly encrypted in transit and at rest.
- [ ] Ensure proper consent mechanisms are in place for data access.

## 25. Documentation Review
- [ ] Review API documentation for completeness and accuracy.
- [ ] Check if documentation includes security best practices for consumers.
- [ ] Ensure deprecated fields or queries are clearly marked.

---

## Resources
Here are some additional resources to help you with GraphQL testing and security:

### **Tools**
- [GraphiQL](https://github.com/graphql/graphiql): An in-browser IDE for exploring GraphQL APIs.
- [Burp Suite GraphQL Plugin](https://portswigger.net/bappstore/4845f0f78e91411aac5b8a0e6d0f5b5b): A Burp Suite extension for testing GraphQL APIs.
- [GraphQLMap](https://github.com/swisskyrepo/GraphQLmap): A scripting engine to interact with GraphQL APIs for security testing.
- [InQL](https://github.com/doyensec/inql): A Burp Suite extension for GraphQL security testing.
- [GraphQL Cop](https://github.com/dolevf/graphql-cop): A security testing tool for GraphQL APIs.
- [Altair GraphQL Client](https://altair.sirmuel.design/): A feature-rich GraphQL client for testing and debugging.

### **Guides and Articles**
- [OWASP GraphQL Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/GraphQL_Cheat_Sheet.html): A comprehensive guide to securing GraphQL APIs.
- [GraphQL Security Best Practices](https://blog.apollographql.com/graphql-security-best-practices-8f6e74f7f1a5): A blog post by Apollo on securing GraphQL APIs.
- [How to Secure Your GraphQL API](https://hasura.io/blog/graphql-security-best-practices/): A guide by Hasura on GraphQL security.
- [GraphQL Security Checklist](https://escape.tech/blog/graphql-security-checklist/): A detailed checklist for securing GraphQL APIs.

### **Books**
- **"GraphQL in Action" by Samer Buna**: A practical guide to building and securing GraphQL APIs.
- **"Learning GraphQL" by Eve Porcello and Alex Banks**: A beginner-friendly book on GraphQL concepts and security.

### **Videos and Tutorials**
- [GraphQL Security: Common Vulnerabilities and How to Fix Them](https://www.youtube.com/watch?v=J7vHXkF4Fcs): A video tutorial on GraphQL security.
- [Securing GraphQL APIs](https://www.youtube.com/watch?v=4tIgDZ6y7-Y): A talk on securing GraphQL APIs by API security experts.

---

## Additional Notes
- [ ] Document any specific business logic or custom implementations.
- [ ] Collaborate with developers for insights into complex queries and mutations.
- [ ] Regularly update the checklist based on new vulnerabilities and testing practices.
