## Docker Image Security -- Scan Docker Images

We will use tools like Trivy to scan our Docker images for vulnerabilities before pushing them to the registry. This helps in identifying and mitigating security risks early in the CI/CD pipeline.

- Docker images consist of an underlying OS, runtime, dependencies
- Images rely on base images
- Tools and packages installed in the image

- **This means** we can have a secure application, but still an insecure runtime environment, which hackers can exploit

### Trivy Security Scanning Tool

Trivy can scan files inside container images for:
- Vulnerabilities in the OS, runtime, and application dependencies (CVEs)
- Exposed Secrets
- Misconfigurations, useful for only if your image includes IaC files
- Licenses

(Trivy utilizes a database containing vulnerabilities information. It downloads the database every 6 hours and is cached and updated as needed)

## Fixing Security Issues is not a zero-sum game

- Sometimes when you upgrade to a newer version to fix a known vulnerability in a previous version, you introduce other, newer vulnerabilities
- Some libraries may have not fixed the issue yet
- It's hard to get to zero vulnerabilities, but the goal is to get to the closest secure state possible

## Docker Security Best Practices

1. Use Official Base Images as Base Image
2. Use Specific Image Versions
3. Use Small Sized Official Images
4. Use .dockerignore to explicitly exclude unneeded files and folders
5. Make use of Multi-Stage Builds:
   1. `From` instruction starts a new build stage, leaving everything you don't want in the final image behind
   2. Selectively copy only the necessary artifacts from previous stages using the `COPY --from=<stage>` instruction
   3. Only the last Dockerfile commands are the image layers
   4. Reduces security attack surfaces
6. Use the Least Priviliged User
   1. **Bad Practice:**
      1. Using root or user with high privilige
      2. Easier privilege escalation for an attacker
   2. **Best Practice:**
      1. Create a dedicated user and group
      2. Set required permissions
      3. Change to non-root user
   3. ```dockerfile
      # Create a dedicated user and group
      RUN groupadd -r tom && useradd -r -g tom tom
      # Set required permissions
      RUN chown -R tom:tom /app
      # Change to non-root user
      USER tom
      CMD ["your-command-here"]
   ```

## Continuously Scan Images in Container Registry

- Cloud providers often offer built-in security scanning for container images stored in their registries.
- These scans can automatically detect vulnerabilities and misconfigurations, providing alerts and recommendations for remediation.