# Week 2 Finding — Cross-Site Scripting

**Attacker:** `neil-kali-2026Q35` (`192.168.110.16`)  
**Target:** `neil-Standardpc-Q35-ICH9-2009` (`192.168.112.138`)  
**Application:** DVWA

## Objective
Test whether attacker-controlled markup/script is returned to the browser
without appropriate output encoding.

## Method
A harmless JavaScript alert payload was submitted to the vulnerable XSS
function. The HTTP response was checked for the unencoded script and the
browser behaviour was observed.

## Result
The payload was reflected/executed in the vulnerable application context.

## Security significance
Successful XSS demonstrates that untrusted data can cross the
application-to-browser trust boundary as executable content. Contextual
output encoding, input handling, and appropriate browser security
controls reduce this risk.

## Evidence
See `W2-03_XSS.txt`.
