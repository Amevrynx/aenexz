# Task 4.3 — Final Client Debrief

## Presentation objective

The handbook requires a 10–15 minute presentation covering SecureCorp's
security posture, key findings, evidence, recommendations and lessons
learned. A live demonstration is optional.

## Suggested delivery structure

1. **Engagement overview** — scope, authorized lab and four-week methodology.
2. **Environment** — Arch/Wazuh manager, Ubuntu/DVWA target and Kali attacker.
3. **Security posture** — why the customer portal and supporting assets matter.
4. **Week 2 findings** — brute force, SQLi, XSS and command injection.
5. **Week 3 detection** — Wazuh rules and web/authentication/auditd telemetry.
6. **Business impact** — account compromise, data disclosure, browser-side
   execution and possible server compromise.
7. **Priority remediation** — command execution and web input handling first.
8. **Monitoring and identity controls** — Wazuh, MFA, authentication controls,
   least privilege.
9. **Recovery and resilience** — backups, restoration testing and incident
   response.
10. **Lessons learned / close** — security is a lifecycle of discovery,
    testing, detection and remediation.

## Closing message

The main conclusion is not simply that DVWA contains vulnerabilities. The
assessment demonstrates why weaknesses need to be connected to business
assets, detected through telemetry and followed by practical controls.
SecureCorp's strongest next step is to reduce the ability of untrusted input
to reach sensitive application or operating-system functions while retaining
the monitoring needed to detect attempted abuse.
