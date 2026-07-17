## Types of Security Tests

1. **SAST (Static Application Security Testing)**
  - Static code analysis (app is not running)
  - Identifies security vulnerabilities in app's source code, configuration files etc.
  - Look for common coding errors, deviations from secure coding practices etc.\

2. **SCA (Software Composition Analysis)**
  - Check thrird-party and open-source libraries and frameworks (dependencies of your application)
  - SCA tools go through our depebndencies -- checks if any known vulnerabilities for that dependency and specific version

3. **DAST (Dynamic Application Security Testing)**
  - Testing the app's running instance or deployed version
  - Analyzing behavior and responses in real-time (e.g. SQL Injection Requests or XSS attacks or CSRF, SSRF, etc.)
  - It does not require access to the code -- DAST tools can automate these attacks

### ? When to run which security checks ?

  - **Basic Security Checks** runs on every commit when the developer pushes code to the repository (to save time)
  - **Comprehensive, complete security checks** run once per night as nightly builds -- which can take a long time to run and can be resource intensive.
  - **Manual Testing** sometimes we need manual function tests and manual security test because some functionality test can't be automated or expensive and time consuming. -- This is called **PEN testing (penetration testing)**
  - **Logging and Monitoring** still required.


