# Week 2 Finding — SQL Injection

**Attacker:** `neil-kali-2026Q35` (`192.168.110.16`)  
**Target:** `neil-Standardpc-Q35-ICH9-2009` (`192.168.112.138`)  
**Application:** DVWA

## Objective
Determine whether attacker-controlled input in the SQL Injection module
is incorporated into the backend query without adequate parameterisation.

## Method
A baseline lookup using `id=1` was compared with a boolean-manipulation
payload. The response was inspected for records returned by the vulnerable
application.

## Result
The manipulated input returned multiple user records, demonstrating that
the input altered the logic of the backend query.

## Security significance
SQL injection can permit unauthorised data access or manipulation when
present in production applications. Parameterised queries/prepared
statements and server-side input validation are the primary remediation
controls.

## Evidence
See `W2-02_SQL_Injection.txt`.
