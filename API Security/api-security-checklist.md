# API Security Checklist

A checklist of the most important security countermeasures when designing, testing, and releasing your API.

## Authentication
- [ ] Don't use Basic Auth. Use standard authentication instead (e.g., JWT).
- [ ] Don't reinvent the wheel in authentication, token generation, or password storage. Use the standards.
- [ ] Use Max Retry and jail features in Login.
- [ ] Use encryption on all sensitive data.

## JWT (JSON Web Token)
- [ ] Use a random complicated key (JWT Secret) to make brute-forcing the token very hard.
- [ ] Don't extract the algorithm from the header. Force the algorithm in the backend (HS256 or RS256).
- [ ] Make token expiration (TTL, RTTL) as short as possible.
- [ ] Don't store sensitive data in the JWT payload, as it can be decoded easily.
- [ ] Avoid storing too much data. JWT is usually shared in headers and they have a size limit.

## Access
- [ ] Limit requests (Throttling) to avoid DDoS/brute-force attacks.
- [ ] Use HTTPS on the server side with TLS 1.2+ and secure ciphers to avoid MITM (Man in the Middle Attack).
- [ ] Use the HSTS header with SSL to avoid SSL Strip attacks.
- [ ] Turn off directory listings.
- [ ] For private APIs, allow access only from safelisted IPs/hosts.

## Authorization

### OAuth
- [ ] Always validate `redirect_uri` server-side to allow only safelisted URLs.
- [ ] Always try to exchange for code and not tokens (don't allow `response_type=token`).
- [ ] Use the state parameter with a random hash to prevent CSRF on the OAuth authorization process.
- [ ] Define the default scope and validate scope parameters for each application.

## Input
- [ ] Use the proper HTTP method according to the operation: `GET` (read), `POST` (create), `PUT/PATCH` (replace/update), and `DELETE` (delete a record). Respond with `405 Method Not Allowed` if the requested method isn't appropriate for the resource.
- [ ] Validate `content-type` on the `Accept` header to allow only supported formats (e.g., `application/xml`, `application/json`) and respond with `406 Not Acceptable` if not matched.
- [ ] Validate `content-type` of posted data (e.g., `application/x-www-form-urlencoded`, `multipart/form-data`, `application/json`).
- [ ] Validate user input to avoid common vulnerabilities (e.g., XSS, SQL Injection, Remote Code Execution).
- [ ] Don't use sensitive data (credentials, passwords, security tokens, or API keys) in the URL; use the `Authorization` header instead.
- [ ] Use only server-side encryption.
- [ ] Use an API Gateway service to enable caching, Rate Limit policies (e.g., Quota, Spike Arrest, or Concurrent Rate Limit), and deploy API resources dynamically.

## Processing
- [ ] Check if all endpoints are protected behind authentication to avoid broken authentication processes.
- [ ] Avoid using user-specific resource IDs directly. Use `/me/orders` instead of `/user/654321/orders`.
- [ ] Don't auto-increment IDs. Use UUID instead.
- [ ] If parsing XML data, ensure entity parsing is disabled to avoid XXE (XML External Entity) attacks.
- [ ] If parsing XML, YAML, or similar, ensure entity expansion is disabled to avoid Billion Laughs/XML bomb attacks.
- [ ] Use a CDN for file uploads.
- [ ] For large data processing, use Workers and Queues to handle operations in the background to avoid HTTP Blocking.
- [ ] Turn DEBUG mode OFF.
- [ ] Use non-executable stacks when available.

## Output
- [ ] Send `X-Content-Type-Options: nosniff` header.
- [ ] Send `X-Frame-Options: deny` header.
- [ ] Send `Content-Security-Policy: default-src 'none'` header.
- [ ] Remove fingerprinting headers (e.g., `X-Powered-By`, `Server`, `X-AspNet-Version`).
- [ ] Force content-type for your response. If returning `application/json`, ensure the response content-type is `application/json`.
- [ ] Don't return sensitive data like credentials, passwords, or security tokens.
- [ ] Return the appropriate status code for each operation (e.g., `200 OK`, `400 Bad Request`, `401 Unauthorized`, `405 Method Not Allowed`).

## CI & CD
- [ ] Audit design and implementation with unit/integration tests coverage.
- [ ] Use a code review process and avoid self-approval.
- [ ] Ensure all components are scanned by AV software before pushing to production, including vendor libraries and dependencies.
- [ ] Continuously run security tests (static/dynamic analysis) on your code.
- [ ] Check dependencies (software and OS) for known vulnerabilities.
- [ ] Design a rollback solution for deployments.

## Monitoring
- [ ] Use centralized logging for all services and components.
- [ ] Use agents to monitor all traffic, errors, requests, and responses.
- [ ] Set up alerts for SMS, Slack, Email, Telegram, Kibana, Cloudwatch, etc.
- [ ] Ensure sensitive data like credit cards, passwords, or PINs are not logged.
- [ ] Use an IDS and/or IPS system to monitor your API requests and instances.
