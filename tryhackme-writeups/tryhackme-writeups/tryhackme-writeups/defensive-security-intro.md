# Defensive Security Intro

**Date:** 2026-07-22
**Difficulty:** Easy
**Category:** SOC / Incident Response / Blue Team
**Platform:** TryHackMe

## Summary
This room simulated a SOC analyst workflow using a Security Analyst Dashboard. 
The task was to investigate an active alert, identify the attacker's behavior, 
and take a containment action by blocking the malicious source IP.

## Tools Used
- Security Analyst Dashboard (SIEM-style alert triage interface)

## Methodology

### 1. Alert Triage
Reviewed the Event Management panel, which listed multiple active alerts 
with varying severity levels (High, Medium, Critical). Prioritized the 
alert flagged as most urgent for investigation.

### 2. Investigating the Alert
The alert identified was a **Web Discovery Attack**, described as automated 
directory enumeration detected on admin endpoints. The dashboard provided 
the source IP responsible for the activity: `32.122.195.63`.

This type of attack is typically an early reconnaissance step — an attacker 
scans for hidden or unlinked pages (such as admin panels) before attempting 
further exploitation, similar to the `dirb` scan performed in the 
Offensive Security Intro room.

### 3. Containment
After confirming the activity was malicious and not legitimate traffic, 
blocked the source IP (`32.122.195.63`) directly from the dashboard to 
stop further reconnaissance attempts from that address.

## Key Takeaways
- Directory enumeration against admin endpoints is a common early-stage 
  reconnaissance technique — seeing it from the attacker's side (Offensive 
  Security Intro) made it much easier to recognize from the defender's side.
- A SOC analyst's first job during triage is prioritization: with multiple 
  alerts of different severities active at once, deciding what to 
  investigate first matters as much as knowing how to investigate it.
- Blocking a source IP is a fast, immediate containment step, but it's 
  usually just the first response — a real investigation would also check 
  whether the same IP appears in other alerts or logs.

## Reflection
This room connected directly to what I learned in the Offensive Security 
Intro room — recognizing the *same* type of attack (directory enumeration) 
from the blue team side helped reinforce how the two perspectives fit 
together. I want to explore how SOC teams handle alert correlation, i.e. 
identifying whether one attacker's activity shows up across multiple 
alerts before taking action.
