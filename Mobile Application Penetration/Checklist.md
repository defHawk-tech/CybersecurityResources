 Reconnaissance
- [ ] Identify platform (Android/iOS)
- [ ] Gather APK/IPA file
- [ ] Extract app metadata (package name, permissions, etc.)
- [ ] Check app version and changelogs
- [ ] Review app store descriptions and screenshots

 Static Analysis
- [ ] Decompile APK/IPA
- [ ] Analyze AndroidManifest.xml / Info.plist
- [ ] Look for hardcoded secrets (API keys, tokens, credentials)
- [ ] Analyze source code (Java/Kotlin/Swift/Obj-C)
- [ ] Identify usage of insecure components/libraries
- [ ] Analyze third-party SDKs
- [ ] Search for debug logs or error messages

 Runtime Analysis (Dynamic Testing)
- [ ] Install app on rooted/jailbroken device or emulator
- [ ] Monitor logs using Logcat / Console
- [ ] Intercept traffic using Burp Suite / Charles Proxy
- [ ] Test for SSL pinning / Certificate validation
- [ ] Bypass SSL pinning (Frida, Objection, etc.)
- [ ] Check for sensitive data in memory
- [ ] Perform UI/UX fuzzing (inputs, buttons, gestures)
- [ ] Monitor file system access and storage

 API Testing
- [ ] Enumerate and analyze backend APIs
- [ ] Check for IDOR/BAC
- [ ] Test rate limiting and brute-force protections
- [ ] Check for authentication & session management issues
- [ ] Test input validation (XSS, SQLi, etc.)
- [ ] Analyze error responses and verbose messages

 Authentication & Authorization
- [ ] Test login/logout flows
- [ ] Check for weak password policies
- [ ] Test multi-factor authentication
- [ ] Check session token handling
- [ ] Test role-based access control (RBAC)

 Data Storage Analysis
- [ ] Check for sensitive data stored in:
  - [ ] SharedPreferences
  - [ ] Keychain (iOS)
  - [ ] SQLite databases
  - [ ] Internal/External storage
  - [ ] NSUserDefaults (iOS)
- [ ] Look for unencrypted or insecure storage

 Network Communication
- [ ] Test for insecure communication (HTTP vs HTTPS)
- [ ] Check for sensitive data leakage in requests/responses
- [ ] Analyze WebSocket communications (if any)
- [ ] Inspect certificate pinning and its bypass

 Reverse Engineering & Tampering
- [ ] Attempt to modify app logic (patch APK, Frida hooks)
- [ ] Look for root/jailbreak detection
- [ ] Check for code obfuscation
- [ ] Identify debug build / test artifacts
- [ ] Try bypassing licensing / in-app purchases

Tools & Utilities
- [ ] APKTool / JADX / MobSF
- [ ] Frida / Objection
- [ ] Burp Suite / Charles Proxy
- [ ] adb / ios-deploy / cycript
- [ ] Ghidra / Hopper / IDA Pro

 Reporting
- [ ] Document all findings with severity & impact
- [ ] Provide PoC (screenshots, logs, scripts)
- [ ] Recommend mitigations

---

*Always follow ethical guidelines and only test apps with proper authorization.*
