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
   
   