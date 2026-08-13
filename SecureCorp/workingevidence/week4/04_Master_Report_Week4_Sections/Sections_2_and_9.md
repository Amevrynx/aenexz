# Week 4 Master Report Sections

## 2. Executive Summary


## SecureCorp Security Assessment

SecureCorp's four-week assessment examined the security of a customer-facing
web environment through controlled testing, centralized monitoring and
remediation planning. The assessment used a self-contained laboratory in
which Kali Linux represented the authorized attacker, Ubuntu hosted the DVWA
target and related services, and an Arch Linux host provided centralized
Wazuh management.

The assessment demonstrated that weaknesses in a deliberately vulnerable web
application can create meaningful business risk when unsafe input reaches
database queries, browser output or operating-system commands. The four
controlled attack scenarios covered brute-force authentication, SQL injection,
cross-site scripting and command injection. Week 3 then examined the
corresponding activity through Wazuh and Linux/web telemetry.

The most serious technical concern is command injection because successful
exploitation can move beyond the web application and result in operating-system
command execution. SQL injection presents a high confidentiality and
integrity risk because attacker-controlled input can reach database queries.
XSS can affect users who interact with vulnerable application content.
Brute-force activity demonstrates the importance of strong authentication,
rate limiting and MFA.

The assessment also established a useful monitoring capability. Wazuh
centralized authentication, web-request and endpoint telemetry, while Linux
auditd provided additional visibility into privileged execution. Documented
Wazuh mappings included 31103/31106 for web attack patterns, 31103/31108 and
auditd/80792 for command-injection investigation, and 5710/5763 for SSH
brute-force detection.

The recommended remediation priority is to address command execution and web
input handling first, followed by authentication hardening and continued
centralized monitoring. SecureCorp should use parameterized database queries,
strict server-side validation, context-aware output encoding, safe APIs
instead of shell execution, strong authentication controls, MFA for sensitive
access, least privilege and reliable logging.

These measures reduce the likelihood that an application-layer weakness can
be converted into unauthorized data access, account compromise or server
compromise. Management should treat the findings as a prioritized improvement
plan rather than as isolated technical issues: application security,
identity security, endpoint monitoring and recovery controls need to work
together.


## 9. Recommendations


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
