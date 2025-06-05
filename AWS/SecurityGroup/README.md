# AWS Security Group Resources

## Overview
This directory contains resources for understanding and securing AWS Security Groups, including an attack tree, a pentesting guide, and supporting documentation. These materials are designed to help security teams identify vulnerabilities and implement best practices.

### What is an AWS Security Group?
An AWS Security Group is a virtual firewall that controls inbound and outbound traffic for AWS resources (e.g., EC2 instances, RDS) within a Virtual Private Cloud (VPC). Key features:
- Defines allowed ports, protocols, and IP ranges (e.g., 0.0.0.0/0 for all IPs).
- Default behavior: All outbound traffic is allowed, all inbound traffic is denied unless explicitly permitted.
- Common misconfigurations, such as permissive rules (e.g., open port 22) or exposed credentials, can lead to vulnerabilities.

## Contents
- **`AttackTree/`**:
  - `aws_security_group_attack_tree.md`: Attack tree in Markdown with a Mermaid diagram.

## How to Pentest AWS Security Groups
Pentesting simulates an attacker’s approach to identify and exploit Security Group weaknesses. Always obtain authorization from the AWS account owner and notify AWS if required.

### Steps
1. **Authorization**:
   - Get written permission and submit a [Vulnerability/Penetration Testing Request](https://aws.amazon.com/security/penetration-testing/) to AWS.
2. **Reconnaissance**:
   - Use Shodan, Nmap, or AWS CLI to scan for exposed endpoints.
   - Goal: Map the network and detect open ports.
3. **Identify Misconfigurations**:
   - Audit with AWS Config or Prowler for permissive rules (e.g., 0.0.0.0/0 on port 22).
   - Goal: Pinpoint vulnerabilities.
4. **Exploit Access**:
   - Test open ports (e.g., SSH on 22) with Metasploit or Hydra.
   - Goal: Gain initial access.
5. **Escalate Privileges** (if needed):
   - Exploit instance metadata (`http://169.254.169.254/latest/meta-data/iam/security-credentials/`) for IAM credentials.
   - Goal: Elevate privileges.
6. **Persist**:
   - Modify Security Groups to allow persistent access.
   - Goal: Maintain access.
7. **Evade Detection**:
   - Make subtle rule changes or disable CloudTrail logging.
   - Goal: Avoid alerts.
8. **Exfiltrate or Maintain**:
   - Extract data or set up a backdoor (e.g., reverse shell).
   - Goal: Achieve the attacker’s objective.

### Best Practices
- Limit testing to authorized resources.
- Enable CloudTrail and VPC Flow Logs for monitoring.
- Clean up after testing (e.g., remove new rules).

## Usage
1. **Understand Security Groups**: Review the overview above to grasp their role and risks.
2. **Explore the Attack Tree**:
   - Navigate to `AttackTree/aws_security_group_attack_tree.md` to view the Mermaid diagram on GitHub.
   - Use `AttackTree/aws_security_group_attack_tree.png` for a static version.
3. **Test Configurations**: Follow the pentesting guide to identify weaknesses in your Security Groups.
4. **Secure Your Environment**: Implement mitigation strategies (see `Mitigation/` when available).

## Disclaimer
These resources are for **educational and defensive purposes only** Provided By DefHawk. Do not use this information for malicious purposes. Misuse may violate AWS terms of service or applicable laws.

## References
- AWS Security Groups: [AWS VPC Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
- Pentesting Tools: See `AttackTree/references/tools.md`

*Last updated: June 5, 2025*
