# Executive Summary

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
