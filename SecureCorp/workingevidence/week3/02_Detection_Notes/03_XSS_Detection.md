Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

# Detection Note 3 — Cross-Site Scripting

**Attacker:** neil-kali-2026Q35 — 192.168.110.16  
**Target:** neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138

## Detection methodology

Primary telemetry: Apache/Nginx access-log line.

Documented Wazuh rules:
- **31103** — web request contains XSS/script-injection signatures.
- **31106** — potential web attack payload resulting in HTTP 200 OK.

## Investigation procedure

1. Filter Wazuh to the Ubuntu target.
2. Review web-server access-log events.
3. Identify requests from the Kali source.
4. Examine rule 31103 for the script-injection signature.
5. Correlate with 31106 when the application returned HTTP 200.
6. Validate the source, endpoint, request and response relationship.

## Finding

The primary detection is Wazuh web-log rule processing. Manual inspection
is used to validate the alert and establish context.

## Evidence

transcript:
`03_Wazuh_Investigation_Transcripts/W3-03_XSS.txt`

Required dashboard evidence:
`week3-xss-detection.png`
