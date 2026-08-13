Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

Exact historical timestamps, alert counts, event IDs, session IDs, rule
levels, decoder names and raw JSON are intentionally not fabricated.
Where real dashboard evidence is unavailable, the wording identifies the
material as reconstructed.

# Task 3.1 — Monitoring Coverage Confirmation

## Objective

Confirm that the Ubuntu Wazuh agent and the relevant telemetry sources are
available before investigating the Week 2 attack simulations.

## Monitoring coverage

| Area | Endpoint | Telemetry used for Week 3 |
|---|---|---|
| Wazuh endpoint monitoring | Ubuntu agent | Wazuh agent events |
| Web application | Ubuntu / DVWA | Apache access-log telemetry |
| Authentication | Ubuntu | Linux authentication / SSHD logs |
| Endpoint execution | Ubuntu | auditd syscall telemetry |
| Central analysis | Arch host | Wazuh manager/dashboard |

## Detection coverage established from the documented rule notes

Web application:
- 31103 — web request containing SQLi/XSS/command-injection signatures.
- 31106 — potential web attack payload with successful HTTP 200 response.
- 31103–31120 — documented OS-command/RCE request-log coverage.

Linux authentication and endpoint:
- 5710 — multiple SSH authentication failures.
- 5763 — SSHD brute-force detection.
- 5716 — successful SSH login.
- 5720 — invalid/non-existent username.
- 5402 — successful sudo command.
- 5403 — sudo authentication failure.
- 5301 — root shell through su.
- 80792 — privileged command execution tracked through auditd/euid=0.

## Evidence placement

Required real dashboard evidence should show the Ubuntu agent as Active,
recent event activity, timestamp and source information.

Suggested screenshot:
`week3-monitoring-coverage.png`
