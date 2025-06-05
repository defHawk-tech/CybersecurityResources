+----------------------------------+
| 1. Reconnaissance                |
| Scan AWS env (Shodan, AWS CLI)   |
+----------------------------------+
                |
                v
+----------------------------------+
| 2. Find Misconfigurations        |
| Look for permissive rules or     |
| exposed credentials              |
+----------------------------------+
                |
                v
+----------------------------------+
| 3. Exploit Access                |
| Try open ports or stolen creds   |
+----------------------------------+
                |
                v
+----------------------------------+    +----------------------------------+
| Access Gained?                   |-->| No: 4. Escalate Attack           |
|                                  |   | Exploit IAM or metadata service |
+----------------------------------+   +----------------------------------+
                | Yes                          |
                v                             |
+----------------------------------+          |
| 5. Persist                       |<---------+
| Modify or create Security Groups |
+----------------------------------+
                |
                v
+----------------------------------+
| 6. Evade Detection               |
| Subtle rule changes, disable logs|
+----------------------------------+
                |
                v
+----------------------------------+
| 7. Exfiltrate or Maintain        |
| Steal data or keep access        |
+----------------------------------+
