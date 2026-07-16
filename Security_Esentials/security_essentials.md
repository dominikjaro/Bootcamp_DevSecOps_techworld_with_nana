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