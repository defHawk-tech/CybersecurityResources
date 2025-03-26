# Docker Security Cheat Sheet

## Introduction
Docker is the most popular containerization technology. When used correctly, it can enhance security compared to running applications directly on the host system. However, certain misconfigurations can reduce security levels or introduce new vulnerabilities.

The aim of this cheat sheet is to provide a straightforward list of common security errors and best practices to assist in securing your Docker containers.

## Rules

### RULE #0 - Keep Host and Docker Up to Date
- Regularly update both the host OS and Docker Engine.
- Protect against container escape vulnerabilities like "Leaky Vessels."
- Containers share the host’s kernel; a vulnerable host kernel means vulnerable containers.
- Example: Dirty COW exploit can lead to root access on a vulnerable host.

### RULE #1 - Do Not Expose the Docker Daemon Socket
- **Never expose** `/var/run/docker.sock`, as it grants root access to the host.
- Do not run the daemon with `-H tcp://0.0.0.0:XXX` unless secured.
- Avoid mounting the socket inside a container, even in read-only mode.
- Example misconfiguration in `docker-compose.yml`:
  ```yaml
  volumes:
    - "/var/run/docker.sock:/var/run/docker.sock"
  ```

### RULE #2 - Set a User
- Run containers with an unprivileged user to prevent privilege escalation.
- Options:
  - At runtime: `docker run -u 4000 alpine`
  - In `Dockerfile`:
    ```dockerfile
    FROM alpine
    RUN groupadd -r myuser && useradd -r -g myuser myuser
    USER myuser
    ```
  - Enable user namespace support: `--userns-remap=default`
  - Kubernetes equivalent:
    ```yaml
    securityContext:
      runAsUser: 4000
    ```

### RULE #3 - Limit Capabilities
- Use `--cap-drop all` and add only necessary capabilities with `--cap-add`.
- **Never use** `--privileged`.
- Example:
  ```bash
  docker run --cap-drop all --cap-add CHOWN alpine
  ```
- Kubernetes equivalent:
  ```yaml
  securityContext:
    capabilities:
      drop:
        - ALL
      add: ["CHOWN"]
  ```

### RULE #4 - Prevent In-Container Privilege Escalation
- Use `--security-opt=no-new-privileges`.
- Kubernetes equivalent:
  ```yaml
  securityContext:
    allowPrivilegeEscalation: false
  ```

### RULE #5 - Be Mindful of Inter-Container Connectivity
- Default `icc=true` allows all containers to communicate.
- Instead, create **custom networks** for controlled communication.
- Kubernetes equivalent: Use **Network Policies**.

### RULE #6 - Use Linux Security Modules (LSM)
- Do **not** disable security profiles.
- Use **Seccomp**, **AppArmor**, or **SELinux**.
- Kubernetes: Configure security context for pods.

### RULE #7 - Limit Resources
- Prevent DoS attacks by limiting:
  - **Memory**: `--memory=<limit>`
  - **CPU**: `--cpu-shares=<limit>`
  - **File descriptors**: `--ulimit nofile=<limit>`
  - **Processes**: `--ulimit nproc=<limit>`
  - **Restarts**: `--restart=on-failure:<number>`
- Kubernetes equivalent: Assign CPU & memory resources.

### RULE #8 - Set Filesystem and Volumes to Read-Only
- Run containers with `--read-only`.
- Example:
  ```bash
  docker run --read-only alpine
  ```
- Kubernetes equivalent:
  ```yaml
  securityContext:
    readOnlyRootFilesystem: true
  ```
- Mount **volumes as read-only**:
  ```bash
  docker run -v volume-name:/path/in/container:ro alpine
  ```

### RULE #9 - Integrate Container Scanning into CI/CD
- Use security linting tools:
  - Ensure `USER` is set.
  - Pin base image and package versions.
  - Prefer `COPY` over `ADD`.
  - Avoid `curl | bash` installs.
- **Free Scanning Tools**:
  - Clair, ThreatMapper, Trivy
- **Commercial Scanning Tools**:
  - Snyk, Anchore, Docker Scout
- **Secret Detection Tools**:
  - ggshield, SecretScanner
- **Kubernetes Misconfiguration Tools**:
  - kubeaudit, kube-bench
- **Docker Security Benchmark**:
  - inspec.io, dev-sec.io, Docker Bench for Security

### RULE #10 - Keep Docker Daemon Logging at 'Info' Level
- Verify log level with:
  ```bash
  ps aux | grep '[d]ockerd.*--log-level'
  ```
- Set logging to `info` to capture important events.
- Do not enable `debug` logging unless troubleshooting.

## Conclusion
By following these security best practices, you can significantly reduce the attack surface of your Docker containers. Regularly audit and monitor your containerized environment to ensure compliance with security standards.

