# API Attacking Checklist

A checklist of techniques and strategies for testing the security and resilience of APIs during a penetration test or attack simulation.

## Authentication Attacks
- [ ] Test for weak credentials using a brute-force or dictionary attack.
- [ ] Check for endpoints vulnerable to credential stuffing (reusing stolen credentials).
- [ ] Look for insecure implementations of Basic Auth or token-based authentication.
- [ ] Test for lack of account lockout or rate-limiting on login endpoints.
- [ ] Inspect for weak or predictable session tokens.
- [ ] Attempt bypassing authentication by altering tokens or manipulating cookies.
- [ ] Exploit poorly implemented multi-factor authentication (MFA) bypass mechanisms.

## Authorization Attacks
- [ ] Test for IDOR (Insecure Direct Object References) by modifying user/resource IDs in requests.
- [ ] Test for privilege escalation by manipulating roles or permissions.
- [ ] Check for improper enforcement of access control on sensitive endpoints (e.g., admin panels).
- [ ] Attempt to access private APIs by bypassing IP or hostname restrictions.
- [ ] Exploit insecure CORS configurations to access restricted endpoints.

## Input Validation Attacks
- [ ] Test for SQL Injection vulnerabilities.
- [ ] Test for XSS (Cross-Site Scripting) in input fields and API responses.
- [ ] Inject malicious payloads to test for Remote Code Execution (RCE).
- [ ] Submit oversized payloads to test for buffer overflow or Denial of Service (DoS).
- [ ] Test for XML External Entity (XXE) vulnerabilities if the API parses XML.
- [ ] Test for insecure deserialization of data.

## JWT Attacks
- [ ] Modify the JWT header algorithm to `none` and attempt bypassing verification.
- [ ] Brute-force weak JWT secrets.
- [ ] Test for token reuse attacks to check for session fixation vulnerabilities.
- [ ] Test for missing expiration times or overly permissive token lifetimes.
- [ ] Decode and inspect JWT payloads for sensitive information leakage.

## Endpoint Enumeration
- [ ] Perform fuzzing to discover hidden endpoints or API functions.
- [ ] Inspect API documentation, responses, and error messages for clues about unused endpoints.
- [ ] Test for verbose error messages that reveal backend logic, paths, or server details.

## API Rate-Limiting and DoS
- [ ] Test for lack of rate-limiting by sending multiple requests per second.
- [ ] Attempt a slow HTTP attack by keeping connections open.
- [ ] Exploit endpoints that allow resource-intensive operations to cause performance degradation.

## Network Attacks
- [ ] Check for APIs served over HTTP instead of HTTPS.
- [ ] Perform MITM (Man-In-The-Middle) attacks to inspect or manipulate traffic.
- [ ] Exploit insecure TLS configurations (e.g., outdated ciphers, SSL/TLS downgrade attacks).

## Data Exposure
- [ ] Test for sensitive data exposure in API responses (e.g., credentials, tokens, or PII).
- [ ] Inspect hidden fields or metadata in JSON/XML responses for sensitive information.
- [ ] Test for information leakage via headers such as `X-Powered-By` or server details.

## OAuth and Token Attacks
- [ ] Test for open redirect vulnerabilities in `redirect_uri`.
- [ ] Test for CSRF vulnerabilities in OAuth flows (e.g., missing state parameter).
- [ ] Attempt to reuse authorization codes multiple times.
- [ ] Test for privilege escalation by requesting excessive scopes.

## Input Manipulation
- [ ] Submit unexpected data types to endpoints (e.g., strings instead of integers).
- [ ] Test for missing input length or format validation.
- [ ] Inject Unicode, special characters, or encodings to bypass filters.
- [ ] Manipulate `content-type` headers to check for improper handling of different formats.

## Response Manipulation
- [ ] Test for cache poisoning by manipulating cache-related headers.
- [ ] Attempt to exploit insecure handling of redirects in responses.
- [ ] Manipulate responses to test for insecure handling of error codes (e.g., bypassing checks with 200 OK).

## File Upload Testing
- [ ] Test file upload endpoints for unrestricted file types (e.g., uploading executables or scripts).
- [ ] Attempt to upload files with malicious payloads or oversized files.
- [ ] Test for insecure handling of file paths (path traversal).

## Business Logic Abuse
- [ ] Test for logic flaws that allow bypassing required steps (e.g., skipping payment verification).
- [ ] Attempt to manipulate order quantities, prices, or discounts via API requests.
- [ ] Test for abuse of batch processing endpoints (e.g., submitting excessive data in one request).

## Logging and Monitoring
- [ ] Check for lack of logging for failed login attempts or suspicious activity.
- [ ] Test for sensitive data stored in logs (e.g., passwords, tokens, or credit card numbers).

## Tools for API Attacking
- [ ] Use **Burp Suite** for intercepting and manipulating requests.
- [ ] Use **Postman** for exploring and testing API endpoints.
- [ ] Use **JWT.io** to decode and analyze JWT tokens.
- [ ] Use **OWASP ZAP** for automated API scanning.
- [ ] Use **ffuf** or **dirbuster** for endpoint discovery and fuzzing.
- [ ] Use **sqlmap** for SQL injection testing.
- [ ] Use **Nmap** or **Shodan** to discover exposed APIs and services.

> **Note:** Always perform testing within the scope of legal permissions. Unauthorized attacks are illegal and unethical.
