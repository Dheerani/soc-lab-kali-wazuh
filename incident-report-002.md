# SOC INCIDENT REPORT #002

## Executive Summary
- Total Alerts Analyzed: [YOUR NUMBER]
- Time Period: 2026-10-09 16:46:45 PKT
- Agent: kali (192.168.1.109)
- Critical Detections: 8 (SSH Brute Force)

## Alert Breakdown

| Rule ID | Description | Count | Level | Category |
|---------|-------------|-------|-------|----------|
| 100002 | SSH Brute Force Attack | 8 | 12 | CRITICAL |
| 5760 | sshd: authentication failed | 2 | 5 | Suspicious |

## MITRE ATT&CK Mapping
- **T1110** — Brute Force (Rule 100002)

## Key Findings
1. 8 SSH brute force attacks detected
2. Custom rule 100002 working as designed
3. Attack source: ::1 (localhost)
4. No successful unauthorized access

## Analysis
- Brute force attacks simulated from localhost
- Custom rule 100002 successfully detected
- Real SOC: block source IP, review auth.log

## Recommended Actions
1. **Immediate:** No escalation (lab activity)
2. **Real SOC:** Block source IP
3. **Improvement:** Add IP-based blocking rules

## Status
**CLOSED** — Lab simulation

## Analyst Notes
SSH brute force is one of the most common attacks.
Custom rule 100002 uses frequency=5, timeframe=120 to correlate failed logins.

