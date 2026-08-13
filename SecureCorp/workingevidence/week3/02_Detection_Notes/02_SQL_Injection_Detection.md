Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

# Detection Note 2 — SQL Injection

**Attacker:** neil-kali-2026Q35 — 192.168.110.16  
**Target:** neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138

## Detection methodology

Primary telemetry: Apache/Nginx access-log line.

Documented Wazuh rules:
- **31103** — web request contains standard SQL injection signatures.
- **31106** — potential web attack payload resulting in HTTP 200 OK.

## Investigation procedure

1. Filter Wazuh to the Ubuntu target.
2. Examine web-server access-log telemetry.
3. Identify the request associated with the Kali source address.
4. Review rule 31103 for the SQL injection signature.
5. Correlate with 31106 where the request produced a successful HTTP 200 response.
6. Compare source, endpoint, request path/payload and response information.

## Finding

The detection methodology is Wazuh web-log rule detection followed by
correlation of the request and HTTP response. Manual review is a validation
step, not the primary detection mechanism.

## Evidence

transcript:
`03_Wazuh_Investigation_Transcripts/W3-02_SQL_Injection.txt`

Required dashboard evidence:
`week3-sqli-detection.png`
