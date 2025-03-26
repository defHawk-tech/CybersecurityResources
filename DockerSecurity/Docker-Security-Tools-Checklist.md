Docker Security Tools Checklist
This checklist covers essential tools for Docker security, including container enumeration, vulnerability scanning, runtime security, privilege escalation, and escape techniques.

1. Enumeration & Information Gathering

docker-bench-security - CIS security benchmark for Docker

docker run --rm --net host --pid host --userns host --cap-add audit_control \
-v /etc:/etc:ro -v /usr/bin/docker-containerd:/usr/bin/docker-containerd:ro \
-v /lib/systemd:/lib/systemd:ro -v /sys:/sys:ro -v /var/lib:/var/lib:ro \
docker/docker-bench-security

Dive - Analyze Docker image layers and detect vulnerabilities

docker run --rm -it wagoodman/dive <image_name>

Dockle - Dockerfile linting for security best practices

docker run --rm -v /var/run/docker.sock:/var/run/docker.sock goodwithtech/dockle <image_name>

2. Vulnerability Scanning

Trivy – A simple and comprehensive vulnerability scanner for Docker containers.

docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy <image_name>

Grype - Vulnerability scanner for container images and filesystems

docker run --rm anchore/grype <image_name>

Clair - Static vulnerability analysis for container images

docker run --rm quay.io/coreos/clair

3. Runtime Security & Monitoring

Falco – Container runtime security and anomaly detection.

docker run --rm -it --privileged falcosecurity/falco

Sysdig - Container runtime analysis and security monitoring

docker run --rm --name=sysdig --privileged -v /var/run/docker.sock:/host/var/run/docker.sock \
-v /dev:/host/dev -v /proc:/host/proc -v /boot:/host/boot -v /lib/modules:/host/lib/modules \
sysdig/sysdig

Snyk - Scan running containers for security vulnerabilities

docker run --rm snyk/snyk-cli container test <image_name>

4. Privilege Escalation & Escape Testing

docker run --rm -it --privileged -v /sys/fs/cgroup:/sys/fs/cgroup my-custom-escape-test

Breakout.py - Test for Docker breakout vulnerabilities

docker run --rm -it --privileged pentestlab/docker-escape

Container Escape Exploits - Prebuilt escape vectors for testing

docker run --rm -it --privileged -v /:/host ubuntu chroot /host

DEEPCE – Docker enumeration, privilege escalation, and container escapes.

docker run --rm -it --privileged qsecure/deepce

5. Malware Analysis & Forensics

Docker Forensic Toolkit - Collect forensic data from compromised containers

docker run --rm -v /var/lib/docker:/var/lib/docker:ro docker-forensics

Volatility for Containers - Memory forensics for Docker containers

docker run --rm -it --privileged volatility

Falco Malware Detection - Detect malicious activity inside containers

docker run --rm falcosecurity/falco

Compliance & Hardening

Docker Bench for Security – Security benchmark compliance tool.

docker run --rm -v /etc:/etc:ro -v /var/lib:/var/lib:ro docker/docker-bench-security

docker run --rm -v /etc:/etc:ro -v /var/lib:/var/lib:ro open-scap/scap-security-guide

Kube-bench - CIS Kubernetes and Docker security benchmark

docker run --rm --net host aquasec/kube-bench

Lynis – Security auditing and compliance testing (HIPAA, ISO27001, PCI DSS).

docker run --rm -it cisofy/lynis audit system

OPA (Open Policy Agent) – Unified policy enforcement.

docker run --rm openpolicyagent/opa

Advanced Pentesting & Red Team Tools

BOtB – Container analysis and exploitation.

docker run --rm -it pentestlab/botb

Gorsair – Discover and attack exposed Docker APIs.

docker run --rm -it gorsair/gorsair

Cloud Container Attack Tool (CCAT) – Tests security of containerized environments.

docker run --rm -it rhisby/ccat


Container Runtime Security & Sandboxing

gVisor – Sandboxed container runtime for high security.
Kata Containers – Secure lightweight virtual machines for isolation.
Sysbox – Enables Docker containers to act as isolated virtual servers.
Firecracker – MicroVM-based secure runtime for container workloads.

Container Scanning Tools

Harbor – Trusted container registry with built-in security scanning.
Anchore Engine – Vulnerability scanning for CI/CD pipelines.
OPA-Docker-Authz – Authorization policy enforcement for Docker.










