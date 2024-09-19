
# Docker Hardening 

## Overview

The following steps will help you harden Docker by addressing both Docker host and container security.

## Hardening Techniques

### 1. Use the Latest Docker Version
- **Step 1:** Regularly update Docker to the latest version to benefit from security patches and 
improvements.
  ```bash
  sudo apt-get update
  sudo apt-get install docker-ce
  ```

### 2. Minimize Docker Daemon Privileges

-   **Step 1:** Run Docker daemon with the least privileges required.

### 3. Use Docker’s User Namespaces

-   **Step 1:** Enable user namespaces in Docker to isolate container users from host users.
    
    
    ```
    sudo dockerd --userns-remap=default
    ``` 
    

### 4. Avoid Running Containers as Root

-   **Step 1:** Set the user in Dockerfile or use `--user` flag to avoid running containers as root.
    
    
    ```
    USER nonrootuser
    ``` 
    

### 5. Limit Container Capabilities

-   **Step 1:** Drop unnecessary capabilities from containers using `--cap-drop`.
    
    
    ```
    docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE myimage
    ``` 
    

### 6. Use Read-Only Filesystems

-   **Step 1:** Run containers with a read-only filesystem using `--read-only`.
    
    
    ```
    docker run --read-only myimage
    ``` 
    

### 7. Apply Security Updates to Images

-   **Step 1:** Regularly update and patch base images used in Dockerfiles.
    
    
    ```
    docker pull baseimage:latest
    ``` 
    

### 8. Scan Images for Vulnerabilities

-   **Step 1:** Use tools like `docker scan` or third-party services to scan images for vulnerabilities.
    
    
    ```
    docker scan myimage
    ``` 
    

### 9. Limit Docker API Exposure

-   **Step 1:** Configure Docker to listen only on specific IP addresses or Unix sockets.
    
    
    ```
    sudo dockerd -H tcp://127.0.0.1:2376 -H unix:///var/run/docker.sock
    ``` 
    

### 10. Secure Docker Daemon Socket

-   **Step 1:** Restrict access to Docker’s Unix socket.
    
    
    ```
    sudo chmod 660 /var/run/docker.sock
    sudo chown root:docker /var/run/docker.sock
    ``` 
    

### 11. Use Trusted Registries

-   **Step 1:** Configure Docker to use trusted image registries and avoid using public registries for 
sensitive applications.

### 12. Implement Container Network Segmentation

-   **Step 1:** Use Docker networks to isolate containers and limit communication between them.
    
    ```
    docker network create mynetwork
    docker run --network=mynetwork myimage
    ``` 
    

### 13. Configure Docker Logs

-   **Step 1:** Set up logging drivers to manage container logs effectively.
    
    
    ```
    docker run --log-driver=json-file myimage
    ``` 
    

### 14. Enable Docker Content Trust

-   **Step 1:** Use Docker Content Trust to ensure the authenticity and integrity of images.
    
    
    ```
    export DOCKER_CONTENT_TRUST=1
    ``` 
    

### 15. Use Multi-Stage Builds

-   **Step 1:** Use multi-stage builds in Dockerfiles to reduce image size and surface area for 
vulnerabilities.
    
    
    ```
    FROM golang:alpine AS builder
    WORKDIR /app
    COPY . .
    RUN go build -o myapp
    
    FROM alpine
    COPY --from=builder /app/myapp /app/myapp
    ``` 
    

### 16. Set Resource Limits

-   **Step 1:** Define resource limits for containers to prevent resource abuse.
    
    
    ```
    docker run --memory="512m" --cpus="1" myimage
    ``` 
    

### 17. Avoid Using `latest` Tag for Images

-   **Step 1:** Use specific image tags instead of `latest` to avoid unexpected updates.
    
    
    ```
    docker pull myimage:1.0.0
    ``` 
    

### 18. Use Docker Bench for Security

-   **Step 1:** Run Docker Bench for Security to assess Docker host and container security.
    
    
    ```
    docker run -it --net host --pid host --cap-add audit_control \
      --label docker_bench_security \
      docker/docker-bench-security
      ``` 
    

### 19. Secure Docker Storage

-   **Step 1:** Configure Docker volumes with appropriate permissions and encryption if necessary.

### 20. Regularly Rotate Docker Secrets

-   **Step 1:** Rotate and manage secrets used by Docker containers regularly.
    
    
    ```
    docker secret create mysecret mysecretfile
    ``` 
    

### 21. Use Static Analysis Tools

