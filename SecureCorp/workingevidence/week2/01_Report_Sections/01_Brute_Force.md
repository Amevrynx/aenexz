# Week 2 Finding — Brute-Force Authentication

**Attacker:** `neil-kali-2026Q35` (`192.168.110.16`)  
**Target:** `neil-Standardpc-Q35-ICH9-2009` (`192.168.112.138`)  
**Assessment date:** 24 June 2026

## Objective
Assess whether repeated credential attempts against the lab authentication
service can result in valid access.

## Method
The Kali VM first confirmed reachability and enumerated the exposed SSH
and HTTP services. A controlled password list was then used against the
Ubuntu SSH service. The successful credential was verified by establishing
an SSH session and checking the authenticated identity.

## Result
The simulation resulted in successful authentication as `labuser`.
Post-authentication commands confirmed the session identity and target
hostname.

## Security significance
The result demonstrates the risk of weak credentials combined with an
authentication service that is reachable from the attacker segment.
Defensive controls should include strong credential policy, rate
limiting/lockout, monitoring of failed authentication, and alerting on
repeated attempts.

## Evidence
See `W2-01_Brute_Force.txt`.
