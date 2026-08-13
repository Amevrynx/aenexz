Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

# Week 3 Incident Report — Defensive Investigation

## 1. Scope

Week 3 investigates the same four controlled attacks simulated in Week 2:
SSH brute force, SQL injection, XSS and command injection/RCE.

## 2. Infrastructure

| Role | Host | IP |
|---|---|---|
| Wazuh manager | Arch Linux host | 192.168.1.8 |
| DVWA target / Wazuh agent | neil-Standardpc-Q35-ICH9-2009 | 192.168.112.138 |
| Attacker | neil-kali-2026Q35 | 192.168.110.16 |

## 3. Detection methodology

### SSH brute force
Linux authentication telemetry is processed by Wazuh. Rules 5710 and 5763
provide the documented brute-force detection path. Rules 5720 and 5716 can
provide surrounding authentication context when those events are present.

### SQL injection
Apache/Nginx access-log telemetry is processed by Wazuh. Rule 31103 identifies
the SQL injection signature and rule 31106 provides correlation with a
successful HTTP 200 response.

### XSS
Apache/Nginx access-log telemetry is processed by Wazuh. Rule 31103 identifies
the script-injection signature and rule 31106 correlates a successful HTTP 200
response.

### Command injection / RCE
The investigation begins with web-server telemetry through rules 31103 and
31108. It then moves to endpoint telemetry. Rule 80792 is examined when auditd
records the documented privileged execution condition.

## 4. Incident timeline

Exact historical timestamps are intentionally omitted from the timeline and should be referred from the screenshots.

| Sequence | Investigation event | Detection / evidence |
|---|---|---|
| 1 | SSH authentication failures | 5710 / 5763 |
| 2 | SQL injection request | 31103 / 31106 |
| 3 | XSS request | 31103 / 31106 |
| 4 | Command-injection request | 31103 / 31108 |
| 5 | Endpoint execution correlation | auditd / 80792 where condition is met |
| 6 | Analyst correlation and incident assessment | Wazuh dashboard + source/target context |

## 5. Findings

The investigation demonstrates centralized detection across two telemetry
layers: application/web requests and Linux endpoint/authentication activity.

The most significant correlation is command injection, where web-layer
activity can be compared with endpoint execution telemetry to determine
whether exploitation progressed beyond the application layer.

## 6. Immediate recommendations

1. Preserve relevant Wazuh, Apache and authentication telemetry.
2. Review SSH authentication controls and investigate unexpected successful
   logins after repeated failures.
3. Use parameterized SQL queries and strict input validation.
4. Apply context-aware output encoding to prevent XSS.
5. Avoid direct shell execution from web input; use allowlists and safe APIs
   where command execution is necessary.
6. Continue endpoint/auditd monitoring so web exploitation can be correlated
   with process execution.
