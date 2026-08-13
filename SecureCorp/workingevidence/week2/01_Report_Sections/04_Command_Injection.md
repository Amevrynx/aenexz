# Week 2 Finding — Command Injection

**Attacker:** `neil-kali-2026Q35` (`192.168.110.16`)  
**Target:** `neil-Standardpc-Q35-ICH9-2009` (`192.168.112.138`)  
**Application:** DVWA

## Objective
Determine whether shell metacharacters allow attacker-controlled commands
to execute on the Ubuntu host through the vulnerable DVWA function.

## Method
A normal ping request was established first. A semicolon was then used to
append `id`, followed by `whoami` and `pwd`, to determine whether arbitrary
commands executed and which account/context executed them.

## Result
The response included command output showing execution in the
`www-data` context and returned the vulnerable application's working
directory.

## Security significance
Command injection can provide direct operating-system command execution
through a web application and can become a path to further compromise.
The correct remediation is to avoid shell invocation where possible and
use strict allow-list validation when system commands are genuinely
required.

## Evidence
See `W2-04_Command_Injection.txt`.
