# Active Directory Tools Checklist

## Enumeration Tools
- [ ] **BloodHound** - Graph-based AD recon (`https://github.com/BloodHoundAD/BloodHound`)
- [ ] **SharpHound** - Data collector for BloodHound (`https://github.com/BloodHoundAD/SharpHound`)
- [ ] **ADExplorer** - GUI tool for exploring AD objects (`https://docs.microsoft.com/en-us/sysinternals/downloads/adexplorer`)
- [ ] **PowerView** - PowerShell AD enumeration (`https://github.com/PowerShellMafia/PowerSploit/tree/master/Recon`)
- [ ] **LDAPDomainDump** - Dumps AD domain info over LDAP (`https://github.com/dirkjanm/ldapdomaindump`)

## Credential Dumping Tools
- [ ] **Mimikatz** - Extracts plaintext passwords and hashes (`https://github.com/gentilkiwi/mimikatz`)
- [ ] **LaZagne** - Retrieves stored passwords (`https://github.com/AlessandroZ/LaZagne`)
- [ ] **SecretsDump** - Dumps credentials from AD database (`https://github.com/SecureAuthCorp/impacket/blob/master/examples/secretsdump.py`)
- [ ] **Rubeus** - Kerberos abuse toolkit (`https://github.com/GhostPack/Rubeus`)

## Lateral Movement Tools
- [ ] **PsExec** - Remote command execution (`https://docs.microsoft.com/en-us/sysinternals/downloads/psexec`)
- [ ] **CrackMapExec** - AD enumeration, lateral movement (`https://github.com/Porchetta-Industries/CrackMapExec`)
- [ ] **WMImplant** - WMI-based remote access (`https://github.com/FortyNorthSecurity/WMImplant`)
- [ ] **Impacket** - Python networking tools for SMB, WMI (`https://github.com/SecureAuthCorp/impacket`)

## Privilege Escalation Tools
- [ ] **WinPEAS** - Local privilege escalation enumeration (`https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS`)
- [ ] **Seatbelt** - Security misconfigurations checker (`https://github.com/GhostPack/Seatbelt`)
- [ ] **PowerUp** - PowerShell privilege escalation (`https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc`)

## Kerberos Attacks Tools
- [ ] **GetUserSPNs.py** - Kerberoasting attacks (`https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetUserSPNs.py`)
- [ ] **ASREPRoast.py** - AS-REP roasting attacks (`https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetNPUsers.py`)
- [ ] **Kerbrute** - Brute-force Kerberos authentication (`https://github.com/ropnop/kerbrute`)

## Persistence Tools
- [ ] **Evil-WinRM** - Windows Remote Management shell (`https://github.com/Hackplayers/evil-winrm`)
- [ ] **PowerSharpPack** - Collection of PowerShell tools (`https://github.com/S3cur3Th1sSh1t/PowerSharpPack`)
- [ ] **Empire** - Post-exploitation framework (`https://github.com/BC-SECURITY/Empire`)
- [ ] **Koadic** - Command & control post-exploitation (`https://github.com/zerosum0x0/koadic`)

Use responsibly. Unauthorized access is illegal.
