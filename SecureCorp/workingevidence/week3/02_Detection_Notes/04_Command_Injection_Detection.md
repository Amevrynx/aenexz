Established lab:
Wazuh manager: Arch Linux host — 192.168.1.8
Ubuntu DVWA/Wazuh agent: neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138
Kali attacker: neil-kali-2026Q35 — 192.168.110.16

# Detection Note 4 — Command Injection / RCE

**Attacker:** neil-kali-2026Q35 — 192.168.110.16  
**Target:** neil-Standardpc-Q35-ICH9-2009 — 192.168.112.138

## Detection methodology

Two telemetry layers are correlated:

1. Apache/Nginx access-log telemetry.
2. Linux auditd endpoint telemetry.

Documented Wazuh rules:
- **31103** — web request contains command-injection signatures.
- **31108** — documented command-injection/RCE detection mapping.
- **80792** — privileged command execution tracked through auditd/euid=0.

## Investigation procedure

1. Identify the suspicious DVWA/web request from the Kali source.
2. Review the corresponding Wazuh web alert.
3. Correlate request timing/source with endpoint telemetry.
4. Examine auditd execution evidence, including execve-type activity where present.
5. Determine whether the request resulted in operating-system command execution.
6. If privileged execution is present, correlate it with rule 80792.

## Finding

This investigation demonstrates web-to-endpoint correlation: a malicious
web request is followed by endpoint execution telemetry. The presence of
80792 must be supported by the underlying event evidence; it is not assumed
to have fired merely because the rule exists.

## Evidence

Reconstructed transcript:
`03_Wazuh_Investigation_Transcripts/W3-04_Command_Injection.txt`

Required dashboard evidence:
`week3-command-injection-detection.png`
