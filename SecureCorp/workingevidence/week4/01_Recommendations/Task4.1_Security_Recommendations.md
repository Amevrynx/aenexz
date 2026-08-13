# Task 4.1 — Security Recommendations

The handbook requires practical, prioritized improvements tied to findings from
Weeks 2 and 3. The following table uses the documented attack simulations and
Wazuh detection methodology.

| Area | Current State | Finding / Risk Link | Recommendation | Priority |
|---|---|---|---|---|
| Web input handling | DVWA demonstrated SQL injection exposure at low security | SQLi — Wazuh 31103/31106 | Use parameterized queries, strict server-side validation, least-privilege DB accounts and safe error handling. | Critical |
| Output encoding | DVWA demonstrated XSS exposure | XSS — Wazuh 31103/31106 | Apply context-aware output encoding, input validation and an appropriate Content Security Policy. | High |
| OS command execution | DVWA command-injection path can pass attacker-controlled input toward the OS | Command injection/RCE — 31103/31108; auditd/80792 correlation | Avoid shell execution where possible. Where unavoidable, use safe APIs, strict allowlists, validation and a least-privilege service account. | Critical |
| Authentication | Repeated SSH authentication failures were detectable through Wazuh | Brute force — 5710/5763 | Enforce strong unique passwords, rate limiting, lockout/anti-automation controls and MFA for sensitive access. | High |
| Privileged access | Linux telemetry includes sudo/su/auditd monitoring | 5402, 5403, 5301, 80792 | Minimize administrative privileges, review sudoers/su access and retain privileged-command auditing. | High |
| Logging & monitoring | Wazuh centralizes authentication, web and endpoint telemetry | Week 3 detection workflow | Maintain Wazuh coverage, retain sufficient logs, tune alerts and periodically test detection of known attack patterns. | High |
| Patch management | Ubuntu web server is a critical service platform | Server compromise risk | Maintain OS, Apache, PHP, MariaDB and application components at supported security-patched versions. | High |
| Network exposure | Customer-facing services increase attack surface | External exploitation risk | Expose only required services, restrict management access and segment public-facing workloads from internal systems. | High |
| Backup & recovery | Business availability depends on recoverable data/services | Compromise or disruption | Maintain protected backups and periodically test restoration procedures. | Medium–High |
| User/identity security | Employee accounts and credentials are business assets | Credential theft / phishing risk | Use MFA, regular access reviews, security awareness and phishing-resistant authentication where practical. | High |