-   **Step 1:** Analyze Dockerfiles and images for security issues using static analysis tools.
    
    
    ```
    hadolint Dockerfile
    ``` 
    

### 22. Restrict Docker Network Access

-   **Step 1:** Use firewall rules and Docker network settings to restrict network access to the Docker 
daemon.

### 23. Use Private Docker Registries

-   **Step 1:** Configure Docker to pull images from private registries with secure credentials.

### 24. Isolate Docker Daemon

-   **Step 1:** Run Docker daemon in a separate environment or VM to isolate it from other services.

### 25. Enable Docker Swarm Security Features

-   **Step 1:** Use Docker Swarm’s built-in security features for cluster management, such as encrypted 
communication.

### 26. Avoid Unnecessary Exposed Ports

-   **Step 1:** Minimize the number of exposed ports by configuring Docker containers appropriately.
    
    
    ```
    docker run -p 8080:80 myimage
    ``` 
    

### 27. Use `docker-compose` Security Best Practices

-   **Step 1:** Follow best practices for securing Docker Compose files, such as using environment 
variables for secrets.

### 28. Regularly Review Docker Security Best Practices

-   **Step 1:** Stay updated with Docker’s security best practices and guidelines.

### 29. Implement Two-Factor Authentication (2FA)

-   **Step 1:** Enable 2FA for Docker Hub and any other Docker-related services that support it.

### 30. Secure Docker Swarm Secrets

-   **Step 1:** Use Docker Swarm secrets to securely manage sensitive data.
    
    
    ```
    docker secret create mysecret mysecretfile
    ``` 
    

### 31. Harden Docker Host Operating System

-   **Step 1:** Apply security hardening practices to the host operating system where Docker is running.

### 32. Use Secure Docker Plugins

-   **Step 1:** Only use plugins from trusted sources and verify their security.

### 33. Limit Docker Container Interactions

-   **Step 1:** Restrict interactions between containers using network policies and firewall rules.

### 34. Use Docker Scan for Vulnerability Management

-   **Step 1:** Use Docker’s built-in vulnerability scanning tool to scan images.
    
    
    ```
    docker scan myimage
    ``` 
    

### 35. Avoid Storing Sensitive Data in Containers

-   **Step 1:** Avoid storing sensitive information directly in Docker containers or images.

### 36. Use Immutable Containers

-   **Step 1:** Design containers to be immutable to avoid changes during runtime.

### 37. Implement Regular Docker Image Builds

-   **Step 1:** Regularly rebuild Docker images to incorporate the latest security patches and updates.

### 38. Secure Docker Daemon Configuration

-   **Step 1:** Secure the Docker daemon configuration file (`/etc/docker/daemon.json`) with appropriate 
permissions.

### 39. Implement Security Scanning Tools

-   **Step 1:** Use security scanning tools like Trivy, Clair, or Anchore to assess container images.

### 40. Use Docker Content Trust (DCT)

-   **Step 1:** Enable Docker Content Trust to ensure image integrity and authenticity.
    
    
    ```
    export DOCKER_CONTENT_TRUST=1
    ``` 
    

### 41. Regularly Review Container Logs

-   **Step 1:** Monitor and review container logs for unusual activity or security incidents.

### 42. Use Docker Health Checks

-   **Step 1:** Implement Docker health checks to ensure containers are running correctly and securely.
    
    
    ```
    HEALTHCHECK CMD curl --fail http://localhost/ || exit 1
    ``` 
    

### 43. Configure Docker Security Options

-   **Step 1:** Configure Docker security options such as seccomp profiles and AppArmor.
    
    
    ```
    docker run --security-opt seccomp:unconfined myimage
    ``` 
    

### 44. Implement Docker Rate Limiting

-   **Step 1:** Use rate limiting for Docker API requests to prevent abuse.

### 45. Secure Docker Swarm Communications

-   **Step 1:** Ensure that Docker Swarm communications are encrypted and secured.

### 46. Use Docker’s Built-In Security Features

-   **Step 1:** Leverage Docker’s built-in security features such as security profiles and encrypted 
storage.

### 47. Apply Container Hardening Techniques

-   **Step 1:** Apply hardening techniques to individual containers, such as reducing attack surface area.

### 48. Limit Use of Privileged Containers

-   **Step 1:** Avoid running containers with the `--privileged` flag unless absolutely necessary.

### 49. Implement Docker Network Security Best Practices

-   **Step 1:** Secure Docker networks by using network policies and isolation techniques.

### 50. Regularly Audit Docker Environment

-   **Step 1:** Perform regular security audits of the Docker environment to identify and address 
potential issues.
