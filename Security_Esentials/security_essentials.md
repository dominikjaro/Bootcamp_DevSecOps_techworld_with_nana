## What needs to be secured?

**Any touchpoint** is a security level that needs to be secured. This includes: Offline and Online touchpoints.

## Types for Security Attacks

1. **Phishing Attack:** Tricking human, instead of a system. Can be through email, phone calls, or social media. The attacker pretends to be a trusted entity to steal sensitive information. (online ad clicks, fake websites, etc.) -- Sensitive company data is at risk.
2. **XSS - Cross Site Scripting:** When the application has security holes. (e.g. the Frontend code allows injection of malicious scripts). -- Sensitive company data is at risk.
3. **CSRF - Cross Site Request Forgery:** When the application has security holes. (e.g. the Frontend code allows injection of malicious scripts). The attacker is stealing an identity first. The attacker could access sensitive data, in cookies or session tokens, and even manipulate the content of the website. This mainly can happen when:
   1. Weak authentication is used (e.g. no 2FA, weak passwords, etc.)
   2. Does not reject external code
   3. Does not properly validate user input
4. **SSRF - Server Side Request Forgery:** SSR Payloads are sent to the server. The attacker manupulates the server to send requests to internal resources.
5. **SQL Injection:** Attacker manipulates or injects malicious SQL code into a database query to do something.
6. **Security Vulnerabilities in Third Party Libraries:** Using third-party libraries can introduce vulnerabilities if they are not properly vetted or updated. Attackers can exploit known vulnerabilities in these libraries to gain unauthorized access or execute malicious code.
   1. **CVE(Common Vulnerabilities and Exposures):** is a list of publicly disclosed cybersecurity vulnerabilities and exposures. It provides a reference-method for publicly known information-security vulnerabilities and exposures.
7. **Brute Force Attack:** e.g. weak passwords, no 2FA, etc.
8. **DoS - Denial of Service Attack:** An attack that aims to make a machine or network resource unavailable to its intended users by overwhelming it with a flood of illegitimate requests.

## OWASP (open web application security project)
OWASP is a nonprofit foundation that works to improve the security of software. It provides free and open resources, including documentation, tools, and community support, to help organizations and developers build secure applications.

### OWASP Top 10
The OWASP Top 10 is a list of the most critical security risks to web applications.

1. **Broken Access Control:** 
   - Vulnabilities in the app to properly control user's permission (e.g. By-passing authorization safeguards, become priviliged users)
   - Phishing attacks
   - Session Hijacking (CSRF)
   - Bypassing access control checks by modifying the URL
2. **Cryptographic Failures:**
   - Lack or weak encryption cryptography
   - Hard-coded credentials
   - Using insecure protocols (e.g. HTTP instead of HTTPS)
- Determin protection needs of **data in transit** and **data at rest**.
  
3. **Injection:**
   - Always validate and sanitize user input
   - Avoid creating templates from user input
   - Expect malicious input by default
4. **Insecure Design:**
   - Threat Modeling: process used to identify, assess and mitigate potential threats in a system or application
   - Secure Design Patterns
   - Reference architectures

5. **Security Misconfiguration:**
   - Unnecessary features enabled (e.g. ports, services, pages, accounts, privileges)...

6. **Vulnerable and Outdated Components:**
   - Using components with known vulnerabilities
   - Not updating components regularly
   - Not monitoring for new vulnerabilities in used components

7. **Identification and Authentication Failures:**
   - **Identification:** identifying a particular user (often through a username or email)
   - **Authentication:** process of validating that a user is who they claim to be (proof of identity, often through a password, token, or biometric data)
   - **Authorization:** process of determining what an authenticated user is allowed to do (permissions, roles, access control)
   - User session or authentication tokens are not properly validated
     (session ID needs ot be invalidated after logout)

8. **Software and Data Integrity Failures:**
   - Code and infrastructure that does not protect against integrity violations
   - Untrusted software updates and CI/CD pipelines
   - Insecure deserialization
   - Using vulnerable components vs **source** of component (e.g. Component: Plugin, Source of component: Repository, Registry, etc.)

9. **Security Logging and Monitoring Failures:**
   - **Logging:** recording security-relevant events (e.g. failed login attempts, access control violations, etc.)
   - **Monitoring:** analyzing logs and other data to detect and respond to security incidents
   - Without logs, you can't do monitoring efficiently
   - Without monitoring, you can't alert and respond to incidents efficiently

10. **Server-Side Request Forgery (SSRF):**
   - SSRF is a vulnerability that allows an attacker to induce the server-side application to make HTTP requests to an arbitrary domain of the attacker's choosing. This can lead to unauthorized access to internal systems.
   - SSRF attacks circumvent firewall, VPN or network access control lists
     - Port scan internal servers (e.g. for an open port and HTTP request with SSRF payload - which can be used to access internal resources)
   - Or Access Metadata storage in a cloud provider


## Security is Layered

Each layer addresses different aspects of security, and together they provide a comprehensive defense against potential threats.
Access Management, Network Security, Application Security, Data Security, Endpoint Security, Physical Security, and Security Awareness Training are all important layers in a security strategy.
- Data
- App
- Host
- Network
- Physical
- Policy and Procedures

**In DevSecOps:** we automate security testing, vulnerability scanning, code analysis, compliance checks, ...
It gives you visibility of the security posture of your application, infrastructure, system.