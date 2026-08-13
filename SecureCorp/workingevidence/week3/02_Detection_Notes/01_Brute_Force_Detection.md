Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

# Detection Note 1 — SSH Brute Force

**Attacker:** neil-kali-2026Q35 — 192.168.110.16  
**Target:** neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138  
**Manager:** Arch — 192.168.1.8

## Detection methodology

The primary telemetry is the Ubuntu Linux authentication/SSHD log.
The documented Wazuh rules for this attack are:

- **5710** — multiple SSH authentication failures from the same source IP.
- **5763** — SSHD brute-force attack detected.

Supporting authentication rules documented for investigation include:
- **5720** — invalid/non-existent username.
- **5716** — successful SSH login.

## Investigation procedure

1. Filter Wazuh to the Ubuntu agent.
2. Narrow the investigation to Linux authentication/SSHD events.
3. Identify repeated failures associated with `192.168.110.16`.
4. Correlate the failures with rules 5710/5763.
5. Review surrounding authentication events for invalid-user and successful-login
   activity where present.
6. Establish the sequence and source/target relationship.

## Finding

The documented detection path is Wazuh rule-based authentication detection,
followed by event correlation. This is not classified as a simple manual
Apache-log search.

## Evidence

transcript:
`03_Wazuh_Investigation_Transcripts/W3-01_Brute_Force.txt`

Required dashboard evidence:
`week3-bruteforce-detection.png`
